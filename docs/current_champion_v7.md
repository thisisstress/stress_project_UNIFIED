# V7 Pair-Neighbor Quantile Blend — Team Lineage Milestone

**Filename compatibility:** `current_champion_v7.md` 유지  
**Historical status:** 2026-08-01 당시 팀 최고 모델  
**Current final:** BS 8/6

## 제출 기록

- 제출번호: **1507714**
- 제출 파일: `submit_v7_pair_neighbor_blend.csv`
- 제출 시각: **2026-08-01 14:43:42**
- Public MAE: **0.1272333333**
- Private MAE: 미공개

## 모델 구조

**V14 dependency:** 없음

```text
round(
    0.85 × V6 52% tree quantile
    + 0.15 × pair-neighbor 52% quantile,
    2
)
```

### V6 Tree 모델 85%

- ExtraTrees `1200`
- `max_features=1`
- `random_state=42`
- 피처 복제 수 → 선택 확률 조정
- Tree prediction Q52
- 0.01 rounding

### Pair-Neighbor 모델 15%

**8 features**

- `mean_working`
- `bmi`
- `cholesterol`
- `height`
- `glucose`
- `weight`
- `cholesterol_glucose_ratio`
- `bone_density`

**Contract**
- 모든 2개 조합 → 28 pair spaces
- Train 기준 empirical rank
- Manhattan 1-NN
- 28 neighbor targets → Q52

## 검증 결과

| 검증 구간 | V6 MAE | V7 MAE | 차이 | Seed 승률 |
|---|---:|---:|---:|---:|
| Development Seed 42 | 0.151283 | **0.150560** | -0.000723 | 1/1 |
| Development Seed 2026·3407 | 0.146502 | **0.146205** | -0.000297 | 2/2 |
| 신규 Audit3 | 0.147019 | **0.146644** | -0.000374 | 3/3 |

- Audit3 paired 95% CI: `[-0.000791, +0.000044]`
- 6 seeds: V7 MAE < V6 MAE
- CI upper bound > 0 → 불확실성 유지

## Public 계보

| 모델 | Public MAE | 역할 |
|---|---:|---|
| V1 Baseline | 0.1282776667 | 초기 기준점 |
| V14 Blend95 | 0.1278085845 | 역사적 보수 블렌드 |
| **Team V7 Pair-Neighbor Blend** | **0.1272333333** | 팀 계보 이정표 |
| BS V34 | 0.1271866667 | 최종 통합 직전 이정표 |
| BS 8/6 | **0.1266866667** | **최종 채택** |

## 누수 방지 계약

- 모델 · 전처리 · 결측 대체 · empirical rank: Train-only
- 동일 입력 중복 그룹: same Fold
- Test 전체 통계 · 행 수 · 인덱스 · 순서 · 다른 Test 행: 미사용
- Test row: Train 정렬 배열에 독립 투영
- 외부 데이터: 미사용
- V14 predictions: 미사용

## 상태

**Historical Team Lineage Milestone**  
V7 → V34 → BS 8/6  
최종 채택 기준: README · `experiments/registry.csv`의 BS 8/6

## 출처

- 원본 리포: `thisisstress/stress_project_JH`
- 보고서: `validation/V7_MODEL_REPORT.md`
- 실행 코드: `final_submission_v7.py`
- 기록 브랜치: `agent/model-history-v2-v4`
