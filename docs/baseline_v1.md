# V1 Weighted Quantile ExtraTrees

## 제출 기록

- 제출번호: **1506127**
- 당시 제출 파일: `submit_v8_repeated_cv_quantile_forest.csv`
- 현재 기준 파일: `submit_v1_weighted_quantile_extratrees.csv`
- Public MAE: **0.1282776667**

## 모델 설정

- `ExtraTreesRegressor`
- Trees: `1200`
- `min_samples_leaf=1`
- `max_features=1`
- `random_state=42`
- Tree prediction aggregation: Q51
- Output clip: `[0, 1]`
- 0.01 rounding: 미적용

## 파생변수

BMI · 맥압 · 평균동맥압 · 혈압 비율 · 콜레스테롤/혈당 비율 · 행별 결측치 수

## 중요 피처 가중

`mean_working` · BMI · 콜레스테롤 · 키 · 혈당 · 체중 · 콜레스테롤/혈당 비율 · 골밀도  
각 피처 복제본 2개 → ExtraTrees 분할 후보 선택 확률 조정

## 검증 결과

| 검증 | MAE |
|---|---:|
| 반복 CV 평균 | 0.147505 |
| 중복 표본 그룹 검증 | 0.149202 |
| Public | 0.1282776667 |

## 명칭 주의

**Filename `repeated_cv` ≠ repeated-CV test ensemble.**  
최종 Test 예측: 전체 Train 학습 단일 ExtraTrees · 1,200 tree predictions · Q51 aggregation.
