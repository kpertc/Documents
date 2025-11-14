#Ai 

`ollama run ...`

macOS default model path
`/Users/username/.ollama/models`

```
ollama list

# remove
ollama rm 

# show status
ollama run xxx -- verbose 

ollama create name -f xxx

 
/clear #clear context 
/bye

OLLAMA_HOST=0.0.0.0:11434 OLLAMA_KEEP_ALIVE=-1
ollama serve

ollama show # show model capability

/? 指令

#set context length
/set parameter num_ctx 128000
```


SYSTEM -> system prompt
qwen
不用推理
/no_think 

```
FROM qwen3:32b
PARAMETER temperature 0.8
SYSTEM


```

`127.0.0.1:11434`