### What should we add?

Include estimated physical-wire availability in SABRE's candidate SWAP score, so routing can favor SWAPs that overlap work already routed on other wires.

The existing distance and lookahead terms can give the same score to two SWAPs even when one must follow a busy sequence and the other can run in parallel with it. Decay discourages repeated use of SWAP wires, but does not track when those wires become available after routed two-qubit operations.

For example, start with the identity layout on the line `0—1—2—3`:

```python
from qiskit import QuantumCircuit

qc = QuantumCircuit(4)
for _ in range(4):
    qc.cx(0, 1)
qc.cx(1, 3)
```

The final CX needs routing. Swapping either `(1, 2)` or `(2, 3)` makes it executable, with the same distance improvement. The first SWAP uses wire 1, which is occupied by the four preceding CX gates. The second uses idle wires and can overlap that work.

With a three-CX SWAP decomposition and unit CX durations:

| Routing choice | Schedule | CX count | CX depth |
| --- | --- | ---: | ---: |
| SWAP `(1, 2)` | Four-CX prefix, then three-CX SWAP, then final CX | 8 | 8 |
| SWAP `(2, 3)` | Prefix and SWAP in parallel, then final CX | 8 | 5 |

This is a routing-only example, before gate cancellation; the repeated CX prefix can cancel during later optimization. The existing random tie can already choose the shallower route. The proposed score makes it prefer that route across seeds.

The proposed change would:

- Track a ready time for each physical wire, counting each routed two-qubit SABRE node as one layer and each inserted SWAP as three layers.
- Add `2.2e-5 * max(ready[a], ready[b])` to the existing score for candidate SWAP `(a, b)`, after the optional decay multiplier. This can resolve equal scores and outweigh sufficiently small lookahead differences.
- Restore ready times when an unsuccessful SWAP search is rolled back, and update them for the fallback route.
- Enable the term by default, with an opt-out through the internal `qiskit._accelerate.sabre.Heuristic(wait_time=False)` configuration passed to `SabreSwap`.

`ready[]` starts at zero for every physical wire in each routing trial. It is updated as follows:

- For each routed two-qubit SABRE node, map its qubits to physical wires `(a, b)` using the current layout, then set both `ready[a]` and `ready[b]` to `max(ready[a], ready[b]) + 1`. This includes nodes routed before the first SWAP and those made executable by later SWAPs.
- For each applied SWAP `(a, b)`, set both entries to `max(ready[a], ready[b]) + 3`. Other wires retain their values. The entries stay attached to physical wires; they are not exchanged when the layout changes.
- Scoring a candidate does not change `ready[]`. Applied SWAPs save the previous values so a failed search can restore them in reverse order; fallback SWAPs then use the same update rule.

The estimate operates on SABRE's contracted interaction graph: the four-CX prefix above counts as one internal node. It is a lightweight two-qubit scheduling proxy, not a prediction of hardware duration. Routing trials would still be selected by SWAP count.

### Initial benchmark evidence

The supplied [Qiskit benchmarks report](files_to_upload_to_the_PR/wait-time-aware-swap-scoring---qiskit-benchmarks.md) reports **21.80% lower two-qubit depth** and **6.19% fewer two-qubit gates** on its primary panel. 

The separate [Benchpress report](files_to_upload_to_the_PR/wait-time-aware-swap-scoring---benchpress.md) measures **1.0% runtime overhead** by geometric mean (ratio 1.0102) across 100 cases at optimization levels 2 and 3.

### Supporting documents

The PR materials include a description of the score and state updates, reproducible examples, and both supplied benchmark reports. The Qiskit benchmark extract does not identify its baseline or candidate revision; its results need that provenance before being attributed to this commit.


### AI disclosure

I developed this as part of IBM Research's Spotlights project on AI-native software optimization; I used Claude Code (Claude Opus 5.5) and OpenAI Codex (GPT-6 Sol) to develop, test and review the implementation.
