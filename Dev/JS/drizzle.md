#TypeScript #data 

- [[SQL Basics]]

https://orm.drizzle.team/docs/get-started

Tutorial:
- [Learn Drizzle ORM in Next.js with Neon Postgres | CRUD Tutorial](https://youtu.be/Tfc5LfHSGmE?si=U7oPO9T8UK1RqIFs)

ORM let work with relational database using your language’s object
Write Typescript instead of writing SQL
Faster than Prisma

Example:

neon database
![[neon-database.png]]

- compute, storage decoupled
- branches, different development
- Time travel
- support serverless connection?

Dependencies
+ @neondatabase/serverless
+ drizzle-kit
+ drizzle-orm

https://orm.drizzle.team/docs/get-started/postgresql-new
```
db
	migrations
	schema.ts
drizzle.config.ts
```

```sh
npx drizzle-kit push # upload database directly

# generate migrations
npx drizzle-kit generate 

# apply migration to database
npx drizzle-kit migrate
```

``` ts
import { db } from "@lumen/db/db-config";
import { todo } from "@lumen/db/schema";

export default async function Page() {
	// get data
	const todos = await db.select().from(todo);
	console.log(todos);
	
	// add data
	await db.insert(todo).values({
		id: 3,
		text: "Hello, world:",
		done: false,
		createdAt: new Date(),
	});
	
	// delete data
	await db.delete(todo).where(eq(todo.id, 3));
	
	// update data
	await db
		.update(todo)
		.set({ text: "Hello, world: updated" })
		.where(eq(todo.id, 1));
	
	return <div>DB</div>;
}
```