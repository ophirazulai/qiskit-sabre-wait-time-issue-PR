# Physical-wire wait time in SABRE's SWAP score

Implementation: `ffcdb2c81a30f32f33786fbc0351ef9f4aeac2d1`, against parent `1298f960b7e814cfcb6aa9338b548ec5c6d2b355`.

The change gives SABRE a small preference for routing SWAPs that can start earlier on their physical wires. A SWAP on idle wires can overlap previously routed gates, even when another SWAP offers the same distance improvement. The implementation adds this preference to candidate scoring and maintains the corresponding ready-time state throughout the search.

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

For a candidate SWAP on physical wires `a` and `b`, let `H_old(a, b)` be the score already computed by SABRE, including decay when enabled. The new score is:

```text
H_new(a, b) = H_old(a, b) + λ × max(r[a], r[b])
λ = 2.2 × 10⁻⁵
```

Lower scores are preferred. `r[q]` is an estimated ready timestamp for physical wire `q`, measured from the start of this routing trial. The added quantity uses the candidate wires' absolute ready times; it does not subtract a global clock or compute the final circuit's critical path.

The existing score has two implementation forms. If `C(π)` is the weighted front-layer and lookahead distance cost for layout `π`, and `π_s` is the layout after a candidate SWAP:

```text
Without decay: H_old(s) = C(π_s) − C(π)
With decay:    H_old(s) = max(decay[a], decay[b]) × C(π_s)
```

The first form uses SABRE's relative distance updates. Subtracting the common `C(π)` preserves the candidate ranking. With decay, the code restores the absolute cost before applying the candidate-dependent multiplier. The wait-time penalty is added after either calculation and is not multiplied by decay.

The coefficient is fixed in this commit. It is small enough to favor early availability when distance costs are close, but it is an additive score term: a sufficiently large ready-time difference can outweigh a nonzero distance/lookahead advantage. Candidates still within `best_epsilon` (default `1e-10`) of the best score are selected using the existing seeded random choice.

## 2. Ready-time updates and rollback

Each routing trial initializes one ready timestamp per physical wire to zero. Initially executable two-qubit nodes advance those timestamps before the first SWAP decision.

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

This prevents abandoned speculative SWAPs from leaving inflated timestamps that would affect later choices. The ready-time bookkeeping also runs when `wait_time=False`; that option skips only the score addition.

## 3. Equal distance, different concurrency

Use the identity layout on `0—1—2—3`, with four `cx(0, 1)` gates followed by `cx(1, 3)`.

The last gate is at distance two. Either SWAP `(1, 2)` or `(2, 3)` reduces that distance to one. In SABRE's interaction graph, the four consecutive CX gates on `(0, 1)` contract into one node, giving ready times `[1, 1, 0, 0]` at the decision.

For the basic heuristic, the candidate scores are:

| Candidate | Old relative distance score | Ready-time penalty | New score |
| --- | ---: | ---: | ---: |
| SWAP `(1, 2)` | -1 | 0.000022 | -0.999978 |
| SWAP `(2, 3)` | -1 | 0 | -1 |

The idle-wire SWAP wins. The same preference occurs for the `lookahead` and `decay` string presets in this example, which has no lookahead interaction and starts with equal decay values.

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

for enabled in (False, True):
    heuristic = Heuristic(wait_time=enabled).with_basic(1.0, SetScaling.Size)
    routed = SabreSwap(
        CouplingMap.from_line(4), heuristic, seed=1, trials=1
    )(qc)
    decomposed = routed.decompose(gates_to_decompose=["swap"])
    print(enabled, decomposed.depth(lambda inst: inst.operation.num_qubits == 2))

# False 8
# True 5
```

Across seeds 0–9, the disabled configuration chooses depth 5 five times and depth 8 five times in the local run. The enabled configuration chooses depth 5 ten times. These seed counts describe this small example, not a general improvement rate.

## 4. A small lookahead advantage can lose

Use the line `0—1—2—3—4` with an extra edge `1—5`. Route ten repetitions of `cx(0, 1); cx(5, 1)`, then `cx(1, 3); cx(3, 4)`.

The alternating prefix remains twenty interaction nodes, so wire 1 is ready at time 20. For the front gate `cx(1, 3)`, both SWAP `(1, 2)` (A) and SWAP `(2, 3)` (B) reduce distance by one. The lookahead gate `cx(3, 4)` prefers A by one distance unit. With constant scaling, basic weight 1, lookahead weight `W` and no decay:

```text
H_new(A) = −1 + 20λ
H_new(B) = −1 + W
20λ = 0.00044
```

B wins when `W < 0.00044`, outside the epsilon tie region. A wins when `W > 0.00044`.

The regression checks `W=0.0001`, the larger preset-like value `0.5/6`, and values `0.000001` below and above the crossover. Disabling the term restores A at `W=0.0001`. The example establishes the first SWAP choice; it does not establish that B minimizes total output depth or SWAP count.

## 5. Configuration and affected paths

The internal Python object accepts `Heuristic(..., wait_time=True)`. The setting survives all `with_*` builders, pickling and copying, participates in equality, and appears in `repr`.

To disable the term for a basic heuristic passed to `SabreSwap`:

```python
from qiskit._accelerate.sabre import Heuristic, SetScaling
from qiskit.transpiler.passes import SabreSwap

heuristic = Heuristic(wait_time=False).with_basic(1.0, SetScaling.Size)
routing_pass = SabreSwap(coupling_map, heuristic=heuristic, seed=1, trials=1)
```

Here `coupling_map` is the caller's coupling map. This object is an internal research interface, not a new public `wait_time` argument on `SabreSwap` or `SabreLayout`. Disabling the term preserves the distance/decay scoring calculation for the supplied heuristic; it does not remove bookkeeping overhead.

`SabreSwap` string presets and the default `SabreLayout` heuristic inherit the enabled default. The Rust transpiler and standalone C SABRE layout constructors explicitly enable it. Effects therefore follow use of SABRE in a pipeline; they are not restricted to optimization levels 2 and 3.

The candidate neighborhood, distance components, seeded selection among remaining ties, and routing-trial selection criterion remain as before. Completed routing trials are ranked by SWAP count and then trial index. Outputs for fixed seeds can change, which is why the commit updates expected layouts in three other test modules.

## 6. Scope and evidence

The estimate omits one-qubit durations and hardware calibration, does not advance timestamps for synchronization nodes, and does not aggregate a complete control-flow schedule. A contracted two-qubit node is always one layer. It provides a local scheduling preference and does not guarantee lower depth or gate count for every circuit.

The [benchmark summary](sabre_wait_time_benchmark_summary.md) records the supplied aggregate gains, per-case regressions and runtime measurements. The [validation notes](validation.md) record the eight focused cases and example script run during preparation. The new tests cover the mechanism and option behavior; a full-suite or native C test result is not claimed here.

## 7. Source map at the reviewed commit

| Source | Relevant behavior |
| --- | --- |
| `crates/transpiler/src/passes/sabre/route.rs` | `SWAP_DEPTH`, `READY_WEIGHT`, `State.ready`, undo log, `advance_swap`, `advance_routed`, candidate scoring and fallback |
| `crates/transpiler/src/passes/sabre/heuristic.rs` | New flag, constructor, builders, serialization, equality and representation |
| `crates/transpiler/src/passes/sabre/dag.rs` | Existing contraction of consecutive two-qubit operations |
| `qiskit/transpiler/passes/routing/sabre_swap.py` | String presets and acceptance of internal heuristic objects |
| `qiskit/transpiler/passes/layout/sabre_layout.py` | Default layout heuristic |
| `crates/transpiler/src/transpiler.rs` | Rust transpiler constructor |
| `crates/cext/src/transpiler/passes/sabre_layout.rs` | Standalone C layout constructor |
| `test/python/transpiler/test_sabre_swap.py` | Idle-wire, crossover, serialization and release-valve checks |
| `releasenotes/notes/sabre-wait-time-scoring-5be6328a79d04f10.yaml` | Default behavior and internal opt-out |
