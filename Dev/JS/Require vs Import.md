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

export 
```

NodeJS modular system is CommonJS




``` js
// at the begining of the file
import * as customName from ''   
import default, { function1, variable1 } from ''
'/path' // absolute path
'./path' // relative path

// at the end of the file
export default User
export { function1, variable1 }
```


```HTML
<script type='module' src='main.js'></script> // only run browser support module
<script nomodule src='main.js'></script> // only run browser does not support module 
