#python 

```sh
uv add python-dotenv
```

``` python
import os
from dotenv import load_dotenv

load_dotenv()

os.getenv("OPENAI_API_KEY") # os.environ["OPENAI_API_KEY"] -> raise KeyError if missing
```