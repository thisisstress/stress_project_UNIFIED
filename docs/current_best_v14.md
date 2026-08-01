# V14 Blend95 — 현재 Public 최고 제출

## 제출 기록

- 제출번호: **1506916**
- 제출 파일: `submit_v14_blend95.csv`
- 제출 시각: **2026-07-31 14:52:53**
- Public MAE: **0.1278085845**
- Private MAE: 미공개

## 모델 구조

```text
최종 예측
= 기준 Weighted Quantile ExtraTrees 95%
+ V10 계열 보조 예측 5%
```

### 기준 모델

- ExtraTrees 1,200개
- `max_features=1`
- Seed 42
- 개별 트리 예측의 51% 분위수
- 중요 건강 피처 복제본 2개
- 반올림 미적용

### 보조 예측

```text
보조 예측
= 다중 Seed 3,600트리 50.5% 분위수 70%
+ 나이·건강 상호작용 ExtraTrees 50% 분위수 30%
```

다중 Seed는 42, 77, 2026이며 Seed별 1,200개, 총 3,600개 트리를 사용합니다.

나이·건강 상호작용 피처:

- 나이×BMI
- 나이×혈당
- 나이×콜레스테롤
- 나이×골밀도
- 나이×평균동맥압

## 검증값 주의

실제 제출 파일 `submit_v14_blend95.csv`의 고정 후보 CV MAE는 **0.149080**입니다.

노트북에서 자동 선택된 V14 Main은 다른 후보입니다.

- 기준 모델 80%
- 보조 예측 20%
- 소수점 둘째 자리 반올림
- CV MAE 0.148953

따라서 0.148953을 `submit_v14_blend95.csv`의 직접 CV로 기록하면 안 됩니다.

## 기준 모델 대비 Public 개선

| 모델 | Public MAE |
|---|---:|
| V1 Weighted Quantile ExtraTrees | 0.1282776667 |
| V14 Blend95 | **0.1278085845** |

- 절대 MAE 감소: **0.0004690822**
- 상대 개선율: 약 **0.37%**

## 해석

기준 모델을 95% 유지하고 서로 다른 오차 패턴을 가진 보조 예측을
5%만 추가한 전략이 Public에서 가장 좋은 결과를 냈습니다.

다만 CV 개선 폭은 작으므로, Public 향상이 완전한 일반화 성능 향상이라고
단정하지 않고 여러 Split Seed와 그룹 검증으로 재확인해야 합니다.

## 출처

- 원본 리포: `thisisstress/stress_project_BS`
- 노트북: `stress_prediction_v14_conservative_blend.ipynb`
- 커밋: `fef33607cb35021dae16f4be8abe108e3963ddf8`
