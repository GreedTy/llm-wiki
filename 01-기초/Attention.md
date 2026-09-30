---
tags: [concept, 기초]
aliases: [어텐션, Self-Attention, 셀프 어텐션, Multi-Head Attention]
updated: 2026-09-30
---

# Attention

## 한 줄 정의
Attention은 각 토큰이 시퀀스의 다른 토큰들을 얼마나 참고할지 가중치로 계산해서, 그 가중합으로 새로운 표현을 만드는 연산입니다.

## 동작 원리
1. 각 토큰 벡터에서 Query(Q), Key(K), Value(V)를 선형 변환으로 만듭니다.
2. Q와 모든 K의 내적을 구하고 √d로 나눈 뒤 softmax를 적용합니다. 이 값이 어텐션 가중치입니다.
3. 가중치로 V를 가중합합니다.

수식으로는 `Attention(Q,K,V) = softmax(QKᵀ/√d)·V` 입니다.

## Multi-Head Attention
Q/K/V를 여러 헤드로 나누어 병렬로 계산합니다. 헤드마다 문법 관계, 지시 대상, 위치 관계처럼 서로 다른 패턴을 학습합니다.

## Causal Mask
디코더 모델은 미래 토큰을 보면 안 됩니다. 그래서 현재 위치 이후의 가중치를 마스킹해 0으로 만듭니다. 이 마스크 덕분에 [[Pretraining|다음 토큰 예측]] 학습이 성립합니다.

## 효율화 기법
- **KV Cache**: 생성 중에 이미 계산한 K/V를 저장해 두고 재사용합니다. 자세한 내용은 [[Inference 최적화]]에 있습니다.
- **GQA/MQA**: 여러 Query 헤드가 K/V 헤드를 공유합니다. KV 캐시 메모리가 줄어듭니다.
- **FlashAttention**: GPU 메모리 계층을 고려해 연산 순서를 바꿉니다. 결과는 같고 속도는 빨라집니다.
- **Sliding Window / Sparse Attention**: 일부 토큰만 보게 해서 긴 [[Context Window]]를 감당합니다.

## 관련 개념
- [[Transformer]]
- [[Embedding]]
