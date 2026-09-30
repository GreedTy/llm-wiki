---
tags: [framework, rag]
aliases: [라마인덱스, GPT Index, LlamaIndex Core]
updated: 2026-09-30
---

# LlamaIndex

## 한 줄 정의
LlamaIndex는 다양한 소스의 데이터를 수집하고, 파싱하고, 색인하고, 검색하는 [[RAG]]용 데이터 프레임워크입니다.

## 핵심 개념
- **Document / Node**: 원본 문서가 Document이고, 청킹한 조각이 Node입니다. Node는 텍스트, 메타데이터, 이웃 노드와의 관계를 가집니다.
- **Reader**: 파일, 웹, Notion, DB 등에서 Document를 읽습니다. `SimpleDirectoryReader`가 대표적입니다.
- **Node Parser**: [[Chunking]]을 담당합니다. `MarkdownNodeParser`는 헤더 단위로, `SentenceSplitter`는 토큰 크기 기준으로 나눕니다.
- **IngestionPipeline**: 파싱 → 변환 → 임베딩 → 저장을 하나의 파이프라인으로 묶습니다. 문서 해시로 변경분만 다시 처리하는 기능도 있습니다.
- **VectorStoreIndex**: [[Vector Database]](pgvector, Qdrant 등) 위에 만드는 인덱스입니다.
- **Retriever / Query Engine**: `index.as_retriever(similarity_top_k=5)`로 검색기를, `as_query_engine()`으로 검색부터 답변까지 하는 엔진을 만듭니다.

## 예시: pgvector 색인
```python
from llama_index.core import VectorStoreIndex, StorageContext, Settings
from llama_index.core.node_parser import MarkdownNodeParser
from llama_index.embeddings.bedrock import BedrockEmbedding
from llama_index.vector_stores.postgres import PGVectorStore

Settings.embed_model = BedrockEmbedding(model_name="amazon.titan-embed-text-v2:0")
store = PGVectorStore.from_params(..., table_name="wiki", embed_dim=1024)
nodes = MarkdownNodeParser().get_nodes_from_documents(docs)
index = VectorStoreIndex(nodes, storage_context=StorageContext.from_defaults(vector_store=store))
```

## LangChain과 비교
| | LlamaIndex | [[LangChain]] |
|---|---|---|
| 강점 | 데이터 수집, 청킹, 색인, 검색 | 에이전트, 도구 생태계, 오케스트레이션 |
| 에이전트 | Workflows, AgentWorkflow | `create_agent`, [[LangGraph]] |

두 프레임워크는 경쟁 관계라기보다 함께 쓰는 경우가 많습니다.

## 관련 개념
- [[RAG]]
- [[Chunking]]
- [[Agentic RAG]]
