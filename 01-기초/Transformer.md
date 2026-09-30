---
tags: [concept, 기초, architecture]
aliases: [트랜스포머, Transformer 아키텍처]
updated: 2026-09-30
---

# Transformer

## 한 줄 정의
Transformer는 순환(RNN) 없이 [[Attention]]만으로 시퀀스를 처리하는 신경망 구조입니다. 2017년 논문 "Attention Is All You Need"에서 처음 제안되었습니다.

## 왜 중요한가
GPT, Claude, Llama, Gemini 같은 거의 모든 현대 LLM이 Transformer를 기반으로 합니다. RNN은 토큰을 순서대로 처리해야 했지만, Transformer는 모든 토큰을 병렬로 처리할 수 있습니다. 이 덕분에 GPU로 대규모 학습이 가능해졌습니다.

## 구조
- **입력 단계**: 텍스트를 [[Tokenization|토큰]]으로 나누고, 각 토큰을 [[Embedding|임베딩]] 벡터로 바꿉니다. 여기에 위치 정보(Positional Encoding, 최근에는 RoPE)를 더합니다.
- **블록 반복**: 각 블록은 Multi-Head Self-Attention과 Feed-Forward Network(FFN)로 구성됩니다. 블록마다 잔차 연결(residual)과 정규화(LayerNorm/RMSNorm)가 붙습니다.
- **출력 단계**: 마지막 은닉 상태를 어휘 크기의 로짓으로 변환하고, softmax로 다음 토큰의 확률을 구합니다.

## 변형
- **Encoder-only** (BERT): 양방향 문맥을 이해합니다. 분류나 임베딩에 강합니다.
- **Decoder-only** (GPT 계열, 대부분의 LLM): 앞 토큰만 보고 다음 토큰을 예측합니다. 생성에 적합합니다.
- **Encoder-Decoder** (T5): 번역이나 요약처럼 입력을 출력으로 변환하는 작업에 씁니다.
- **MoE(Mixture of Experts)**: FFN을 여러 전문가로 나누고 토큰마다 일부만 활성화합니다. 파라미터 수에 비해 계산량이 작습니다.

## 실무 팁
- 모델 크기를 이야기할 때는 파라미터 수와 함께 [[Context Window]] 길이, 활성 파라미터(MoE인 경우)를 같이 봐야 합니다.
- Attention 계산량은 시퀀스 길이의 제곱에 비례합니다. 그래서 긴 입력은 비용과 지연시간이 급격히 늘어납니다. 이 문제는 [[Inference 최적화]]에서 다룹니다.

## 관련 개념
- [[Attention]]
- [[Pretraining]]
- [[Tokenization]]
