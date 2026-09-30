---
tags: [concept, agent]
aliases: [LLM 에이전트, AI 에이전트, Agent, 에이전트]
updated: 2026-09-30
---

# LLM Agent

## 한 줄 정의
LLM 에이전트는 LLM이 목표를 달성하기 위해 스스로 다음 행동을 결정하고, 도구를 호출하고, 결과를 관찰하는 과정을 반복하는 시스템입니다.

## 구성 요소
- **모델(두뇌)**: 계획을 세우고, 어떤 도구를 쓸지 결정하고, 최종 답을 만듭니다.
- **도구([[Tool Calling|Tools]])**: 검색, API 호출, 코드 실행, DB 조회 같은 외부 행동입니다.
- **메모리**: 단기 메모리는 현재 대화와 도구 결과입니다. 장기 메모리는 사용자 정보나 과거 대화를 담은 외부 저장소입니다.
- **루프 제어**: 최대 반복 횟수, 종료 조건, 에러 처리를 정합니다.

## 에이전트 루프
```
while not done and steps < max_steps:
    action = llm(context)           # 생각: 다음에 뭘 할까
    if action.is_final: return action.answer
    observation = run_tool(action)  # 행동
    context.append(observation)     # 관찰
```

## 워크플로 vs 에이전트
- **워크플로**: 개발자가 흐름을 미리 코드로 정합니다. 예측 가능하고 디버깅이 쉽습니다.
- **에이전트**: 모델이 흐름을 동적으로 정합니다. 유연하지만 비용과 행동을 예측하기 어렵습니다.
- 실무에서는 가능하면 단순한 워크플로로 시작합니다. 동적 판단이 정말 필요한 부분에만 에이전트를 씁니다. [[LangGraph]]는 두 방식을 섞는 데 적합합니다.

## 운영 시 고려사항
- 도구 권한은 최소한으로 줍니다. 되돌릴 수 없는 행동(결제, 삭제)에는 사람 확인 단계를 둡니다.
- 도구 결과 안의 지시문(프롬프트 인젝션)을 따르지 않도록 [[Guardrails]]를 적용합니다.
- 단계별 트레이스를 남겨야 문제를 추적할 수 있습니다([[LLM Observability]]).

## 관련 개념
- [[Tool Calling]]
- [[Agentic RAG]]
- [[MCP]]
- [[Chain-of-Thought]]
