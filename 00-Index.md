---
tags: [moc]
aliases: [인덱스, 목차, 홈]
updated: 2026-09-30
---

# LLM Wiki 인덱스

LLM을 이해하고 서비스에 적용하는 데 필요한 개념을 학습 순서대로 정리했습니다.

## 1. 기초
- [[Transformer]] — 현대 LLM의 기본 구조
- [[Attention]] — 토큰 간 관계를 계산하는 핵심 연산
- [[Tokenization]] — 텍스트를 모델 입력 단위로 쪼개는 방법
- [[Embedding]] — 의미를 벡터로 표현하기
- [[Context Window]] — 모델이 한 번에 볼 수 있는 입력 길이

## 2. 학습
- [[Pretraining]] — 대규모 텍스트로 다음 토큰 예측 학습
- [[Fine-tuning]] — 특정 작업·도메인에 맞추는 추가 학습
- [[LoRA]] — 적은 파라미터만 학습하는 효율적 파인튜닝
- [[RLHF]] — 사람 선호도로 정렬하기

## 3. 프롬프트
- [[Prompt Engineering]] — 원하는 출력을 이끌어내는 입력 설계
- [[Chain-of-Thought]] — 단계적 추론 유도

## 4. RAG
- [[RAG]] — 검색으로 외부 지식을 주입하는 구조
- [[Chunking]] — 문서를 검색 단위로 나누기
- [[Vector Database]] — 임베딩 저장·검색
- [[Hybrid Search]] — 키워드 검색과 벡터 검색 결합
- [[Reranking]] — 검색 결과 재정렬
- [[Agentic RAG]] — 에이전트가 검색 전략을 스스로 결정하는 RAG
- [[RAG 평가]] — 검색·생성 품질 측정

## 5. 에이전트
- [[LLM Agent]] — 목표를 위해 도구를 쓰며 반복 추론하는 시스템
- [[Tool Calling]] — 모델이 함수를 호출하는 방식
- [[MCP]] — 모델과 도구를 잇는 표준 프로토콜

## 6. 프레임워크
- [[LangChain]] — LLM 애플리케이션 구성 요소 라이브러리
- [[LangGraph]] — 상태 기반 에이전트 워크플로
- [[LlamaIndex]] — 데이터 수집·색인·검색 특화 프레임워크

## 7. 운영
- [[Hallucination]] — 사실이 아닌 내용을 생성하는 문제
- [[Guardrails]] — 입출력 안전장치
- [[LLM Observability]] — 로그·메트릭·트레이스로 품질과 비용 추적
- [[Inference 최적화]] — 지연시간과 비용 줄이기
- [[Quantization]] — 가중치 정밀도를 낮춰 경량화
