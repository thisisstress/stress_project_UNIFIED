# V1 Weighted Quantile ExtraTrees

## 제출 기록

- 제출번호: **1506127**
- 당시 제출 파일: `submit_v8_repeated_cv_quantile_forest.csv`
- 현재 기준 파일: `submit_v1_weighted_quantile_extratrees.csv`
- Public MAE: **0.1282776667**

## 모델 설정

- `ExtraTreesRegressor`
- 트리 1,200개
- `min_samples_leaf=1`
- `max_features=1`
- `random_state=42`
- 개별 트리 예측의 51% 분위수 사용
- 예측값을 0~1로 제한
- 0.01 단위 반올림 미적용

## 파생변수

- BMI
- 맥압
- 평균동맥압
- 혈압 비율
- 콜레스테롤·혈당 비율
- 행별 결측치 개수

## 중요 피처 가중

`mean_working`, BMI, 콜레스테롤, 키, 혈당, 체중, 콜레스테롤·혈당 비율, 골밀도마다 복제본 2개를 추가합니다.

## 검증 결과

| 검증 | MAE |
|---|---:|
| 반복 CV 평균 | 0.147505 |
| 중복 표본 그룹 검증 | 0.149202 |
| Public | 0.1282776667 |

## 명칭 주의

당시 제출 파일에는 `repeated_cv`가 포함됐지만 최종 Test 예측은 반복 CV 모델의 앙상블이 아닙니다. 전체 Train으로 학습한 단일 ExtraTrees 모델 안의 1,200개 트리 예측을 51% 분위수로 집계합니다.
