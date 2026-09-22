#web-dev

Vite 7 (Node 20.19+ / 22.12+)
dev: native ESM + esbuild (dep pre-bundling / transforms) → instant HMR; build: Rollup (→ Rolldown)

Hot module replace(HMR)
update part of the code and re-instantiate, not reload the page

.env file import.meta.env [Env Variables and Modes](https://vitejs.dev/guide/env-and-mode.html)

Webpack
-   Bundles all JS modules, CSS, and other assets
`create react app` (sunset) → [[Webpack]]

Hot Module Replacement (HMR) → Watch

Speedy Web Compiler, SWC → opt-in via `@vitejs/plugin-react-swc`, not Vite's default

```shell
npm create vite@latest projectname

npm init vite@latest
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
```ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
	host: true,
	port: 3000, // port
  },
  build: {
	outDir: "../dist",
	emptyOutDir: true, // Empty the folder first
	sourcemap: true,
	target: "esnext" // for modern browser, (may not be able to run on some old browser)
  }
})
```