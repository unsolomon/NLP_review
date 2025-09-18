# LSTM과 GRU 정리

## 1. LSTM (Long Short-Term Memory)

### 핵심 아이디어

-   RNN의 장기 의존성 문제(long-term dependency)를 해결하기 위해
    설계됨.
-   **Cell state**라는 별도의 정보 통로가 있어서, 정보가 왜곡되지 않고
    길게 전달됨.
-   여러 **Gate(문)**을 두어 어떤 정보를 기억하고, 버리고, 출력할지를
    선택함.

### 주요 구성 요소

-   **Forget gate (ft):** 이전 상태(ct-1)를 얼마나 유지할지 결정
-   **Input gate (it):** 새로운 정보를 얼마나 저장할지 결정
-   **Candidate (gt):** 새로 추가될 정보 후보
-   **Output gate (ot):** 현재 hidden state(ht)를 얼마나 외부로 보낼지
    결정

### 계산 흐름

1.  **이전 상태 + 현재 입력** → 게이트들(sigmoid, tanh) 통해 각각 계산

2.  Cell state 업데이트:

        ct = ft ⊙ ct-1 + it ⊙ gt

3.  Hidden state 계산:

        ht = ot ⊙ tanh(ct)

👉 쉽게 말해:
- "잊을 건 잊고(ft), 새로 들어온 걸 적당히 추가(it), 최종적으로
결과(ht)를 내보내자(ot)"

------------------------------------------------------------------------

## 2. GRU (Gated Recurrent Unit)

### 핵심 아이디어

-   LSTM을 단순화한 버전.
-   **Cell state와 hidden state를 합쳐서 하나의 벡터로 관리**.
-   계산량이 줄고 구조가 간단해짐.

### 주요 구성 요소

-   **Update gate (zt):** 얼마나 새로운 정보로 업데이트할지 결정 (LSTM의
    input + forget gate 역할)
-   **Reset gate (rt):** 이전 hidden state 정보를 얼마나 초기화할지
    결정
-   **Candidate hidden (h\~t):** 새로운 hidden state 후보

### 계산 흐름

1.  Update gate와 Reset gate 계산

        zt = σ(Wz[ht-1, xt])
        rt = σ(Wr[ht-1, xt])

2.  Candidate hidden 계산

        h~t = tanh(W[rt ⊙ ht-1, xt])

3.  최종 hidden state 업데이트

        ht = (1 - zt) ⊙ ht-1 + zt ⊙ h~t

👉 쉽게 말해:
- "이전 정보(ht-1)를 얼마나 유지할지(zt), 얼마나 리셋할지(rt) 결정 →
새로운 후보(h\~t)를 계산 → 최종 ht를 업데이트"

------------------------------------------------------------------------

## 3. LSTM vs GRU 비교

  ------------------------------------------------------------------------
  구분                      LSTM                      GRU
  ------------------------- ------------------------- --------------------
  게이트 수                 3개(Forget, Input,        2개(Update, Reset) +
                            Output) + Candidate       Candidate

  상태 관리                 Cell state + Hidden state Hidden state 하나
                            (2개)                     

  구조                      복잡, 계산량 많음         단순, 계산 효율적

  성능                      긴 시퀀스 학습에서 강점   작은 데이터셋·빠른
                                                      학습에 유리
  ------------------------------------------------------------------------

------------------------------------------------------------------------

👉 요약하면,
- **LSTM = 장기 기억에 강한 꼼꼼한 구조**
- **GRU = 계산 효율을 높인 간단한 구조**
