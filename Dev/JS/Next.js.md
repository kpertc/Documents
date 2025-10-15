#JavaScript #TypeScript 

Routing
API route
Rendering
Data Fetching
Styling
Optimization
Dev and prod build system

[[Vercel AI SDK]]

### Tutorial
- [NextJS 15 Full Course 2025 | Become a NextJS Pro in 1.5 Hours by PedroTech](https://www.youtube.com/watch?v=6jQdZcYY8OY)
- [Codevolution](https://www.youtube.com/@Codevolution)


```sh 
npx create-next-app
```

`next-env.d.ts` auto-generated file

tsconfig
`"strict": true`



Tanstack router

Pages Router
App Router

Turbopack

### Route
```
app/api/route.ts

app/layout.tsx // root layout
app/page.tsx

app/not-found.tsx // customized not found page

app/xxx/page.tsx // /xxx/page.tsx
app/xxx/layout.tsx // layout page
app/xxx/template.tsx // template page
app/xxx/loading.tsx // loading page
app/xxx/error.tsx // error page
```

 File-based routing, in `app` folder, named `page.js` or `page.tsx`
```
app/xxx/users/page.tsx // the export default function component
```

 ##### Dynamic routing
```
// dynamic routing
app/xxx/users/[userID]/page.tsx
[userID] -> parameter

// nested dynamic routing
app/product/[productId]/reviews/[reviewId]/page.tsx

// catch-all segments
app/docs/[...slug]/page.tsx // any /params under docs
app/docs/[[...slug]]/page.tsx // optional -> will, show default page when no params
```
##### Private folder `_`
the folder and all its subfolders are excluded from routing
```
app/xxx/_lib
```
if want to use `_` in path, use "%5F" URL-encoded

##### Route Group
```
app/(auth)/register // accessab;e /register 
app/(auth)/layout.tsx // root layout for the route group
```

``` tsx
import { notFound } from "next/navigation"

export default async function UserPage({
	params,
}: {
	params: Promise<{ userId: string }>
}) {
	const {} await params;
	
	if (!user) {
		notFound(); // manual trigger not found page / 404 page
		// import { notFound } from "next/navigation";
		// not-found.tsx
	}
	
	return <div></div>
}
```
##### slug and params
``` tsx
export default async function UserPage({
	params, // [[articleId]] /articleId/
	searchParams, // ?&lang=en
}: {
	params: Promise<{ slug: string[] }>
	searchParams: Promise<{ lang?: "en" | "fr" }>
}) {
	// in server render component
	const { slug } = await params;
	
	const { lang } = await searchParams;
	
	// in clinet render component
	
	import { use } from "react"
	
	const { slug } = use(params);
	const { lang } = use(searchParams);
}
```

```
/components // UI, resuable components
/lib // utils
```

### Navigation
### `<Link />`
client side
``` tsx
import Link from "next/link";
// to page app/about/page.tsx
<Link href={"/about"}>About</Link>
<Link href={"/about"} replace>About</Link> // replace, clear, navigate history
<Link href={"/"}>Home</Link>
```

``` tsx
import Image from "next/image";
```

``` ts
"use clinet";
import { usePathname } from 'next/navigation'

... {
	const pathname = usePathname()
	const xx = pathname.split("/")[2]
}
```

``` tsx
import { useRouter } from "next/navigation"

export default function OrderProduct() {
	const router = useRouter()
	
	const handleClick = () => {
		router.replace("/")
		router.back()
	}
}
```

`redirect()`
``` ts
import { redirect } from "next/navigation"

redirect("/product")
```

### Layout
root layout is mandatory
- layout component need a `children` prop
- nested layout
- multiple root layout - route group
### Template
similar to layout use `template.js` or `template.tsx`
- new instance
- DOM elements are recreated
- state is cleared
- effect re-synchronized
### Error
```tsx
export default function Error({ error, reset }: { error: Error, reset: () => void }) {
	return <div>{error.message}</div>
}
```

slot → @folder
### Server Side Rendering and Client Side Rendering

##### React Server Component (RSC)
default is server component
- async, handle reading files, fetching data
- no React hooks or interaction

prefix `server`  will should when using `console.log()` on RSC

`use client` on top of the file to change to Client Component
``` tsx
"use client"; // on top of the file
```


`<button />` onClick does not work on server component
- faster
- SEO
- async component

To make <button /> work, import client side render component (button) into server side render component.

### API
`route.ts`
``` ts
import { NextResponse } from 'next/server';

export async function GET() {
	return NextResponse.json({
		message: "Hello"
	})
}

export async function POST(request: Request) {
	const data = await request.json()

	return NextResponse.json({
		message: "Hello"
	})
}

```

Use in `page.tsx`
``` ts
async function makePostRequest() {
	const res = await fetch("/api/hello", { // server render component: ${fullUrl}/api/hello
		method: "POST",
		headers:{
			"Content-Type": "application/json",
		},
		body: JSON.stringify({ name: "Pedro" }),
	});
	const data = await res.json()
}
```

### MetaData
handle in `layout.tsx` or `page.tsx` 
in server rendering component
``` tsx
import { Metadata } from 'next'

export const metadata: Metadata = {
	title: "About Us",
	description: "Generated by next app",
}
```

``` ts
	// in main layout
	title: {
		default: "Default Title",
		template: "%s | Website Name",
	},
	
	// in pages
	title: {
		absolute: "", // overwrite using absolute
	}
```