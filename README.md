
# 🧠 성별 예측 분류 모델링 보고서

## 📌 프로젝트 개요
이 프로젝트는 백화점 고객의 1년치 구매 데이터를 바탕으로 고객의 성별을 예측하는 머신러닝 분류 모델을 구축하는 데 목적이 있습니다. 총 3,500명의 고객 데이터를 기반으로 다양한 피처를 전처리 및 변환하고, 여러 알고리즘을 테스트하여 최적의 모델을 선정했습니다.

---

## 🗂️ 데이터 구성
- **X.csv**: 고객의 구매 관련 변수(피처) 데이터  
- **y.csv**: 고객의 성별 (타겟값: 0 또는 1)

### 주요 변수 예시
- 총구매액, 최대구매액, 환불금액, 내점일수, 내점당구매건수, 구매주기, 주말방문비율 등  
- 파생 변수: 방문당평균구매액, 환불비율, 총구매건수, 잠재고객충성도 등

---

## ⚙️ 분석 절차
1. 데이터 불러오기  
2. 기초 탐색(EDA) – 변수 간 분포 및 상관관계 시각화  
3. 전처리 – 결측치 확인 및 처리, 정규화(스케일링), 범주형 변수 인코딩  
4. 특성 공학 – 파생변수 생성 (예: 방문당평균구매액 = 총구매액 / 내점일수)  
5. 학습/테스트 데이터 분리  
6. 모델 학습 – 로지스틱 회귀, 랜덤포레스트, KNN  
7. 성능 평가 – 정확도, 정밀도, 재현율, 혼동행렬 등  
8. GridSearchCV를 통한 하이퍼파라미터 튜닝

---

## 🤖 사용한 알고리즘

| 알고리즘               | 주요 특징                                 |
|------------------------|--------------------------------------------|
| Logistic Regression     | 기준 모델, 선형적 해석 가능               |
| Random Forest Classifier| 앙상블 기반 모델, 중요 변수 파악 가능     |
| K-Nearest Neighbors     | 거리 기반 비선형 분류기                   |

---

## 📊 모델 성능 평가

- 다양한 모델을 테스트한 결과, 일부 모델은 Threshold를 조정하여 정밀도/재현율 균형을 맞춤
- 최종 모델은 `RandomForestClassifier` 또는 `XGBoost` 등 성능이 높은 분류기를 기반으로 선택

### 최종 모델 기준 성능 지표
- **혼동 행렬**  
  ```
  [[375  88]
   [154  83]]
  ```

- **정량적 성능 지표**
  - 🎯 정확도(Accuracy): 0.654  
  - 🎯 정밀도(Precision): 0.485  
  - 🎯 재현율(Recall): 0.350

---

## 🔍 시사점 및 해석

- 정확도는 약 65% 수준으로, 불균형한 성별 데이터를 고려했을 때 baseline 모델보다 조금 나은 수준으로 판단됩니다.
- **정밀도(0.485)**는 모델이 "남성(1)"이라고 예측한 샘플 중 실제로 남성일 확률이 약 48.5%임을 의미합니다.
- **재현율(0.350)**은 실제 남성 중에서 모델이 남성으로 정확히 맞춘 비율로, 놓치는 케이스가 많음을 시사합니다.
- 전체적으로 모델이 ‘1(남성)’ 클래스를 잘 탐지하지 못함 → 이는 학습 데이터 내 성별 불균형 혹은 남성을 대표하는 명확한 특성이 부족할 수 있음을 나타냅니다.

---

## 💡 향후 개선 방향 제안

- 데이터 불균형 처리: SMOTE, 언더샘플링 등을 활용해 학습 데이터 균형 맞추기  
- 정교한 파생변수 추가: 방문 시간대, 고가/저가 구매 여부 등  
- 모델 앙상블 및 하이퍼파라미터 튜닝: XGBoost나 LightGBM 등을 도입해 성능 향상 가능성 모색  
- SHAP 등 해석 가능한 AI 기법을 도입해 어떤 특성이 성별 분류에 영향을 주는지 분석
