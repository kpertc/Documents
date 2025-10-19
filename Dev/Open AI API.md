#python 

[[Vercel AI SDK]]

``` python
import openai 

openai.api_key = "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" 

completion = openai.ChatCompletion.create( 
	model = "gpt-3.5-turbo", 
	message = [{"role": "user", "content": "hello"}] 
) 

print (completion)
```