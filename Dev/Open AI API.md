#python 

[[Vercel AI SDK]]

``` python
import openai 

openai.api_key = "***REMOVED***" 

completion = openai.ChatCompletion.create( 
	model = "gpt-3.5-turbo", 
	message = [{"role": "user", "content": "hello"}] 
) 

print (completion)
```