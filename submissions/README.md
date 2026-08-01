# Submissions

제출 CSV는 이 폴더에 둘 수 있지만 `.gitignore`에 의해 Git에는 올라가지 않습니다.

## 현재 Public 최고

- 제출번호: 1506916
- 파일명: `submit_v14_blend95.csv`
- Public MAE: 0.1278085845
- 모델: 기준 Weighted Quantile ExtraTrees 95% + 보조 예측 5%

## 기준 모델 표준 출력

V1 표준 파일명은 다음과 같습니다.

```text
submit_v1_weighted_quantile_extratrees.csv
```

## 기록 규칙

제출 후 `docs/leaderboard.md`에 다음 내용을 기록합니다.

- 제출번호
- 파일명
- 제출 시각
- Public Score
- Private Score
- 실험 번호

실제 제출 파일의 설정과 일치하는 CV만 기록합니다.
