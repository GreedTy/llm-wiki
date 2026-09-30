# LLM Wiki

LLM(대규모 언어 모델)의 개념, RAG, 에이전트, 운영 지식을 정리한 Obsidian 볼트입니다.
이 저장소는 LLM Wiki Q&A 챗봇(https://llmwiki-qna.com)의 지식 소스로도 쓰입니다.
`main` 브랜치에 push하면 GitHub Actions가 챗봇 서버에 재색인을 요청합니다.

## 사용법

1. 이 저장소를 clone합니다.
2. Obsidian에서 `Open folder as vault`로 clone한 폴더를 엽니다.
3. 시작점은 [[00-Index]]입니다.

## 작성 규칙

- 노트 하나에 개념 하나를 다룹니다. 파일명이 곧 개념 이름입니다.
- 관련 개념은 반드시 `[[위키링크]]`로 연결합니다. 챗봇 에이전트는 이 링크를 따라가며 답을 찾습니다.
- 맨 위 frontmatter에 `tags`, `aliases`, `updated`를 적습니다. `aliases`는 검색 정확도를 높입니다.
- 새 노트는 `_templates/개념 템플릿.md`로 시작합니다(Obsidian 명령 `Templates: Insert template`).
- 개인 작업 상태(`.obsidian/workspace.json`)는 커밋하지 않습니다.

## 폴더 구조

| 폴더 | 내용 |
|---|---|
| 01-기초 | Transformer, Attention, 토큰화, 임베딩, 컨텍스트 윈도우 |
| 02-학습 | 사전학습, 파인튜닝, LoRA, RLHF |
| 03-프롬프트 | 프롬프트 엔지니어링, Chain-of-Thought |
| 04-RAG | RAG, 청킹, 벡터 DB, 하이브리드 검색, 리랭킹, Agentic RAG, RAG 평가 |
| 05-에이전트 | LLM 에이전트, Tool Calling, MCP |
| 06-프레임워크 | LangChain, LangGraph, LlamaIndex |
| 07-운영 | 환각, 가드레일, 관측성, 추론 최적화, 양자화 |
