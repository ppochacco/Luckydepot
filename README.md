# Lucky Depot — 배송일자 예측 모델
**Office E-commerce Delivery Date Prediction**

> 고객의 주문 정보와 지역을 기반으로 예상 배송 소요일을 예측하는 e-commerce 서비스

📄 **[포트폴리오 상세 보기](#)** *(링크 추가 예정)*

---

## 📌 프로젝트 개요

| 항목 | 내용 |
|------|------|
| 기간 | 2025.01.14 – 2025.02.06 |
| 팀 구성 | 5인 |
| 담당 역할 | 데이터 분석 100%, iOS 앱 개발 참여 |

---

## 💡 핵심 인사이트

- **창고 위치 정보 없는 데이터 한계**를 지리적 클러스터링으로 극복 — Standard Class 배송 데이터 기반 지역별 배송 소요일 분포로 창고 위치 역추론
- **허리케인(Hurricane) 변수** 생성 및 통계 검증 → 모델 성능 개선에 유의미한 영향 확인
- **Badweather 변수** 추가 후 PCA로 클러스터링 → Main/Sub 데이터 분리 후 F-test로 통계적 유의성 검증 (p-value 기준)
- Main + Sub 클러스터 결합 모델에서 **GradientBoosting 최종 채택**

→ **"어느 지역 고객이 주문하면 배송이 며칠 걸리는가"를 예측해 주문 전 배송 예정일 제공**

---

## 🛠 기술 스택

| 분류 | 사용 기술 |
|------|-----------|
| 언어 | Python, Swift, Dart |
| 분석 | Pandas, NumPy, Scikit-learn |
| 모델 | GradientBoosting, RandomForest, KNN, PCA |
| 통계 검증 | F-test (p-value) |
| 앱 | SwiftUI, Flutter, FastAPI |
| DB | PostgreSQL |
| 협업 | GitHub, Notion, Figma, Miro, Jira |

---

## 📊 데이터

| 데이터 | 출처 | 기간 |
|--------|------|------|
| Superstore Sales Dataset | Kaggle | 2015 – 2018 |
| New York Housing Market | Kaggle | - |

- 총 9,800건 / Postal Code 결측 11건 처리
- Alaska, Hawaii 제외 미국 본토 48개 주 + D.C. 대상

---

## 🔍 분석 흐름

```
데이터 탐색 & 전처리
  ↓ Order Date / Ship Date → Shipping Duration 컬럼 생성
  ↓ Postal Code 결측 처리 / State 표준화
  ↓ unique_city 컬럼 생성 (State + City 조합)

창고 위치 역추론
  ↓ Standard Class 배송 기준 지역별 Shipping Duration 분포 분석
  ↓ CircleMarker 시각화로 배송 지연 지역 파악

변수 생성 및 검증
  ↓ Hurricane 변수 생성 (Ship Date 기준 이진 분류)
  ↓ PCA → Hurricane/Badweather 기반 클러스터링
  ↓ Main(941건) / Sub(137건) 분리
  ↓ F-test로 Main-Sub 간 Shipping Duration 차이 통계 검증

모델링
  ↓ 다중 모델 비교 (GradientBoosting, RandomForest, DecisionTree 등)
  ↓ GridSearch 하이퍼파라미터 튜닝
  ↓ Main + Sub 결합 → GradientBoosting 최종 채택
```

---

## 📁 디렉토리 구조

```
Luckydepot/
│
├── DataAnalysis/
│   ├── data_preprocessing.ipynb   # 전처리 및 EDA
│   ├── feature_engineering.ipynb  # 변수 생성 및 검증
│   └── modeling.ipynb             # 모델링 및 성능 비교
│
├── Model/
│   └── gradient_boosting.joblib
│
└── README.md
```

---

## 📈 모델 성능

| 모델 | 비고 |
|------|------|
| GradientBoosting | **최종 채택**(정확도 약 80% R^2 기준) |
| RandomForest | 비교 모델 |
| DecisionTree | 비교 모델 |
| KNN | 비교 모델 |

---

## 🤔 한계 및 개선점

- 2015–2018년 데이터로 최신 물류 패턴 반영 한계
- 실제 창고 위치 데이터 없이 역추론한 한계
- 실시간 기상 데이터 연동 시 Hurricane 변수 정확도 개선 가능
