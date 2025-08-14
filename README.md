# 📊 Sentiment Analysis Pipeline

이 프로젝트는 **YouTube 댓글 데이터**를 기반으로 **감성 분석(Sentiment Analysis)** 을 수행하는 **Python 파이프라인**입니다.  
텍스트 데이터 **전처리 → 모델 학습 → 예측 → 결과 저장**까지의 전 과정을 포함합니다.

---

## ✨ 주요 기능

### 📂 데이터 로드 및 전처리
- CSV/JSON에서 댓글 데이터 불러오기
- HTML 태그, 특수문자 제거 및 토큰화

### 🏷 데이터 라벨링 방법

본 프로젝트의 초기 라벨링은 **VADER Sentiment Analyzer**를 사용한 사전 기반 방식으로 수행되었습니다.

- **긍정(positive)**: 감성 점수 ≥ 0.05
- **중립(neutral)**: -0.05 < 감성 점수 < 0.05
- **부정(negative)**: 감성 점수 ≤ -0.05

라벨링 과정:
1. 댓글 텍스트를 전처리 (HTML 태그, 특수문자 제거)
2. VADER 분석기를 통해 감성 점수(`compound`) 계산
3. 위 기준에 따라 라벨 부여
4. 이후 Logistic Regression 모델 학습 데이터로 사용

### 🧠 감성 분석 모델 학습
- **TF-IDF** 벡터화
- **Logistic Regression** 분류기 사용
- `GroupShuffleSplit`을 이용해 `video_id` 기준으로 학습/검증 데이터 분리

### 🔍 결과 예측
- 예측 라벨(`positive`, `neutral`, `negative`) 부여
- 각 예측의 **신뢰도(confidence)** 계산

### 💾 결과 저장
- CSV 및 JSON 파일로 저장
- 시각화를 통한 분포 확인 가능

---

## 🛠 기술 스택

| 구분 | 내용 |
|------|------|
| **언어** | Python 3.11+ |
| **라이브러리** | `pandas`, `numpy`, `scikit-learn`, `tqdm`, `vaderSentiment`, `joblib` |

---

## 📂 프로젝트 구조

```plaintext
Sentiment Analysis.ipynb          # 메인 코드 (Jupyter Notebook)
data/
    example.csv                   # 입력 데이터 예시
output/
    comments_with_sentiment.csv   # 예측 결과 CSV
    comments_with_sentiment.json  # 예측 결과 JSON
