***
# NLP Tokenization 

## 1. 시퀀스 데이터와 Tokenization

### 시퀀스 데이터(Sequence Data)

- 시간 또는 순서에 따라 배열된 데이터로, 각 요소가 인접 요소들과 관계를 가짐.


### Tokenization(토큰화) 개념

- **Tokenization**은 자연어 텍스트를 의미 있는 최소 단위인 토큰(Token)으로 분할하는 과정.
- 토큰은 주로 단어, 형태소, 문자, 또는 서브워드 단위를 뜻하며, 처리 가능한 토큰 목록을 **Vocabulary**(단어 사전)이라 부름


#### 필수 개념 정리

- 텍스트를 모델이 이해할 수 있도록 **가장 작은 단위(토큰)**로 분해
- 모든 NLP 작업의 첫 단계로, 이후 임베딩 및 모델링의 토대가 됨

***

## 2. Tokenization 주요 방식

### 2.1 Word-level Tokenization

- 띄어쓰기나 형태소를 기준으로 텍스트를 단어별로 분할
- 한국어는 형태소 분석도 활용; 입력 예시: "나는 밥을 먹었다" → ['나', '는', '밥', '을', '먹', '었다'].
- **장점**: 직관적이고 구현이 쉬움, 대부분의 전통적 NLP에 사용됨.
- **단점**: 사전에 없는 단어(OOV)는 모두 "Unknown" 토큰으로 처리되며 정보 손실이 발생할 수 있음.


### 2.2 Character-level Tokenization

- 각 텍스트를 문자 단위로 분할.
- **장점**: 모든 단어를 커버(OOV 없음), 다국어에서도 문제 없음
- **단점**: 토큰 수가 매우 많아지고, 의미 해석이 힘들어 예측 성능 저하·메모리 사용 급증.


### 2.3 Subword-level Tokenization

- 자주 등장하는 문자 또는 음절 조합을 Subword로 분할
- **장점**: OOV 문제 해결, 적절한 어휘 크기와 뛰어난 표현력·성능.
- **단점**: 분할 단위가 직관적이지 않을 수 있음.

***

## 3. OOV(Out-of-Vocabulary) 처리

- **Word-level**에서는 사전 밖의 모든 단어를 "Unknown" 토큰으로 처리해 정보가 손실된다.
- **Character/Subword-level**에서는 OOV 문제가 사실상 사라져, 학습 및 예측 효율성이 증가한다.

***

## 4. Subword Tokenization 알고리즘

### 4.1 BPE(Byte Pair Encoding)

- 텍스트를 문자 단위로 분할한 후, 가장 빈번하게 등장하는 문자쌍(n-gram)을 반복적으로 병합하여 의미 있는 서브워드 단위 토큰을 생성.
- 예시: "lower" → ['l', 'o', 'w', 'e', 'r'], 빈도가 높은 쌍 "lo" 합쳐서 ['lo', 'w', 'e', 'r'].
- 병합을 반복해 최적의 어휘집 구성.


### 4.2 WordPiece

- 데이터 내 우도(likelihood)가 높은 문자·음절 쌍을 반복·추가해서 어휘 사전을 구성.
- 활용 모델: **BERT, DistilBERT, ELECTRA**.


### 4.3 SentencePiece

- 공백을 포함한 다양한 문장 단위 분할로, 언어별 종속성 없이 서브워드 단위를 생성.
- 활용 모델: **ALBERT, XLNet, T5**.
***

## 5. 요약 Table: Tokenization 방식 \& 필수 포인트

| 방식 | 장점 | 단점 | OOV 문제 | 대표 활용 모델 |
| :-- | :-- | :-- | :-- | :-- |
| Word-level | 직관적, 구현 쉬움 | OOV 발생, 정보 손실 | 있음 | 형태소 분석기 |
| Character-level | 모든 단어 커버, OOV 없음 | 토큰 다수, 성능 저하 가능 | 없음 | 일부 다국어 모델 |
| Subword-level | OOV 없음, 우수한 표현력 | 분할 기준 불명확할 수 있음 | 없음 | BERT, T5 등 |


***

## 6. 실전 복습을 위한 핵심 CHECKLIST

- Tokenization의 정의와 목적
- 모든 Tokenization 방식의 장단점(Word/Character/Subword)
- OOV 개념 및 처리 방식
- BPE, WordPiece, SentencePiece 알고리즘 특징
- 각 알고리즘을 사용하는 대표 NLP 모델과 적용 사례

***