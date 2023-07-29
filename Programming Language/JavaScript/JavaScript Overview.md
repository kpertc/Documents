#JavaScript 

>Any application that can be written in JavaScript, will eventually be written in JavaScript. - Jeff Atwood

- JavaScript is Single-Threaded language
- JavaScript is **synchronous language** with asynchronous capabilities

<br>

[State of JS](https://stateofjs.com/en-us/)
[[TypeScript]]
[[JavaScript API]]

<br>

### [[node.js]]
  

### [[Yarn]] (Yet Another Resources Negotiator) developed by Facebook

---
Anything is not Primitive is Object
Primitive Value: Boolean
Objects:


### History

> 1993 - First Browser -> Mosaic
> 1994 - Mosaic founded company -> Netscape, and release browser
> Need a more interactive language as glue language, at the same time, Java was popular,
> `MOCHA` -> `LiveScript` -> `JavaScript`
> `JScript` Microsoft version JavaScript

<br>

### [[ECMA (ES)]]

<br>

Transpilers: 
- Babel
- Traceur
- Closure

Babel -> https://babeljs.io/
Advanced JS -> backward JS
> Babel is a toolchain that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript in current and older browsers or environments.

[[Webpack]]
[[Vite]]


Run JavaScript in Chrome console
or in node.js


Chrome dev-tool check Call Stack

![[chrome dev-tool debug.gif]]



[JavaScript Under The Hood [2] - Execution Context](https://youtu.be/Fd9VaW0M7K4)

##### Execution context (Execution Phase)

When you run any JavaScript, a special environment is created to handle the transformation & execution of code. This is called the execution context. It contains the currently running code and everything that aids in its execution

There is a global execution context as well as a function execution context for every function invoked

##### Memory Creation Phase (Creation Phase)

1. Create the global object (browser = `window`, Node.js = `global`)
2. Create the "this’ object and bind it to the global object
3. Setup memory heap for storing variables and function references
    1. objects will be inited as `undefined`
4. Store functions and variables in global execution context and set to `undefined`

Execution Phase:

1. Execute code line by line
2. Create a new execution context for each function call
