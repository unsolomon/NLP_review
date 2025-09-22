# Self-Supervised Learning & BERT 요약

## 1. Self-Supervised Learning
- 데이터 일부를 숨기고, 숨겨진 부분을 예측하도록 학습  
- 라벨 없이 대규모 데이터 활용 가능  

## 2. Transfer Learning
- **Pre-training (사전 학습)**: Self-supervised 방법으로 대규모 데이터에서 일반적 표현 학습  
- **Fine-tuning (전이 학습)**: 사전 학습된 모델을 특정 다운스트림(Task)에 맞게 미세 조정  
- 필요에 따라 일부 모듈은 Target task용으로 교체  

---

## 3. BERT (Bidirectional Encoder Representations from Transformers)
- 구조: 대형 Transformer Encoder  
- 학습 태스크:
  - **Masked Language Modeling (MLM)**  
    - 입력 토큰의 15%를 마스킹 후 예측  
    - 80%: `[MASK]`, 10%: 랜덤 토큰, 10%: 원래 토큰 유지  
  - **Next Sentence Prediction (NSP)**  
    - 문장 A 뒤에 문장 B가 실제 이어지는지 판별  

### Input Embedding
- **Token Embedding**: WordPiece 기반  
- **Segment Embedding**: 문장 구분  
- **Position Embedding**: 위치 정보 (trainable)  
- Special Tokens: `[CLS]`, `[SEP]`  

### 모델 크기
- **BERT-Base**: 12층, hidden 768, 12-head attention  
- **BERT-Large**: 24층, hidden 1024, 16-head attention  

---

## 4. Downstream Tasks
1. **Sentence Classification**  
   - 단일 문장 분류 (e.g., SST-2, CoLA)  
   - `[CLS]` 벡터로 분류  

2. **Sentence Pair Classification**  
   - 두 문장 관계 예측 (e.g., MNLI, QQP, STS-B)  
   - `[CLS]` 벡터 + `[SEP]`, segment embedding 활용  

3. **Sentence Tagging**  
   - 토큰 단위 속성 예측 (e.g., NER, CoNLL-2003)  

4. **Machine Reading Comprehension (MRC)**  
   - 질문에 대한 답변 span 예측 (e.g., SQuAD)  

---

## 5. 정리
- Self-supervised → Pre-training → Fine-tuning 과정  
- BERT 핵심 학습 태스크: MLM, NSP  
- 입력: Token + Segment + Position Embedding  
- 다양한 NLP Task에 효과적으로 적용 가능  
