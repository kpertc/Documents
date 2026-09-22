#TypeScript 

tRPC v11

server and client code in the same repo

`npm i @trpc/server @trpc/client`
React: `npm i @trpc/tanstack-react-query @tanstack/react-query` (v11 path, `@trpc/react-query` = classic integration, still supported)

``` ts
import { initTRPC } from "@trpc/server"

const t = initTRPC.create()

const appRouter = t.router({
	greeting: t.procedure.query(() => "hi"),
})

export type AppRouter = typeof appRouter // the client gets its types from here
```

client
``` ts
import { createTRPCClient, httpBatchLink } from "@trpc/client"

const client = createTRPCClient<AppRouter>({
	links: [httpBatchLink({ url: "/api/trpc" })],
})
```