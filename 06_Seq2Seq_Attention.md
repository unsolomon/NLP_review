# Seq2Seq와 Attention 정리

## 1. Seq2Seq 기본 개념

-   **구조:**
    1.  **Encoder** → 입력 문장(`I go to school`)을 순차적으로 읽어
        고정된 크기의 벡터(Latent vector)로 압축.
    2.  **Decoder** → 이 벡터를 받아서 출력 문장(`나는 학교에 간다`)을
        생성.
-   **특징:**
    -   입력/출력 길이가 달라도 처리 가능.
    -   기계 번역, 대화 시스템, 질의응답 등 다양한 NLP 응용에 사용.
-   **문제점 (Bottleneck problem):**
    -   긴 입력 문장을 하나의 고정된 벡터로만 요약하려다 보니, 정보가
        손실됨.
    -   특히 문장이 길수록 성능 저하.


------------------------------------------------------------------------

## 2. Attention 개념

-   **핵심 아이디어:**
    Decoder가 매 시점마다 Encoder 전체 hidden state를 다시 참조하면서,
    **중요한 단어에 더 집중(attend)** 하도록 함.

-   **동작 방식:**

    1.  Decoder의 현재 hidden state(예: `ht`)와 Encoder의 각 hidden
        state(입력 단어별) 사이의 **유사도 점수(score)** 계산.
    2.  Softmax로 정규화하여 "어떤 입력 단어가 중요한지" 확률
        분포(Attention weight)를 얻음.
    3.  이 가중치로 Encoder hidden state들을 **가중합(Weighted sum)** →
        Context vector 생성.
    4.  Decoder는 이 Context vector + 자신의 hidden state를 결합해 출력
        단어 예측.

👉 쉽게 말해:
- "I go to school"을 번역할 때,
- "나는"을 생성할 땐 `I`에 집중
- "학교에"를 생성할 땐 `school`에 집중
- 이런 식으로 **필요한 입력 부분만 골라 보는 것**

------------------------------------------------------------------------

## 3. Attention의 장점

-   **Bottleneck 해결:** Decoder가 고정 벡터 대신 Encoder의 전체 정보를
    직접 참고 가능.
-   **Vanishing gradient 문제 완화:** 먼 과거 단어에도 직접 연결 경로
    제공.
-   **성능 향상:** 기계 번역 등에서 품질 급상승.
-   **해석 가능성:** Attention 분포를 보면 모델이 어느 단어에 집중했는지
    알 수 있음 → 단어 Alignment 자동 학습.

------------------------------------------------------------------------


👉 요약:
- Seq2Seq는 번역 같은 시퀀스 변환에 필수 구조지만, 긴 문장에서 정보 손실
문제가 있음.
- Attention은 **Decoder가 Encoder 전체를 다시 보며 필요한 정보만 뽑아
쓰는 메커니즘**으로 이 문제를 해결함.
