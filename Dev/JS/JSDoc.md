https://jsdoc.app/

Comment -> JS Documentation generator

`jsdoc.json` -> config file

jsdoc/templates/

```bash
npm run doc
```

```js
/**
 * Student Name
 * @type {string}
 */
const studentName = 'John Doe';

/**
 * Array of grades
 * @type {Array}
 */
const grades = [98. 97.7, 76, true]

/**
 * Array of grades
 * @type {Array<number>}
 */
const grades = [98. 97.7, 76]

/**
 * @type {{id: number, text}}
 */
const todo = {id: 1, text: 'Hello'}

/**
 * @type {{id: number|string, text}}
 */
const todo = {id: "string", text: 'Hello'}
```



type check
 ![[vscode-checking.png | 200]]
``` js
// @ts-check

or

//  VSCode setting
"javascript.implicitProjectConfig.checkJs": true
```