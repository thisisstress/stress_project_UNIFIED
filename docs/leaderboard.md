# 팀 모델 점수 기록

**Scope:** 최종 발표 대표 계보 · 제출 ledger · provenance link  
**Rule:** 서로 다른 검증 계약의 미세 내부 MAE 차이 직접 순위화 제외.

## 최종 발표 대표 계보

| 단계 | 모델 | 내부 MAE | Public MAE | Private MAE | 상태 |
|---:|---|---:|---:|---:|---|
| 1 | V1 Weighted Quantile ExtraTrees | 0.147505 | 0.1282776667 | — | Initial baseline anchor |
| 2 | Team V7 Pair-Neighbor Blend | 0.146644 | 0.1272333333 | — | Team lineage milestone |
| 3 | BS V34 Tree·Pair Joint Tuning | 0.148033 | 0.1271866667 | — | BS lineage milestone |
| 4 | **BS 8/6 Final Integrated Model** | **0.147300** | **0.1266866667** | **0.1473** | **Final adopted** |

**V34 / BS 8/6 source:** `thisisstress/stress_project_BS`

## Historical UNIFIED submission ledger

| 순서 | 제출번호 | 파일명 | 제출 시각 | Public MAE | 상태 |
|---:|---:|---|---|---:|---|
| 1 | 1506073 | `submission.csv` | 2026-07-30 15:18:18 | 0.1686788978 | 초기 모델 |
| 2 | 1506110 | `submit_v7_weighted_median_forest.csv` | 2026-07-30 16:01:25 | 0.1287733333 | 후보 |
| 3 | 1506127 | `submit_v8_repeated_cv_quantile_forest.csv` | 2026-07-30 16:21:49 | 0.1282776667 | V1 계보 기준점 |
| 4 | 1506797 | `submit_v10_v9_age_ensemble.csv` | 2026-07-31 11:15:05 | 0.1283466667 | 역사 후보 |
| 5 | 1506850 | `submit_v13_quantile_tabpfn.csv` | 2026-07-31 13:07:36 | 0.1287000000 | 독립 후보 |
| 6 | 1506896 | `submit_v2_weighted_median_extratrees.csv` | 2026-07-31 14:28:01 | 0.1284666667 | 통제 실험 |
| 7 | 1506916 | `submit_v14_blend95.csv` | 2026-07-31 14:52:53 | 0.1278085845 | Former Public Best |
| 8 | 1507566 | `submit_v4_conservative_quantile_extratrees.csv` | 2026-08-01 10:26:44 | 0.1286866667 | 미채택 통제 실험 |
| 9 | 1507714 | `submit_v7_pair_neighbor_blend.csv` | 2026-08-01 14:43:42 | 0.1272333333 | Team V7 milestone |

**Private score policy:** 추정치 미기록. BS 8/6 `0.1473`만 최종 발표 확인값으로 표기.
