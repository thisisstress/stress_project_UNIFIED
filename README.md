<div align="center">

# 🧠 Stress Score Prediction — UNIFIED

### 스트레스 점수 예측 팀 모델 계보와 최종 결과 허브

<p>
  <img src="https://img.shields.io/badge/Task-Tabular%20Regression-2563EB?style=flat-square" alt="Task">
  <img src="https://img.shields.io/badge/Metric-MAE-7C3AED?style=flat-square" alt="Metric">
  <img src="https://img.shields.io/badge/Core-ExtraTrees-059669?style=flat-square" alt="ExtraTrees">
  <img src="https://img.shields.io/badge/Hybrid-Pair--Neighbor-EA580C?style=flat-square" alt="Pair Neighbor">
  <img src="https://img.shields.io/badge/Final-Public%200.126687-9333EA?style=flat-square" alt="Final Public MAE">
</p>

**Weighted Quantile ExtraTrees에서 시작해 Pair-Neighbor와 Tree·Pair 공동 조정을 거쳐  
최종 BS 8/6 통합 모델로 이어진 팀의 대표 연구 계보를 연결·정리한 저장소입니다.**

</div>

---

> **UNIFIED의 역할**  
> 이 저장소는 각 연구 저장소의 성과를 다시 소유하는 곳이 아니라, **팀에서 확인된 대표 모델·점수·원본 위치를 하나의 계보로 연결하는 공통 허브**입니다.  
> 모델의 실제 연구·실행 원본과 provenance는 각 출처 저장소에 그대로 남기고, UNIFIED에서는 중복 복사보다 검증된 연결 관계를 보존합니다.

## 🧬 최종 발표 기준 대표 계보

<p align="center">
  <img src="docs/assets/model_lineage.svg" alt="Stress Project UNIFIED final model lineage" width="100%">
</p>

> 이 계보도는 **최종 발표에 등장하는 대표 모델 중 UNIFIED에서 추적하는 팀의 주요 연결 계보**만 표시합니다.  
> V14 Blend95, V4 Conservative Quantile과 독립 Gower 연구는 실제 연구 기록이지만 메인 발표 계보에서는 제외하고 역사 자료로 보존합니다.

---

## 🏆 최종 결과

| 항목 | 결과 |
|---|---:|
| 최종 채택 모델 | **BS 8/6 — ExtraTrees + Pair-Neighbor** |
| 내부 검증 MAE | **0.147300** |
| Public MAE | **0.1266866667** |
| Private MAE | **0.1473** |
| 최종 블렌드 | **ExtraTrees 76% + Pair-Neighbor 24%** |
| 평가 지표 | Mean Absolute Error — 낮을수록 우수 |

최종 발표에서 채택된 BS 8/6 모델은 `stress_project_BS`의
[`8_6/stress_prediction_combined_final_0806_1.ipynb`](https://github.com/thisisstress/stress_project_BS/blob/main/8_6/stress_prediction_combined_final_0806_1.ipynb)에 기록되어 있습니다.

---

## 📊 대표 모델 비교

| 단계 | 대표 모델 | 내부 MAE | Public MAE | 역할 |
|---|---|---:|---:|---|
| ① | **V1 Weighted Quantile ExtraTrees** | 0.147505 | 0.1282776667 | 초기 Public 기준점 |
| ② | **Team V7 Pair-Neighbor Blend** | 0.146644 | 0.1272333333 | 팀 계보 이정표 |
| ③ | **BS V34 Tree·Pair Joint Tuning** | 0.148033 | 0.1271866667 | BS 최종 통합 직전 이정표 |
| ④ | **BS 8/6 Final Integrated Model** | **0.147300** | **0.1266866667** | **최종 채택** |

> **점수 해석 주의**  
> 내부 MAE는 실험별 split·seed·검증 계약이 다를 수 있으므로 작은 차이를 직접적인 우열로 해석하지 않습니다.  
> Public MAE는 실제 제출 결과를 기록한 값입니다.

---

## ✨ 계보의 핵심 변화

### 1. V1 — Weighted Quantile ExtraTrees

1,200개의 ExtraTree 예측을 단순 평균 대신 분위수로 집계하고, 중요한 피처가 분할 후보로 더 자주 선택되도록 feature weighting을 적용한 초기 기준 모델입니다.

- Public MAE `0.1282776667`
- UNIFIED에 보존된 초기 frozen baseline
- 현재 대표 연결 계보의 출발점

### 2. Team V7 — Pair-Neighbor Blend

ExtraTrees 전역 예측에 8개 핵심 피처의 28개 2차원 조합에서 찾은 최근접 Train 타깃을 결합해 국소 유사 프로필을 보완했습니다.

- 내부 MAE `0.146644`
- Public MAE `0.1272333333`
- 팀 공통 계보의 주요 이정표

세부 구조는 [`docs/current_champion_v7.md`](docs/current_champion_v7.md)에 역사 기록으로 보존합니다.

### 3. BS V34 — Tree·Pair 공동 조정

V7에서 발전한 Tree + Pair 구조를 바탕으로 Tree quantile `0.54`, Pair quantile `0.48`, Pair weight `0.28`을 사용하는 공동 조정 구조로 이어졌습니다.

- 내부 MAE `0.148033`
- Public MAE `0.1271866667`
- 최종 8/6 통합 모델의 직접 기준점

원본 후보 비교는 [`stress_prediction_final_candidates_0806.ipynb`](https://github.com/thisisstress/stress_project_BS/blob/main/8_6/stress_prediction_final_candidates_0806.ipynb)에서 확인할 수 있습니다.

### 4. BS 8/6 — Final Integrated Model

V34 계열에 **gender 제거**, **Fold-local Winsorization**, **근접중복 Override**, **Pair weight 0.24**를 결합해 최종 발표 모델을 완성했습니다.

```text
ExtraTrees 76%
+ Pair-Neighbor 24%
→ Near-duplicate Override
→ round / clip
```

- Tree quantile `0.54`
- Pair quantile `0.48`
- Pair weight `0.24`
- Public MAE `0.1266866667`
- Private MAE `0.1473`

---

## 🗃️ 역사적으로 보존하는 분기

UNIFIED에는 최종 발표의 대표 연결 계보 외에도 당시 중요한 실험 기록을 그대로 남깁니다.

| 모델 | Public MAE | 현재 역할 |
|---|---:|---|
| V14 Blend95 | 0.1278085845 | 보수적 블렌딩 역사 기록 |
| V4 Conservative Quantile | 0.1286866667 | Quantile 통제 실험 |

이 모델들은 잘못된 모델이 아니라 **최종 발표 계보의 핵심 네 단계에서 벗어난 역사적 분기**이므로 삭제하지 않습니다.

---

## 🚀 처음 보는 사람을 위한 읽기 순서

1. **이 README** — 최종 계보와 대표 점수
2. [`docs/assets/model_lineage.svg`](docs/assets/model_lineage.svg) — 고해상도 벡터 계보도
3. [`docs/leaderboard.md`](docs/leaderboard.md) — 대표 계보와 역사 제출 기록
4. [`experiments/registry.csv`](experiments/registry.csv) — 실험 상태 레지스트리
5. [`docs/baseline_v1.md`](docs/baseline_v1.md) — V1 기준 모델
6. [`docs/current_champion_v7.md`](docs/current_champion_v7.md) — V7 역사 상세

최종 V34와 BS 8/6의 실행 원본은 `stress_project_BS`에 보존되어 있으며, UNIFIED에서는 중복 복사보다 **검증된 원본 위치와 계보를 연결**합니다.

---

## 🗂️ 저장소 구조

```text
stress_project_UNIFIED/
│
├── README.md
├── baseline/       # 고정 V1 기준 실행
├── configs/        # 버전별 설정 기록
├── docs/           # 모델 설명 · 리더보드 · 계보 이미지
├── experiments/    # 실험 문서와 registry
├── src/            # 공통 모듈 안내
└── submissions/    # 제출 관리 원칙
```

대회 데이터와 실제 제출 CSV는 Git에 중복 저장하지 않고 각 원본 연구 저장소와 로컬 실행 환경에서 관리합니다.

---

## 📐 점수 기록 원칙

- Public / Private 점수와 내부 CV 점수를 구분합니다.
- 서로 다른 split·seed·전처리 계약의 내부 MAE는 작은 차이로 직접 순위를 매기지 않습니다.
- 최종 발표의 대표 모델명과 점수는 원본 Notebook 및 팀 기록과 교차 확인합니다.
- 독립 연구 분기는 메인 계보에 억지로 합치지 않습니다.
- 과거 모델은 삭제하지 않고 역사적 역할을 명시합니다.
- UNIFIED의 표기는 **계보·점수·원본 위치를 연결하는 인덱스 역할**이며 각 연구 저장소의 실제 성과 소유와 provenance를 대체하지 않습니다.

---

<div align="center">

### Final Adopted Model

**BS 8/6 · ExtraTrees 76% + Pair-Neighbor 24%**

**Public MAE 0.1266866667 · Private MAE 0.1473**

</div>
