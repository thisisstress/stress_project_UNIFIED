# 팀 모델 점수 기록

> 이 문서의 첫 표는 **최종 발표에 등장하는 대표 모델 중 UNIFIED에서 추적하는 팀의 주요 연결 계보**를 정리합니다.  
> UNIFIED는 점수·원본 위치·계보를 연결하는 허브이며, 각 모델의 실제 연구 소유와 provenance는 원본 저장소에 그대로 남습니다.  
> 내부 MAE는 서로 다른 검증 계약이 섞일 수 있으므로 작은 차이를 직접 순위화하지 않습니다.

## 최종 발표 대표 계보

| 단계 | 모델 | 내부 MAE | Public MAE | Private MAE | 상태 |
|---:|---|---:|---:|---:|---|
| 1 | V1 Weighted Quantile ExtraTrees | 0.147505 | 0.1282776667 | — | Initial baseline anchor |
| 2 | Team V7 Pair-Neighbor Blend | 0.146644 | 0.1272333333 | — | Team lineage milestone |
| 3 | BS V34 Tree·Pair Joint Tuning | 0.148033 | 0.1271866667 | — | BS lineage milestone |
| 4 | **BS 8/6 Final Integrated Model** | **0.147300** | **0.1266866667** | **0.1473** | **Final adopted** |

V34와 BS 8/6의 실행 원본은 `thisisstress/stress_project_BS`에 보존되어 있습니다.

## Historical UNIFIED submission ledger

아래 표는 UNIFIED가 처음 만들어질 당시 수집한 제출 이력입니다. 최종 발표 대표 계보와 직접 연결되지 않는 실험도 역사 기록으로 유지합니다.

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

추정 Private Score는 기록하지 않습니다. 최종 BS 8/6의 Private `0.1473`은 최종 발표 결과로 확인된 값만 별도로 표시합니다.
