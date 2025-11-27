#web-dev #python 

https://fastapi.tiangolo.com/

```sh
pip install fastapi uvicorn
```

```sh
uvicorn src.langchain.fastapi:app --reload
```

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello from FastAPI"}
```

``` python
raise HTTPExeception(status_code=404, detail=f"")
```