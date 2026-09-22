LLM challenges:
- no source
- out of date

Retrieve data from Internet / database?
Reduce hallucination

### Chunking data

require good data parser

Primitive
Data → Text Splitting → Index → TopK → Response

Retrieve and Ranking
TopK, top K relevant results

### Vector Database
Semantic Gap that traditional database can not

Hybrid with traditional text search (BM25 keyword)

Vector Embedding
by embedding models
Vector indexing -> Methods: HNSW, IVF
RAG use vector database

### RAG vs Finetune
RAG → 外部知识, 可随时更新, 有来源
Finetune → 改风格 / 格式 / 领域语气, 不适合塞新事实