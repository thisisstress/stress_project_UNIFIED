# E002 V4 Conservative Quantile ExtraTrees

## 목적

V1 구조를 유지하고 집계 분위수만 51%에서 50.5%로 변경해
분위수 선택의 민감도를 확인합니다.

## 결과

- 대표 Train-only MAE: 0.147434
- Public MAE: 0.1286866667
- V1 Public 대비: +0.000409
- 상태: 미채택

## 재감사

- Development 평균 MAE: 0.148947
- Audit 평균 MAE: 0.149289
- Audit Seed 승률: 2/3
- Audit 쌍대 95% CI: [-0.000237, +0.000096]

## 결론

V1의 51% 분위수 선택을 확인한 통제 실험으로 보존합니다.
