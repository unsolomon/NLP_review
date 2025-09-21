# Transformer Block 정리

## 1. Transformer Block 구조

-   각 Block은 **두 개의 Sub-layer**로 구성
    1.  **Multi-Head Attention**
        -   Sequence dimension(시퀀스 길이 축)에 대해 Attention 적용
    2.  **Two-Layer Perceptron (MLP)**
        -   Hidden dimension 축에 대해 적용
        -   ReLU activation 사용
-   각 Sub-layer에는 공통적으로 포함됨:
    -   **Residual Connection** (입력 + 출력 더하기)
    -   **Layer Normalization** (정규화)

------------------------------------------------------------------------

## 2. Layer Normalization

-   입력을 평균 0, 분산 1로 변환
-   **Batch Normalization과의 차이점**
    -   BatchNorm: 배치 전체 단위로 정규화
    -   LayerNorm: **입력 시퀀스 내 단어/토큰 단위**로 정규화
-   장점: 시퀀스 길이에 독립적 → NLP에 적합

------------------------------------------------------------------------

## 3. Add & Norm

-   Multi-Head Attention의 출력과 입력 벡터를 더함 (**Residual**)
-   그 결과를 **Layer Normalization**으로 정규화
-   안정적인 학습과 성능 향상에 도움

------------------------------------------------------------------------

## 4. Masked Attention (Decoder)

-   **필요성:** 언어 생성 과정에서, 아직 생성되지 않은 단어에 접근하면
    안 됨
-   **방법:** Softmax 출력을 수정하여 미래 단어를 참조하지 못하도록
    제한
-   다른 말로 **Causal Attention**이라고도 부름
-   적용 위치: Decoder의 Self-Attention

------------------------------------------------------------------------

## 5. Positional Encoding (Transformer 특징 보완)

-   Transformer는 RNN이 아니므로 입력 순서를 구분하지 못함
    (Permutation-invariant)
-   따라서 **위치 정보를 추가**해야 함
-   원 논문에서는 **Sinusoidal 함수 기반 인코딩** 사용
-   이후 학습 가능한 Positional Embedding 기법도 많이 사용됨

------------------------------------------------------------------------

## 6. 핵심 요약

-   Transformer Block = **Multi-Head Attention + MLP + Residual +
    LayerNorm**
-   Layer Normalization: 시퀀스 단위 정규화
-   Decoder의 **Masked Attention**: 미래 단어 차단
-   Positional Encoding: 단어 순서 정보 추가
