#python 

```sh
uv add python-dotenv
```

``` python
from dotenv import load_dotenv

load_dotenv()

os.getenv("OPENAI_API_Key")
```