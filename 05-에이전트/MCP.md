---
tags: [concept, agent, protocol]
aliases: [Model Context Protocol, 모델 컨텍스트 프로토콜, MCP 서버]
updated: 2026-09-30
---

# MCP

## 한 줄 정의
MCP(Model Context Protocol)는 LLM 애플리케이션(호스트)이 외부 도구, 데이터, 프롬프트에 표준화된 방식으로 연결되도록 Anthropic이 공개한 개방형 프로토콜입니다.

## 왜 필요한가
MCP 이전에는 앱마다 도구 연동을 각자 구현해야 했습니다. 앱 N개와 도구 M개를 연결하려면 N×M개의 통합이 필요했습니다. MCP는 이것을 N+M 문제로 줄입니다. 흔히 "AI를 위한 USB-C"에 비유합니다.

## 구조
- **Host**: 사용자가 쓰는 AI 애플리케이션입니다(예: Claude 앱, IDE).
- **Client**: 호스트 안에서 서버 하나와 1:1로 연결되는 커넥터입니다.
- **Server**: 기능을 노출하는 프로세스입니다. 세 가지를 제공합니다.
  - **Tools**: 모델이 호출하는 함수입니다([[Tool Calling]]).
  - **Resources**: 읽을 수 있는 데이터입니다(파일, DB 레코드).
  - **Prompts**: 재사용할 수 있는 프롬프트 템플릿입니다.

## 전송 방식
- **stdio**: 로컬 프로세스로 실행합니다.
- **Streamable HTTP**: 원격 서버로 운영합니다. 인증에는 OAuth 2.1을 씁니다.

## 보안 주의점
- 서버가 반환하는 데이터에 악의적인 지시가 섞일 수 있습니다(프롬프트 인젝션).
- 도구마다 권한 범위를 최소화하고, 신뢰할 수 있는 서버만 연결합니다.

## 관련 개념
- [[Tool Calling]]
- [[LLM Agent]]
