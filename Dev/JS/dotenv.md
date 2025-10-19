#JavaScript 

https://www.dotenv.org/
Documentation: https://github.com/motdotla/dotenv

- `.env`
- `.env.local`
- `.env.production`
- `.env.example`

```sh
npm i dotenv
```

```js
import { config } from "dotenv"

config({path: '.env.local'})
```

use in the project
```js
process.env.KEYNAME
```
