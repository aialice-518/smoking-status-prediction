# 🚬 건강 검진 데이터 기반 흡연 여부 예측

건강 검진 수치를 활용하여 흡연 여부를 예측하는 이진 분류 프로젝트입니다.

## 📊 데이터셋

| 구분 | 샘플 수 | 피처 수 |
|------|---------|---------|
| Train | 7,000 | 16 |
| Test | 3,000 | 15 |

**주요 변수:** 나이, 키, 몸무게, BMI, 시력, 공복 혈당, 혈압, 중성 지방, 콜레스테롤, 헤모글로빈 등

## 🗂️ 프로젝트 구조

```
├── data/                          # 원본 및 전처리 데이터
│   ├── train.csv
│   ├── test.csv
│   └── sample_submission.csv
├── notebooks/                     # 단계별 분석 노트북
│   ├── 01_EDA.ipynb               # 데이터 탐색
│   ├── 02_Preprocessing.ipynb     # 전처리 및 피처 엔지니어링
│   ├── 03_Modeling.ipynb          # 모델 학습 및 튜닝
│   └── 04_Evaluation.ipynb        # 평가 및 시각화
├── outputs/                       # 모델 저장 및 제출 파일
│   └── figures/                   # 시각화 이미지
│       ├── model_comparison.png
│       ├── confusion_matrix.png
│       ├── roc_curve.png
│       └── feature_importance.png
├── requirements.txt
└── README.md
```

## 🔍 분석 파이프라인

### 1. 데이터 탐색 (EDA)
- 변수별 분포 확인 (히스토그램 + 박스플롯)
- 결측치·이상치 탐지
- 상관관계 히트맵 및 타겟 변수와의 상관계수 Top 10 분석

### 2. 데이터 전처리
- 결측치: 평균값 대체
- 이상치: IQR 기반 클리핑 + 의학적 정상 범위 기반 클리핑
- 피처 엔지니어링: 지질 비율, 비만도 지표, 대사증후군 점수, 교호작용 변수 등 **30개+ 파생 변수** 생성
- KMeans 클러스터링 피처 추가

### 3. 모델링
- **기본 모델 비교:** RandomForest, LightGBM, XGBoost (5-Fold CV)
- **하이퍼파라미터 튜닝:** Ray Tune + Optuna (LightGBM, XGBoost)
- **AutoML:** AutoGluon `best_quality` (Auto Stacking + Bagging, 10-Fold)
- **앙상블:** 상위 모델 Soft Voting

### 4. 평가 및 시각화
- Accuracy, Precision, Recall, F1-score 비교
- Confusion Matrix, ROC Curve
- Feature Importance Top 20

## 🏆 주요 결과

> ⚠️ 아래는 예시 수치입니다. 노트북 실행 후 실제 결과로 업데이트해주세요.

| Model | Accuracy | Precision | Recall | F1-score |
|-------|----------|-----------|--------|----------|
| RandomForest | 0.74 | 0.72 | 0.68 | 0.70 |
| LightGBM | 0.78 | 0.76 | 0.73 | 0.74 |
| XGBoost | 0.77 | 0.75 | 0.72 | 0.73 |
| **AutoGluon Ensemble** | **0.80** | **0.78** | **0.76** | **0.77** |

## 📈 Visualization

모델 분석에 사용한 주요 시각화입니다. (`04_Evaluation.ipynb` 실행 시 자동 생성)

| 모델 성능 비교 | Confusion Matrix |
|:-:|:-:|
| ![Model Comparison](outputs/figures/model_comparison.png) | ![Confusion Matrix](outputs/figures/confusion_matrix.png) |

| ROC Curve | Feature Importance Top 20 |
|:-:|:-:|
| ![ROC Curve](outputs/figures/roc_curve.png) | ![Feature Importance](outputs/figures/feature_importance.png) |

## 🛠️ 기술 스택

- **언어:** Python
- **데이터 분석:** Pandas, NumPy
- **시각화:** Matplotlib, Seaborn
- **머신러닝:** Scikit-learn, LightGBM, XGBoost
- **AutoML:** AutoGluon
- **하이퍼파라미터 튜닝:** Ray Tune, Optuna
- **클러스터링:** KMeans

## ⚙️ 실행 방법

```bash
pip install -r requirements.txt
```

`notebooks/` 폴더의 노트북을 01 → 02 → 03 → 04 순서로 실행하세요.  
04번 노트북 실행 시 `outputs/figures/`에 시각화 이미지가 자동 저장됩니다.
