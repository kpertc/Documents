#JavaScript #TypeScript 

Schema Type validation
https://zod.dev/
Zod 4 (v3 differences noted)

``` ts
import { z } from "zod"
```

``` ts
const UserSchema = z.object({
	username: z.string()
})

// create type from zod
type User = z.infer<typeof UserSchema>
```

object
``` ts
.partial()
.deepPartial() // (v3 only, removed in v4) make all nested property partial

.extend() // add property
.merge()

.omit()
.pick()

.passthrough() // allow additional properties during validation -> v4: z.looseObject({})
.strict() // not allow -> v4: z.strictObject({})
```

``` ts
z.string().min(5) // chained method, not z.min()
z.number().max(10)

z.number().gt(4) // greater than 4
z.int() // integer (v4 top-level, not in v3)

z.nullish() // null | undefine
z.nullable() // null  

z.string().default("value") // default when input is undefined
z.string().catch("value") // fallback when validation fails

z.enum(["aaa", "bbb"])
z.nativeEnum()

z.date()

// array
z.array(z.string()) // string array
z.array(z.string()).nonempty()
.length()

// tuple -> fixed length array
coords: z.tuple([z.number(), z.number(), z.number()])

.rest(z.number()) // the reset of any value is number
```

``` ts
z.union([z.string(), z.number()]) // number | string
z.string().or(z.number()) // same

// conditional type base on value
z.discriminatedUnion("status", [
	z.object({ status: z.literal("success"), data: z.string() }),
	z.object({ status: z.literal("failed"), data: z.instanceof(Error) }),
])
```

``` ts
UserSchema.parse(input) // throw on invalid

const r = UserSchema.safeParse(input) // no throw
if (!r.success) r.error.issues
else r.data

// parseAsync / safeParseAsync -> async refinement
```
