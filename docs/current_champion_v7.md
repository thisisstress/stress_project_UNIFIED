# V7 Pair-Neighbor Quantile Blend — Team Lineage Milestone

> 파일명 `current_champion_v7.md`은 기존 링크 호환을 위해 유지합니다.  
> V7은 2026-08-01 당시의 팀 최고 모델이었고, 최종 발표 기준 현재 채택 모델은 **BS 8/6**입니다.

## 제출 기록

- 제출번호: **1507714**
- 제출 파일: `submit_v7_pair_neighbor_blend.csv`
- 제출 시각: **2026-08-01 14:43:42**
- Public MAE: **0.1272333333**
- Private MAE: 미공개

## 모델 구조

V7은 V14 코드나 예측을 사용하지 않고 독립적으로 개발했습니다.

```text
round(
    0.85 × V6 52% tree quantile
    + 0.15 × pair-neighbor 52% quantile,
    2
)
```

### V6 Tree 모델 85%

- ExtraTrees 1,200개
- `max_features=1`
- `random_state=42`
- 피처별 복제 수로 선택 확률 조정
- 개별 Tree 예측의 52% 분위수
- 0.01 단위 반올림

### Pair-Neighbor 모델 15%

다음 8개 핵심 피처의 모든 2개 조합, 총 28개 피처쌍을 사용합니다.

- `mean_working`
- `bmi`
- `cholesterol`
- `height`
- `glucose`
- `weight`
- `cholesterol_glucose_ratio`
- `bone_density`

각 피처를 Train 기준 경험적 순위로 변환하고,
각 피처쌍에서 Manhattan 거리가 가장 가까운 Train 1개 행의
타깃을 가져옵니다. 28개 타깃의 52% 분위수를 보조 예측으로 사용합니다.

## 검증 결과

| 검증 구간 | V6 MAE | V7 MAE | 차이 | Seed 승률 |
|---|---:|---:|---:|---:|
| Development Seed 42 | 0.151283 | **0.150560** | -0.000723 | 1/1 |
| Development Seed 2026·3407 | 0.146502 | **0.146205** | -0.000297 | 2/2 |
| 신규 Audit3 | 0.147019 | **0.146644** | -0.000374 | 3/3 |

- Audit3 쌍대 95% 신뢰구간: `[-0.000791, +0.000044]`
- 여섯 Seed에서 모두 V6보다 낮은 MAE
- 신뢰구간 상한이 0을 아주 조금 포함한다는 한계는 유지

## Public 계보

| 모델 | Public MAE | 역할 |
|---|---:|---|
| V1 Baseline | 0.1282776667 | 초기 기준점 |
| V14 Blend95 | 0.1278085845 | 역사적 보수 블렌드 |
| **Team V7 Pair-Neighbor Blend** | **0.1272333333** | 팀 계보 이정표 |
| BS V34 | 0.1271866667 | 최종 통합 직전 이정표 |
| BS 8/6 | **0.1266866667** | **최종 채택** |

## 누수 방지

- 모델, 전처리, 결측 대체값과 경험적 순위는 Train에서만 학습
- 동일 입력 중복 그룹은 같은 Fold에 배치
- Test 전체 통계, 행 수, 인덱스, 순서와 다른 Test 행을 사용하지 않음
- Test 값은 Train 정렬 배열에 행별로 독립 투영
- 외부 데이터와 V14 예측을 사용하지 않음

## 상태

- **Historical Team Lineage Milestone**
- V7은 최종 계보에서 V34와 BS 8/6으로 이어지는 핵심 기준점으로 보존
- 최종 채택 상태는 README와 `experiments/registry.csv`의 BS 8/6 항목을 따름

## 출처

- 원본 리포: `thisisstress/stress_project_JH`
- 보고서: `validation/V7_MODEL_REPORT.md`
- 실행 코드: `final_submission_v7.py`
- 기록 브랜치: `agent/model-history-v2-v4`
