#JavaScript #TypeScript 

Schema Type validation
https://zod.dev/

``` ts
import { z } from zod 
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
.deepPartial() // make all nested property partial

.extend() // add property
.merge()

.omit()
.pick()

.passthrought() // allow additional properties during validation
.strict() // not allow
```

``` ts
z.min()
z.max()

z.gt(4) // greater than 4
z.int() // integer

z.nullish() // null | undefine
z.nullable() // null  

z.deafult() // add defaut value

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
parse
safeparse 
```
