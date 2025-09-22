# Decoding을 통한 자연어 생성

## 1. 자연어 생성에서 Decoding 과정

-   입력 문장 **x** → 출력 문장 **y** 생성
-   목표: 학습된 LM을 통해 확률이 가장 높은 **y** 선택

\[ `\arg`{=tex}`\max`{=tex}*y `\log `{=tex}P*{LM}(y\|x) \]

-   **문제**: Exhaustive search는 어휘 크기 (v)와 문장 길이 (t)에 따라
    (v\^t) 계산 필요 → 불가능
-   해결: Auto-regressive LM 활용 → 다음 단어 확률
    (P(y_i\|y_1,`\dots`{=tex},y\_{i-1},x)) 로 분해

------------------------------------------------------------------------

## 2. Greedy Decoding

-   매 Time-step에서 가장 확률 높은 Token 선택
-   단점:
    -   초기 선택이 잘못되면 이후 전체 문장에 영향
    -   최적해 보장 불가

------------------------------------------------------------------------

## 3. Beam Search

-   **Beam size = k**: 매 단계에서 상위 k개의 후보 유지
-   후보 Score:

\[ `\text{score}`{=tex}(y_1,`\dots`{=tex},y_t) = `\sum`{=tex}*{i=1}\^t
`\log `{=tex}P*{LM}(y_i\|y\_{1:i-1},x) \]

-   특징:
    -   log 확률 합으로 Score 계산 (모두 음수 → 값이 클수록 적절)
    -   각 단계마다 확률 높은 후보 k개 선택 → 최종적으로 가장 높은 Score
        문장 선택
-   종료 기준:
    -   `<END>` 토큰 도달 시 종료
    -   Beam size 유지하며 후보 관리
    -   일정 개수 문장 생성 시 종료
-   **문제점**:
    -   긴 문장은 불리 → 길이 Normalize 필요
    -   반복에 취약, 다양성 부족

------------------------------------------------------------------------

## 4. Sampling 기반 기법

### 4.1 기본 Sampling

-   확률 분포에 따라 단어를 무작위 선택
-   동일 입력에서도 다양한 출력 가능

### 4.2 Temperature (τ)

-   확률 분포를 조정하는 파라미터
-   τ \> 1 → 확률 분포 평탄화 → **다양성 ↑**
-   τ \< 1 → 확률 분포 뾰족화 → **정확성 ↑**
-   τ → 0 → Greedy decoding과 동일

### 4.3 Top-k Sampling

-   상위 k개 단어만 후보로 두고 Sampling
-   단점: k개로만 제한 시 비슷한 단어 간 구분 어려움

### 4.4 Top-p Sampling (Nucleus Sampling)

-   누적 확률이 p가 될 때까지 후보 선택
-   확률 분포에 따라 후보 개수 유동적
    -   평평한 분포 → 많은 단어 포함
    -   뾰족한 분포 → 적은 단어 포함

------------------------------------------------------------------------

## 5. 방법론 정리

-   **Tokenization**: Character, Word, BPE
-   **Statistical NLP**: Word Embedding, Word2Vec, Skip-gram
-   **RNN 계열**: RNN, LSTM, GRU, Seq2Seq, Seq2Seq+Attention
-   **Advanced NLP**: Transformer, BERT
-   **Decoding 기법**: Greedy, Beam, Top-k, Top-p
