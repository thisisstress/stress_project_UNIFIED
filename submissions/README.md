# Submissions

제출 CSV는 이 폴더에 둘 수 있지만 `.gitignore`에 의해 Git에는 올라가지 않습니다.  
이 문서는 **역사적 제출 ledger 보조 문서**이며, 현재 팀 final은 루트 README와 `experiments/registry.csv`를 기준으로 합니다.

## Current canonical final

- 모델: **BS 8/6 — ExtraTrees + Pair-Neighbor**
- Public MAE: **0.1266866667**
- Private MAE: **0.1473**
- Canonical implementation: [stress_project_BS final notebook](https://github.com/thisisstress/stress_project_BS/blob/main/8_6/stress_prediction_combined_final_0806_1.ipynb)

최종 BS 8/6의 제출번호는 이 historical ledger에 별도로 확정 기록하지 않았으므로 추정하지 않습니다.

## Historical submissions

### Team V7 lineage milestone

- 제출번호: 1507714
- 파일명: `submit_v7_pair_neighbor_blend.csv`
- Public MAE: `0.1272333333`
- 상태: Historical team-lineage milestone

### V14 historical public reference

- 제출번호: 1506916
- 파일명: `submit_v14_blend95.csv`
- Public MAE: `0.1278085845`
- 상태: Historical conservative-blend branch

## Frozen baseline output

```text
submit_v1_weighted_quantile_extratrees.csv
```

V1은 현재 champion이 아니라 초기 비교 기준점입니다.

## 기록 규칙

제출 후 [`docs/leaderboard.md`](../docs/leaderboard.md)에 다음을 기록합니다.

- 제출번호
- 파일명
- 제출 시각
- Public Score
- Private Score
- 실험 번호
- 실제 제출 설정과 일치하는 검증값

추정 Private Score는 공식 기록에 넣지 않습니다.  
점수 비교 규칙은 [`docs/EVALUATION_NOTES.md`](../docs/EVALUATION_NOTES.md)를 따릅니다.
