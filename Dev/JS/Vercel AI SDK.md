#JavaScript #TypeScript #Ai 
snippets below target AI SDK 5.x
### Related Topics:
- [[Zod]]
- [[Dev/JS/dotenv]]
- [[Next.js]]
### Tutorials
- https://ai-sdk.dev/docs/introduction
- [Vercel AI SDK Masterclass: From Fundamentals to Deep Research](https://youtu.be/kDlqpN1JyIw?si=3a1M_8tkeWKCn-VX)
- [A Complete Guide To Vercel’s AI SDK // The ESSENTIAL Tool For Shipping AI Apps](https://youtu.be/mojZpktAiYQ?si=GJvSKAF3ZfNPvyzw)
- [Build a RAG Chatbot from Scratch | React, Next.js, AI SDK, AI Elements, Neon, Drizzle, Clerk](https://youtu.be/3E5OxozYuA8?si=Gk4982CsMrYLkhFz)
### Docs
- streamText
- [generateText](https://ai-sdk.dev/docs/reference/ai-sdk-core/generate-text#messages.user-model-message.content.image-part.image)
- AI Elements: UI elements based on shadcn/ui https://ai-sdk.dev/elements/overview

- AI SDK
- AI SDK UI
- AI SDK RSC (React Server Components) — deprecated, use AI SDK UI for new projects

``` ts
import { streamText } from "ai";
import "dotenv/config";

async function main() {

	const result = streamText({
		model: "openai/gpt-5-mini", // "provider/model" string goes through AI Gateway -> needs AI_GATEWAY_API_KEY; the openai("...") form needs OPENAI_API_KEY
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
			model: openai("gpt-5-mini"),
			prompt: "Tell me a joke",
			
			// system prompt, equal to role: system in messages
			system: `You are a text summarizer`,
			
			// or
			messages: [
				{"role": "system", "content": "You are a text summarizer" }
			]
		}
	)
}

console.log(result.text)

result.steps // for debug?
result.steps[0]?.toolCalls
result.steps[0]?.toolResults
```

``` ts
import type { ModelMessage } from 'ai' // v4 was CoreMessage

const messages: ModelMessage[] = [
	{ role: "system", content: "You are a friendly greeter" },
	{ role: "user", content: "Hello" },
	{ role: "assistant", content: "Hi there!" },
]
```
### Usage
``` ts 
const result = await generateText ...

// generateText: usage is a plain object
result.usage.inputTokens
result.usage.outputTokens
result.usage.totalTokens

// streamText: usage is a promise -> await result.usage first
```
### OpenAI Compatible
use Poe API
```js
// use .env / .env.local file for key
import "dotenv/config";
apiKey: process.env.POE_API_KEY,
```
``` ts
import { createOpenAICompatible } from "@ai-sdk/openai-compatible";

const provider = createOpenAICompatible({
	name: "provider-name",
	apiKey: process.env.POE_API_KEY,
	baseURL: process.env.POE_BASE_URL,
	// includeUsage: true, // Include usage information in streaming responses
});

const result = await generateObject({
	model: provider("gpt-5-mini"),
	prompt: "please come up with 10 jokes.",
	schema: z.object({ jokes: z.array(z.string()) }), // required, or output: 'no-schema'
});
```

### Chat
``` tsx
`convertToModelMessages(messages)` // extract essential messages
```

UI side
``` tsx
import { useChat } from '@ai-sdk/react'

useChat()
useCompletion() // no memory
```
##### Reasoning
```ts
// reasoning
const result = streamText({
	model: openai("gpt-5-nano"), // openai  has reasoning, poe provider does not
	system: "You are a helpful assistant.",
	messages: convertToModelMessages(messages),
	providerOptions: {
	  openai: {
		reasoningSummary: "auto",
		reasoningEffort: "low",
	  },
	},
});

return result.toUIMessageStreamResponse({ sendReasoning: true });
```

output `type: 'reasoning'`
![[console-reasoning.png]]

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
		inputSchema: z.object({ // v4 was `parameters:`, renamed in AI SDK 5
			num1: z.number(), // .describe()
			num2: z.number()
		}),
		execute: async ({num1, num2}) => {
			return num1 + num2
		}
	}),
}

// fake tool
tools: {
      getCurrentTime: {
        description: "Get current time base on city",
        inputSchema: z.object({
          city: z.string().describe("The city to get the current time for"),
        }),
        execute: async ({ city }) => {
          if (city === "New York") {
            return "10:00 AM";
          } else if (city === "London") {
            return "11:00 AM";
          } else {
            return "12:00 PM";
          }
        },
      },
    },
stopWhen: stepCountIs(2), // to proces

result.toolResults
result.steps.length
```

``` tsx
// type for tools
export type ChatTools = InferUITools<typeof tools>
export type ChatMessage = UIMessage<never, UIDataTypes, ChatTools>

const { messages } : { messages: ChatMessage[] } = await req.json() // server route
```

base on the tool to create custom UI
``` tsx
message.parts.map((part) => ...) // each message has a parts array

part.type === "text" // normal text is "text"
part.type === "tool-getCurrentTime"// tool reuslt is start with "tool-"

part.state
part.input // input
part.input.{argument}
part.output // output
```

Multi-step tool call
getLocation -> getWeather
Tool orchestra

### Web Search
by model provider
```tsx
// openai
const tools = {
	webSearchPreview: openai.tools.webSearchPreview({}), // GA name is openai.tools.webSearch({})
};

// reasoning
const result = streamText({
	model: openai.responses("gpt-5-mini"), // gpt has reasoning
	tools,
	messages: convertToModelMessages(messages),
});

// anthropic
const anthropicTools = {
	webSearch: anthropic.tools.webSearch_20250305({ maxUses: 5 }),
};
```



### MCP Tools
```ts
// connection
const httpTransport = new StreamableHTTPClientTransport(
	// mock mcp demo api
	new URL("https://app.mockmcp.com/servers/fpFnWsRviXla/mcp"),
	{
	  requestInit: {
		headers: {
		  authorization:
			"Bearer <YOUR_MCP_TOKEN>",
		},
	  },
	},
);

// client
const mcpClient = await createMCPClient({
	transport: httpTransport,
});

// tools
const mcpTools = await mcpClient.tools();

const result = streamText({
	model: provider("gpt-5-mini"),
	system: "You are a helpful assistant.",
	messages: convertToModelMessages(messages),
	tools: mcpTools, // add mcp tools to model
	// properly close the connection
	onFinish: async () => {
	  await mcpClient.close();
	},
	onError: async (error) => {
	  await mcpClient.close();
	  console.error(error);
	},
});
```

### Structured Output

experimental_output
``` ts
import { Output } from 'ai'

// in generate text
experimental_output: Output.object({
	schema: z.object({
		sum: z.number()
	})
})

result.experimental_output.sum
```

`generateObject()`
``` ts
const result = await generateObject({
	model: openai("gpt-5-mini"),
	prompt: "please come up with 10 jokes.",
	schema: z.object({
		definitions: z.array(z.string()
			.describe("use as much jargon as possible.") 
			// describle is metadata in zod
		)
	}),
	schemaName: "Definitions" // schema metadata passed to the provider
})

result.object.definitions
```

classify object using enum
``` ts
const result = await generateObject({
	model: openai("gpt-5-mini"),
	prompt: ".",
	output: 'enum',
	enum: ['positive', 'negative', 'neutral'],
	system: "Classify the text as either positive, negative, or neutral"
})

```

ai-sdk 6



`streamObject()`
[streamObject()](https://ai-sdk.dev/docs/reference/ai-sdk-core/stream-object)
``` ts
const { partialObjectStream } = streamObject({
	model: openai("gpt-5-mini"),
	prompt: "please come up with 10 jokes.",
	schema: z.object({ jokes: z.array(z.string()) }),
})

for await (const partial of partialObjectStream) {
	console.log(partial) // object filled in progressively
}
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
					mediaType: "application/pdf"
				}
			] },
		]
	}
)
```

### Embedding
vector data base → RAG

use [[drizzle]] to store vector with Neon database

``` ts
import { embedMany, embed, cosineSimilarity } from 'ai'
```

 embed one text
```ts
export async function generateEmbedding(text: string) {

	const input = text.replaceAll("\n", " "); // replace() only swaps the first one
	
	const { embedding } = await embed({
		model: provider.textEmbeddingModel("text-embedding-3-small"),
		value: input,
	});
	
	return embedding;
}
```

embed many texts in one request
```ts
export async function generateEmbeddings(texts: string[]) {

	const inputs = texts.map((text) => text.replaceAll("\n", " "));
	
	const { embeddings } = await embedMany({
		model: provider.textEmbeddingModel("text-embedding-3-small"),
		values: inputs,
	});
	
	return embeddings;
}
```

```ts
import { cosineDistance, desc, gt, sql } from "drizzle-orm";

export async function searchDocuments(
	query: string,
	limit: number = 5,
	threshold: number = 0.5
) {
	const queryEmbedding = await generateEmbedding(query)
	
	const similarity = sql<number>`1 - (${cosineDistance(
		documents.embedding,
		queryEmbedding
	)})`
	
	const similarDocuments = await db.select(
		{
			id: documents.id,
			content: documents.content,
			similarity,
		})
		.from(documents)
		.where(gt(similarity, threshold))
		.orderBy(desc(similarity)) // desc -> descending
		.limit(limit)

	return similarDocuments
}
```

// todo add try catch for text generation
### Audio
 ``` ts
 import { experimental_transcribe as transcribe } from 'ai' // no bare `transcribe` export

 const transcript = await transcribe({
	 model: openai.transcription("whisper-1"),
	 audio: uint8Array
 })
 ```