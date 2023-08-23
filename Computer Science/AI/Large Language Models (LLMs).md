Large Language Models (LLMs) are a subset of Deep Learning
LLMs can be pre-trained and then fine-tuned for specific purposes

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
