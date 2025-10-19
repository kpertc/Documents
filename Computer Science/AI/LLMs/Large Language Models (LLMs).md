Large Language Models (LLMs) are a subset of Deep Learning

GPT, Generative Pre-trained ==Transformer==
Transformer → Specific neural network
Introduced in 2017 by Google, Paper “Attention is All You Need”

Predict next words

LLMs can be pre-trained and then fine-tuned for specific purposes

> [Deep Dive into LLMs like ChatGPT](https://youtu.be/7xTGNNLPyMI?si=-zVK05j1ZUyNo76U)
### 1. Pre-Training (预训练)

	Data set such as [FineWeb](https://huggingface.co/spaces/HuggingFaceFW/blogpost-fineweb-v1)
	then filtering and deduplicate data

 - Tokenization 
	bytes -> token (symbol), world or subword
	GPT4 ~100,277 tokens
	See token:
	- https://platform.openai.com/tokenizer
	- https://github.com/openai/tiktoken tiktoken by OpenAI
	- https://tiktokenizer.vercel.app/
	token also could be a part of image or sound

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

Minimizing hallucination by grounding
- right context
	- access information
	- Retrieve and Generate (RAG), (searching result)
- use better model

parameters → vague recollection
text in context window → direct access working memory

Model need more tokens to think, try to spread thinking process on more token, better than give just one token answer

Supervised Fine-Tuning, SFT
Expert response
监督微调：从自动补全到遵循人类指令回答问题

Reasoning: 
Reinforcement Learning (RF)
Answer question, check with answer, good answer will get rewarded and be trained for further cycles

RL tend to find trick to win
RL Model (Not standard yet)

### 3. Reinforcement Learning from Human Feedback (RLHF)

### Tuning
The process of adapting a model to a new domain or set of custom use cases by training the model on new data. For example, we may collect training data and "tune" the LLM specifically for the legal or medical domain.

- (Large) Pre-trained -> General purpose
- (Small) Fine tuned -> Special purpose 

Fine tuning
Bring your own dataset of and retrain the model by tuning every weight in the LLM. This requires a big training job (like really big) and hosting your own fine-tuned model. (train for a few days?)

> ↓ [CS 194/294-196 (LLM Agents) - Lecture 4, Burak Gokturk](https://www.youtube.com/live/Sy1psHS3w3I?si=1p9NqZUeJR6aTiMW)
![[CS 194_294-196 (LLM Agents) - Lecture 4, Burak Gokturk 39-23 screenshot.png]]

Parameter-Efficient Fine-Tuning (PEFT)
- cheaper, faster than conventional Fine-tuning
- generally not as good as conventional Fine-tuning
e.g. LoRA, Low-Rank Adaptation
- apply weights to any dense layers in the founding models
- only applying adaptation on attention weights, not on MLPs

Prompt Engineering - Guide LLMs for specific task
Prompt Design 
- hard prompts - human written prompts
- soft prompts - a small set of trainable vectors, embeddings, not understand by human

Prompt tuning
- prepend a soft prompt to the input, (like regular prompting?)
- more effect than hard prompt
- Compare to fine-tuning
	- cheaper than fine tuning
	- easy to switch to switch different task

 Distillation
 Huge model mean expensive and higher latency
- Teacher Model - The original (large model) that we want to extract the knowledge from it
- Student Model - new model with smaller size
- Soft label - probable target - The outpuit of teacher model when the temperature > 1
- Soft Prediction - The output of student model when the temperature > 1
- Hard label - definitive target softmax (T=1)
- Hard Prediction
No need a lot of labels

Train smaller model based on the hard labels annd the teacher soft labels
![[CS 194_294-196 (LLM Agents) - Lecture 4, Burak Gokturk 47-51 screenshot.png]]

Better to hybrid fine-tuning with RAG database

### Context Window & Tokens
- GPT-4.1-nano 1 million tokens in a single conversation
- One million tokens is roughly 2,500 to 3,000 pages of text. That's equivalent to feeding the entire Lord of the Rings trilogy.
- When you hit that limit, older information starts getting pushed out to make room for new stuff

Input & output tokens
- for LLMs, depending on the context and the model you're using, the same word might be tokenized differently, 1 token ≈ 4 words
- different model has different input/output token limit
- input and output token cost differently, GPT 4.1, output token cost 4x than input token

- [[Vercel AI SDK#Usage]]
- Final input token might be more than input toke because, for example, hidden system prompts are added.

LangChain 
LLM Framework -> Python / JavaScript [[LangChain.js]]
Document -> Document Chunks -> VectorStore (Vector database)

---
- [[Improve the performance of LLMs]]
- [[Retrieval-Augmented Generation (RAG)]]
- [[Model Context Protocol MCP]]

JS Framework
- [[Vercel AI SDK]]

Constrained vs unConstrained Flows
- Constrained: route -> if-else
- UnConstrained: Agent Orchestrator -> tools (ReAct)
	- ReAct / Dynamic Planning + Execution
	- Less reliable, more expensive

模式：
ReAct Reasoning and Acting
- Thought
- Action
- Observation
- Final Answer

Plan-And-Execute

---
### Trends

LLMs replace traditional search
- Before LLMs, enterprise need collect data of training sets
- (Compare to traditional algorithm) everyone can develop AI

Anthropic - Claude
- Haiku - small, fast, cheap
- Sonnet - medium
- Opus - smartest, slow