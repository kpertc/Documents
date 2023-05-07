#web-dev

-   `npm run` → dev server: directly serve ES module to the browser
-   `npm build` → Rollup bundle

Hot module replace(HMR)

.env file import.meta.env [Env Variables and Modes](https://vitejs.dev/guide/env-and-mode.html)

Webpack
-   Bundles all JS modules, CSS, and other assets
`create react app` → [[Webpack]]


Speedy Web Compiler, SWC

<br>

```shell
npm create vite@latest projectname

npm init @vitejs/app

npm init vite
```
  
No command
```shell
npm install vite
```

<br>

### vite.config.ts
```jsx
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000, // port
  }
})
```