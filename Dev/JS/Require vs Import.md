#JavaScript 

CommonJS|ES6
---|---
`require`|`import`
`module.exports` / `exports`|`export` / `export default`

`require` can work  inside condition and function
``` js
if ( ... ) {
	const _module = require("./theModule"); // path
}
```

dynamic `import()` does the same in both systems (ES2020), returns a promise, and is the only way to load ESM lazily
``` js
if ( ... ) {
	const _module = await import("./theModule.js");
}
```

<br>

```js
// In Module
const someFunc = () => {};

module.exports = someFunc; // only export one module
```

```js
const someFunc1 = () => {};
const someFunc2 = () => {};

module.exports = {
	someFunc1,
	someFunc2
};
```

Common JS Module

```jsx
// In Script
const _module = require("./theModule"); // path

_module(); // contain only one function

_module.functionName(); // contain multiple functions
```

NodeJS supports both: CommonJS is the historical default, ESM is selected per package or per file
- package.json `"type": "module"` → `.js` is ESM, `.cjs` for CommonJS
- no `"type"` / `"type": "commonjs"` → `.js` is CommonJS, `.mjs` for ESM
- `Cannot use import statement outside a module` / `require() of ES Module not supported` → the file is in the wrong mode




``` js
// at the begining of the file
import * as customName from ''   
import defaultExport, { function1, variable1 } from '' // default is a reserved word, can not be a binding name
'/path' // absolute path
'./path' // relative path, ESM in Node needs the extension → './mod.js'

// at the end of the file
export default User
export { function1, variable1 }
```


```HTML
<script type='module' src='main.js'></script> // only run browser support module
<script nomodule src='main.js'></script> // only run browser does not support module 
```
