# E003 V7 Pair-Neighbor Quantile Blend — Historical Team Milestone

## 목적

V6 Tree 모델의 전역 비선형 예측과
2차원 피처쌍 최근접 이웃의 국소 예측을 결합합니다.

## 가설

ExtraTrees와 다른 오차 구조를 가진 Pair-Neighbor 예측을
15%만 혼합하면 주 모델의 안정성을 유지하면서 잔차를 보정할 수 있습니다.

## 구조

```text
round(
    0.85 × V6 52% tree quantile
    + 0.15 × pair-neighbor 52% quantile,
    2
)
```

## 검증

| 구간 | V6 | V7 | ΔMAE |
|---|---:|---:|---:|
| Development Seed 42 | 0.151283 | 0.150560 | -0.000723 |
| Development 확인 Seed | 0.146502 | 0.146205 | -0.000297 |
| Audit3 | 0.147019 | 0.146644 | -0.000374 |

- Audit3 Seed 승률: 3/3
- Audit3 paired 95% CI: `[-0.000791, +0.000044]`
- CI가 0을 포함하므로 내부 검증 불확실성을 함께 보존

## 제출 결과

- 제출번호: `1507714`
- Public MAE: **0.1272333333**
- V1 `0.1282776667` 대비 약 **0.81% 상대 MAE 감소**
- V14 `0.1278085845` 대비 약 **0.45% 상대 MAE 감소**

## 현재 계보상 상태

- V7: **Historical team-lineage milestone**
- V1: Frozen initial baseline anchor
- Current team final: **BS 8/6 — Public MAE 0.1266866667 · Private MAE 0.1473**

현재 상태와 비교 규칙은 [Evaluation Notes](../docs/EVALUATION_NOTES.md)를 따릅니다.
