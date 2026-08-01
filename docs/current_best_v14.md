# V14 Blend95 — Former Public Best

## 현재 상태

V14 Blend95는 2026-07-31 당시 Public 최고였으나,
2026-08-01 V7 Pair-Neighbor Blend가 더 낮은 Public MAE를 기록해
현재 상태를 **Former Public Best**로 변경합니다.

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

실제 제출한 고정 95:5 후보의 CV MAE는 **0.149080**입니다.
자동 선택 Main의 CV 0.148953은 80:20 반올림 후보로 다른 설정입니다.

## 역할

- V1: Frozen Baseline
- V7: Current Champion
- V14: Former Public Best 및 보수적 블렌딩 계보

V14는 삭제하지 않고 향후 앙상블 다양성 비교 대상으로 보존합니다.

## 출처

- 원본 리포: `thisisstress/stress_project_BS`
- 노트북: `stress_prediction_v14_conservative_blend.ipynb`
- 커밋: `fef33607cb35021dae16f4be8abe108e3963ddf8`
