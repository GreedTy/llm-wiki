---
tags: [framework]
aliases: [랭체인, LangChain Core, LCEL]
updated: 2026-09-30
---

# LangChain

## 한 줄 정의
LangChain은 모델, 프롬프트, 도구, 검색기, 출력 파서 같은 LLM 애플리케이션 구성 요소를 공통 인터페이스로 묶어 주는 Python/JS 프레임워크입니다.

## 핵심 추상화
- **Chat Model**: 제공자별 모델을 같은 인터페이스(`invoke`, `stream`, `bind_tools`)로 씁니다. 예: `ChatBedrockConverse`, `ChatAnthropic`, `ChatOpenAI`.
- **Messages**: `SystemMessage`, `HumanMessage`, `AIMessage`, `ToolMessage`로 대화를 표현합니다.
- **Tools**: `@tool` 데코레이터로 Python 함수를 도구로 만듭니다. 함수의 docstring이 도구 설명이 됩니다.
- **Runnable / LCEL**: `prompt | model | parser`처럼 파이프로 구성 요소를 조합합니다.
- **Agents**: LangChain 1.x에서는 `create_agent(model, tools, system_prompt=...)`로 [[LangGraph]] 기반의 도구 호출 에이전트를 만듭니다. 미들웨어로 요약, 사람 확인, 재시도 같은 동작을 끼워 넣을 수 있습니다.

## 예시
```python
from langchain.agents import create_agent
from langchain_aws import ChatBedrockConverse
from langchain_core.tools import tool

@tool
def search_wiki(query: str) -> str:
    """LLM 위키에서 query와 관련된 내용을 검색합니다."""
    ...

model = ChatBedrockConverse(model_id="global.anthropic.claude-sonnet-4-6", region_name="ap-northeast-2")
agent = create_agent(model, tools=[search_wiki], system_prompt="위키 근거로만 답하세요.")
result = agent.invoke({"messages": [{"role": "user", "content": "LoRA가 뭐야?"}]})
```

## LlamaIndex와 함께 쓰기
[[LlamaIndex]]는 색인과 검색에 강하고, LangChain은 에이전트 오케스트레이션과 도구 생태계에 강합니다. 흔한 조합은 "LlamaIndex 검색기를 LangChain 도구로 감싸서 에이전트에 주는 것"입니다. 이 위키의 [[Agentic RAG]] 챗봇이 이 구조를 씁니다.

## 관련 개념
- [[LangGraph]]
- [[LlamaIndex]]
- [[Tool Calling]]
