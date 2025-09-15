#JavaScript #TypeScript 
### Related Topics:
- [[Zod]]
### Tutorials
- https://ai-sdk.dev/docs/introduction
- [Vercel AI SDK Masterclass: From Fundamentals to Deep Research](https://youtu.be/kDlqpN1JyIw?si=3a1M_8tkeWKCn-VX)
- https://youtu.be/mojZpktAiYQ?si=GJvSKAF3ZfNPvyzw
### Docs
- streamText
- [generateText](https://ai-sdk.dev/docs/reference/ai-sdk-core/generate-text#messages.user-model-message.content.image-part.image)

``` ts
import { streamText } from "ai";
import "dotenv/config";

async function main() {

	const result = streamText({
		model: "openai/gpt-5-mini",
		prompt: "Invent a new holiday and describe its traditions.",
	});
	
	for await (const textPart of result.textStream) {
		process.stdout.write(textPart);
	}
	
	console.log("Token usage:", await result.usage);
	console.log("Finish reason:", await result.finishReason);
}


```

``` ts
import { openai } from "@ai-sdk/openai";

async function main () {
	const result = await generateText(
		{
			model: openai("gpt-4o"),
			prompt: "Tell me a joke",
			
			// system prompt, equal to role: system in messages
			system: `You are a text summarizer`,
			
			// or
			messages: [
				{"role": "system", "message": "You are a text summarizer" }
			]
		}
	)
}

console.log(result.txt)

result.steps // for debug?
result.steps[0]?.toolCalls
result.steps[0]?.toolResults
```

``` ts
import type { CoreMessage } from 'ai'

const messages: [
	{ role: "system", content: "You are a friendly greeter" },
	{ role: "user", content: "Hello" },
	{ role: "assistant", content: "Hi there!" },
]
```

### OpenAI Compatible

use Poe API
``` ts
const provider = createOpenAICompatible({
	name: "provider-name",
	apiKey: POE_API_KEY,
	baseURL: POE_BASE_URL,
	// includeUsage: true, // Include usage information in streaming responses
});

const result = await generateObject({
	model: provider("gpt-5-mini"),
	prompt: "please come up with 10 jokes.",
}),

```


next.js AI Chatbot

Image generation
https://vercel.com/docs/ai-gateway/image-generation

### Tool Call
function call
max step -> loop?
```ts
tools: {
	addNumbers: tool({
		description: "Add two numbers together",
		parameters: z.object({
			num1: z.number(), // .describe()
			num2: z.number()
		}),
		execute: async ({num1, num2}) => {
			return num1 + num2
		}
	})
}


result.toolResults
result.steps.length
```

### Structured Output

experimentalOutput
``` ts
// in generate text
experimental_output: Output.object({
	schema: z.object({
		sum: z.number()
	})
})

result.experimentalOutput.sum
```

`generateObject()`
``` ts
const result = await generateObject({
	model: openai("gpt-4o"),
	prompt: "please come up with 10 jokes.",
	schema: z.object({
		definitions: z.array(z.string()
			.describe("use as much jargon as possible.") 
			// describle is metadata in zod
		)
	})
	schemaName: ""
})

result.object.definitions
```

classify object using enum
``` ts
const result = await generateObject({
	model: openai("gpt-4o"),
	prompt: ".",
	output: 'enum',
	enum: ['relevant', 'irrelevant']
	system: "Classify the text as either positive, negative, or neutral"
})

```

`streamObject()`
``` ts
await streamObject({

})
```

### Reading Image

``` ts
const imageAsUint8Array = readFileSync(imagePath)

const result = await generateText(
	{
		...
		system: `You are a text summarizer`,
		// or
		messages: [
			// file
			{"role": "user", "content": [
				{
					type: "image",
					image: imageAsUint8Array
				}
			] },
			
			// url
			{"role": "user", "content": [
				{
					type: "image",
					image: new URL(imageURL)
				}
			] }
		]
	}
)
```

PDF File
``` ts
const result = await generateText(
	{
		...
		system: `You are a text summarizer`,
		// or
		messages: [
			// file
			{"role": "user", "content": [
				{
					type: "file",
					data: readFileSync(filePath),
					mimeType: "application/pdf"
				}
			] },
		]
	}
)
```

### Embedding
vector data base

``` ts
import { embedMany, embed, cosineSimilarity } from 'ai'
```