#JavaScript 

fast
reuse → content-addressed global store (`pnpm store path`), `node_modules` are hard links / symlinks into it, so a package is downloaded and stored once per machine

strict `node_modules`: only declared dependencies are importable (no phantom deps)

``` sh
pnpm install
pnpm add <pkg> / pnpm add -D <pkg>
pnpm remove <pkg>
pnpm dlx <pkg> # = npx
pnpm -r <cmd> # run in every workspace package
pnpm store prune
```