---
tags: [concept, rag, agent]
aliases: [에이전틱 RAG, Agentic Retrieval, 에이전트 RAG, Self-RAG, Corrective RAG]
updated: 2026-09-30
---

# Agentic RAG

## 한 줄 정의
Agentic RAG는 "검색 한 번 하고 답변"하는 고정 파이프라인 대신, [[LLM Agent|에이전트]]가 검색 여부, 검색어, 읽을 문서, 추가 탐색 필요성을 스스로 판단하며 반복하는 RAG 방식입니다.

## Naive RAG와의 차이
| 항목 | Naive [[RAG]] | Agentic RAG |
|---|---|---|
| 검색 횟수 | 항상 1회 | 0회부터 여러 회까지 필요한 만큼 |
| 검색어 | 사용자 질문 그대로 | 에이전트가 재작성하고 분해함 |
| 도구 | 벡터 검색 하나 | 검색, 문서 열람, 링크 탐색, 계산 등 여러 개 |
| 품질 검증 | 없음 | 결과를 보고 부족하면 다시 검색 |

## 주요 패턴
- **Query Rewriting / Decomposition**: 복합 질문을 하위 질문으로 나누어 각각 검색합니다.
- **Routing**: 질문 유형에 따라 검색할 소스나 도구를 고릅니다.
- **Self-Reflection (Self-RAG, Corrective RAG)**: 검색된 문서가 질문에 충분한지 평가하고, 부족하면 검색어를 바꿔 다시 검색합니다.
- **Graph Traversal**: 문서 간 링크(예: 위키의 `[[위키링크]]`)를 따라가며 관련 지식을 확장합니다.

## 구현 예: 이 위키의 챗봇
이 위키를 지식 소스로 쓰는 챗봇은 다음과 같이 동작합니다.
1. [[LlamaIndex]]로 노트를 헤더 단위로 청킹하고 pgvector에 색인합니다.
2. [[LangChain]] 에이전트에게 세 가지 도구를 줍니다: `search_wiki`(의미 검색), `read_note`(노트 전문 읽기), `get_linked_notes`(연결된 노트 목록).
3. 에이전트는 [[Chain-of-Thought|ReAct]] 루프로 검색하고, 읽고, 링크를 따라간 뒤 출처와 함께 답합니다.

## 트레이드오프
- **장점**: 복잡하거나 여러 단계에 걸친 질문의 정확도가 높고, 근거를 찾지 못하면 모른다고 답할 수 있습니다.
- **단점**: LLM 호출이 여러 번이라 지연과 비용이 늘어납니다. 반드시 최대 반복 횟수 제한을 두어야 합니다.
- **관측 필수**: 도구 호출 횟수, 단계별 지연, 토큰 사용량을 [[LLM Observability|관측]]해야 운영할 수 있습니다.

## 관련 개념
- [[RAG]]
- [[LLM Agent]]
- [[Tool Calling]]
- [[LangGraph]]
