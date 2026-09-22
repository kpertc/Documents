#python 

[[Vercel AI SDK]]

``` python
import os
from openai import OpenAI

# Never hard-code the key in a note. Load it from the environment.
client = OpenAI(api_key=os.environ.get("OPENAI_API_KEY"))

completion = client.chat.completions.create(
	model = "gpt-4o-mini",
	messages = [{"role": "user", "content": "hello"}]
) 

print (completion)
```