#JavaScript 

https://jsdoc.app/

Comment -> JS Documentation generator

`jsdoc.json` -> config file

```bash
npm i -D jsdoc
# package.json: "doc": "jsdoc -c jsdoc.json"
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
const grades = [98, 97.7, 76, true]

/**
 * Array of grades
 * @type {Array<number>}
 */
const grades = [98, 97.7, 76]

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

### Function
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

### Custom Type
```js
/**
 * A student
 * @typedef {Object} Student
 * @property {number} id - Student ID
 * @property {string} name - Student name
 * @property {string | number} [age] - Student age (optional)
 * @property {boolean} isActive - Student is active
 */

/**
 * @type {Student}
 */

const student = {
	id: 1,
	name: "John Doe",
	age: 20,
	isActive: true
}
```

### Class
```js
/**
 * Class to create a person object
 */

class Person {
	/**
	 * @param {Object} personInfo Infomation about the person
	 */
	constructor(personInfo) {
		/**
		 * @property {string} name Persons name
		 */
		this.name = personInfo.name;
		/**
		 * @property {number} age Persons age
		 */
		this.age = personInfo.age;
	}
	/**
	 * @property {Function} greet A greeting with the name and age
	 * @return {void}
	 */
	 greet() {
		 console.log(`Hello, my name is ${this.name} and I am ${this.age}`);
	 }
}
```



### type check
 ![[vscode-checking.png | 200]]
``` js
// @ts-check

or

//  VSCode setting
"js/ts.implicitProjectConfig.checkJs": true
```


Duplicate from `jsdoc/templates/default`

`jsdoc.json` (JSON has no comments):
```json
{
	"opts": {
		"template": "./my-template"
	}
}
```
![[jsdoc-templates-default.png | 300]]