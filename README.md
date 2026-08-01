# Stress Project UNIFIED

스트레스 점수 예측 대회의 팀 통합 실험 허브입니다.

## 현재 최고 제출 모델

- 버전: **V14 Blend95**
- 모델: **Conservative Blend**
- 평가 지표: MAE
- Public MAE: **0.1278085845**
- 제출번호: **1506916**
- 제출 파일: `submit_v14_blend95.csv`
- 제출 시각: **2026-07-31 14:52:53**
- 해당 고정 후보 5-Fold CV MAE: **0.149080**

V14 Blend95는 기존 기준 모델인 Weighted Quantile ExtraTrees 예측을
**95% 유지**하고, 다중 Seed ExtraTrees와 나이·건강 상호작용 모델로
구성한 보조 예측을 **5% 혼합**한 보수적 블렌딩입니다.

## 기준 모델

재현성과 비교 기준을 위한 Baseline은 기존 **V1 Weighted Quantile ExtraTrees**를 유지합니다.

- Public MAE: **0.1282776667**
- 반복 CV 평균 MAE: **0.147505**
- 중복 표본 그룹 검증 MAE: **0.149202**

V1은 행 단위 건강 파생변수와 중요 피처 가중치를 적용한
ExtraTrees 1,200개의 개별 트리 예측을 51% 분위수로 집계합니다.

## 현재 최고 모델과 기준 모델의 역할

- **V1 Baseline**: 모든 신규 실험의 비교 기준
- **V14 Blend95**: 현재 Public 최고 제출 모델
- V1 코드는 기준점 보존을 위해 직접 수정하지 않습니다.
- V14는 BS 리포의 검증 기록과 제출 결과를 UNIFIED에 등록한 것입니다.

## 폴더 구조

```text
baseline/       재현 가능한 기준 모델
configs/        모델 설정 기록
docs/           기준 모델, 실험 규칙, 리더보드
experiments/    실험 문서와 레지스트리
src/            향후 공통 모듈
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

## V1 실행

```bash
python3 baseline/v1_weighted_quantile_extratrees.py \
  --data-dir data \
  --output-dir outputs
```

생성 파일:

```text
outputs/submit_v1_weighted_quantile_extratrees.csv
```

## 팀 운영 원칙

- 신규 실험의 검증 비교 기준은 V1으로 유지합니다.
- Public 최고 기록은 별도 상태로 관리합니다.
- 한 실험에서는 핵심 가설을 가능한 한 하나만 바꿉니다.
- Public Score만으로 모델을 선택하지 않습니다.
- 전처리기는 Train 데이터에서만 학습합니다.
- 원본 데이터, 제출 CSV, 모델 파일은 Git에 올리지 않습니다.
- 신규 실험은 `exp/E002-...` 형태의 브랜치와 PR로 기록합니다.
