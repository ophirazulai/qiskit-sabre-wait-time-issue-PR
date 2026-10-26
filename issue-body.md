### What should we add?

I'd like to add an optional wait-time term to SABRE's SWAP scoring, so it can prefer SWAPs on wires that become available earlier. The distance and lookahead scores can tie even when one SWAP must wait for earlier gates and another can run in parallel with them. Decay discourages repeated use of SWAP wires, but doesn't track their availability after routed two-qubit gates.

For example, start with the identity layout on the line `0—1—2—3`:

```python
from qiskit import QuantumCircuit

qc = QuantumCircuit(4)
for _ in range(4):
    qc.cx(0, 1)
qc.cx(1, 3)
```

Either SWAP `(1, 2)` or `(2, 3)` makes the final CX executable. The first has to wait for the four CX gates on wire 1; the second can run alongside them. With three CX gates per SWAP and unit CX durations, both routes use eight CX gates, but their CX depths are eight and five respectively. This example is before optimization, which can cancel the repeated CX gates. SABRE can already choose the shallower route by random tie-breaking; the new term would give it a preference for that route.

The idea is to track a ready time for each physical wire and add `weight * max(ready[a], ready[b])` to the score for SWAP `(a, b)`, after decay. A small weight would favor earlier availability when distance scores are equal or close. The estimate would count each contracted two-qubit SABRE node as one layer and each SWAP as three. The four-CX prefix above counts as one such node, so these ready times are only a rough estimate of scheduling, not hardware durations.

I'd expose this as `SabreSwap(heuristic="wait_time")`, adding the term to the existing `"decay"` heuristic. It would be disabled by default.

On a collection of Qiskit's benchmarks, this gave 21.80% lower two-qubit depth and 6.19% fewer two-qubit gates, at 1.0% higher runtime.

### AI disclosure

I developed this as part of IBM Research's Spotlights project on AI-native software optimization. I used Claude Code and OpenAI Codex to develop, test and review the implementation.
