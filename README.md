# Stress Project UNIFIED

스트레스 점수 예측 대회의 팀 통합 실험 허브입니다.

## 모델 상태

### 현재 채택 모델 — V7 Pair-Neighbor Quantile Blend

- 모델: **V7 Pair-Neighbor Quantile Blend**
- Public MAE: **0.1272333333**
- 제출번호: **1507714**
- 제출 파일: `submit_v7_pair_neighbor_blend.csv`
- 제출 시각: **2026-08-01 14:43:42**
- 신규 Audit3 MAE: **0.146644**
- 상태: **Current Champion**

V7은 V6의 52% 분위수 ExtraTrees 예측 85%와,
8개 핵심 피처의 28개 2차원 조합에서 만든
Pair-Neighbor 1-NN 분위수 예측 15%를 혼합합니다.

```text
round(
    0.85 × V6 tree quantile
    + 0.15 × pair-neighbor quantile,
    2
)
```

### 고정 기준 모델 — V1 Weighted Quantile ExtraTrees

- Public MAE: **0.1282776667**
- 반복 CV 평균 MAE: **0.147505**
- 중복 표본 그룹 검증 MAE: **0.149202**
- 상태: **Frozen Baseline**

V1은 모든 신규 실험을 비교하기 위한 고정 기준입니다.
현재 최고 모델이 바뀌어도 V1의 코드와 설정은 수정하지 않습니다.

### 이전 최고 제출 — V14 Blend95

- Public MAE: **0.1278085845**
- 제출번호: **1506916**
- 상태: **Former Public Best**

V14는 기준 모델 95%와 다중 Seed·나이 건강 보조 예측 5%를
혼합한 보수적 블렌딩입니다. V7 승격 전 최고 제출로 보존합니다.

## 세 모델의 역할

| 역할 | 모델 | 용도 |
|---|---|---|
| Frozen Baseline | V1 | 모든 신규 실험의 공통 비교 기준 |
| Current Champion | V7 | 현재 재현·제출·후속 개선의 주 모델 |
| Former Public Best | V14 Blend95 | 이전 최고 제출과 앙상블 계보 보존 |

## 폴더 구조

```text
baseline/       고정 기준 모델 V1
champion/       현재 채택 모델 실행 코드
configs/        버전별 설정 기록
docs/           실험 규칙, 리더보드, 모델 보고서
experiments/    실험 문서와 레지스트리
src/            공통 모듈
submissions/    제출 파일 관리 규칙
```

## 데이터 배치

대회 데이터는 Git에 올리지 않고 로컬 `data` 폴더에 배치합니다.

```text
data/
├─ train.csv
├─ test.csv
└─ sample_submission.csv
```

## 환경 설치

```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install --upgrade pip
pip install -r requirements.txt
```

## V1 Baseline 실행

```bash
python3 baseline/v1_weighted_quantile_extratrees.py   --data-dir data   --output-dir outputs
```

## 운영 원칙

- V1은 삭제하거나 최고 모델로 덮어쓰지 않습니다.
- 신규 모델은 V1과 동일 Fold의 쌍대 비교를 우선합니다.
- 승격 후보는 새로운 Audit Seed에서도 확인합니다.
- Current Champion은 검증 기록과 제출 결과를 함께 보고 결정합니다.
- Public Score만 보고 설정을 반복 변경하지 않습니다.
- 제출 CSV, 데이터와 학습 모델은 Git에 올리지 않습니다.
