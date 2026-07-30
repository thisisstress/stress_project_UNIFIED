# Stress Project UNIFIED

스트레스 점수 예측 대회의 팀 통합 실험 허브입니다.

## 현재 기준 모델

- 버전: **V1**
- 모델: **Weighted Quantile ExtraTrees**
- 평가 지표: MAE
- Public MAE: **0.1282776667**
- 반복 CV 평균 MAE: **0.147505**
- 중복 표본 그룹 검증 MAE: **0.149202**

V1은 행 단위 건강 파생변수와 중요 피처 가중치를 적용한 ExtraTrees 1,200개의 개별 트리 예측을 **51% 분위수**로 집계합니다.

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

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## V1 실행

```powershell
python baseline\v1_weighted_quantile_extratrees.py --data-dir data --output-dir outputs
```

생성 파일:

```text
outputs/submit_v1_weighted_quantile_extratrees.csv
```

## 팀 운영 원칙

- 모든 신규 실험은 V1과 비교합니다.
- 한 실험에서는 핵심 가설을 가능한 한 하나만 바꿉니다.
- Public Score만으로 모델을 선택하지 않습니다.
- 전처리기는 Train 데이터에서만 학습합니다.
- 원본 데이터, 제출 CSV, 모델 파일은 Git에 올리지 않습니다.
- 신규 실험은 `exp/E001-...` 형태의 브랜치와 PR로 기록합니다.
