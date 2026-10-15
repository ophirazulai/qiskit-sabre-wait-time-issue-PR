# Quality stage improvement


- Primary D2 improvement: +21.80%. Improvement rule `CA2/improvement`: passed.
- Primary N2 improvement: +6.19%. Guard `CA3/primary/N2`: passed.

## Quality tests

One row per quality test, including guards. D2 (two-qubit depth) and N2 (two-qubit gate count) are arithmetic means over the test's frozen B0 seeds. Each improvement is 100 × (baseline mean − evolved mean) / baseline mean. These descriptive means do not change the verdict or its weighted geometric estimates, and can differ slightly from the geometric ratios under Per-case changes.

Missing or invalid seed pairs make that metric unavailable. Percentages with a zero baseline are N/A (undefined). Seeds is the expected count per revision.

| Test | Seeds | Baseline D2 | Evolved D2 | D2 improvement | Baseline N2 | Evolved N2 | N2 improvement |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| confirm/qft_n100/heavy_hex_d9_cz/L0 | 100 | 4091.96 | 2935.01 | +28.27% | 45353.64 | 43402.05 | +4.30% |
| confirm/qft_n100/heavy_hex_d9_cz/L1 | 100 | 2870.76 | 2159.07 | +24.79% | 26232.18 | 25085.37 | +4.37% |
| confirm/qft_n100/heavy_hex_d9_cz/L2 | 100 | 1823.86 | 1685.65 | +7.58% | 9563.88 | 9316.94 | +2.58% |
| confirm/qft_n100/heavy_hex_d9_cz/L3 | 100 | 1774.88 | 1652.78 | +6.88% | 9311.66 | 9171.18 | +1.51% |
| confirm/qft_cp_n14/melbourne_14_u/L0 | 100 | 209.19 | 158.62 | +24.17% | 490.37 | 449.51 | +8.33% |
| confirm/qft_cp_n14/melbourne_14_u/L1 | 100 | 141.49 | 136.56 | +3.48% | 348.35 | 347.24 | +0.32% |
| confirm/qft_cp_n14/melbourne_14_u/L2 | 100 | 120.27 | 120.28 | -0.01% | 281.29 | 285.25 | -1.41% |
| confirm/qft_cp_n14/melbourne_14_u/L3 | 100 | 118.76 | 118.96 | -0.17% | 281.33 | 283.77 | -0.87% |
| confirm/qft_full_n32/rochester_53/L0 | 100 | 898.30 | 638.56 | +28.91% | 3727.46 | 3446.57 | +7.54% |
| confirm/qft_full_n32/rochester_53/L1 | 100 | 501.23 | 473.99 | +5.43% | 2563.37 | 2528.72 | +1.35% |
| confirm/qft_full_n32/rochester_53/L2 | 100 | 380.89 | 347.95 | +8.65% | 1576.01 | 1535.09 | +2.60% |
| confirm/qft_full_n32/rochester_53/L3 | 100 | 355.54 | 347.18 | +2.35% | 1517.74 | 1520.33 | -0.17% |
| confirm/qft_cp_n8/melbourne_14_u/L0 | 100 | 80.74 | 65.15 | +19.31% | 146.84 | 140.00 | +4.66% |
| confirm/qft_cp_n8/melbourne_14_u/L1 | 100 | 58.90 | 55.84 | +5.20% | 96.68 | 97.28 | -0.62% |
| confirm/qft_cp_n8/melbourne_14_u/L2 | 100 | 51.62 | 45.29 | +12.26% | 81.28 | 79.59 | +2.08% |
| confirm/qft_cp_n8/melbourne_14_u/L3 | 100 | 47.31 | 37.53 | +20.67% | 78.21 | 75.96 | +2.88% |
| confirm/qft_full_n64/heavy_hex_d9_cz/L0 | 100 | 2183.56 | 1553.17 | +28.87% | 16596.03 | 15416.10 | +7.11% |
| confirm/qft_full_n64/heavy_hex_d9_cz/L1 | 100 | 1080.95 | 1071.93 | +0.83% | 10043.28 | 9921.42 | +1.21% |
| confirm/qft_full_n64/heavy_hex_d9_cz/L2 | 100 | 885.99 | 860.42 | +2.89% | 4534.05 | 4470.22 | +1.41% |
| confirm/qft_full_n64/heavy_hex_d9_cz/L3 | 100 | 863.12 | 857.27 | +0.68% | 4414.47 | 4377.02 | +0.85% |
| confirm/qft16_cancel/mumbai_27/L0 | 100 | 306.99 | 239.65 | +21.94% | 754.83 | 718.77 | +4.78% |
| confirm/qft16_cancel/mumbai_27/L1 | 100 | 217.25 | 195.07 | +10.21% | 578.55 | 560.43 | +3.13% |
| confirm/qft16_cancel/mumbai_27/L2 | 10 | 0.00 | 0.00 | N/A | 0.00 | 0.00 | N/A |
| confirm/qft16_cancel/mumbai_27/L3 | 10 | 0.00 | 0.00 | N/A | 0.00 | 0.00 | N/A |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L0 | 100 | 1182.27 | 873.66 | +26.10% | 5413.65 | 5621.28 | -3.84% |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L1 | 100 | 953.46 | 859.26 | +9.88% | 3656.61 | 3638.55 | +0.49% |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L2 | 100 | 401.94 | 339.57 | +15.52% | 1823.88 | 1775.28 | +2.66% |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L3 | 100 | 355.71 | 314.13 | +11.69% | 1608.93 | 1563.54 | +2.82% |
| confirm/trotter_chain_n32/rochester_53/L0 | 100 | 872.94 | 680.61 | +22.03% | 3856.44 | 3743.07 | +2.94% |
| confirm/trotter_chain_n32/rochester_53/L1 | 10 | 178.00 | 178.00 | +0.00% | 1860.00 | 1860.00 | +0.00% |
| confirm/trotter_chain_n32/rochester_53/L2 | 10 | 178.00 | 178.00 | +0.00% | 1860.00 | 1860.00 | +0.00% |
| confirm/trotter_chain_n32/rochester_53/L3 | 10 | 178.00 | 178.00 | +0.00% | 1860.00 | 1860.00 | +0.00% |
| confirm/trotter_chain_n16/mumbai_27/L0 | 100 | 528.19 | 423.25 | +19.87% | 1635.81 | 1512.24 | +7.55% |
| confirm/trotter_chain_n16/mumbai_27/L1 | 10 | 146.00 | 146.00 | +0.00% | 900.00 | 900.00 | +0.00% |
| confirm/trotter_chain_n16/mumbai_27/L2 | 10 | 146.00 | 146.00 | +0.00% | 900.00 | 900.00 | +0.00% |
| confirm/trotter_chain_n16/mumbai_27/L3 | 10 | 146.00 | 146.00 | +0.00% | 900.00 | 900.00 | +0.00% |
| confirm/dtc_n100/heavy_hex_d9_cz/L0 | 100 | 3823.42 | 2945.32 | +22.97% | 52496.61 | 57438.93 | -9.41% |
| confirm/dtc_n100/heavy_hex_d9_cz/L1 | 10 | 400.00 | 400.00 | +0.00% | 19800.00 | 19800.00 | +0.00% |
| confirm/dtc_n100/heavy_hex_d9_cz/L2 | 10 | 400.00 | 400.00 | +0.00% | 19800.00 | 19800.00 | +0.00% |
| confirm/dtc_n100/heavy_hex_d9_cz/L3 | 10 | 400.00 | 400.00 | +0.00% | 19800.00 | 19800.00 | +0.00% |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L0 | 100 | 2227.18 | 1123.58 | +49.55% | 14710.14 | 14328.78 | +2.59% |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L1 | 100 | 1648.19 | 1371.48 | +16.79% | 9056.64 | 9418.89 | -4.00% |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L2 | 100 | 1531.56 | 1284.71 | +16.12% | 8610.32 | 9005.52 | -4.59% |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L3 | 100 | 1517.19 | 1284.88 | +15.31% | 8522.39 | 8940.49 | -4.91% |
| confirm/qaoa_complete_n8/mumbai_27/L0 | 100 | 691.36 | 589.50 | +14.73% | 1083.21 | 1063.08 | +1.86% |
| confirm/qaoa_complete_n8/mumbai_27/L1 | 100 | 540.33 | 450.21 | +16.68% | 891.24 | 859.54 | +3.56% |
| confirm/qaoa_complete_n8/mumbai_27/L2 | 100 | 497.24 | 394.54 | +20.65% | 787.62 | 710.47 | +9.80% |
| confirm/qaoa_complete_n8/mumbai_27/L3 | 100 | 498.85 | 394.54 | +20.91% | 788.26 | 710.47 | +9.87% |
| confirm/qaoa_complete_n16/mumbai_27/L0 | 100 | 2111.17 | 1647.95 | +21.94% | 6387.93 | 6225.39 | +2.54% |
| confirm/qaoa_complete_n16/mumbai_27/L1 | 100 | 1279.26 | 1205.12 | +5.80% | 4634.46 | 4577.90 | +1.22% |
| confirm/qaoa_complete_n16/mumbai_27/L2 | 100 | 1106.06 | 1060.83 | +4.09% | 3750.94 | 3676.16 | +1.99% |
| confirm/qaoa_complete_n16/mumbai_27/L3 | 100 | 1115.30 | 1032.47 | +7.43% | 3769.04 | 3664.89 | +2.76% |
| confirm/qaoa_complete_n32/rochester_53/L0 | 100 | 5952.62 | 4550.85 | +23.55% | 33532.26 | 32647.89 | +2.64% |
| confirm/qaoa_complete_n32/rochester_53/L1 | 100 | 2581.07 | 2559.16 | +0.85% | 19837.29 | 20323.32 | -2.45% |
| confirm/qaoa_complete_n32/rochester_53/L2 | 100 | 2176.55 | 2017.97 | +7.29% | 15163.06 | 14875.32 | +1.90% |
| confirm/qaoa_complete_n32/rochester_53/L3 | 100 | 2218.41 | 2020.37 | +8.93% | 15195.38 | 14876.02 | +2.10% |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L0 | 100 | 2781.00 | 1931.97 | +30.53% | 20346.09 | 19771.02 | +2.83% |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L1 | 100 | 2714.28 | 2340.06 | +13.79% | 17051.55 | 16776.48 | +1.61% |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L2 | 100 | 2560.56 | 2220.87 | +13.27% | 16200.54 | 15981.72 | +1.35% |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L3 | 100 | 2556.63 | 2216.04 | +13.32% | 16195.44 | 15955.65 | +1.48% |
| confirm/qv_n14_d14/melbourne_14/L0 | 100 | 257.64 | 199.35 | +22.62% | 696.63 | 689.13 | +1.08% |
| confirm/qv_n14_d14/melbourne_14/L1 | 100 | 206.58 | 191.73 | +7.19% | 575.01 | 575.16 | -0.03% |
| confirm/qv_n14_d14/melbourne_14/L2 | 100 | 187.74 | 177.63 | +5.39% | 532.05 | 533.01 | -0.18% |
| confirm/qv_n14_d14/melbourne_14/L3 | 100 | 191.49 | 175.08 | +8.57% | 533.52 | 531.93 | +0.30% |
| confirm/qv_n27_d27/mumbai_27_loose/L0 | 100 | 884.91 | 680.70 | +23.08% | 3828.57 | 3796.11 | +0.85% |
| confirm/qv_n27_d27/mumbai_27_loose/L1 | 100 | 776.01 | 722.04 | +6.95% | 3314.43 | 3297.93 | +0.50% |
| confirm/qv_n27_d27/mumbai_27_loose/L2 | 100 | 722.76 | 671.97 | +7.03% | 3083.61 | 3056.10 | +0.89% |
| confirm/qv_n27_d27/mumbai_27_loose/L3 | 100 | 722.10 | 665.97 | +7.77% | 3093.36 | 3062.16 | +1.01% |
| confirm/qv_n50_d20/rochester_53_u/L0 | 100 | 1141.26 | 814.50 | +28.63% | 8047.32 | 8017.53 | +0.37% |
| confirm/qv_n50_d20/rochester_53_u/L1 | 100 | 1048.11 | 934.74 | +10.82% | 6745.92 | 6720.60 | +0.38% |
| confirm/qv_n50_d20/rochester_53_u/L2 | 100 | 996.69 | 874.83 | +12.23% | 6392.25 | 6353.07 | +0.61% |
| confirm/qv_n50_d20/rochester_53_u/L3 | 100 | 988.65 | 876.21 | +11.37% | 6388.38 | 6350.76 | +0.59% |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L0 | 100 | 242.88 | 203.31 | +16.29% | 774.69 | 751.56 | +2.99% |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L1 | 100 | 200.43 | 193.32 | +3.55% | 641.73 | 643.83 | -0.33% |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L2 | 100 | 180.99 | 176.25 | +2.62% | 575.55 | 582.87 | -1.27% |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L3 | 100 | 178.47 | 176.61 | +1.04% | 572.97 | 580.62 | -1.34% |
| confirm/ripple_adder_10/grid_5x5_u/L0 | 100 | 312.57 | 209.83 | +32.87% | 522.15 | 513.69 | +1.62% |
| confirm/ripple_adder_10/grid_5x5_u/L1 | 100 | 243.92 | 220.56 | +9.58% | 400.96 | 394.47 | +1.62% |
| confirm/ripple_adder_10/grid_5x5_u/L2 | 100 | 206.02 | 197.41 | +4.18% | 349.95 | 359.14 | -2.63% |
| confirm/ripple_adder_10/grid_5x5_u/L3 | 100 | 201.73 | 196.04 | +2.82% | 347.77 | 355.32 | -2.17% |
| confirm/mcx_kg24_n6/mumbai_27/L0 | 100 | 48.19 | 42.12 | +12.60% | 57.21 | 63.21 | -10.49% |
| confirm/mcx_kg24_n6/mumbai_27/L1 | 100 | 28.95 | 28.89 | +0.21% | 32.79 | 32.73 | +0.18% |
| confirm/mcx_kg24_n6/mumbai_27/L2 | 100 | 23.85 | 23.84 | +0.04% | 27.04 | 27.00 | +0.15% |
| confirm/mcx_kg24_n6/mumbai_27/L3 | 100 | 23.85 | 23.84 | +0.04% | 27.04 | 27.00 | +0.15% |
| confirm/mcx_kg24_n5/mumbai_27/L0 | 100 | 19.43 | 18.06 | +7.05% | 23.19 | 22.32 | +3.75% |
| confirm/mcx_kg24_n5/mumbai_27/L1 | 10 | 14.00 | 14.00 | +0.00% | 15.00 | 15.00 | +0.00% |
| confirm/mcx_kg24_n5/mumbai_27/L2 | 10 | 14.00 | 14.00 | +0.00% | 15.00 | 15.00 | +0.00% |
| confirm/mcx_kg24_n5/mumbai_27/L3 | 10 | 14.00 | 14.00 | +0.00% | 15.00 | 15.00 | +0.00% |
| confirm/multiplier_h18_n32/rochester_53/L0 | 100 | 9855.77 | 7189.91 | +27.05% | 14421.67 | 11928.58 | +17.29% |
| confirm/multiplier_h18_n32/rochester_53/L1 | 100 | 6995.49 | 6758.33 | +3.39% | 9697.23 | 9401.42 | +3.05% |
| confirm/multiplier_h18_n32/rochester_53/L2 | 100 | 6048.58 | 5803.35 | +4.05% | 8394.16 | 8129.60 | +3.15% |
| confirm/multiplier_h18_n32/rochester_53/L3 | 100 | 6044.97 | 5804.61 | +3.98% | 8383.71 | 8121.32 | +3.13% |
| confirm/mcx_kg24_n16/mumbai_27/L0 | 100 | 271.35 | 200.37 | +26.16% | 413.46 | 470.88 | -13.89% |
| confirm/mcx_kg24_n16/mumbai_27/L1 | 100 | 137.04 | 140.81 | -2.75% | 202.05 | 206.40 | -2.15% |
| confirm/mcx_kg24_n16/mumbai_27/L2 | 100 | 117.85 | 117.68 | +0.14% | 166.39 | 167.89 | -0.90% |
| confirm/mcx_kg24_n16/mumbai_27/L3 | 100 | 117.81 | 117.79 | +0.02% | 166.08 | 167.19 | -0.67% |
| confirm/ripple_adder_20/grid_7x7_u/L0 | 100 | 686.87 | 454.94 | +33.77% | 1288.56 | 1279.50 | +0.70% |
| confirm/ripple_adder_20/grid_7x7_u/L1 | 100 | 536.77 | 494.23 | +7.93% | 896.52 | 891.50 | +0.56% |
| confirm/ripple_adder_20/grid_7x7_u/L2 | 100 | 460.54 | 451.76 | +1.91% | 797.93 | 822.09 | -3.03% |
| confirm/ripple_adder_20/grid_7x7_u/L3 | 100 | 450.97 | 441.73 | +2.05% | 786.23 | 803.92 | -2.25% |
| confirm/adder_modular_v17_n8/mumbai_27/L0 | 100 | 135.31 | 106.16 | +21.54% | 178.38 | 173.22 | +2.89% |
| confirm/adder_modular_v17_n8/mumbai_27/L1 | 100 | 88.18 | 86.54 | +1.86% | 107.33 | 106.77 | +0.52% |
| confirm/adder_modular_v17_n8/mumbai_27/L2 | 100 | 70.86 | 67.77 | +4.36% | 89.92 | 90.24 | -0.36% |
| confirm/adder_modular_v17_n8/mumbai_27/L3 | 100 | 70.70 | 67.77 | +4.14% | 89.90 | 90.24 | -0.38% |
| confirm/adder_modular_v17_n16/mumbai_27/L0 | 100 | 382.68 | 254.64 | +33.46% | 573.73 | 613.30 | -6.90% |
| confirm/adder_modular_v17_n16/mumbai_27/L1 | 100 | 297.41 | 294.24 | +1.07% | 344.78 | 352.96 | -2.37% |
| confirm/adder_modular_v17_n16/mumbai_27/L2 | 100 | 249.74 | 247.85 | +0.76% | 295.64 | 297.02 | -0.47% |
| confirm/adder_modular_v17_n16/mumbai_27/L3 | 100 | 247.04 | 245.05 | +0.81% | 289.44 | 285.02 | +1.53% |
| confirm/adder_modular_v17_n32/rochester_53/L0 | 100 | 1026.64 | 551.85 | +46.25% | 1697.28 | 1665.48 | +1.87% |
| confirm/adder_modular_v17_n32/rochester_53/L1 | 100 | 709.68 | 703.65 | +0.85% | 853.78 | 852.97 | +0.09% |
| confirm/adder_modular_v17_n32/rochester_53/L2 | 100 | 602.65 | 588.55 | +2.34% | 723.80 | 713.30 | +1.45% |
| confirm/adder_modular_v17_n32/rochester_53/L3 | 100 | 587.11 | 580.25 | +1.17% | 702.23 | 694.25 | +1.14% |
| confirm/multiplier_h18_n16/mumbai_27/L0 | 100 | 2305.24 | 1749.97 | +24.09% | 3243.08 | 2789.03 | +14.00% |
| confirm/multiplier_h18_n16/mumbai_27/L1 | 100 | 1631.41 | 1594.21 | +2.28% | 2127.51 | 2084.84 | +2.01% |
| confirm/multiplier_h18_n16/mumbai_27/L2 | 100 | 1387.24 | 1356.89 | +2.19% | 1804.00 | 1777.87 | +1.45% |
| confirm/multiplier_h18_n16/mumbai_27/L3 | 100 | 1387.54 | 1361.83 | +1.85% | 1801.08 | 1780.42 | +1.15% |
| confirm/adder_modular_v17_n6/mumbai_27/L0 | 100 | 77.99 | 67.40 | +13.58% | 92.06 | 86.51 | +6.03% |
| confirm/adder_modular_v17_n6/mumbai_27/L1 | 100 | 52.26 | 50.50 | +3.37% | 60.39 | 60.05 | +0.56% |
| confirm/adder_modular_v17_n6/mumbai_27/L2 | 100 | 40.92 | 40.09 | +2.03% | 45.66 | 45.56 | +0.22% |
| confirm/adder_modular_v17_n6/mumbai_27/L3 | 100 | 40.93 | 40.09 | +2.05% | 45.66 | 45.56 | +0.22% |
| confirm/multiplier_h18_n20/heavy_hex_d9_cz/L2 | 100 | 2296.31 | 2224.52 | +3.13% | 3092.49 | 3016.80 | +2.45% |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L0 | 100 | 927.11 | 377.06 | +59.33% | 1659.81 | 2586.66 | -55.84% |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L1 | 100 | 755.92 | 406.56 | +46.22% | 901.86 | 650.61 | +27.86% |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L2 | 100 | 649.53 | 295.01 | +54.58% | 802.43 | 513.39 | +36.02% |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L3 | 100 | 563.23 | 257.17 | +54.34% | 660.36 | 337.21 | +48.94% |
| confirm/bv_all_ones_n16/mumbai_27/L0 | 100 | 76.00 | 58.40 | +23.16% | 109.89 | 135.63 | -23.42% |
| confirm/bv_all_ones_n16/mumbai_27/L1 | 100 | 51.15 | 50.14 | +1.97% | 56.76 | 55.80 | +1.69% |
| confirm/bv_all_ones_n16/mumbai_27/L2 | 100 | 49.34 | 48.77 | +1.16% | 53.50 | 52.65 | +1.59% |
| confirm/bv_all_ones_n16/mumbai_27/L3 | 100 | 49.53 | 48.60 | +1.88% | 53.34 | 52.62 | +1.35% |
| confirm/bv_all_ones_n50/rochester_53/L0 | 100 | 304.10 | 191.24 | +37.11% | 476.44 | 715.33 | -50.14% |
| confirm/bv_all_ones_n50/rochester_53/L1 | 100 | 219.67 | 216.32 | +1.53% | 224.68 | 222.04 | +1.18% |
| confirm/bv_all_ones_n50/rochester_53/L2 | 100 | 192.02 | 187.85 | +2.17% | 196.86 | 193.29 | +1.81% |
| confirm/bv_all_ones_n50/rochester_53/L3 | 100 | 193.78 | 190.01 | +1.95% | 199.74 | 196.35 | +1.70% |
| confirm/bvlike_n100/heavy_hex_d9_cz/L0 | 100 | 1686.67 | 696.47 | +58.71% | 2996.94 | 3907.44 | -30.38% |
| confirm/bvlike_n100/heavy_hex_d9_cz/L1 | 100 | 1308.72 | 756.05 | +42.23% | 1519.80 | 934.11 | +38.54% |
| confirm/bvlike_n100/heavy_hex_d9_cz/L2 | 10 | 0.00 | 0.00 | N/A | 0.00 | 0.00 | N/A |
| confirm/bvlike_n100/heavy_hex_d9_cz/L3 | 10 | 0.00 | 0.00 | N/A | 0.00 | 0.00 | N/A |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L0 | 100 | 1787.71 | 650.22 | +63.63% | 3214.47 | 4386.60 | -36.46% |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L1 | 100 | 1460.59 | 569.13 | +61.03% | 1723.56 | 901.50 | +47.70% |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L2 | 100 | 1400.54 | 552.01 | +60.59% | 1640.53 | 836.20 | +49.03% |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L3 | 10 | 1239.60 | 502.90 | +59.43% | 1419.30 | 711.00 | +49.90% |
| confirm/ring_random_n8/melbourne_14_u/L0 | 100 | 86.75 | 73.10 | +15.73% | 189.61 | 200.20 | -5.59% |
| confirm/ring_random_n8/melbourne_14_u/L1 | 10 | 16.00 | 16.00 | +0.00% | 64.00 | 64.00 | +0.00% |
| confirm/ring_random_n8/melbourne_14_u/L2 | 10 | 16.00 | 16.00 | +0.00% | 64.00 | 64.00 | +0.00% |
| confirm/ring_random_n8/melbourne_14_u/L3 | 10 | 16.00 | 16.00 | +0.00% | 64.00 | 64.00 | +0.00% |
| confirm/ring_random_n14/melbourne_14_u/L0 | 100 | 104.97 | 103.28 | +1.61% | 316.33 | 310.72 | +1.77% |
| confirm/ring_random_n14/melbourne_14_u/L1 | 10 | 84.00 | 84.00 | +0.00% | 280.00 | 280.00 | +0.00% |
| confirm/ring_random_n14/melbourne_14_u/L2 | 10 | 84.00 | 84.00 | +0.00% | 280.00 | 280.00 | +0.00% |
| confirm/ring_random_n14/melbourne_14_u/L3 | 10 | 84.00 | 84.00 | +0.00% | 280.00 | 280.00 | +0.00% |
| confirm/su2_circular_n100/heavy_hex_d9_cz/L0 | 100 | 2200.24 | 742.61 | +66.25% | 4004.40 | 4696.11 | -17.27% |
| confirm/su2_circular_n100/heavy_hex_d9_cz/L1 | 10 | 300.00 | 300.00 | +0.00% | 300.00 | 300.00 | +0.00% |
| confirm/su2_circular_n100/heavy_hex_d9_cz/L2 | 10 | 300.00 | 300.00 | +0.00% | 300.00 | 300.00 | +0.00% |
| confirm/su2_circular_n100/heavy_hex_d9_cz/L3 | 10 | 300.00 | 300.00 | +0.00% | 300.00 | 300.00 | +0.00% |
| confirm/queko_bss_53+sabre/rochester_53/L0 | 100 | 507.71 | 439.62 | +13.41% | 2767.79 | 2747.06 | +0.75% |
| confirm/queko_bss_53+sabre/rochester_53/L1 | 100 | 373.13 | 307.34 | +17.63% | 1901.88 | 1832.26 | +3.66% |
| confirm/queko_bss_53+sabre/rochester_53/L2 | 100 | 230.24 | 204.35 | +11.24% | 1104.81 | 1112.28 | -0.68% |
| confirm/queko_bss_53+sabre/rochester_53/L3 | 100 | 197.72 | 180.64 | +8.64% | 947.01 | 948.38 | -0.14% |
| confirm/queko_bigd_20+sabre/tokyo_20/L0 | 100 | 56.56 | 55.07 | +2.63% | 62.31 | 63.12 | -1.30% |
| confirm/queko_bigd_20+sabre/tokyo_20/L1 | 100 | 31.17 | 29.23 | +6.22% | 34.08 | 33.28 | +2.35% |
| confirm/queko_bigd_20+sabre/tokyo_20/L2 | 100 | 20.39 | 20.14 | +1.23% | 21.72 | 22.98 | -5.80% |
| confirm/queko_bigd_20+sabre/tokyo_20/L3 | 100 | 19.77 | 19.82 | -0.25% | 21.25 | 22.54 | -6.07% |
| confirm/queko_bntf_54+sabre/sycamore_54/L0 | 100 | 157.60 | 125.46 | +20.39% | 814.05 | 776.97 | +4.56% |
| confirm/queko_bntf_54+sabre/sycamore_54/L1 | 100 | 111.97 | 87.85 | +21.54% | 574.45 | 557.15 | +3.01% |
| confirm/queko_bntf_54+sabre/sycamore_54/L2 | 100 | 96.73 | 77.72 | +19.65% | 486.45 | 476.36 | +2.07% |
| confirm/queko_bntf_54+sabre/sycamore_54/L3 | 100 | 84.06 | 67.21 | +20.05% | 441.75 | 418.84 | +5.19% |
| confirm/queko_bss_53/rochester_53/L0 | 100 | 899.63 | 651.82 | +27.55% | 5929.85 | 6311.33 | -6.43% |
| confirm/queko_bss_53/rochester_53/L1 | 10 | 56.00 | 56.00 | +0.00% | 647.00 | 647.00 | +0.00% |
| confirm/queko_bss_53/rochester_53/L2 | 10 | 46.00 | 46.00 | +0.00% | 363.00 | 363.00 | +0.00% |
| confirm/queko_bss_53/rochester_53/L3 | 10 | 46.00 | 46.00 | +0.00% | 355.00 | 355.00 | +0.00% |
| confirm/queko_bigd_20/tokyo_20/L0 | 100 | 82.97 | 64.94 | +21.73% | 99.48 | 96.42 | +3.08% |
| confirm/queko_bigd_20/tokyo_20/L1 | 10 | 23.00 | 23.00 | +0.00% | 23.00 | 23.00 | +0.00% |
| confirm/queko_bigd_20/tokyo_20/L2 | 10 | 17.00 | 17.00 | +0.00% | 17.00 | 17.00 | +0.00% |
| confirm/queko_bigd_20/tokyo_20/L3 | 10 | 17.00 | 17.00 | +0.00% | 17.00 | 17.00 | +0.00% |
| confirm/queko_bntf_54/sycamore_54/L0 | 100 | 338.78 | 212.67 | +37.22% | 1670.76 | 1655.64 | +0.90% |
| confirm/queko_bntf_54/sycamore_54/L1 | 10 | 18.00 | 18.00 | +0.00% | 190.00 | 190.00 | +0.00% |
| confirm/queko_bntf_54/sycamore_54/L2 | 10 | 18.00 | 18.00 | +0.00% | 172.00 | 172.00 | +0.00% |
| confirm/queko_bntf_54/sycamore_54/L3 | 10 | 18.00 | 18.00 | +0.00% | 172.00 | 172.00 | +0.00% |
| confirm/long_2q_sequence/rochester_53_u/L2 | 10 | 3.00 | 3.00 | +0.00% | 3.00 | 3.00 | +0.00% |
| confirm/long_2q_sequence/rochester_53_u/L3 | 10 | 3.00 | 3.00 | +0.00% | 3.00 | 3.00 | +0.00% |
| confirm/a2a_qft_n16/a2a_clifford_rz_16/L0 | 10 | 58.00 | 58.00 | +0.00% | 240.00 | 240.00 | +0.00% |
| confirm/a2a_qft_n16/a2a_clifford_rz_16/L1 | 10 | 58.00 | 58.00 | +0.00% | 240.00 | 240.00 | +0.00% |
| confirm/a2a_qft_n16/a2a_clifford_rz_16/L2 | 10 | 58.00 | 58.00 | +0.00% | 238.00 | 238.00 | +0.00% |
| confirm/a2a_qft_n16/a2a_clifford_rz_16/L3 | 10 | 58.00 | 58.00 | +0.00% | 238.00 | 238.00 | +0.00% |
| confirm/a2a_trotter_n16/a2a_clifford_rz_16/L0 | 10 | 146.00 | 146.00 | +0.00% | 900.00 | 900.00 | +0.00% |
| confirm/a2a_trotter_n16/a2a_clifford_rz_16/L1 | 10 | 146.00 | 146.00 | +0.00% | 900.00 | 900.00 | +0.00% |
| confirm/a2a_trotter_n16/a2a_clifford_rz_16/L2 | 10 | 146.00 | 146.00 | +0.00% | 900.00 | 900.00 | +0.00% |
| confirm/a2a_trotter_n16/a2a_clifford_rz_16/L3 | 10 | 146.00 | 146.00 | +0.00% | 900.00 | 900.00 | +0.00% |
| confirm/a2a_qaoa_n16/a2a_clifford_rz_16/L0 | 10 | 324.00 | 324.00 | +0.00% | 2100.00 | 2100.00 | +0.00% |
| confirm/a2a_qaoa_n16/a2a_clifford_rz_16/L1 | 10 | 324.00 | 324.00 | +0.00% | 2100.00 | 2100.00 | +0.00% |
| confirm/a2a_qaoa_n16/a2a_clifford_rz_16/L2 | 10 | 324.00 | 324.00 | +0.00% | 2100.00 | 2100.00 | +0.00% |
| confirm/a2a_qaoa_n16/a2a_clifford_rz_16/L3 | 10 | 324.00 | 324.00 | +0.00% | 2100.00 | 2100.00 | +0.00% |
| confirm/a2a_multiplier_n16/a2a_clifford_rz_16/L0 | 10 | 704.00 | 704.00 | +0.00% | 806.00 | 806.00 | +0.00% |
| confirm/a2a_multiplier_n16/a2a_clifford_rz_16/L1 | 10 | 704.00 | 704.00 | +0.00% | 802.00 | 802.00 | +0.00% |
| confirm/a2a_multiplier_n16/a2a_clifford_rz_16/L2 | 10 | 696.00 | 696.00 | +0.00% | 794.00 | 794.00 | +0.00% |
| confirm/a2a_multiplier_n16/a2a_clifford_rz_16/L3 | 10 | 696.00 | 696.00 | +0.00% | 794.00 | 794.00 | +0.00% |
| confirm/a2a_adder_modular_n16/a2a_clifford_rz_16/L0 | 10 | 109.00 | 109.00 | +0.00% | 115.00 | 115.00 | +0.00% |
| confirm/a2a_adder_modular_n16/a2a_clifford_rz_16/L1 | 10 | 109.00 | 109.00 | +0.00% | 115.00 | 115.00 | +0.00% |
| confirm/a2a_adder_modular_n16/a2a_clifford_rz_16/L2 | 10 | 107.00 | 107.00 | +0.00% | 113.00 | 113.00 | +0.00% |
| confirm/a2a_adder_modular_n16/a2a_clifford_rz_16/L3 | 10 | 107.00 | 107.00 | +0.00% | 113.00 | 113.00 | +0.00% |
| confirm/a2a_mcx_n16/a2a_clifford_rz_16/L0 | 10 | 68.00 | 68.00 | +0.00% | 78.00 | 78.00 | +0.00% |
| confirm/a2a_mcx_n16/a2a_clifford_rz_16/L1 | 10 | 68.00 | 68.00 | +0.00% | 78.00 | 78.00 | +0.00% |
| confirm/a2a_mcx_n16/a2a_clifford_rz_16/L2 | 10 | 68.00 | 68.00 | +0.00% | 78.00 | 78.00 | +0.00% |
| confirm/a2a_mcx_n16/a2a_clifford_rz_16/L3 | 10 | 68.00 | 68.00 | +0.00% | 78.00 | 78.00 | +0.00% |
| confirm/qft_n100/heavy_hex_d9_cx/L2 | 100 | 1807.94 | 1666.59 | +7.82% | 9497.18 | 9226.94 | +2.85% |
| confirm/qft_n100/heavy_hex_d9_ecr/L2 | 100 | 1823.86 | 1685.65 | +7.58% | 9563.88 | 9316.94 | +2.58% |
| confirm/square_heisenberg_n100/heavy_hex_d9_cx/L2 | 100 | 401.94 | 339.57 | +15.52% | 1823.88 | 1775.28 | +2.66% |
| confirm/square_heisenberg_n100/heavy_hex_d9_ecr/L2 | 100 | 401.94 | 339.57 | +15.52% | 1823.88 | 1775.28 | +2.66% |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cx/L2 | 100 | 1526.66 | 1281.35 | +16.07% | 8591.44 | 8990.44 | -4.64% |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_ecr/L2 | 100 | 1531.56 | 1284.71 | +16.12% | 8610.32 | 9005.52 | -4.59% |

## Quality estimates

| Panel | Ratio | Paired SE (log) | Upper 2 SE | Seeds |
| --- | ---: | ---: | ---: | ---: |
| CA2/improvement | 0.781982 | 0.001483 | -0.242957 | 100 |
| CA3/primary/N2 | 0.938118 | 0.001282 | -0.061315 | 100 |
| CA3/cx/D2 | 0.867647 | 0.005356 | -0.131258 | 100 |
| CA3/cx/N2 | 0.996419 | 0.002598 | 0.001608 | 100 |
| CA3/ecr/D2 | 0.868233 | 0.005357 | -0.130580 | 100 |
| CA3/ecr/N2 | 0.997139 | 0.002629 | 0.002393 | 100 |

## Marginal quality estimates

| Dimension | Value | Metric | Ratio | Paired SE | Cases | Seeds |
| --- | --- | --- | ---: | ---: | ---: | ---: |
| family | G1 | D2 | 0.869901 | 0.004183 | 20 | 100 |
| family | G1 | N2 | 0.973521 | 0.001458 | 20 | 100 |
| family | G2 | D2 | 0.851132 | 0.005340 | 7 | 100 |
| family | G2 | N2 | 0.981142 | 0.003000 | 7 | 100 |
| family | G3 | D2 | 0.829225 | 0.004475 | 16 | 100 |
| family | G3 | N2 | 0.990691 | 0.001251 | 16 | 100 |
| family | G4 | D2 | 0.876110 | 0.002082 | 20 | 100 |
| family | G4 | N2 | 0.992988 | 0.000638 | 20 | 100 |
| family | G5 | D2 | 0.902694 | 0.001653 | 37 | 100 |
| family | G5 | N2 | 0.993311 | 0.000904 | 37 | 100 |
| family | G6 | D2 | 0.720645 | 0.002248 | 12 | 100 |
| family | G6 | N2 | 0.959435 | 0.002764 | 12 | 100 |
| family | G7 | D2 | 0.442775 | 0.005509 | 6 | 100 |
| family | G7 | N2 | 0.669625 | 0.006488 | 6 | 100 |
| family | G8 | D2 | 0.902467 | 0.006423 | 12 | 100 |
| family | G8 | N2 | 1.000384 | 0.006285 | 12 | 100 |
| native_basis | cx | D2 | 0.893108 | 0.001747 | 101 | 100 |
| native_basis | cx | N2 | 1.000080 | 0.001508 | 101 | 100 |
| native_basis | cz | D2 | 0.632670 | 0.002560 | 29 | 100 |
| native_basis | cz | N2 | 0.847157 | 0.002383 | 29 | 100 |
| optimization_level | 0 | D2 | 0.701514 | 0.001957 | 38 | 100 |
| optimization_level | 0 | N2 | 1.045859 | 0.001619 | 38 | 100 |
| optimization_level | 1 | D2 | 0.780981 | 0.002847 | 31 | 100 |
| optimization_level | 1 | N2 | 0.882643 | 0.002091 | 31 | 100 |
| optimization_level | 2 | D2 | 0.779631 | 0.002986 | 31 | 100 |
| optimization_level | 2 | N2 | 0.876249 | 0.002731 | 31 | 100 |
| optimization_level | 3 | D2 | 0.894457 | 0.003058 | 30 | 100 |
| optimization_level | 3 | N2 | 0.961249 | 0.002084 | 30 | 100 |
| size_band | large | D2 | 0.603625 | 0.002782 | 21 | 100 |
| size_band | large | N2 | 0.828319 | 0.002738 | 21 | 100 |
| size_band | medium | D2 | 0.862611 | 0.002472 | 53 | 100 |
| size_band | medium | N2 | 0.995226 | 0.001414 | 53 | 100 |
| size_band | small | D2 | 0.916609 | 0.002511 | 56 | 100 |
| size_band | small | N2 | 1.001314 | 0.002213 | 56 | 100 |
| topology | grid | D2 | 0.899218 | 0.003992 | 30 | 100 |
| topology | grid | N2 | 1.000804 | 0.003371 | 30 | 100 |
| topology | heavy_hex | D2 | 0.751986 | 0.001620 | 100 | 100 |
| topology | heavy_hex | N2 | 0.921280 | 0.001372 | 100 | 100 |

Score without the iterations profile's scored groups (report-only):
- D2 ratio 0.772201 (paired SE 0.001661; cases: 118; seeds: 100).
- N2 ratio 0.927088 (paired SE 0.001516; cases: 118; seeds: 100).

Instance bootstrap (report-only): 95% upper log effect -0.113272.
Input groups by family: G1: 5, G2: 4, G3: 4, G4: 5, G5: 10, G6: 3, G7: 4, G8: 3.


## Per-case changes

| Case / metric | Ratio | Worst seed |
| --- | ---: | ---: |
| confirm/qft_n100/heavy_hex_d9_cz/L0/D2 | 0.717031 | 68 |
| confirm/qft_n100/heavy_hex_d9_cz/L0/N2 | 0.956702 | 94 |
| confirm/qft_n100/heavy_hex_d9_cz/L1/D2 | 0.755227 | 77 |
| confirm/qft_n100/heavy_hex_d9_cz/L1/N2 | 0.956441 | 69 |
| confirm/qft_n100/heavy_hex_d9_cz/L2/D2 | 0.922930 | 64 |
| confirm/qft_n100/heavy_hex_d9_cz/L2/N2 | 0.974021 | 29 |
| confirm/qft_n100/heavy_hex_d9_cz/L3/D2 | 0.930586 | 64 |
| confirm/qft_n100/heavy_hex_d9_cz/L3/N2 | 0.984645 | 53 |
| confirm/qft_cp_n14/melbourne_14_u/L0/D2 | 0.760401 | 97 |
| confirm/qft_cp_n14/melbourne_14_u/L0/N2 | 0.916991 | 97 |
| confirm/qft_cp_n14/melbourne_14_u/L1/D2 | 0.965816 | 48 |
| confirm/qft_cp_n14/melbourne_14_u/L1/N2 | 0.996922 | 13 |
| confirm/qft_cp_n14/melbourne_14_u/L2/D2 | 1.002151 | 77 |
| confirm/qft_cp_n14/melbourne_14_u/L2/N2 | 1.014825 | 98 |
| confirm/qft_cp_n14/melbourne_14_u/L3/D2 | 1.003215 | 90 |
| confirm/qft_cp_n14/melbourne_14_u/L3/N2 | 1.009157 | 5 |
| confirm/qft_full_n32/rochester_53/L0/D2 | 0.710467 | 82 |
| confirm/qft_full_n32/rochester_53/L0/N2 | 0.924559 | 82 |
| confirm/qft_full_n32/rochester_53/L1/D2 | 0.947956 | 13 |
| confirm/qft_full_n32/rochester_53/L1/N2 | 0.986398 | 4 |
| confirm/qft_full_n32/rochester_53/L2/D2 | 0.918468 | 97 |
| confirm/qft_full_n32/rochester_53/L2/N2 | 0.974219 | 28 |
| confirm/qft_full_n32/rochester_53/L3/D2 | 0.980409 | 65 |
| confirm/qft_full_n32/rochester_53/L3/N2 | 1.001603 | 65 |
| confirm/qft_cp_n8/melbourne_14_u/L0/D2 | 0.809110 | 19 |
| confirm/qft_cp_n8/melbourne_14_u/L0/N2 | 0.954054 | 7 |
| confirm/qft_cp_n8/melbourne_14_u/L1/D2 | 0.943284 | 62 |
| confirm/qft_cp_n8/melbourne_14_u/L1/N2 | 1.006299 | 48 |
| confirm/qft_cp_n8/melbourne_14_u/L2/D2 | 0.871032 | 43 |
| confirm/qft_cp_n8/melbourne_14_u/L2/N2 | 0.979225 | 43 |
| confirm/qft_cp_n8/melbourne_14_u/L3/D2 | 0.796082 | 45 |
| confirm/qft_cp_n8/melbourne_14_u/L3/N2 | 0.971206 | 54 |
| confirm/qft_full_n64/heavy_hex_d9_cz/L0/D2 | 0.710254 | 38 |
| confirm/qft_full_n64/heavy_hex_d9_cz/L0/N2 | 0.928493 | 94 |
| confirm/qft_full_n64/heavy_hex_d9_cz/L1/D2 | 0.998842 | 86 |
| confirm/qft_full_n64/heavy_hex_d9_cz/L1/N2 | 0.987905 | 96 |
| confirm/qft_full_n64/heavy_hex_d9_cz/L2/D2 | 0.971290 | 15 |
| confirm/qft_full_n64/heavy_hex_d9_cz/L2/N2 | 0.985599 | 69 |
| confirm/qft_full_n64/heavy_hex_d9_cz/L3/D2 | 0.998221 | 94 |
| confirm/qft_full_n64/heavy_hex_d9_cz/L3/N2 | 0.991550 | 94 |
| confirm/qft16_cancel/mumbai_27/L0/D2 | 0.780447 | 67 |
| confirm/qft16_cancel/mumbai_27/L0/N2 | 0.952394 | 67 |
| confirm/qft16_cancel/mumbai_27/L1/D2 | 0.898212 | 65 |
| confirm/qft16_cancel/mumbai_27/L1/N2 | 0.968651 | 50 |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L0/D2 | 0.738880 | 77 |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L0/N2 | 1.038349 | 3 |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L1/D2 | 0.901408 | 36 |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L1/N2 | 0.995056 | 21 |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L2/D2 | 0.845432 | 47 |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L2/N2 | 0.973195 | 28 |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L3/D2 | 0.882990 | 77 |
| confirm/square_heisenberg_n100/heavy_hex_d9_cz/L3/N2 | 0.971384 | 70 |
| confirm/trotter_chain_n32/rochester_53/L0/D2 | 0.780809 | 63 |
| confirm/trotter_chain_n32/rochester_53/L0/N2 | 0.969024 | 67 |
| confirm/trotter_chain_n16/mumbai_27/L0/D2 | 0.803427 | 56 |
| confirm/trotter_chain_n16/mumbai_27/L0/N2 | 0.925722 | 2 |
| confirm/dtc_n100/heavy_hex_d9_cz/L0/D2 | 0.773817 | 12 |
| confirm/dtc_n100/heavy_hex_d9_cz/L0/N2 | 1.093864 | 13 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L0/D2 | 0.504516 | 40 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L0/N2 | 0.974062 | 64 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L1/D2 | 0.831903 | 0 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L1/N2 | 1.040026 | 77 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L2/D2 | 0.838805 | 90 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L2/N2 | 1.045921 | 93 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L3/D2 | 0.846761 | 59 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cz/L3/N2 | 1.049059 | 4 |
| confirm/qaoa_complete_n8/mumbai_27/L0/D2 | 0.853144 | 75 |
| confirm/qaoa_complete_n8/mumbai_27/L0/N2 | 0.981523 | 26 |
| confirm/qaoa_complete_n8/mumbai_27/L1/D2 | 0.829124 | 16 |
| confirm/qaoa_complete_n8/mumbai_27/L1/N2 | 0.963750 | 83 |
| confirm/qaoa_complete_n8/mumbai_27/L2/D2 | 0.791213 | 42 |
| confirm/qaoa_complete_n8/mumbai_27/L2/N2 | 0.901411 | 51 |
| confirm/qaoa_complete_n8/mumbai_27/L3/D2 | 0.788455 | 42 |
| confirm/qaoa_complete_n8/mumbai_27/L3/N2 | 0.900662 | 51 |
| confirm/qaoa_complete_n16/mumbai_27/L0/D2 | 0.780380 | 46 |
| confirm/qaoa_complete_n16/mumbai_27/L0/N2 | 0.974436 | 64 |
| confirm/qaoa_complete_n16/mumbai_27/L1/D2 | 0.954422 | 46 |
| confirm/qaoa_complete_n16/mumbai_27/L1/N2 | 0.988080 | 47 |
| confirm/qaoa_complete_n16/mumbai_27/L2/D2 | 0.964859 | 58 |
| confirm/qaoa_complete_n16/mumbai_27/L2/N2 | 0.980594 | 52 |
| confirm/qaoa_complete_n16/mumbai_27/L3/D2 | 0.934120 | 66 |
| confirm/qaoa_complete_n16/mumbai_27/L3/N2 | 0.973628 | 66 |
| confirm/qaoa_complete_n32/rochester_53/L0/D2 | 0.761098 | 96 |
| confirm/qaoa_complete_n32/rochester_53/L0/N2 | 0.972375 | 34 |
| confirm/qaoa_complete_n32/rochester_53/L1/D2 | 0.997053 | 76 |
| confirm/qaoa_complete_n32/rochester_53/L1/N2 | 1.024509 | 62 |
| confirm/qaoa_complete_n32/rochester_53/L2/D2 | 0.933646 | 85 |
| confirm/qaoa_complete_n32/rochester_53/L2/N2 | 0.981127 | 69 |
| confirm/qaoa_complete_n32/rochester_53/L3/D2 | 0.919483 | 5 |
| confirm/qaoa_complete_n32/rochester_53/L3/N2 | 0.979192 | 5 |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L0/D2 | 0.694791 | 4 |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L0/N2 | 0.971731 | 81 |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L1/D2 | 0.862226 | 26 |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L1/N2 | 0.983879 | 84 |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L2/D2 | 0.867361 | 84 |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L2/N2 | 0.986502 | 12 |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L3/D2 | 0.866971 | 50 |
| confirm/qv_n50_d50/heavy_hex_d9_cz/L3/N2 | 0.985204 | 21 |
| confirm/qv_n14_d14/melbourne_14/L0/D2 | 0.775139 | 72 |
| confirm/qv_n14_d14/melbourne_14/L0/N2 | 0.989150 | 20 |
| confirm/qv_n14_d14/melbourne_14/L1/D2 | 0.928456 | 74 |
| confirm/qv_n14_d14/melbourne_14/L1/N2 | 1.000304 | 69 |
| confirm/qv_n14_d14/melbourne_14/L2/D2 | 0.945144 | 55 |
| confirm/qv_n14_d14/melbourne_14/L2/N2 | 1.001781 | 6 |
| confirm/qv_n14_d14/melbourne_14/L3/D2 | 0.914397 | 66 |
| confirm/qv_n14_d14/melbourne_14/L3/N2 | 0.997083 | 18 |
| confirm/qv_n27_d27/mumbai_27_loose/L0/D2 | 0.769567 | 74 |
| confirm/qv_n27_d27/mumbai_27_loose/L0/N2 | 0.991588 | 20 |
| confirm/qv_n27_d27/mumbai_27_loose/L1/D2 | 0.930222 | 10 |
| confirm/qv_n27_d27/mumbai_27_loose/L1/N2 | 0.995025 | 31 |
| confirm/qv_n27_d27/mumbai_27_loose/L2/D2 | 0.929538 | 97 |
| confirm/qv_n27_d27/mumbai_27_loose/L2/N2 | 0.991057 | 4 |
| confirm/qv_n27_d27/mumbai_27_loose/L3/D2 | 0.922441 | 7 |
| confirm/qv_n27_d27/mumbai_27_loose/L3/N2 | 0.989903 | 75 |
| confirm/qv_n50_d20/rochester_53_u/L0/D2 | 0.713921 | 25 |
| confirm/qv_n50_d20/rochester_53_u/L0/N2 | 0.996296 | 63 |
| confirm/qv_n50_d20/rochester_53_u/L1/D2 | 0.892040 | 19 |
| confirm/qv_n50_d20/rochester_53_u/L1/N2 | 0.996262 | 96 |
| confirm/qv_n50_d20/rochester_53_u/L2/D2 | 0.877937 | 28 |
| confirm/qv_n50_d20/rochester_53_u/L2/N2 | 0.993875 | 40 |
| confirm/qv_n50_d20/rochester_53_u/L3/D2 | 0.886349 | 40 |
| confirm/qv_n50_d20/rochester_53_u/L3/N2 | 0.994115 | 88 |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L0/D2 | 0.837503 | 58 |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L0/N2 | 0.970138 | 58 |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L1/D2 | 0.965467 | 5 |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L1/N2 | 1.003212 | 54 |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L2/D2 | 0.974200 | 3 |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L2/N2 | 1.012639 | 6 |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L3/D2 | 0.989784 | 71 |
| confirm/qv_n14_d14_s10/mumbai_27_loose/L3/N2 | 1.013263 | 43 |
| confirm/ripple_adder_10/grid_5x5_u/L0/D2 | 0.673438 | 94 |
| confirm/ripple_adder_10/grid_5x5_u/L0/N2 | 0.984166 | 64 |
| confirm/ripple_adder_10/grid_5x5_u/L1/D2 | 0.907310 | 83 |
| confirm/ripple_adder_10/grid_5x5_u/L1/N2 | 0.983853 | 45 |
| confirm/ripple_adder_10/grid_5x5_u/L2/D2 | 0.959699 | 28 |
| confirm/ripple_adder_10/grid_5x5_u/L2/N2 | 1.026045 | 55 |
| confirm/ripple_adder_10/grid_5x5_u/L3/D2 | 0.970690 | 37 |
| confirm/ripple_adder_10/grid_5x5_u/L3/N2 | 1.021572 | 1 |
| confirm/mcx_kg24_n6/mumbai_27/L0/D2 | 0.878530 | 21 |
| confirm/mcx_kg24_n6/mumbai_27/L0/N2 | 1.112836 | 35 |
| confirm/mcx_kg24_n6/mumbai_27/L1/D2 | 0.997995 | 0 |
| confirm/mcx_kg24_n6/mumbai_27/L1/N2 | 0.998178 | 0 |
| confirm/mcx_kg24_n6/mumbai_27/L2/D2 | 0.999608 | 49 |
| confirm/mcx_kg24_n6/mumbai_27/L2/N2 | 0.998666 | 49 |
| confirm/mcx_kg24_n6/mumbai_27/L3/D2 | 0.999608 | 49 |
| confirm/mcx_kg24_n6/mumbai_27/L3/N2 | 0.998666 | 49 |
| confirm/mcx_kg24_n5/mumbai_27/L0/D2 | 0.937322 | 40 |
| confirm/mcx_kg24_n5/mumbai_27/L0/N2 | 0.963772 | 40 |
| confirm/multiplier_h18_n32/rochester_53/L0/D2 | 0.729550 | 6 |
| confirm/multiplier_h18_n32/rochester_53/L0/N2 | 0.827233 | 26 |
| confirm/multiplier_h18_n32/rochester_53/L1/D2 | 0.966129 | 15 |
| confirm/multiplier_h18_n32/rochester_53/L1/N2 | 0.969592 | 14 |
| confirm/multiplier_h18_n32/rochester_53/L2/D2 | 0.959480 | 35 |
| confirm/multiplier_h18_n32/rochester_53/L2/N2 | 0.968603 | 71 |
| confirm/multiplier_h18_n32/rochester_53/L3/D2 | 0.960267 | 74 |
| confirm/multiplier_h18_n32/rochester_53/L3/N2 | 0.968738 | 8 |
| confirm/mcx_kg24_n16/mumbai_27/L0/D2 | 0.740823 | 13 |
| confirm/mcx_kg24_n16/mumbai_27/L0/N2 | 1.142200 | 13 |
| confirm/mcx_kg24_n16/mumbai_27/L1/D2 | 1.027046 | 56 |
| confirm/mcx_kg24_n16/mumbai_27/L1/N2 | 1.021245 | 56 |
| confirm/mcx_kg24_n16/mumbai_27/L2/D2 | 0.998263 | 70 |
| confirm/mcx_kg24_n16/mumbai_27/L2/N2 | 1.008493 | 70 |
| confirm/mcx_kg24_n16/mumbai_27/L3/D2 | 0.999272 | 70 |
| confirm/mcx_kg24_n16/mumbai_27/L3/N2 | 1.006166 | 70 |
| confirm/ripple_adder_20/grid_7x7_u/L0/D2 | 0.663827 | 26 |
| confirm/ripple_adder_20/grid_7x7_u/L0/N2 | 0.992901 | 40 |
| confirm/ripple_adder_20/grid_7x7_u/L1/D2 | 0.921066 | 89 |
| confirm/ripple_adder_20/grid_7x7_u/L1/N2 | 0.994382 | 3 |
| confirm/ripple_adder_20/grid_7x7_u/L2/D2 | 0.979463 | 63 |
| confirm/ripple_adder_20/grid_7x7_u/L2/N2 | 1.030199 | 27 |
| confirm/ripple_adder_20/grid_7x7_u/L3/D2 | 0.979973 | 70 |
| confirm/ripple_adder_20/grid_7x7_u/L3/N2 | 1.022381 | 78 |
| confirm/adder_modular_v17_n8/mumbai_27/L0/D2 | 0.785637 | 44 |
| confirm/adder_modular_v17_n8/mumbai_27/L0/N2 | 0.971836 | 44 |
| confirm/adder_modular_v17_n8/mumbai_27/L1/D2 | 0.981119 | 31 |
| confirm/adder_modular_v17_n8/mumbai_27/L1/N2 | 0.994918 | 31 |
| confirm/adder_modular_v17_n8/mumbai_27/L2/D2 | 0.957298 | 18 |
| confirm/adder_modular_v17_n8/mumbai_27/L2/N2 | 1.003489 | 7 |
| confirm/adder_modular_v17_n8/mumbai_27/L3/D2 | 0.959496 | 18 |
| confirm/adder_modular_v17_n8/mumbai_27/L3/N2 | 1.003684 | 7 |
| confirm/adder_modular_v17_n16/mumbai_27/L0/D2 | 0.665863 | 86 |
| confirm/adder_modular_v17_n16/mumbai_27/L0/N2 | 1.069836 | 21 |
| confirm/adder_modular_v17_n16/mumbai_27/L1/D2 | 0.988387 | 12 |
| confirm/adder_modular_v17_n16/mumbai_27/L1/N2 | 1.023550 | 28 |
| confirm/adder_modular_v17_n16/mumbai_27/L2/D2 | 0.992432 | 37 |
| confirm/adder_modular_v17_n16/mumbai_27/L2/N2 | 1.005006 | 26 |
| confirm/adder_modular_v17_n16/mumbai_27/L3/D2 | 0.992112 | 37 |
| confirm/adder_modular_v17_n16/mumbai_27/L3/N2 | 0.984666 | 86 |
| confirm/adder_modular_v17_n32/rochester_53/L0/D2 | 0.537780 | 75 |
| confirm/adder_modular_v17_n32/rochester_53/L0/N2 | 0.981572 | 74 |
| confirm/adder_modular_v17_n32/rochester_53/L1/D2 | 0.991390 | 60 |
| confirm/adder_modular_v17_n32/rochester_53/L1/N2 | 0.999059 | 33 |
| confirm/adder_modular_v17_n32/rochester_53/L2/D2 | 0.976622 | 65 |
| confirm/adder_modular_v17_n32/rochester_53/L2/N2 | 0.985540 | 35 |
| confirm/adder_modular_v17_n32/rochester_53/L3/D2 | 0.988813 | 15 |
| confirm/adder_modular_v17_n32/rochester_53/L3/N2 | 0.988899 | 20 |
| confirm/multiplier_h18_n16/mumbai_27/L0/D2 | 0.759258 | 15 |
| confirm/multiplier_h18_n16/mumbai_27/L0/N2 | 0.860279 | 11 |
| confirm/multiplier_h18_n16/mumbai_27/L1/D2 | 0.977267 | 93 |
| confirm/multiplier_h18_n16/mumbai_27/L1/N2 | 0.980062 | 60 |
| confirm/multiplier_h18_n16/mumbai_27/L2/D2 | 0.978136 | 19 |
| confirm/multiplier_h18_n16/mumbai_27/L2/N2 | 0.985550 | 19 |
| confirm/multiplier_h18_n16/mumbai_27/L3/D2 | 0.981541 | 47 |
| confirm/multiplier_h18_n16/mumbai_27/L3/N2 | 0.988544 | 70 |
| confirm/adder_modular_v17_n6/mumbai_27/L0/D2 | 0.865886 | 30 |
| confirm/adder_modular_v17_n6/mumbai_27/L0/N2 | 0.939929 | 30 |
| confirm/adder_modular_v17_n6/mumbai_27/L1/D2 | 0.965704 | 31 |
| confirm/adder_modular_v17_n6/mumbai_27/L1/N2 | 0.994562 | 0 |
| confirm/adder_modular_v17_n6/mumbai_27/L2/D2 | 0.979897 | 23 |
| confirm/adder_modular_v17_n6/mumbai_27/L2/N2 | 0.997888 | 23 |
| confirm/adder_modular_v17_n6/mumbai_27/L3/D2 | 0.979682 | 23 |
| confirm/adder_modular_v17_n6/mumbai_27/L3/N2 | 0.997888 | 23 |
| confirm/multiplier_h18_n20/heavy_hex_d9_cz/L2/D2 | 0.968750 | 7 |
| confirm/multiplier_h18_n20/heavy_hex_d9_cz/L2/N2 | 0.975547 | 9 |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L0/D2 | 0.406848 | 85 |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L0/N2 | 1.558181 | 14 |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L1/D2 | 0.537412 | 45 |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L1/N2 | 0.717404 | 45 |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L2/D2 | 0.451967 | 2 |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L2/N2 | 0.635601 | 45 |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L3/D2 | 0.455287 | 68 |
| confirm/bv_all_ones_n100/heavy_hex_d9_cz/L3/N2 | 0.506984 | 70 |
| confirm/bv_all_ones_n16/mumbai_27/L0/D2 | 0.770409 | 41 |
| confirm/bv_all_ones_n16/mumbai_27/L0/N2 | 1.234335 | 73 |
| confirm/bv_all_ones_n16/mumbai_27/L1/D2 | 0.980774 | 53 |
| confirm/bv_all_ones_n16/mumbai_27/L1/N2 | 0.983291 | 0 |
| confirm/bv_all_ones_n16/mumbai_27/L2/D2 | 0.988150 | 9 |
| confirm/bv_all_ones_n16/mumbai_27/L2/N2 | 0.984334 | 38 |
| confirm/bv_all_ones_n16/mumbai_27/L3/D2 | 0.981418 | 6 |
| confirm/bv_all_ones_n16/mumbai_27/L3/N2 | 0.986940 | 97 |
| confirm/bv_all_ones_n50/rochester_53/L0/D2 | 0.629341 | 80 |
| confirm/bv_all_ones_n50/rochester_53/L0/N2 | 1.500796 | 89 |
| confirm/bv_all_ones_n50/rochester_53/L1/D2 | 0.984843 | 0 |
| confirm/bv_all_ones_n50/rochester_53/L1/N2 | 0.988195 | 0 |
| confirm/bv_all_ones_n50/rochester_53/L2/D2 | 0.978947 | 21 |
| confirm/bv_all_ones_n50/rochester_53/L2/N2 | 0.982244 | 21 |
| confirm/bv_all_ones_n50/rochester_53/L3/D2 | 0.980718 | 8 |
| confirm/bv_all_ones_n50/rochester_53/L3/N2 | 0.983313 | 12 |
| confirm/bvlike_n100/heavy_hex_d9_cz/L0/D2 | 0.413000 | 89 |
| confirm/bvlike_n100/heavy_hex_d9_cz/L0/N2 | 1.303551 | 60 |
| confirm/bvlike_n100/heavy_hex_d9_cz/L1/D2 | 0.577886 | 53 |
| confirm/bvlike_n100/heavy_hex_d9_cz/L1/N2 | 0.611699 | 52 |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L0/D2 | 0.363259 | 92 |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L0/N2 | 1.361699 | 1 |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L1/D2 | 0.389021 | 56 |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L1/N2 | 0.520775 | 56 |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L2/D2 | 0.393354 | 22 |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L2/N2 | 0.506832 | 98 |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L3/D2 | 0.405344 | 4 |
| confirm/su2_circular_n89/heavy_hex_d9_cz/L3/N2 | 0.498523 | 0 |
| confirm/ring_random_n8/melbourne_14_u/L0/D2 | 0.859474 | 25 |
| confirm/ring_random_n8/melbourne_14_u/L0/N2 | 1.069284 | 85 |
| confirm/ring_random_n14/melbourne_14_u/L0/D2 | 0.983851 | 14 |
| confirm/ring_random_n14/melbourne_14_u/L0/N2 | 0.982434 | 85 |
| confirm/su2_circular_n100/heavy_hex_d9_cz/L0/D2 | 0.337126 | 91 |
| confirm/su2_circular_n100/heavy_hex_d9_cz/L0/N2 | 1.170691 | 75 |
| confirm/queko_bss_53+sabre/rochester_53/L0/D2 | 0.868354 | 72 |
| confirm/queko_bss_53+sabre/rochester_53/L0/N2 | 0.991677 | 73 |
| confirm/queko_bss_53+sabre/rochester_53/L1/D2 | 0.823655 | 66 |
| confirm/queko_bss_53+sabre/rochester_53/L1/N2 | 0.961990 | 43 |
| confirm/queko_bss_53+sabre/rochester_53/L2/D2 | 0.890616 | 41 |
| confirm/queko_bss_53+sabre/rochester_53/L2/N2 | 1.006151 | 84 |
| confirm/queko_bss_53+sabre/rochester_53/L3/D2 | 0.914236 | 74 |
| confirm/queko_bss_53+sabre/rochester_53/L3/N2 | 1.000945 | 45 |
| confirm/queko_bigd_20+sabre/tokyo_20/L0/D2 | 0.973424 | 80 |
| confirm/queko_bigd_20+sabre/tokyo_20/L0/N2 | 1.011336 | 80 |
| confirm/queko_bigd_20+sabre/tokyo_20/L1/D2 | 0.938951 | 98 |
| confirm/queko_bigd_20+sabre/tokyo_20/L1/N2 | 0.974007 | 80 |
| confirm/queko_bigd_20+sabre/tokyo_20/L2/D2 | 0.988296 | 23 |
| confirm/queko_bigd_20+sabre/tokyo_20/L2/N2 | 1.055959 | 23 |
| confirm/queko_bigd_20+sabre/tokyo_20/L3/D2 | 1.002676 | 80 |
| confirm/queko_bigd_20+sabre/tokyo_20/L3/N2 | 1.059716 | 49 |
| confirm/queko_bntf_54+sabre/sycamore_54/L0/D2 | 0.794030 | 49 |
| confirm/queko_bntf_54+sabre/sycamore_54/L0/N2 | 0.953810 | 49 |
| confirm/queko_bntf_54+sabre/sycamore_54/L1/D2 | 0.783938 | 26 |
| confirm/queko_bntf_54+sabre/sycamore_54/L1/N2 | 0.970894 | 59 |
| confirm/queko_bntf_54+sabre/sycamore_54/L2/D2 | 0.812418 | 61 |
| confirm/queko_bntf_54+sabre/sycamore_54/L2/N2 | 0.980017 | 61 |
| confirm/queko_bntf_54+sabre/sycamore_54/L3/D2 | 0.801364 | 61 |
| confirm/queko_bntf_54+sabre/sycamore_54/L3/N2 | 0.949729 | 61 |
| confirm/queko_bss_53/rochester_53/L0/D2 | 0.724583 | 66 |
| confirm/queko_bss_53/rochester_53/L0/N2 | 1.064437 | 42 |
| confirm/queko_bigd_20/tokyo_20/L0/D2 | 0.782450 | 20 |
| confirm/queko_bigd_20/tokyo_20/L0/N2 | 0.969704 | 20 |
| confirm/queko_bntf_54/sycamore_54/L0/D2 | 0.627369 | 95 |
| confirm/queko_bntf_54/sycamore_54/L0/N2 | 0.990667 | 86 |
| confirm/qft_n100/heavy_hex_d9_cx/L2/D2 | 0.920514 | 64 |
| confirm/qft_n100/heavy_hex_d9_cx/L2/N2 | 0.971408 | 29 |
| confirm/qft_n100/heavy_hex_d9_ecr/L2/D2 | 0.922930 | 64 |
| confirm/qft_n100/heavy_hex_d9_ecr/L2/N2 | 0.974021 | 29 |
| confirm/square_heisenberg_n100/heavy_hex_d9_cx/L2/D2 | 0.845432 | 47 |
| confirm/square_heisenberg_n100/heavy_hex_d9_cx/L2/N2 | 0.973195 | 28 |
| confirm/square_heisenberg_n100/heavy_hex_d9_ecr/L2/D2 | 0.845432 | 47 |
| confirm/square_heisenberg_n100/heavy_hex_d9_ecr/L2/N2 | 0.973195 | 28 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cx/L2/D2 | 0.839305 | 90 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_cx/L2/N2 | 1.046463 | 93 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_ecr/L2/D2 | 0.838805 | 90 |
| confirm/qaoa_ba_n100_3reps/heavy_hex_d9_ecr/L2/N2 | 1.045921 | 93 |

## Zero-baseline changes

| Case | Metric | Worst delta | Seed | Baseline | Evolved |
| --- | --- | ---: | ---: | ---: | ---: |
| confirm/qft16_cancel/mumbai_27/L2 | D2 | 0 | 0 | 0 | 0 |
| confirm/qft16_cancel/mumbai_27/L2 | N2 | 0 | 0 | 0 | 0 |
| confirm/qft16_cancel/mumbai_27/L3 | D2 | 0 | 0 | 0 | 0 |
| confirm/qft16_cancel/mumbai_27/L3 | N2 | 0 | 0 | 0 | 0 |
| confirm/bvlike_n100/heavy_hex_d9_cz/L2 | D2 | 0 | 0 | 0 | 0 |
| confirm/bvlike_n100/heavy_hex_d9_cz/L2 | N2 | 0 | 0 | 0 | 0 |
| confirm/bvlike_n100/heavy_hex_d9_cz/L3 | D2 | 0 | 0 | 0 | 0 |
| confirm/bvlike_n100/heavy_hex_d9_cz/L3 | N2 | 0 | 0 | 0 | 0 |
