---
tags: [concept, 운영, performance]
aliases: [추론 최적화, Inference Optimization, KV Cache, KV 캐시, 프롬프트 캐싱, Prompt Caching, vLLM, Speculative Decoding]
updated: 2026-09-30
---

# Inference 최적화

## 한 줄 정의
추론 최적화는 LLM 응답의 지연시간을 줄이고 처리량을 높이며 비용을 낮추기 위한 모델, 서빙, 애플리케이션 계층의 기법들입니다.

## 지연시간 구성
- **Prefill**: 입력 토큰 전체를 한 번에 처리하는 단계입니다. 입력이 길수록 TTFT가 늘어납니다.
- **Decode**: 출력 토큰을 하나씩 생성하는 단계입니다. 메모리 대역폭이 병목입니다.

## 서빙 계층 기법
- **KV Cache**: 이미 계산한 [[Attention]]의 Key와 Value를 저장해 둡니다. 다음 토큰을 생성할 때 재계산하지 않습니다.
- **PagedAttention(vLLM)**: KV 캐시를 페이지 단위로 관리해 메모리 단편화를 줄입니다.
- **Continuous Batching**: 요청마다 끝나는 시점이 달라도 배치에 동적으로 넣고 뺍니다. GPU 활용률이 크게 오릅니다.
- **Speculative Decoding**: 작은 모델이 여러 토큰을 미리 제안하고, 큰 모델이 한 번에 검증합니다.
- **[[Quantization]]**: 가중치 정밀도를 낮춰 메모리와 대역폭을 줄입니다.

## 애플리케이션 계층 기법
- **프롬프트 캐싱**: 시스템 프롬프트나 긴 문서처럼 반복되는 앞부분을 캐시합니다. 입력 비용과 TTFT가 줄어듭니다. Anthropic API와 Bedrock이 지원합니다.
- **스트리밍**: 토큰을 생성되는 대로 보여줍니다. 전체 시간은 같아도 체감 지연이 크게 줄어듭니다.
- **모델 라우팅**: 쉬운 질문은 작고 빠른 모델로, 어려운 질문은 큰 모델로 보냅니다.
- **컨텍스트 절약**: [[Reranking]]으로 필요한 청크만 넣고, 대화 이력은 요약합니다.
- **응답 캐싱**: 같은 질문에는 캐시된 답을 돌려줍니다. 의미가 비슷한 질문까지 묶는 시맨틱 캐시도 있습니다.

## 관련 개념
- [[Quantization]]
- [[Context Window]]
- [[LLM Observability]]
