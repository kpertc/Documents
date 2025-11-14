#python #Ai

orchestration framework

[[LangChain.js]]
        
LangGraph -> LangSmith

DAG

RPA robotic process automation

Text Splitter
Doc Loader

Chroma
this vari
### Ollama
``` python
import os
from langchain_ollama.llms import OllamaLLM
from langchain_core.prompts import ChatPromptTemplate

model= OllamaLLM(model="qwen3") 

template = """
    You are helpful assistant.
    {input}
"""

prompt = ChatPromptTemplate.from_template(template)

chain = prompt | model

input = 'what is machine learning'

response = chain.invoke({"input": input})
print(response)
```

### LangGraph
stateful multi-agent
state
more complex, more control
 