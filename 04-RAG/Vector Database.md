---
tags: [concept, rag, infra]
aliases: [벡터 DB, 벡터 데이터베이스, Vector Store, 벡터스토어, pgvector, ANN]
updated: 2026-09-30
---

# Vector Database

## 한 줄 정의
벡터 데이터베이스는 [[Embedding]] 벡터를 저장하고, 질의 벡터와 가까운 벡터를 빠르게 찾는 근사 최근접 이웃(ANN) 검색을 제공하는 저장소입니다.

## ANN 인덱스
- **HNSW**: 계층형 그래프 구조입니다. 검색이 빠르고 재현율이 높지만 메모리를 많이 씁니다. 가장 널리 씁니다.
- **IVF**: 벡터를 클러스터로 나누고 가까운 클러스터 안에서만 검색합니다. 메모리 효율이 좋습니다.
- **PQ(Product Quantization)**: 벡터를 압축해서 저장합니다. 대규모 데이터에 씁니다.

## 선택지
| 종류 | 예시 | 특징 |
|---|---|---|
| 기존 DB 확장 | PostgreSQL + pgvector | 트랜잭션, 조인, 권한을 그대로 씁니다. 수백만 건까지 운영이 단순합니다. |
| 전용 벡터 DB | Qdrant, Weaviate, Milvus, Pinecone | 대규모 처리, 필터링 성능, 관리형 옵션이 강점입니다. |
| 검색 엔진 | OpenSearch, Elasticsearch | 키워드 검색과 벡터 검색을 함께 해서 [[Hybrid Search]]에 유리합니다. |

## pgvector 실무 팁
- `CREATE EXTENSION vector;`로 활성화합니다. AWS RDS PostgreSQL에서도 지원합니다.
- 코사인 거리는 `vector_cosine_ops`, HNSW 인덱스는 `USING hnsw`로 만듭니다.
- 메타데이터를 JSONB로 저장하면 문서 출처나 권한으로 필터링하기 좋습니다.
- 임베딩 차원은 컬럼 정의에 고정됩니다. 모델을 바꾸면 테이블을 다시 만들어야 합니다.

## 관련 개념
- [[Embedding]]
- [[Hybrid Search]]
- [[RAG]]
