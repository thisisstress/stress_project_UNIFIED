# Evaluation Notes

이 문서는 `thisisstress` 조직의 공개 결과를 해석할 때 사용하는 기준 문서입니다.  
점수의 의미, 비교 가능한 범위, 최종 모델 선정 기준을 한곳에 고정해 과장되거나 잘못된 비교를 방지합니다.

## Project scope

- **Task:** 건강·생활 정형 데이터 기반 `stress_score` 회귀
- **Train rows:** 3,000
- **Target range:** `0~1`
- **Primary metric:** MAE — 낮을수록 우수
- **External data:** 사용하지 않음
- **Use boundary:** 해커톤·연구 프로젝트이며 임상 의사결정용 모델이 아님

## Canonical final result

| 항목 | 값 |
|---|---:|
| 최종 채택 모델 | **BS 8/6 — ExtraTrees + Pair-Neighbor** |
| 내부 검증 MAE | **0.147300** |
| Public MAE | **0.1266866667** |
| Private MAE | **0.1473** |
| Blend | **ExtraTrees 76% + Pair-Neighbor 24%** |

Canonical implementation:  
[`stress_project_BS/8_6/stress_prediction_combined_final_0806_1.ipynb`](https://github.com/thisisstress/stress_project_BS/blob/main/8_6/stress_prediction_combined_final_0806_1.ipynb)

## Public-score comparison rules

Public MAE끼리는 동일한 대회 Public 평가 축에서 비교할 수 있습니다.  
다만 비교 기준 모델을 명시하지 않은 채 단순히 “성능이 X% 향상됐다”고 표현하지 않습니다.

| Reference | Public MAE | Final vs reference | Relative MAE reduction | 해석 |
|---|---:|---:|---:|---|
| V1 initial baseline anchor | `0.1282776667` | `-0.0015910` | **약 1.24%** | 초기 공통 기준점 대비 |
| V14 historical public reference | `0.1278085845` | `-0.0011219` | **약 0.88%** | 역사적 Public 제출 대비, canonical baseline 아님 |
| Team V7 lineage milestone | `0.1272333333` | `-0.0005467` | **약 0.43%** | 후반 팀 계보 이정표 대비 |

따라서 **약 0.88%라는 수치는 V14를 비교 기준으로 명시할 때만 성립**합니다.  
포트폴리오나 외부 설명에서는 원 점수와 기준을 함께 적는 것을 기본 규칙으로 합니다.

권장 예시:

> Public MAE `0.12781 → 0.12669`, ΔMAE `-0.00112` (V14 historical public reference 대비 약 0.88% 상대 감소)

## Internal validation comparison rules

내부 MAE는 실험마다 split, seed, 전처리, fold 계약이 다를 수 있습니다.  
따라서 서로 다른 검증 계약에서 나온 미세 MAE 차이를 직접 순위화하지 않습니다.

특히 다음 두 문장을 구분합니다.

- **가능:** “같은 검증 계약에서 A가 B보다 MAE가 낮았다.”
- **금지:** “서로 다른 OOF 계약의 숫자만 보고 A가 B보다 우수하다.”

## Why the final model is not the lowest Public score ever observed

실험 과정에는 Public MAE `0.1265`를 기록한 Fresh V6도 있습니다.  
그러나 해당 후보는 최종 채택 모델과 동등한 수준의 내부/Private 검증 계약과 재현 근거가 확보되지 않아 **최종 채택 계보에 포함하지 않았습니다**.

이 프로젝트는 Public leaderboard 단일 점수만으로 모델을 선택했다는 주장을 하지 않습니다.  
최종 보고에서는 내부 검증, 재현 가능한 실행 계약, Private 결과와 모델 계보를 함께 봅니다.

## Leaderboard claims

순위 주장은 별도 보존된 공식 근거가 없는 경우 사용하지 않습니다.  
공개 문서에서는 재현 가능한 **점수와 제출 시각**을 우선 기록합니다.

## Attribution

프로젝트 저자는 **김지현 · 박빛샘 · 안상균** 3인입니다.  
저장소 이름이나 브랜치는 소유권 또는 단독 기여를 뜻하지 않습니다.

- 역할 표기는 발표 자료와 저장소 기록의 주요 담당 영역을 요약한 것
- 가설 수립, 실험, 검증, 최종 모델 선정은 팀 협업
- 세부 변경 이력은 각 저장소 Git history로 확인 가능

## Evidence map

- [최종 계보와 결과](../README.md)
- [제출 ledger](leaderboard.md)
- [실험 registry](../experiments/registry.csv)
- [V1 baseline anchor](baseline_v1.md)
- [V7 lineage milestone](current_champion_v7.md)
- [BS 최종 모델 저장소](https://github.com/thisisstress/stress_project_BS)
- [JH V7 재현·검증 저장소](https://github.com/thisisstress/stress_project_JH)

## What this project does not claim

- 임상적 유효성 또는 의료 진단 성능
- 외부 모집단에 대한 일반화 성능
- 단일 Public leaderboard 점수만으로 입증된 우월성
- 서로 다른 내부 검증 계약 간 미세 점수 차이의 직접 우열
- 기준을 명시하지 않은 단일 퍼센트 성능 향상 표현
