#python #Ai

orchestration framework

[[Dev/Python/dotEnv|dotEnv]]
[[LangChain.js]]

LangGraph -> LangSmith

DAG

RPA robotic process automation

Text Splitter
Doc Loader

Chroma
this vari

Runnable


``` python
.strip() # clean whitespace
```

### Messages

- Function Message
- AI Message
- Tool Message

``` python
from langchain_core.messages import HumanMessage, SystemMessage
 
messages=[
	SystemMessage(content="111")
	HumanMessage(content="111")
]
```

``` python
model.invoke([
	# messages
])

# stream
for chunck in model.stream("Hello")
	print(chunk.text, end="|", flush=True)

# return when all complete
model.batch([

])

# return when one complete
for response in mode.batch_as_completed([
	"",
	"",
	""
])
```

Structure Output
[[Pydantic]]
``` python
from pydantic import BaseModel, Field

class Movie(BaseModel):
	title: str = Field(..., description="the titel of the movie")
	
structureOuput = model.with_structured_output(Movie).invoke("input")
	
```

``` python
create_agent()
# create_react_agent()
# create_json_agent()
# create_tool_calling._agent

agent = create_agent( # base on langgraph
	model=model,
	tools=[web_search],
	system_prompt=""
)

result = agent.invoke(
	q
)
```

Static Model

Dynamic Model

### MCP
``` python
server_params = StdioServerParameters(
	command=""
)
```

### Ollama
``` python
import os
from langchain_ollama.llms import OllamaLLM
from langchain_core.prompts import ChatPromptTemplate

model= OllamaLLM(model="qwen3") 

# deprecated chain langchain 1.0

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

https://docs.langchain.com/oss/python/langgraph/overview

``` python
from pydantic import BaseModel, Field

class MessageClassifier(BaseModel):
    message_type: Literal["emotional", "logical"] = Field(
        ...,
        description="Classify if the message requires an emotional (therapist) or logical response."
    )
```

### LLM
``` python
llm = ChatOllama(
    model="qwen3",
)
```
##### State
``` python
from typing import Annotated, Literal
from typing_extensions import TypedDict

class State(TypedDict):
    messages: Annotated[list, add_messages]
    message_type: str | None
    
# init state
input = HumanMessage(content="1 + 1 = 2")
state = {"messages": [input], "message_type": None}
```

### Graph
``` python
from langgraph.graph import StateGraph, START, END

graph_builder = StateGraph(State)

graph_builder.add_node("simpleChat", simpleChat)
graph_builder.add_edge(START, "simpleChat")
graph_builder.add_edge("simpleChat", END)
graph = graph_builder.compile()

# run
graph.invoke(state)
```

``` python
graph_builder.set_entry_point("nodeName")
graph_builder.set_finish_point("")
```
##### Visualize Graph 
``` python
from IPython.display import Image, display
display(Image(app.get_graph().draw_mermaid_png()))
```