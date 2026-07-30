# 실험 운영 규칙

## 기준 모델

모든 신규 실험은 V1과 비교합니다.

- 반복 CV 평균 MAE: 0.147505
- 중복 그룹 검증 MAE: 0.149202
- Public MAE: 0.1282776667

## 실험 번호와 브랜치

```text
E001 / exp/E001-change-quantile
E002 / exp/E002-add-health-features
E003 / exp/E003-tune-leaf-size
```

## 원칙

- 한 실험에서는 핵심 가설을 가능한 한 하나만 변경합니다.
- 1차는 Seed 42 단일 5-Fold로 빠르게 검증합니다.
- 승격 후보는 Seed 42, 2026, 3407과 중복 그룹 분할로 확인합니다.
- Public Score만 보고 설정을 반복 변경하지 않습니다.
- 제출 CSV는 Git에 올리지 않습니다.

## PR 필수 기록

- 실험 가설
- V1 대비 변경점
- 검증 방식
- Fold별 MAE와 전체 OOF MAE
- 기존 모델 대비 개선율
- 제출 여부
- 위험 또는 한계
