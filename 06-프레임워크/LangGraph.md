---
tags: [framework, agent]
aliases: [랭그래프, StateGraph]
updated: 2026-09-30
---

# LangGraph

## 한 줄 정의
LangGraph는 에이전트와 워크플로를 "상태(State)를 공유하는 노드와 엣지의 그래프"로 정의하고 실행하는 LangChain 팀의 저수준 오케스트레이션 프레임워크입니다.

## 핵심 개념
- **State**: 그래프 전체가 공유하는 데이터입니다. 보통 TypedDict로 정의하고, 메시지 목록 같은 필드를 가집니다.
- **Node**: 상태를 받아서 업데이트를 반환하는 함수입니다. LLM 호출, 도구 실행, 검증 로직이 노드가 됩니다.
- **Edge / Conditional Edge**: 다음에 실행할 노드를 정합니다. 조건부 엣지로 분기와 루프를 만듭니다.
- **Checkpointer**: 단계마다 상태를 저장합니다. 대화 이어가기, 장애 복구, 중간 개입(human-in-the-loop), 과거 상태로 되돌리기(time travel)가 가능해집니다.

## 언제 쓰나
- 단순한 도구 호출 에이전트라면 [[LangChain]]의 `create_agent`로 충분합니다. 이것도 내부적으로 LangGraph로 동작합니다.
- 다음과 같은 경우에는 LangGraph로 직접 그래프를 설계합니다.
  - 검색 → 평가 → 재검색 같은 명시적 제어 흐름이 필요할 때([[Agentic RAG|Corrective RAG]])
  - 여러 에이전트가 협업할 때
  - 긴 작업 중간에 사람의 승인이 필요할 때

## 스트리밍
`stream_mode`로 무엇을 스트리밍할지 고릅니다. `"messages"`는 LLM 토큰 단위, `"updates"`는 노드별 상태 변화, `"values"`는 전체 상태입니다. 웹 UI에서 토큰 스트리밍과 "지금 검색 중" 같은 진행 상태를 함께 보여줄 때 씁니다.

## 관련 개념
- [[LangChain]]
- [[LLM Agent]]
- [[Agentic RAG]]
