# Physical-wire wait time in SABRE's SWAP score

Implementation: `319fa5fa703bc924008db812f5ddfec6b56c38f7`, against parent `1298f960b7e814cfcb6aa9338b548ec5c6d2b355`.

The change adds an optional "wait time" component to SABRE's heuristic. When enabled, it gives SABRE a small preference for routing SWAPs that can start earlier on their physical wires. A SWAP on idle wires can overlap previously routed gates, even when another SWAP offers the same distance improvement. The component adds this preference to candidate scoring and maintains the corresponding ready-time state throughout the search. It is disabled by default: it is enabled by `SabreSwap(heuristic="wait_time")` or by adding it to a custom heuristic (section 5).

## Background: SABRE and its existing scoring formulas

SABRE routes a quantum circuit onto a device's coupling graph by inserting SWAPs. A layout `π` maps logical qubits to physical wires. A two-qubit interaction can execute when its predecessors have been routed and its mapped wires are adjacent. Otherwise, SABRE scores candidate SWAPs on coupling edges touching qubits in the front layer, chooses a lowest-scoring candidate, updates the layout, and repeats. Qiskit's implementation includes LightSABRE improvements and can run multiple seeded trials, selecting a result with the fewest inserted SWAPs. See the [Qiskit SABRE overview](https://quantum.cloud.ibm.com/docs/en/api/qiskit/qiskit.transpiler.passes.SabreSwap).

The baseline below is the parent commit cited above, before the wait-time addition. Define:

- `F`: the front layer of pending two-qubit interactions whose predecessors have been routed.
- `E`: a lookahead set of upcoming two-qubit interactions.
- `D[u, v]`: the shortest-path distance between physical wires `u` and `v` in the routing coupling graph; adjacent wires have distance 1.
- `π_s`: the layout that would result from candidate SWAP `s = (a, b)`.
- `d_s = max(decay[a], decay[b])`: the candidate's decay multiplier.
- `W`: the relative lookahead weight; `|S|` denotes the number of interactions in set `S`.

For any interaction set `S`, write its total distance as:

```text
A(S, π) = Σ over g in S of D[π(g.q₁), π(g.q₂)]
```

The conventional basic, lookahead, and decay scores are:

```text
H_basic(s)     = A(F, π_s)
H_lookahead(s) = A(F, π_s) / |F| + W × A(E, π_s) / |E|
H_decay(s)     = d_s × [A(F, π_s) / |F| + W × A(E, π_s) / |E|]
```

An empty lookahead set contributes zero. Lower scores are preferred: the basic term brings front-layer interactions closer to execution, the lookahead term anticipates later interactions, and decay discourages repeatedly using the same physical wires. These are the [formulas presented in Qiskit's API documentation](https://quantum.cloud.ibm.com/docs/en/api/qiskit/qiskit.transpiler.passes.SabreSwap); the implementation at the reviewed parent uses configurable weights and scaling, so its exact presets require the distinction below.

### Exact distance cost at the reviewed parent

The implementation supports several lookahead layers `E₁, …, Eₖ`, each with its own weight `w_j`, and a front-layer weight `w_F`. Its general distance cost is:

```text
C(π) = w_F × α(F) × A(F, π)
       + Σ over j = 1…k of w_j × α(E_j) × A(E_j, π)

α(S) = 1       for SetScaling.Constant
α(S) = 1 / |S| for SetScaling.Size, with an empty set contributing zero
```

Front-layer and lookahead scaling are configured separately. The `SabreSwap` string presets at this parent are:

| Preset | Distance cost `C(π)` | Decay |
| --- | --- | --- |
| `basic` | `A(F, π) / \|F\|` | Disabled |
| `lookahead` | `A(F, π) + (0.5 / N) × A(E₁, π)` | Disabled |
| `decay` | `A(F, π) + (0.5 / N) × A(E₁, π)` | Enabled |

Here `N` is the number of physical qubits in the coupling map. In particular, these lookahead and decay presets use one lookahead layer and constant scaling, rather than dividing each term by its interaction-set size. The basic preset's normalization preserves its distance-only candidate ranking, but the scale matters when adding the wait-time term. These settings come from the [parent's preset constructors](https://github.com/AI-native-Systems-Research/qiskit-evolved/blob/1298f960b7e814cfcb6aa9338b548ec5c6d2b355/qiskit/transpiler/passes/routing/sabre_swap.py) and [heuristic definitions](https://github.com/AI-native-Systems-Research/qiskit-evolved/blob/1298f960b7e814cfcb6aa9338b548ec5c6d2b355/crates/transpiler/src/passes/sabre/heuristic.rs).

For the decay preset, all wire multipliers start at 1. The router adds `0.001` to each selected SWAP endpoint's multiplier, except on every fifth search SWAP, when it resets all multipliers to 1 instead. It also resets them after routing progress. Decay therefore tracks recent wire reuse; it does not estimate when each wire becomes available. The [parent's routing implementation](https://github.com/AI-native-Systems-Research/qiskit-evolved/blob/1298f960b7e814cfcb6aa9338b548ec5c6d2b355/crates/transpiler/src/passes/sabre/route.rs) evaluates distance changes for efficiency and restores the absolute cost before applying decay, as detailed next.

## 1. The score

For a candidate SWAP on physical wires `a` and `b`, let `H_old(a, b)` be the score already computed by SABRE, including decay when enabled. With the wait-time component enabled with weight `λ`, the new score is:

```text
H_new(a, b) = H_old(a, b) + λ × max(r[a], r[b])
λ = 2.2 × 10⁻⁵ in the "wait_time" preset
```

Lower scores are preferred. `r[q]` is an estimated ready timestamp for physical wire `q`, measured from the start of this routing trial. The added quantity uses the candidate wires' absolute ready times; it does not subtract a global clock or compute the final circuit's critical path.

The existing score has two implementation forms. If `C(π)` is the weighted front-layer and lookahead distance cost for layout `π`, and `π_s` is the layout after a candidate SWAP:

```text
Without decay: H_old(s) = C(π_s) − C(π)
With decay:    H_old(s) = max(decay[a], decay[b]) × C(π_s)
```

Here `H_old` means the existing score for the **selected heuristic configuration**, before adding wait time. It does not mean the sum of `H_basic`, `H_lookahead`, and `H_decay`: lookahead already includes the front-layer term, and decay multiplies the combined distance cost.

If the weights and scaling are configured to match the conventional formulas in the background section, the relationship is:

```text
B₀ = A(F, π)
L₀ = A(F, π) / |F| + W × A(E, π) / |E|

Basic:     H_old(s) = H_basic(s) − B₀
Lookahead: H_old(s) = H_lookahead(s) − L₀
Decay:     H_old(s) = H_decay(s)
```

`B₀` and `L₀` evaluate the current layout before the candidate SWAP, using the same interaction sets and weights as the candidate scores. They are constant across candidates at that decision. Subtracting them preserves both the candidate ranking and score differences, so using a relative score also preserves the effect of adding the wait-time penalty.

For decay, the code restores the absolute distance cost before multiplying by `d_s`. Using `d_s × [C(π_s) − C(π)]` would subtract `d_s × C(π)`, which varies between candidates when their decay multipliers differ and can change their ranking.

The exact string presets at the reviewed parent use the scaling listed in the background table. Writing `ΔA(S) = A(S, π_s) − A(S, π)`, their implemented scores are:

```text
basic:     H_old(s) = ΔA(F) / |F|
lookahead: H_old(s) = ΔA(F) + (0.5 / N) × ΔA(E₁)
decay:     H_old(s) = d_s × [A(F, π_s) + (0.5 / N) × A(E₁, π_s)]
```

These are the `H_old` values to which the wait-time component adds `λ × max(r[a], r[b])`. The wait-time penalty is added after the selected distance/decay calculation and is not multiplied by decay. Unlike subtracting a common baseline, rescaling the distance terms changes their strength relative to the wait-time weight, so the conventional and preset normalizations should not be interchanged when evaluating `H_new`.

The weight is configurable; the `"wait_time"` preset's `2.2 × 10⁻⁵` is small enough to favor early availability when distance costs are close, but it is an additive score term: a sufficiently large ready-time difference can outweigh a nonzero distance/lookahead advantage. Candidates still within `best_epsilon` (default `1e-10`) of the best score are selected using the existing seeded random choice.

## 2. Ready-time updates and rollback

When the component is enabled, each routing trial initializes one ready timestamp per physical wire to zero. Initially executable two-qubit nodes advance those timestamps before the first SWAP decision.

For a routed two-qubit SABRE node mapped to physical wires `a` and `b`:

```text
t = max(r[a], r[b]) + 1
r[a] = r[b] = t
```

For an inserted SWAP:

```text
t = max(r[a], r[b]) + 3
r[a] = r[b] = t
```

The three-layer cost models a SWAP decomposed into three two-qubit gates. The one-layer cost applies to each `InteractionKind::TwoQ` node, even when the node contains several contracted circuit operations. Ready times stay attached to physical wires when logical states move.

The routing loop maintains the state as follows:

1. At the start of a search step, clear the previous step's undo log.
2. For every selected SWAP, save both wires' previous ready times and advance them by the SWAP rule.
3. Once gates become routable, advance the ready times for the newly routed two-qubit nodes at the current layout.
4. If the search exhausts its attempt limit without progress, reverse the speculative layout SWAPs and restore the saved ready times in reverse order.
5. Apply the existing forced-route fallback, advancing ready times for its SWAPs and newly routed nodes.

This prevents abandoned speculative SWAPs from leaving inflated timestamps that would affect later choices. When the component is disabled, none of these updates run: the ready-time helpers return immediately and the score is unchanged.

## 3. Equal distance, different concurrency

Use the identity layout on `0—1—2—3`, with four `cx(0, 1)` gates followed by `cx(1, 3)`.

The last gate is at distance two. Either SWAP `(1, 2)` or `(2, 3)` reduces that distance to one. In SABRE's interaction graph, the four consecutive CX gates on `(0, 1)` contract into one node, giving ready times `[1, 1, 0, 0]` at the decision.

For the basic heuristic with the component added at weight `2.2 × 10⁻⁵`, the candidate scores are:

| Candidate | Old relative distance score | Ready-time penalty | New score |
| --- | ---: | ---: | ---: |
| SWAP `(1, 2)` | -1 | 0.000022 | -0.999978 |
| SWAP `(2, 3)` | -1 | 0 | -1 |

The idle-wire SWAP wins. The same preference occurs when the component is added to the `lookahead` or `decay` configuration, including the `"wait_time"` preset, in this example, which has no lookahead interaction and starts with equal decay values.

The output's decomposed CX schedule counts the actual circuit operations, separately from the contracted readiness proxy:

```text
SWAP (1, 2): prefix [0,4) → SWAP [4,7) → final CX [7,8)

SWAP (2, 3): prefix [0,4) ─┐
             SWAP [0,3) ──┴→ final CX [4,5)
```

Both routes use one SWAP and eight CX gates after decomposition. Their CX depths are 8 and 5. This assumes unit CX durations and no gate cancellation. A subsequent optimization pass can cancel the repeated-CX prefix, so the example demonstrates a routing choice rather than an end-to-end transpilation gain.

With this commit's extension, the following reproduces both routes at seed 1:

```python
from qiskit import QuantumCircuit
from qiskit._accelerate.sabre import Heuristic, SetScaling
from qiskit.transpiler import CouplingMap
from qiskit.transpiler.passes import SabreSwap

qc = QuantumCircuit(4)
for _ in range(4):
    qc.cx(0, 1)
qc.cx(1, 3)

basic = Heuristic().with_basic(1.0, SetScaling.Size)
for name, heuristic in [("disabled", basic), ("enabled", basic.with_wait_time(2.2e-5))]:
    routed = SabreSwap(
        CouplingMap.from_line(4), heuristic, seed=1, trials=1
    )(qc)
    decomposed = routed.decompose(gates_to_decompose=["swap"])
    print(name, decomposed.depth(lambda inst: inst.operation.num_qubits == 2))

# disabled 8
# enabled 5
```

Across seeds 0–9, the disabled configuration chooses depth 5 five times and depth 8 five times in the local run. The enabled configuration chooses depth 5 ten times. The `"decay"` and `"wait_time"` string presets give the same split. These seed counts describe this small example, not a general improvement rate.

## 4. A small lookahead advantage can lose

Use the line `0—1—2—3—4` with an extra edge `1—5`. Route ten repetitions of `cx(0, 1); cx(5, 1)`, then `cx(1, 3); cx(3, 4)`.

The alternating prefix remains twenty interaction nodes, so wire 1 is ready at time 20. For the front gate `cx(1, 3)`, both SWAP `(1, 2)` (A) and SWAP `(2, 3)` (B) reduce distance by one. The lookahead gate `cx(3, 4)` prefers A by one distance unit. With constant scaling, basic weight 1, lookahead weight `W`, no decay and the component at the preset weight `λ = 2.2 × 10⁻⁵`:

```text
H_new(A) = −1 + 20λ
H_new(B) = −1 + W
20λ = 0.00044
```

B wins when `W < 0.00044`, outside the epsilon tie region. A wins when `W > 0.00044`.

The regression checks `W=0.0001`, the larger preset-like value `0.5/6`, and values `0.000001` below and above the crossover. It repeats the crossover check with a non-default weight `λ = 0.001` (crossover at `W = 0.02`). Without the component, A wins at `W=0.0001`. The example establishes the first SWAP choice; it does not establish that B minimizes total output depth or SWAP count.

## 5. Configuration and affected paths

The component is a `WaitTimeHeuristic(weight)` on the internal `qiskit._accelerate.sabre.Heuristic`, alongside the existing `basic`, `lookahead` and `decay` components. It defaults to `None`, meaning disabled, and can be set with the `with_wait_time(weight)` builder or the `wait_time` constructor argument. The setting survives the other `with_*` builders, pickling and copying, participates in equality, and appears in `repr`.

There are two ways to enable it. The new `"wait_time"` string preset of `SabreSwap` is the `"decay"` preset plus `with_wait_time(2.2e-5)`:

```python
from qiskit.transpiler.passes import SabreSwap

routing_pass = SabreSwap(coupling_map, heuristic="wait_time", seed=1)
```

A custom heuristic object can also add the component at any weight:

```python
from qiskit._accelerate.sabre import Heuristic, SetScaling
from qiskit.transpiler.passes import SabreSwap

heuristic = Heuristic().with_basic(1.0, SetScaling.Size).with_wait_time(2.2e-5)
routing_pass = SabreSwap(coupling_map, heuristic=heuristic, seed=1, trials=1)
```

Here `coupling_map` is the caller's coupling map. The `Heuristic` object is an internal interface; the public entry point is the `"wait_time"` string.

Everything else leaves the component disabled: the existing `"basic"`, `"lookahead"` and `"decay"` presets, the default `SabreLayout` heuristic, the Rust transpiler and the standalone C SABRE layout, whose constructors pass `None`. The preset pass managers therefore produce the same output as before, and existing fixed-seed test expectations are unchanged. With the component disabled, the ready-time helpers return immediately, so the only added work is a check of whether the component is set.

When it is enabled, the candidate neighborhood, distance components, seeded selection among remaining ties, and routing-trial selection criterion remain as before. Completed routing trials are ranked by SWAP count and then trial index. A weight of zero tracks ready times without changing any score, and the tests confirm that it reproduces the `"decay"` preset's output exactly.

## 6. Scope and evidence

The estimate omits one-qubit durations and hardware calibration, does not advance timestamps for synchronization nodes, and does not aggregate a complete control-flow schedule. A contracted two-qubit node is always one layer. It provides a local scheduling preference and does not guarantee lower depth or gate count for every circuit.

The [benchmark summary](sabre_wait_time_benchmark_summary.md) records the supplied aggregate gains, per-case regressions and runtime measurements. Those were measured on an earlier revision (`ffcdb2c81`) that enabled the term by default in every SABRE path, with the same rules and weight; they describe the effect of enabling the component throughout the pipeline. A [separate correctness check](https://github.com/AI-native-Systems-Research/qiskit-sabre-wait-time-validation/blob/codex/validation-simplified/report.md) routes 16 ten-qubit circuits with 6 seeds each through `SabreSwap(heuristic="wait_time")` and confirms unitary equivalence and connectivity in all 96 cases. The new tests cover the mechanism, unitary preservation and option behavior; a full-suite or native C test result is not claimed here.

## 7. Source map at the reviewed commit

| Source | Relevant behavior |
| --- | --- |
| `crates/transpiler/src/passes/sabre/route.rs` | `SWAP_DEPTH`, `State.ready`, undo log, `advance_swap`, `advance_routed` (no-ops when disabled), candidate scoring and fallback |
| `crates/transpiler/src/passes/sabre/heuristic.rs` | `WaitTimeHeuristic`, the `wait_time` field and constructor argument, `with_wait_time`, serialization, equality and representation |
| `crates/transpiler/src/passes/sabre/mod.rs` | Registration of `WaitTimeHeuristic` in the Python module |
| `crates/transpiler/src/passes/sabre/dag.rs` | Existing contraction of consecutive two-qubit operations |
| `qiskit/transpiler/passes/routing/sabre_swap.py` | New `"wait_time"` preset and its documentation |
| `crates/transpiler/src/transpiler.rs` | Rust transpiler constructor, passing `None` |
| `crates/cext/src/transpiler/passes/sabre_layout.rs` | Standalone C layout constructor, passing `None` |
| `test/python/transpiler/test_sabre_swap.py` | Idle-wire, crossover, release-valve, unitary-preservation, zero-weight and serialization checks |
| `releasenotes/notes/sabre-wait-time-scoring-5be6328a79d04f10.yaml` | Opt-in component and the `"wait_time"` preset |
