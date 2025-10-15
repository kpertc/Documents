#TypeScript 

server and client code in the same repo

`npm i @trpc/server`

``` ts
import { initTRPC } from "@trpc/server"

const t = initTRPC.create()

const appRouter = t.router()
```