# E000 V1 Baseline

## 목적

팀 최고 Public 기록 모델을 통합 리포지토리의 기준 모델로 고정합니다.

## 모델

- Weighted Quantile ExtraTrees
- 1,200 trees
- `max_features=1`
- 중요 피처 복제본 2개
- 트리별 예측 51% 분위수

## 결과

| 검증 | MAE |
|---|---:|
| 반복 CV 평균 | 0.147505 |
| 중복 그룹 검증 | 0.149202 |
| Public | 0.1282776667 |

## 결론

- 상태: Baseline
- 버전: V1
