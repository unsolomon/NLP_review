# 📘 부스트캠프 NLP 이론 2강 정리 (Word Embedding)

## 1. Vector Representation

데이터를 수치적/기하학적으로 표현하여 컴퓨터가 이해할 수 있도록 만드는
방법.

### 1.1 One-Hot Encoding

-   단어를 **범주형 변수(Categorical Variable)**로 인코딩한 벡터
-   특징
    -   각 차원은 하나의 단어에 해당\
    -   나머지는 `0`으로 채워져 **희소 표현(Sparse Representation)**이
        됨\
    -   예시: 혈액형 (A, B, AB, O) → `[1,0,0,0]`, `[0,1,0,0]` ...
-   한계
    -   단어 간 **내적 유사도 = 항상 0**\
    -   단어 간 **유클리드 거리 = 항상 √2**

------------------------------------------------------------------------

### 1.2 Distributed Vector Representation (Dense Vector)

-   단어 의미를 여러 차원에 **0이 아닌 값**으로 분산 표현
-   장점
    -   유클리드 거리, 내적, 코사인 유사도 → **의미론적 유사성** 반영
        가능
-   대표적 방법: **Word2Vec**
    -   주변 단어 정보를 활용하여 단어 벡터를 학습\
    -   **"You shall know a word by the company it keeps."** -- J.R.
        Firth (1957)

------------------------------------------------------------------------

## 2. Word2Vec

### 2.1 핵심 아이디어

-   단어 의미는 **주변 단어 등장 확률 분포**에 의해 정의됨\
-   예: "cat" → "meow"(0.57), "pet"(0.34) 등은 높은 확률 /
    "potato"(0.03) 낮음

------------------------------------------------------------------------

### 2.2 학습 방법

1.  **Continuous Bag of Words (CBOW)**
    -   주변 단어들로 중심 단어를 예측\
2.  **Skip-gram (자주 사용됨)**
    -   중심 단어로 주변 단어들을 예측\
    -   `Window size` 만큼 앞뒤 단어 학습\
    -   주변 단어 개수만큼 학습 기회 제공

------------------------------------------------------------------------

### 2.3 작동 원리

-   **Window size** 설정 (예: 3 → 앞뒤 3 단어)\
-   중심 단어 → 주변 단어 예측\
-   학습 과정에서 **의미 유사 단어 벡터가 가까워짐**
    -   `drink` → juice, milk, water\
    -   `eat` → apple, orange, rice

------------------------------------------------------------------------

### 2.4 Word2Vec 속성

-   **벡터 연산 가능 (Analogy reasoning)**
    -   `vec[queen] - vec[king] ≈ vec[woman] - vec[man]`\
-   **Semantic Similarity**
    -   유사 단어 간 내적값이 높음\
    -   예: `study ↔ math`, `drink ↔ water`

------------------------------------------------------------------------

## 3. Summary

-   One-hot encoding → 가장 기본적인 표현 방식 (희소 표현)\
-   Word Embedding → 의미 기반 분산 표현\
-   Word2Vec → Skip-gram / CBOW 학습 방식\
-   학습된 임베딩 활용 → **시각화, 유사 단어 탐색, 관계 추론**

------------------------------------------------------------------------

## 📖 References

-   Mikolov et al., *Distributed Representations of Words and Phrases
    and their Compositionality*, NeurIPS 2013\
-   [논문
    링크](https://proceedings.neurips.cc/paper/2013/file/9aa42b31882ec039965f3c4923ce901b-Paper.pdf)