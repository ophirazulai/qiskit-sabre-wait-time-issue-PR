Fix #ISSUE_NUMBER

<!-- Replace ISSUE_NUMBER with the Qiskit/qiskit issue number. Replace the supporting-document URLs after uploading the attachments. -->

### Summary

SABRE can assign equal distance scores to SWAPs with different opportunities to overlap already-routed work. This change adds an optional "wait time" component to the SABRE heuristic. It tracks estimated physical-wire ready times and adds a small penalty for SWAPs whose wires become available later. The component is disabled by default. On the issue's four-qubit example, `SabreSwap(heuristic="wait_time")` chooses the idle pair and gives CX depth 5 instead of 8 with the same single routing SWAP, before gate cancellation.

### Changes

- Add a `WaitTimeHeuristic(weight)` component to the internal `qiskit._accelerate.sabre.Heuristic`, set with `with_wait_time(weight)` or the new `wait_time` constructor argument. It defaults to `None` (disabled) and is preserved through builders, pickling, copying, equality and representation.
- When enabled, add `weight * max(ready[a], ready[b])` to each candidate SWAP's score after decay, so the term is not scaled by the decay multiplier. It acts as a tie-break and can outweigh small distance/lookahead differences.
- When enabled, advance physical-wire ready times by one layer per routed two-qubit SABRE node and three layers per inserted SWAP, including the initially routed prefix and fallback SWAPs. Restore ready times when the release valve rolls back an unsuccessful search. When disabled, no ready times are tracked.
- Add a `heuristic="wait_time"` option to `SabreSwap`: the `"decay"` preset plus `with_wait_time(2.2e-5)`.
- Leave the existing `SabreSwap` heuristics, `SabreLayout`, the preset pass managers, the Rust transpiler and the standalone C SABRE layout unchanged; their heuristic constructors pass `None` for the new component.
- Add tests for idle-wire preference, the lookahead crossover (including a non-default weight and the component disabled), ready-time restoration after the release valve, unitary equivalence and connectivity of routed circuits, a zero weight matching `"decay"` exactly, and serialization. Run the existing infinite-loop test with and without the component and the existing per-heuristic tests with `"wait_time"`. Add a release note.

The ready-time estimate counts contracted two-qubit nodes, so it does not model native gate durations or a complete control-flow schedule. Routing trial selection still minimizes SWAP count.


#### Qiskit benchmarks

The supplied Qiskit benchmark report gives the following weighted geometric estimates for two-qubit depth (D2) and two-qubit gate count (N2). Ratios are evolved/baseline; negative changes mean lower depth or count. The optimization-level rows are the report's marginal estimates, and the primary aggregate uses the report's primary weighting. These estimates report 100 seeds.

| Optimization level / aggregate | Cases | 2Q depth ratio (change) | 2Q count ratio (change) |
| --- | ---: | ---: | ---: |
| 0 | 38 | 0.701514 (-29.85%) | 1.045859 (+4.59%) |
| 1 | 31 | 0.780981 (-21.90%) | 0.882643 (-11.74%) |
| 2 | 31 | 0.779631 (-22.04%) | 0.876249 (-12.38%) |
| 3 | 30 | 0.894457 (-10.55%) | 0.961249 (-3.88%) |
| Primary aggregate | — | 0.781982 (-21.80%) | 0.938118 (-6.19%) |

The depth improvement rule (`CA2/improvement`) and primary gate-count guard (`CA3/primary/N2`) both passed. The report's per-test arithmetic means are separate from the weighted geometric estimates shown here.

The Qiskit extract lacks baseline/candidate identifiers, so these figures remain supplementary evidence pending provenance confirmation for this exact revision.

#### Benchpress

Benchpress compares `sabre-wait-time-aware-swap-scoring` @ `ffcdb2c81` against parent `main` @ `1298f960b` using the `quality` profile: 50 panel entries at each of optimization levels 2 and 3, with seeds 0, 1 and 2. All 300 paired seeds completed and all 600 invocations passed on the first attempt. Values below are geometric mean candidate/baseline ratios of per-case median paired-seed ratios; negative changes mean lower depth, count or runtime.

| Level | 2Q depth ratio (change) | 2Q count ratio (change) | Runtime ratio (change) |
| --- | ---: | ---: | ---: |
| 2 | 0.9645 (-3.6%) | 0.9934 (-0.7%) | 1.0102 (+1.0%) |
| 3 | 0.9634 (-3.7%) | 0.9972 (-0.3%) | 1.0102 (+1.0%) |
| Combined | 0.9639 (-3.6%) | 0.9953 (-0.5%) | 1.0102 (+1.0%) |


### Runtime

The [Benchpress report](files_to_upload_to_the_PR/wait-time-aware-swap-scoring---benchpress.md) measures **1.0% runtime overhead** by geometric mean (ratio 1.0102) across 100 cases at optimization levels 2 and 3.


### Validation

A separate correctness check confirms that routing with the wait-time heuristic preserves circuit semantics. It passed **96/96 cases and 2/2 self-checks**. 

**Setup.** 16 ten-qubit circuits, mostly built with Qiskit's own `test/benchmarks` builders, are each routed with 6 seeds (`0, 1, 42, 2, 7, 123`). The circuits are QFT, quantum volume (two seeds), random circuits of depth 20/40/60, ring, DTC, Bernstein-Vazirani and a BV-like variant, Trotter, QAOA, Grover, MCX, a ripple-carry adder and a modular adder. Each circuit is routed onto a bidirectional 10-qubit line, the most constrained connectivity, by `TrivialLayout` → `ApplyLayout` → `SabreSwap(heuristic="wait_time", trials=1)`. A single trial makes each run deterministic, and the check runs with `QISKIT_PARALLEL=FALSE`.

**Input preparation.** Final measurements are removed, QAOA parameters are bound to fixed values, and gates on three or more qubits are unrolled. The prepared input must have 10 qubits and only one- and two-qubit instructions. Its 1024×1024 unitary is the reference for every seed.

**Checks per case.** A routed circuit passes only if all four hold:

1. The width is still 10 qubits; no ancillas are added and no qubits are dropped.
2. The initial and final layout metadata are both present.
3. Every non-directive two-qubit instruction acts on a coupling-map edge.
4. `Operator.from_circuit(out)`, which uses the layout to undo the initial placement and the final SWAP permutation, equals the reference. The comparison uses default `np.allclose` tolerances and keeps the global phase.

References:
- [Validation script (`run_validation.py`)](https://github.com/AI-native-Systems-Research/qiskit-sabre-wait-time-validation/blob/codex/validation-simplified/run_validation.py)
- [Validation report (`report.md`)](https://github.com/AI-native-Systems-Research/qiskit-sabre-wait-time-validation/blob/codex/validation-simplified/report.md)


### Supporting documents

1. [How the score works](files_to_upload_to_the_PR/sabre_wait_time_detailed_description.md): `sabre_wait_time_detailed_description.md`.
2. [Benchmark summary and limitations](files_to_upload_to_the_PR/sabre_wait_time_benchmark_summary.md): `sabre_wait_time_benchmark_summary.md`.
3. [Benchpress per-case results](files_to_upload_to_the_PR/wait-time-aware-swap-scoring---benchpress.md): `wait-time-aware-swap-scoring---benchpress.md`.
4. [Qiskit benchmark extract](files_to_upload_to_the_PR/wait-time-aware-swap-scoring---qiskit-benchmarks.md): `wait-time-aware-swap-scoring---qiskit-benchmarks.md`.
5. [Slides: background, equations and a worked example](files_to_upload_to_the_PR/sabre_wait_time.pdf): `sabre_wait_time.pdf`.


### AI/LLM disclosure

- [x] Some written text was generated by: Claude Code (Claude Opus 5.5) and OpenAI Codex (GPT-6 Sol).
- [x] Some submitted code was generated by: Claude Code (Claude Opus 5.5) and OpenAI Codex (GPT-6 Sol), used to develop, test and review the implementation.