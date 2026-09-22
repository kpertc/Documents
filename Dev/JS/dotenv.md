#JavaScript 

https://www.dotenv.org/
Documentation: https://github.com/motdotla/dotenv

- `.env` - raw dotenv loads only this one, no cascade / merge
- `.env.example` - the only one to commit, placeholder values only

framework convention (Vite / Next.js / CRA), not dotenv → [[Vite]]
- `.env.local`
- `.env.production`

> [!DANGER] gitignore before the first commit
> `.env`, `.env.local`, `.env.*.local`
> `git rm --cached` does NOT remove a secret from history — once pushed, rotate the key

Node 20.6+ has it built-in, no dependency needed
```sh
node --env-file=.env app.js
# --env-file-if-exists (22.9+ / 20.18+)
# process.loadEnvFile() (21.7+) — programmatic
```

`dotenv` is for older runtimes / bundler contexts
```sh
npm i dotenv
```

```js
import { config } from "dotenv"

config({path: '.env.local'}) // path REPLACES the default, `.env` is no longer loaded
config({ path: ['.env.local', '.env'] }) // 16.4+, load both, earlier entries win
```

> [!WARNING] ESM
> `import` is hoisted and runs before the module body, so `config()` here fires *after* imported modules already read `process.env`
> use `import 'dotenv/config'` as the first import, or `node --env-file=.env`

use in the project
```js
process.env.KEYNAME
```
