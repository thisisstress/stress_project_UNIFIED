<div align="center">

# 🧠 Stress Score Prediction — UNIFIED

### 스트레스 지수 예측 프로젝트 · 팀 최종 결과와 모델 계보

<p>
  <img src="https://img.shields.io/badge/Task-Tabular%20Regression-2563EB?style=flat-square" alt="Task">
  <img src="https://img.shields.io/badge/Metric-MAE-7C3AED?style=flat-square" alt="Metric">
  <img src="https://img.shields.io/badge/Final-Public%200.1266866667-9333EA?style=flat-square" alt="Final Public MAE">
</p>

건강·생활 데이터를 이용해 `stress_score`를 예측한 팀 프로젝트입니다. 이 저장소는 최종 결과와 주요 모델의 발전 과정을 한곳에서 볼 수 있도록 정리합니다.

</div>

## 최종 결과

| 항목 | 결과 |
|---|---:|
| 평가 지표 | MAE — 낮을수록 우수 |
| 최종 채택 모델 | **BS 8/6 — ExtraTrees + Pair-Neighbor** |
| 내부 검증 MAE | **0.147300** |
| Public MAE | **0.1266866667** |
| Private MAE | **0.1473** |
| 최종 블렌드 | **ExtraTrees 76% + Pair-Neighbor 24%** |

최종 발표에서는 Public 점수만 가장 낮은 모델보다 내부 검증과 Private 결과까지 확인된 8월 6일 통합 모델을 채택했습니다. Public `0.1265`를 기록한 Fresh V6는 같은 수준의 검증 기록이 없어 최종 모델로 사용하지 않았습니다.

최종 실행 Notebook은 [`stress_project_BS/8_6/stress_prediction_combined_final_0806_1.ipynb`](https://github.com/thisisstress/stress_project_BS/blob/main/8_6/stress_prediction_combined_final_0806_1.ipynb)에 있습니다.

## 모델 계보

<p align="center">
  <img src="docs/assets/model_lineage.svg" alt="Stress Project model lineage" width="100%">
</p>

| 단계 | 모델 | 내부 MAE | Public MAE | 의미 |
|---|---|---:|---:|---|
| V1 | Weighted Quantile ExtraTrees | `0.147505` | `0.1282776667` | 초기 기준 모델 |
| V7 | Pair-Neighbor Blend | `0.146644` | `0.1272333333` | 국소 유사성 결합 |
| V34 | Tree·Pair Joint Tuning | `0.148033` | `0.1271866667` | 최종 통합 직전 후보 |
| **BS 8/6** | **Final Integrated Model** | **`0.147300`** | **`0.1266866667`** | **최종 채택** |

내부 MAE는 실험마다 split과 seed가 다를 수 있어 아주 작은 차이를 같은 조건의 순위처럼 해석하지 않습니다.

## 최종 모델

최종 모델은 전역 패턴을 학습하는 ExtraTrees와 국소적으로 비슷한 Train 샘플을 찾는 Pair-Neighbor를 결합합니다.

```text
Fold-local preprocessing
        ↓
row-level derived features
        ↓
ExtraTrees 1,200 trees · Q54  ─┐
                               ├─ 76:24 blend
Pair-Neighbor 8 features       │
28 pairs · Q48              ───┘
        ↓
near-duplicate override (< 0.2)
        ↓
round to 0.01 · clip [0, 1]
```

최종 단계에서 `gender`를 제외했고, `mean_working`, 이완기 혈압, 콜레스테롤, 혈당의 Winsorization 경계는 각 Fold의 Train partition에서 계산했습니다.

주요 파생변수는 BMI, 맥압, 평균동맥압, 혈압 비율, 콜레스테롤·혈당 비율, 결측치 개수입니다.

## 관련 연구 저장소

| Repository | 내용 |
|---|---|
| [`stress_project_BS`](https://github.com/thisisstress/stress_project_BS) | 최종 BS 8/6 모델, ExtraTrees·Pair-Neighbor 개선 과정 |
| [`stress_project_JH`](https://github.com/thisisstress/stress_project_JH) | V7 Pair-Neighbor 연구와 재현 코드 |
| `stress_project_SK` | 대안 모델, UQC/Gower, 강건성 검증과 후속 R&D 기록 |

`stress_project_SK`는 팀 최종 모델과 별개의 연구축입니다. 최종 발표 결과는 이 UNIFIED 저장소와 BS 8/6 모델을 기준으로 봅니다.

## 더 보기

- [`docs/leaderboard.md`](docs/leaderboard.md) — 제출 결과와 주요 모델 기록
- [`docs/baseline_v1.md`](docs/baseline_v1.md) — V1 기준 모델
- [`docs/current_champion_v7.md`](docs/current_champion_v7.md) — V7 상세
- [`experiments/registry.csv`](experiments/registry.csv) — 실험 목록

대회 원본 `train.csv`·`test.csv`와 정답 레이블은 저장소에 포함하지 않습니다.

## License, attribution and citation

팀이 작성한 소스 코드와 문서는 [MIT License](LICENSE)로 공개합니다. 공동 저자와 역할은 [AUTHORS.md](AUTHORS.md), 데이터·제3자 자료의 제외 범위는 [LICENSE_SCOPE.md](LICENSE_SCOPE.md)에서 확인할 수 있습니다.

연구 또는 프로젝트에서 이 결과를 활용할 때에는 GitHub의 **Cite this repository** 메뉴가 제공하는 [`CITATION.cff`](CITATION.cff) 정보를 사용해 세 팀원을 함께 인용해 주세요.
