#web-dev #python 

https://fastapi.tiangolo.com/

```sh
pip install "fastapi[standard]" # bundles the fastapi CLI (0.111+), or: pip install fastapi uvicorn
```

```sh
fastapi dev src/langchain/fastapi.py # dev
fastapi run src/langchain/fastapi.py # prod

uvicorn src.langchain.fastapi:app --reload # explicit host / port / workers
```

```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello from FastAPI"}
```

``` python
raise HTTPException(status_code=404, detail="Item not found")
```