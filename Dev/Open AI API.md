#python 

[[Vercel AI SDK]]

``` python
import os
import openai 

# Never hard-code the key in a note. Load it from the environment.
openai.api_key = os.environ.get("OPENAI_API_KEY") 

completion = openai.ChatCompletion.create( 
	model = "gpt-3.5-turbo", 
	message = [{"role": "user", "content": "hello"}] 
) 

print (completion)
```