---
tags: [concept, 프롬프트, reasoning]
aliases: [CoT, 사고의 사슬, 단계적 추론, Extended Thinking, ReAct]
updated: 2026-09-30
---

# Chain-of-Thought

## 한 줄 정의
Chain-of-Thought(CoT)는 모델이 최종 답을 내기 전에 중간 추론 단계를 텍스트로 생성하게 해서, 복잡한 문제의 정확도를 높이는 기법입니다.

## 방식
- **Zero-shot CoT**: 프롬프트에 "단계별로 생각해 보자"처럼 추론을 유도하는 문장을 넣습니다.
- **Few-shot CoT**: 추론 과정이 포함된 예시를 함께 제공합니다.
- **Self-Consistency**: 추론을 여러 번 샘플링하고 다수결로 답을 고릅니다.
- **추론 모델 / Extended Thinking**: 모델이 학습 단계에서부터 긴 내부 추론을 하도록 훈련되어 있습니다. 사용자는 추론 예산만 설정합니다.

## ReAct
Reasoning(생각)과 Acting(도구 실행)을 번갈아 하는 패턴입니다. "생각 → 행동 → 관찰"을 반복하며 문제를 풉니다. [[LLM Agent]]와 [[Agentic RAG]]의 기본 루프가 이 패턴입니다.

## 주의점
- 추론 텍스트가 길어지면 토큰 비용과 지연이 늘어납니다.
- 생성된 추론이 모델의 실제 내부 계산 과정을 그대로 반영한다고 단정할 수는 없습니다.
- 단순한 조회형 질문에는 이득이 거의 없습니다.

## 관련 개념
- [[Prompt Engineering]]
- [[LLM Agent]]
