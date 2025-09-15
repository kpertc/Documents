Large Language Models (LLMs) are a subset of Deep Learning
LLMs can be pre-trained and then fine-tuned for specific purposes

> [Deep Dive into LLMs like ChatGPT](https://youtu.be/7xTGNNLPyMI?si=-zVK05j1ZUyNo76U)
### 1. Pre-Training
	Data set such as [FineWeb](https://huggingface.co/spaces/HuggingFaceFW/blogpost-fineweb-v1)
	then filtering and deduplicate data

 - Tokenization 
	bytes -> token (symbol)
	GPT4 ~100,277 tokens
	See token: https://tiktokenizer.vercel.app/

- Neural network
	sequence of Token to neural network
	guess the possibility of next token with billions of parameters, was set randomly initially
	inference: to generate data, just predict one token at a time

loss -> low is better
- base model → Token simulator, will generate a lot of token (text)

### 2. Post-Training (Supervised FineTuning)
- instruct model (assistant)  → train with Q&A sets
	special token such as：
		`<im_start> <im_end>`
		`<search_start> <search_end>`

LLM models does not recognize world / letters, only recognize token
could specify "use code" for better math / counting ability

Hallucination (幻觉)
- influenced by tone of instruction
- use another LLM to test accuracy 
- train to say "I dont know"

parameters → vague recollection
text in context window → direct access working memory

Model need more tokens to think, try to spread thinking process on more token, better than give just one token answer

SFT Model

Reasoning: 
Reinforcement Learning (RF)
Answer question, check with answer, good answer will get rewarded and betrained for further cycles

RL tend to find trick to win

RL Model (Not standard yet)

### 3. Reinforcement Learning from Human Feedback (RLHF)

---

- (Large) Pre-trained -> General purpose
- (Small) Fine tuned -> Special purpose 

Prompt Design
Prompt Engineering

Tuning
The process of adapting a model to a new domain or set of custom use cases by training the model on new data. For example, we may collect training data and "tune" the LLM specifically for the legal or medical domain.

Fine tuning
Bring your own dataset of and retrain the model by tuning every weight in the LLM. This requires a big training job (like really big) and hosting your own fine-tuned model.
  
LangChain 
LLM Framework -> Python / JavaScript
Document -> Document Chunks -> VectorStore (Vector database)




---
LLM JSON Output -> Validate Schema 
Valid ->

---
### Retrieval-Augmented Generation (RAG)

LLM challenges:
- no source
- out of date
- 
Retrieve data from Internet / database?

Reduce hallucination

Vector Database
Semantic Gap that traditional database can not

Vector Embedding
thru embedding models
Vector indexing -> Methods: HNSW, IVF

RAG use vector database


RAG vs Finetune


### Model Context Protocol MCP 
"API" for LLM?
like REST API / GraphQL

MCP Host (LLM)

MCP Clients
|
MCP Protocol (API / “USB-C”)
|
MCP Servers (functions)

Server
- Tools
- Resource
- Prompts
- Samplings

---
### Implement
[[Vercel AI SDK]]