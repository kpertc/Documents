https://jsdoc.app/

Comment -> JS Documentation generator

`jsdoc.json` -> config file

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

// Multiple Types

/**
 * @type {{id: number|string, text}}
 */
const todo = {id: "string", text: 'Hello'}
```

Function
```js
/**
 * Calculate tax
 * @param {number} amount - Total amount
 * @param {number} tax - Tax percentage
 * @returns {string} - Total with a dollar sign
 */

const calculateTax = (amount, tax) => {
	return `$${amount + tax * amount}`;
}
```



type check
 ![[vscode-checking.png | 200]]
``` js
// @ts-check

or

//  VSCode setting
"javascript.implicitProjectConfig.checkJs": true
```


Duplicate from `jsdoc/templates/default`
```json
// jsdoc.json
"opts": {
	"template": 
}
```
![[jsdoc-templates-default.png | 300]]