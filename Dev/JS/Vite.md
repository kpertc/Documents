#web-dev

Hot module replace(HMR)
update part of the code and re-instantiate, not reload the page

.env file import.meta.env [Env Variables and Modes](https://vitejs.dev/guide/env-and-mode.html)

Webpack
-   Bundles all JS modules, CSS, and other assets
`create react app` → [[Webpack]]

Hot Module Replacement (HMT) → Watch

Speedy Web Compiler, SWC

```shell
npm create vite@latest projectname

npm init @vitejs/app

npm init vite
```
  
No command
```shell
npm install vite
```

``` sh
# host on public
npm run dev -- --host

# not using cache
npm run dev -- --force
```

### `vite.config.ts`
```jsx
export default defineConfig({
  plugins: [react()],
  server: {
	host: true,
	port: 3000, // port
  },
  build: {
	outDir: "../dist",
	emptyOutDir: true, // Empty the folder first
	sourcemap: true, // 
	target: "esnext" // for morden browser, (may not be able to run on some old browser)
  }
})
```