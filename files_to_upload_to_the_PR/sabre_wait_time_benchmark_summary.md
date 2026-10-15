# SABRE wait-time scoring: supplied benchmark evidence

The [Qiskit benchmark extract](wait-time-aware-swap-scoring---qiskit-benchmarks.md) contains no revision identifiers. The [Benchpress report](wait-time-aware-swap-scoring---benchpress.md) explicitly compares candidate `ffcdb2c81` against its parent `1298f960b`. Both are included as supplied; the benchmark suites were not rerun while preparing these materials.

`D2` denotes two-qubit depth and `N2` two-qubit gate count. Ratios below are candidate/baseline, so values below one are improvements. Signed percentage changes use `100 * (ratio - 1)`: negative is better. The Qiskit source uses the opposite sign when labeling a percentage as an "improvement".

## Qiskit benchmark extract: revision provenance pending

The extract reports primary weighted geometric ratios of **0.781982 for D2 (-21.80%)** and **0.938118 for N2 (-6.19%)**, with 100 seeds in those estimates. Its optimization-level marginal rows are:

| Level | Marginal cases | D2 ratio (change) | N2 ratio (change) |
| --- | ---: | ---: | ---: |
| 0 | 38 | 0.701514 (-29.85%) | 1.045859 (+4.59%) |
| 1 | 31 | 0.780981 (-21.90%) | 0.882643 (-11.74%) |
| 2 | 31 | 0.779631 (-22.04%) | 0.876249 (-12.38%) |
| 3 | 30 | 0.894457 (-10.55%) | 0.961249 (-3.88%) |

These are the extract's reported weighted estimates. They are not equal-weight averages of the printed arithmetic means and should not be combined with Benchpress's aggregates. The full quality-test table includes guard cases, some with 10 seeds, while the primary/marginal estimate tables above use 100. The printed per-test D2/N2 means are arithmetic means and can differ from geometric ratio estimates.

For example, the arithmetic means for `qaoa_ba_n100_3reps/heavy_hex_d9_cz/L2` show depth decreasing from 1531.56 to 1284.71 (16.12%) while count increases from 8610.32 to 9005.52 (4.59%). For `qft_cp_n14/melbourne_14_u/L3`, depth increases from 118.76 to 118.96 (0.17%) and count from 281.33 to 283.77 (0.87%). The level-0 marginal also shows an aggregate count regression despite its depth improvement.

The extract does not provide baseline/candidate commit IDs, the benchmark harness revision, raw paired samples, or runtime results. Until its revision provenance is confirmed, its percentages should be presented as supplied results rather than verified measurements of `ffcdb2c81`. The primary 21.80% reduction covers the reported cross-level panel; it is not an L2/L3-only result.

## Benchpress: confirmed commit comparison

Profile `quality`, optimization levels 2 and 3, seeds 0/1/2: 50 panel entries × 2 levels = 100 cases, 300 paired seeds and 600 successful invocations, all on the first attempt.

Each case ratio is the median of its three paired-seed ratios. Aggregates are unweighted geometric means of those case ratios. The two `BVlike_simplification` cases have zero two-qubit baselines and are excluded from D2/N2 geometric means, leaving 49 cases per level and 98 overall. They remain ties in the win/tie/loss counts.

| Level | D2 cases | D2 ratio | D2 change | D2 win/tie/loss | N2 ratio | N2 change | N2 win/tie/loss |
| --- | ---: | ---: | ---: | --- | ---: | ---: | --- |
| 2 | 49 | 0.9645 | -3.6% | 24/19/7 | 0.9934 | -0.7% | 19/20/11 |
| 3 | 49 | 0.9634 | -3.7% | 24/19/7 | 0.9972 | -0.3% | 17/20/13 |
| Combined | 98 | 0.9639 | -3.6% | 48/38/14 | 0.9953 | -0.5% | 36/40/24 |

The per-case report includes both material gains and regressions. Selected examples, using the reported paired ratios:

| Circuit / topology | Level | D2 ratio (change) | N2 ratio (change) |
| --- | ---: | ---: | ---: |
| `QAOA_100` / `fake_torino` | 3 | 0.819 (-18.1%) | 1.067 (+6.7%) |
| `QV_100` / `fake_torino` | 3 | 0.815 (-18.5%) | 0.994 (-0.6%) |
| `clifford_100` / `fake_torino` | 2 | 0.868 (-13.2%) | 1.024 (+2.4%) |
| `BH_D-1_d-4` / linear | 3 | 1.141 (+14.1%) | 1.140 (+14.0%) |
| `circSU2_89` / `fake_torino` | 2 | 1.058 (+5.8%) | 1.057 (+5.7%) |

The source also gives each build's median depth/count for scale. Dividing those medians can differ from the paired-ratio statistic, because the medians may come from different seeds. The changes above use the ratio columns directly.

Runtime measures one wall-clock `pm.run(circuit)` call per invocation, without warmup:

| Level | Cases | Geometric mean runtime ratio | Ratio of summed per-case median runtimes |
| --- | ---: | ---: | ---: |
| 2 | 50 | 1.0102 (+1.0%) | 1.0687 (+6.9%) |
| 3 | 50 | 1.0102 (+1.0%) | 1.0926 (+9.3%) |
| Combined | 100 | 1.0102 (+1.0%) | 1.0864 (+8.6%) |

The geometric mean weights cases equally, whereas the summed-time ratio is dominated by expensive circuits. The report notes a few percent of timing noise, including on all-to-all cases without routing. The data do not establish a precise 1% implementation overhead.

## Available artifacts and limits

- The two full Markdown reports are copied unchanged into this attachment folder, preserving their tables and wording.
- The Benchpress source links `tables/paired_seeds.csv`, `tables/cases.csv` and `report.md` are references to its original report bundle. Those files were not supplied here, so those links do not resolve in this package.
- No new confidence interval, combined score, or L2/L3-only Qiskit aggregate has been inferred from the extracts. Reconstructing weighted estimates requires the original manifest/weights and paired data.
- Benchpress has only three paired seeds per case. Local mechanism tests and successful invocations do not establish universal depth improvement or hardware runtime/fidelity gains.
