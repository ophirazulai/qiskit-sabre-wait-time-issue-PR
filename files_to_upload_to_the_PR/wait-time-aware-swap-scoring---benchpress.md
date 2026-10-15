# main vs wait-time-aware Sabre swap scoring: Benchpress report

**Baseline:** `main` @ `1298f960b`. **Candidate:** `sabre-wait-time-aware-swap-scoring` @ `ffcdb2c81`.

Profile `quality`; optimization levels 2 and 3; seeds 0, 1, 2. 50 panel entries × 2 levels = 100 cases, 300/300 paired seeds, 600/600 invocations passed on the first attempt.

**Metrics.** `d2` = two-qubit depth, `n2` = two-qubit gate count. Every ratio is candidate / baseline, so **below 1 is better** (fewer gates, shallower circuit, faster transpile).

**How numbers are built.** For each case the per-seed ratio is computed for every seed, and the case ratio is the median of those. Aggregates are geometric means of case ratios. One case pair (`BVlike_simplification`, O2 and O3) has a zero 2Q baseline and is left out of the `d2`/`n2` geomeans, so those use 49 cases per level (98 overall); W / T / L (sign of the median per-seed change) still counts all 50, with the zero-baseline cases as ties. In tables, **bold** means a ratio ≤ 0.95 and ⚠ means ≥ 1.05.

## Overall d2 and n2

| Level | Geomean cases | d2 geomean ratio | d2 change | d2 W / T / L | n2 geomean ratio | n2 change | n2 W / T / L |
| --- | ---: | ---: | ---: | --- | ---: | ---: | --- |
| O2 | 49 | 0.9645 | -3.6% | 24 / 19 / 7 | 0.9934 | -0.7% | 19 / 20 / 11 |
| O3 | 49 | 0.9634 | -3.7% | 24 / 19 / 7 | 0.9972 | -0.3% | 17 / 20 / 13 |
| All | 98 | 0.9639 | -3.6% | 48 / 38 / 14 | 0.9953 | -0.5% | 36 / 40 / 24 |

## Runtime ratio

Runtime is wall-clock seconds of the single `pm.run(circuit)` call (`perf_counter`), one call per invocation with no warmup. Per case, the runtime ratio is the median of the 3 per-seed ratios.

| Level | Cases | Geomean ratio | Arithmetic mean ratio | Median ratio | Faster / slower | Total baseline (s) | Total candidate (s) | Total-time ratio |
| --- | ---: | ---: | ---: | ---: | --- | ---: | ---: | ---: |
| O2 | 50 | 1.0102 (+1.0%) | 1.0112 | 1.0072 | 18 / 32 | 50.9 | 54.4 | 1.0687 |
| O3 | 50 | 1.0102 (+1.0%) | 1.0189 | 1.0208 | 18 / 32 | 145.1 | 158.5 | 1.0926 |
| All | 100 | 1.0102 (+1.0%) | 1.0151 | 1.0131 | 36 / 64 | 196.0 | 213.0 | 1.0864 |

Totals sum the per-case median runtimes, so they are dominated by the large `device-summit` circuits. The geomean weights every case equally. Single-call timings carry a few percent of noise (compare the `all-to-all` rows in the family section, where no routing happens).

## Per family

Family = Benchpress suite.

| Family | Level | Cases | d2 geomean | d2 W / T / L | n2 geomean | n2 W / T / L | Runtime geomean |
| --- | --- | ---: | ---: | --- | ---: | --- | ---: |
| abstract-hamlib | O2 | 8 | 0.987 | 6 / 2 / 0 | 0.996 | 5 / 2 / 1 | 1.018 |
| abstract-hamlib | O3 | 8 | 1.008 | 5 / 2 / 1 | 1.013 | 4 / 2 / 2 | 0.943 |
| abstract-qasmbench-small | O2 | 8 | 0.998 | 2 / 5 / 1 | 0.999 | 1 / 6 / 1 | 0.999 |
| abstract-qasmbench-small | O3 | 8 | 0.990 | 2 / 5 / 1 | 0.998 | 2 / 5 / 1 | 1.005 |
| abstract-qasmbench-medium | O2 | 8 | **0.943** | 2 / 5 / 1 | 0.971 | 3 / 5 / 0 | 0.992 |
| abstract-qasmbench-medium | O3 | 8 | **0.919** | 3 / 5 / 0 | 0.981 | 3 / 5 / 0 | 1.009 |
| abstract-qasmbench-large | O2 | 8 | 0.968 | 3 / 3 / 2 | 0.993 | 3 / 3 / 2 | 0.996 |
| abstract-qasmbench-large | O3 | 8 | 0.969 | 4 / 3 / 1 | 0.994 | 2 / 4 / 2 | 1.063 |
| device-hamlib | O2 | 4 | 0.964 | 4 / 0 / 0 | 0.981 | 3 / 0 / 1 | 0.988 |
| device-hamlib | O3 | 4 | 0.975 | 3 / 0 / 1 | 0.974 | 3 / 0 / 1 | 0.997 |
| device-feynman | O2 | 5 | 0.959 | 2 / 1 / 2 | 0.995 | 2 / 1 / 2 | 1.012 |
| device-feynman | O3 | 5 | 0.965 | 2 / 1 / 2 | 1.002 | 1 / 1 / 3 | 0.981 |
| device-summit | O2 | 9 | **0.932** | 5 / 3 / 1 | 1.013 | 2 / 3 / 4 | 1.052 |
| device-summit | O3 | 9 | **0.927** | 5 / 3 / 1 | 1.010 | 2 / 3 / 4 | 1.055 |

### Per topology

| Topology | Level | Cases | d2 geomean | d2 W / T / L | n2 geomean | n2 W / T / L | Runtime geomean |
| --- | --- | ---: | ---: | --- | ---: | --- | ---: |
| all-to-all | O2 | 8 | 1.000 | 0 / 8 / 0 | 1.000 | 0 / 8 / 0 | 1.004 |
| all-to-all | O3 | 8 | 1.000 | 0 / 8 / 0 | 1.000 | 0 / 8 / 0 | 1.017 |
| linear | O2 | 8 | **0.940** | 4 / 4 / 0 | 0.993 | 2 / 4 / 2 | 0.999 |
| linear | O3 | 8 | **0.927** | 3 / 4 / 1 | 1.004 | 2 / 4 / 2 | 1.019 |
| heavy-hex | O2 | 8 | 0.988 | 4 / 2 / 2 | 0.979 | 5 / 2 / 1 | 1.018 |
| heavy-hex | O3 | 8 | 1.003 | 5 / 2 / 1 | 0.987 | 5 / 2 / 1 | 1.026 |
| square | O2 | 8 | 0.969 | 5 / 1 / 2 | 0.988 | 5 / 2 / 1 | 0.983 |
| square | O3 | 8 | 0.957 | 6 / 1 / 1 | 0.994 | 4 / 2 / 2 | 0.956 |
| fake_torino | O2 | 18 | **0.947** | 11 / 4 / 3 | 1.000 | 7 / 4 / 7 | 1.027 |
| fake_torino | O3 | 18 | **0.949** | 10 / 4 / 4 | 0.999 | 6 / 4 / 8 | 1.021 |

## Per case

`base → cand` is each build's own median over the seeds, for scale. The ratio column is the case ratio (median of per-seed ratios), so it can differ from `cand / base` when the two medians come from different seeds.

| Circuit | Qubits | Family | Topology | Level | Seeds | d2 base → cand | d2 ratio | n2 base → cand | n2 ratio | Runtime ratio |
| --- | ---: | --- | --- | --- | ---: | --- | ---: | --- | ---: | ---: |
| `BH_D-1_d-4` | 28 | abstract-hamlib | all-to-all | O2 | 3 | 978 → 978 | 1.000 | 1066 → 1066 | 1.000 | 1.006 |
| `BH_D-1_d-4` | 28 | abstract-hamlib | all-to-all | O3 | 3 | 981 → 981 | 1.000 | 1068 → 1068 | 1.000 | 1.012 |
| `BH_D-1_d-4` | 28 | abstract-hamlib | linear | O2 | 3 | 1082 → 1076 | 0.994 | 1199 → 1205 | 1.010 | 0.995 |
| `BH_D-1_d-4` | 28 | abstract-hamlib | linear | O3 | 3 | 1082 → 1235 | 1.141 ⚠ | 1199 → 1367 | 1.140 ⚠ | 1.064 |
| `BH_D-1_d-4` | 28 | abstract-hamlib | heavy-hex | O2 | 3 | 947 → 931 | 0.986 | 1010 → 995 | 0.987 | 0.983 |
| `BH_D-1_d-4` | 28 | abstract-hamlib | heavy-hex | O3 | 3 | 937 → 937 | 0.986 | 1002 → 979 | 0.975 | 1.173 |
| `BH_D-1_d-4` | 28 | abstract-hamlib | square | O2 | 3 | 947 → 935 | 0.987 | 1004 → 1003 | 0.995 | 1.022 |
| `BH_D-1_d-4` | 28 | abstract-hamlib | square | O3 | 3 | 925 → 925 | 0.991 | 983 → 987 | 0.982 | 0.471 |
| `Li2` | 14 | abstract-hamlib | all-to-all | O2 | 3 | 2332 → 2332 | 1.000 | 3332 → 3332 | 1.000 | 1.005 |
| `Li2` | 14 | abstract-hamlib | all-to-all | O3 | 3 | 2334 → 2334 | 1.000 | 3335 → 3335 | 1.000 | 1.034 |
| `Li2` | 14 | abstract-hamlib | linear | O2 | 3 | 5953 → 5934 | 0.997 | 6869 → 6851 | 0.997 | 1.023 |
| `Li2` | 14 | abstract-hamlib | linear | O3 | 3 | 5099 → 5080 | 0.996 | 5942 → 5923 | 0.996 | 1.020 |
| `Li2` | 14 | abstract-hamlib | heavy-hex | O2 | 3 | 6274 → 6260 | 0.987 | 7286 → 7324 | 0.998 | 1.118 |
| `Li2` | 14 | abstract-hamlib | heavy-hex | O3 | 3 | 5064 → 4986 | 0.992 | 6035 → 5976 | 0.991 | 1.030 |
| `Li2` | 14 | abstract-hamlib | square | O2 | 3 | 5459 → 5166 | **0.946** | 6324 → 6207 | 0.981 | 0.996 |
| `Li2` | 14 | abstract-hamlib | square | O3 | 3 | 4802 → 4641 | 0.967 | 5570 → 5720 | 1.027 | 0.971 |
| `adder_n10` | 10 | abstract-qasmbench-small | all-to-all | O2 | 3 | 55 → 55 | 1.000 | 65 → 65 | 1.000 | 0.992 |
| `adder_n10` | 10 | abstract-qasmbench-small | all-to-all | O3 | 3 | 55 → 55 | 1.000 | 65 → 65 | 1.000 | 1.007 |
| `adder_n10` | 10 | abstract-qasmbench-small | linear | O2 | 3 | 84 → 84 | 1.000 | 94 → 94 | 1.000 | 0.984 |
| `adder_n10` | 10 | abstract-qasmbench-small | linear | O3 | 3 | 84 → 84 | 1.000 | 94 → 94 | 1.000 | 1.037 |
| `adder_n10` | 10 | abstract-qasmbench-small | heavy-hex | O2 | 3 | 87 → 85 | **0.938** | 96 → 96 | 0.979 | 1.004 |
| `adder_n10` | 10 | abstract-qasmbench-small | heavy-hex | O3 | 3 | 87 → 85 | **0.938** | 96 → 96 | 0.979 | 1.023 |
| `adder_n10` | 10 | abstract-qasmbench-small | square | O2 | 3 | 79 → 72 | **0.911** | 91 → 99 | 1.011 | 0.947 |
| `adder_n10` | 10 | abstract-qasmbench-small | square | O3 | 3 | 79 → 73 | **0.924** | 90 → 94 | 1.044 | 0.964 |
| `qaoa_n6` | 6 | abstract-qasmbench-small | all-to-all | O2 | 3 | 22 → 22 | 1.000 | 36 → 36 | 1.000 | 1.070 |
| `qaoa_n6` | 6 | abstract-qasmbench-small | all-to-all | O3 | 3 | 22 → 22 | 1.000 | 36 → 36 | 1.000 | 1.045 |
| `qaoa_n6` | 6 | abstract-qasmbench-small | linear | O2 | 3 | 49 → 49 | 1.000 | 72 → 72 | 1.000 | 1.046 |
| `qaoa_n6` | 6 | abstract-qasmbench-small | linear | O3 | 3 | 53 → 49 | 1.000 | 72 → 72 | 1.000 | 1.015 |
| `qaoa_n6` | 6 | abstract-qasmbench-small | heavy-hex | O2 | 3 | 48 → 48 | 1.000 | 63 → 62 | 1.000 | 1.004 |
| `qaoa_n6` | 6 | abstract-qasmbench-small | heavy-hex | O3 | 3 | 48 → 48 | 1.000 | 60 → 60 | 1.000 | 1.023 |
| `qaoa_n6` | 6 | abstract-qasmbench-small | square | O2 | 3 | 40 → 46 | 1.150 ⚠ | 54 → 52 | 1.000 | 0.953 |
| `qaoa_n6` | 6 | abstract-qasmbench-small | square | O3 | 3 | 45 → 48 | 1.067 ⚠ | 54 → 52 | 0.963 | 0.933 |
| `ising_n26` | 26 | abstract-qasmbench-medium | all-to-all | O2 | 3 | 4 → 4 | 1.000 | 50 → 50 | 1.000 | 1.000 |
| `ising_n26` | 26 | abstract-qasmbench-medium | all-to-all | O3 | 3 | 4 → 4 | 1.000 | 50 → 50 | 1.000 | 0.990 |
| `ising_n26` | 26 | abstract-qasmbench-medium | linear | O2 | 3 | 4 → 4 | 1.000 | 50 → 50 | 1.000 | 1.004 |
| `ising_n26` | 26 | abstract-qasmbench-medium | linear | O3 | 3 | 4 → 4 | 1.000 | 50 → 50 | 1.000 | 1.035 |
| `ising_n26` | 26 | abstract-qasmbench-medium | heavy-hex | O2 | 3 | 4 → 4 | 1.000 | 50 → 50 | 1.000 | 1.018 |
| `ising_n26` | 26 | abstract-qasmbench-medium | heavy-hex | O3 | 3 | 4 → 4 | 1.000 | 50 → 50 | 1.000 | 1.058 |
| `ising_n26` | 26 | abstract-qasmbench-medium | square | O2 | 3 | 4 → 4 | 1.000 | 50 → 50 | 1.000 | 1.017 |
| `ising_n26` | 26 | abstract-qasmbench-medium | square | O3 | 3 | 4 → 4 | 1.000 | 50 → 50 | 1.000 | 0.978 |
| `qft_n18` | 18 | abstract-qasmbench-medium | all-to-all | O2 | 3 | 66 → 66 | 1.000 | 294 → 294 | 1.000 | 1.003 |
| `qft_n18` | 18 | abstract-qasmbench-medium | all-to-all | O3 | 3 | 66 → 66 | 1.000 | 294 → 294 | 1.000 | 1.032 |
| `qft_n18` | 18 | abstract-qasmbench-medium | linear | O2 | 3 | 145 → 101 | **0.697** | 513 → 459 | **0.895** | 0.908 |
| `qft_n18` | 18 | abstract-qasmbench-medium | linear | O3 | 3 | 157 → 101 | **0.643** | 526 → 459 | **0.873** | 0.864 |
| `qft_n18` | 18 | abstract-qasmbench-medium | heavy-hex | O2 | 3 | 169 → 181 | 1.053 ⚠ | 545 → 502 | **0.910** | 0.972 |
| `qft_n18` | 18 | abstract-qasmbench-medium | heavy-hex | O3 | 3 | 213 → 183 | **0.883** | 532 → 506 | 0.998 | 0.993 |
| `qft_n18` | 18 | abstract-qasmbench-medium | square | O2 | 3 | 214 → 179 | **0.854** | 526 → 503 | 0.972 | 1.021 |
| `qft_n18` | 18 | abstract-qasmbench-medium | square | O3 | 3 | 217 → 195 | **0.899** | 512 → 502 | 0.984 | 1.147 |
| `qft_n29` | 29 | abstract-qasmbench-large | all-to-all | O2 | 3 | 110 → 110 | 1.000 | 602 → 602 | 1.000 | 1.011 |
| `qft_n29` | 29 | abstract-qasmbench-large | all-to-all | O3 | 3 | 110 → 110 | 1.000 | 602 → 602 | 1.000 | 1.028 |
| `qft_n29` | 29 | abstract-qasmbench-large | linear | O2 | 3 | 277 → 229 | **0.881** | 1347 → 1404 | 1.049 | 1.042 |
| `qft_n29` | 29 | abstract-qasmbench-large | linear | O3 | 3 | 274 → 179 | **0.743** | 1373 → 1392 | 1.043 | 1.143 |
| `qft_n29` | 29 | abstract-qasmbench-large | heavy-hex | O2 | 3 | 353 → 322 | 1.040 | 1352 → 1404 | 1.038 | 1.040 |
| `qft_n29` | 29 | abstract-qasmbench-large | heavy-hex | O3 | 3 | 326 → 344 | 1.328 ⚠ | 1284 → 1344 | 1.023 | 1.023 |
| `qft_n29` | 29 | abstract-qasmbench-large | square | O2 | 3 | 383 → 353 | **0.888** | 1259 → 1205 | 0.957 | 1.047 |
| `qft_n29` | 29 | abstract-qasmbench-large | square | O3 | 3 | 386 → 344 | **0.855** | 1214 → 1161 | 0.956 | 0.953 |
| `swap_test_n41` | 41 | abstract-qasmbench-large | all-to-all | O2 | 3 | 102 → 102 | 1.000 | 140 → 140 | 1.000 | 0.953 |
| `swap_test_n41` | 41 | abstract-qasmbench-large | all-to-all | O3 | 3 | 102 → 102 | 1.000 | 140 → 140 | 1.000 | 0.991 |
| `swap_test_n41` | 41 | abstract-qasmbench-large | linear | O2 | 3 | 184 → 184 | 1.000 | 235 → 235 | 1.000 | 1.001 |
| `swap_test_n41` | 41 | abstract-qasmbench-large | linear | O3 | 3 | 184 → 184 | 1.000 | 235 → 235 | 1.000 | 1.000 |
| `swap_test_n41` | 41 | abstract-qasmbench-large | heavy-hex | O2 | 3 | 302 → 274 | **0.907** | 369 → 343 | **0.922** | 1.008 |
| `swap_test_n41` | 41 | abstract-qasmbench-large | heavy-hex | O3 | 3 | 298 → 293 | 0.951 | 373 → 359 | **0.935** | 0.905 |
| `swap_test_n41` | 41 | abstract-qasmbench-large | square | O2 | 3 | 208 → 213 | 1.042 | 291 → 281 | 0.986 | 0.875 |
| `swap_test_n41` | 41 | abstract-qasmbench-large | square | O3 | 3 | 221 → 214 | 0.968 | 298 → 293 | 1.000 | 1.590 |
| `BH_D-1_d-4` | 28 | device-hamlib | fake_torino | O2 | 3 | 961 → 922 | 0.959 | 1066 → 961 | **0.902** | 0.941 |
| `BH_D-1_d-4` | 28 | device-hamlib | fake_torino | O3 | 3 | 961 → 922 | 0.972 | 1030 → 961 | **0.931** | 1.001 |
| `graph-complete_bipart` | 10 | device-hamlib | fake_torino | O2 | 3 | 222 → 222 | 0.973 | 277 → 296 | 1.045 | 1.000 |
| `graph-complete_bipart` | 10 | device-hamlib | fake_torino | O3 | 3 | 229 → 227 | 1.009 | 288 → 297 | 1.042 | 1.023 |
| `Li2` | 14 | device-hamlib | fake_torino | O2 | 3 | 5383 → 5362 | 0.996 | 6267 → 6262 | 1.000 | 1.020 |
| `Li2` | 14 | device-hamlib | fake_torino | O3 | 3 | 4975 → 4950 | 0.996 | 5832 → 5853 | 0.999 | 1.033 |
| `TSP_Ncity-5` | 25 | device-hamlib | fake_torino | O2 | 3 | 153 → 142 | **0.928** | 473 → 465 | 0.981 | 0.995 |
| `TSP_Ncity-5` | 25 | device-hamlib | fake_torino | O3 | 3 | 167 → 158 | **0.924** | 509 → 472 | **0.927** | 0.933 |
| `adder_8` | 24 | device-feynman | fake_torino | O2 | 3 | 307 → 250 | **0.866** | 755 → 745 | 0.980 | 1.029 |
| `adder_8` | 24 | device-feynman | fake_torino | O3 | 3 | 279 → 253 | **0.907** | 752 → 753 | 1.009 | 0.942 |
| `barenco_tof_5` | 9 | device-feynman | fake_torino | O2 | 3 | 92 → 95 | 1.033 | 117 → 118 | 1.009 | 0.990 |
| `barenco_tof_5` | 9 | device-feynman | fake_torino | O3 | 3 | 92 → 95 | 1.033 | 117 → 118 | 1.009 | 0.953 |
| `gf2^8_mult` | 24 | device-feynman | fake_torino | O2 | 3 | 487 → 438 | **0.899** | 1139 → 1122 | 1.006 | 1.048 |
| `gf2^8_mult` | 24 | device-feynman | fake_torino | O3 | 3 | 533 → 472 | **0.886** | 1161 → 1128 | 0.985 | 0.987 |
| `qft_4` | 5 | device-feynman | fake_torino | O2 | 3 | 75 → 81 | 1.000 | 78 → 83 | 1.000 | 1.030 |
| `qft_4` | 5 | device-feynman | fake_torino | O3 | 3 | 75 → 81 | 1.000 | 78 → 83 | 1.000 | 1.003 |
| `rc_adder_6` | 14 | device-feynman | fake_torino | O2 | 3 | 97 → 98 | 1.010 | 154 → 153 | 0.981 | 0.965 |
| `rc_adder_6` | 14 | device-feynman | fake_torino | O3 | 3 | 88 → 98 | 1.011 | 152 → 153 | 1.007 | 1.022 |
| `BV_100` | 100 | device-summit | fake_torino | O2 | 3 | 196 → 196 | 1.000 | 196 → 196 | 1.000 | 1.066 |
| `BV_100` | 100 | device-summit | fake_torino | O3 | 3 | 196 → 196 | 1.000 | 196 → 196 | 1.000 | 1.094 |
| `BVlike_simplification` | 100 | device-summit | fake_torino | O2 | 3 | 0 → 0 | n/a | 0 → 0 | n/a | 0.982 |
| `BVlike_simplification` | 100 | device-summit | fake_torino | O3 | 3 | 0 → 0 | n/a | 0 → 0 | n/a | 1.016 |
| `circSU2_100` | 100 | device-summit | fake_torino | O2 | 3 | 300 → 300 | 1.000 | 300 → 300 | 1.000 | 1.052 |
| `circSU2_100` | 100 | device-summit | fake_torino | O3 | 3 | 300 → 300 | 1.000 | 300 → 300 | 1.000 | 0.989 |
| `circSU2_89` | 89 | device-summit | fake_torino | O2 | 3 | 312 → 330 | 1.058 ⚠ | 318 → 336 | 1.057 ⚠ | 1.089 |
| `circSU2_89` | 89 | device-summit | fake_torino | O3 | 3 | 312 → 330 | 1.058 ⚠ | 318 → 336 | 1.057 ⚠ | 1.138 |
| `clifford_100` | 100 | device-summit | fake_torino | O2 | 3 | 20464 → 17680 | **0.868** | 58170 → 59680 | 1.024 | 1.056 |
| `clifford_100` | 100 | device-summit | fake_torino | O3 | 3 | 20162 → 17758 | **0.873** | 58232 → 59763 | 1.026 | 1.054 |
| `QAOA_100` | 100 | device-summit | fake_torino | O2 | 3 | 1552 → 1316 | **0.807** | 8743 → 9065 | 1.046 | 1.076 |
| `QAOA_100` | 100 | device-summit | fake_torino | O3 | 3 | 1499 → 1315 | **0.819** | 8455 → 9005 | 1.067 ⚠ | 1.092 |
| `QFT_100` | 100 | device-summit | fake_torino | O2 | 3 | 1879 → 1579 | **0.924** | 9774 → 9113 | 0.973 | 1.074 |
| `QFT_100` | 100 | device-summit | fake_torino | O3 | 3 | 1755 → 1627 | 0.956 | 9113 → 9279 | 1.015 | 1.074 |
| `QV_100` | 100 | device-summit | fake_torino | O2 | 3 | 10395 → 8658 | **0.851** | 95718 → 94509 | 0.987 | 1.071 |
| `QV_100` | 100 | device-summit | fake_torino | O3 | 3 | 10404 → 8475 | **0.815** | 95730 → 95019 | 0.994 | 1.067 |
| `square_heisenberg_100` | 100 | device-summit | fake_torino | O2 | 3 | 339 → 357 | 0.973 | 1548 → 1584 | 1.023 | 1.010 |
| `square_heisenberg_100` | 100 | device-summit | fake_torino | O3 | 3 | 342 → 336 | **0.926** | 1554 → 1485 | **0.925** | 0.977 |

Source data: [paired seeds](tables/paired_seeds.csv), [case summaries](tables/cases.csv), [full harness report](report.md).
