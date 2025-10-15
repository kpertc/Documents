#JavaScript #TypeScript 

FullStack Framework
- server side rendering
- type safety

competitor:
- [[Next.js]] 
- React Router


Tutorial: 
[Learn TanStack Start in 7 Minutes](https://www.youtube.com/watch?v=WG7x4kG9pFI)

generate type?

``` ts
createFileRoute('/users/$userId') ({
	loader:
	component:
	errorComponent:
	notFoundComponent:	
})
```

``` ts
head: () => ({
	meta: [
		{
			title: "Collax: Your online space to collect and share it all.",
		},
		{
			name: "description",
			content:
			"Collax is a free and easy-to-use online space to showcase portfolios, manage digital content, and create with high-quality templates.",
		},
	],
	links: [
		{
			rel: "icon",
			href: "/favicon.ico",
		},
	],
}),
```

Example:
![[route.png]]

Server example:
``` tsx
createServerFn({})
	.validator()
```


createRouter()