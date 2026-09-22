#JavaScript #TypeScript 

App Router, Next 15+

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

Turbopack // default for `next dev` and `next build` since Next 16

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
	const { userId } = await params;
	const user = await getUser(userId);
	
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
// in server render component
export default async function UserPage({
	params, // [articleId] -> /articleId/
	searchParams, // ?&lang=en
}: {
	params: Promise<{ slug: string[] }>
	searchParams: Promise<{ lang?: "en" | "fr" }>
}) {
	const { slug } = await params;
	
	const { lang } = await searchParams;
}
```

``` tsx
// in client render component, not async
"use client";
import { use } from "react"

export default function UserPage({
	params,
	searchParams,
}: {
	params: Promise<{ slug: string[] }>
	searchParams: Promise<{ lang?: "en" | "fr" }>
}) {
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
"use client";
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
"use client"; // error boundary must be a client component

export default function Error({ error, reset }: { error: Error & { digest?: string }, reset: () => void }) {
	return <div>{error.message}</div>
}
```
errors thrown in the root `layout.tsx` are not caught here, use `global-error.tsx`

slot → @folder
`app/@team/page.tsx` is a named slot, passed to the layout as a prop next to `children`; every slot needs a `default.tsx` or a hard refresh on a sub-route 404s
### Server Side Rendering and Client Side Rendering

##### React Server Component (RSC)
default is server component
- async, handle reading files, fetching data
- no React hooks or interaction

`console.log()` in RSC prints to the terminal running `next dev`, not the browser console

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
relative URL only resolves in the browser, in a server component `fetch("/api/hello")` throws `Failed to parse URL` → use an absolute URL, or skip the HTTP round trip and call the data function / Server Action directly

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

Image
``` tsx
import Image from "next/image";

<Image src="/a.png" alt="" width={800} height={600} /> // width + height required
<Image src="/a.png" alt="" fill /> // or fill + parent with position: relative
// sizes -> responsive srcset
// priority -> LCP image, turn off lazy loading
// external host -> images.remotePatterns in next.config
```

Google Font
``` tsx
import { Bokor } from "next/font/google";

const bokorFont = Bokor(
	{
		subsets: ["latin"],
		weight: "400"
	}
)

return (
	<div className={`${bokorFont.className}`}>
		1111
	</div>
)
```