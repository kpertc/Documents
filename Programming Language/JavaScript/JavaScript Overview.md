#JavaScript 

>Any application that can be written in JavaScript, will eventually be written in JavaScript. - Jeff Atwood

- JavaScript is Single-Threaded language
- JavaScript is **synchronous language** with asynchronous capabilities
- A thread has a call stack & memory

JScript -> Microsoft JavaScript

<br>

[State of JS](https://stateofjs.com/en-us/)
[[TypeScript]]
[[JavaScript API]]

<br>

### [[node.js]]  NPM

### [[Yarn]] (Yet Another Resources Negotiator) developed by Facebook

---

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
or in Node.js


Chrome dev-tool check Call Stack

![[chrome dev-tool debug.gif]]

### JS

[JavaScript Under The Hood [2] - Execution Context](https://youtu.be/Fd9VaW0M7K4)

##### Execution context

When you run any JavaScript, a special environment is created to handle the transformation & execution of code. This is called the execution context. It contains the currently running code and everything that aids in its execution

There is a global execution context as well as a function execution context for every function invoked

###### Memory Creation Phase (Creation Phase)

1. Create the global object (browser = `window`, Node.js = `global`)
2. Create the "this’ object and bind it to the global object
3. Setup memory heap for storing variables and function references
    1. objects will be inited as `undefined`
4. Store functions and variables in global execution context and set to `undefined`

> [!info]
>All var → undefined [[JavaScript#Hoisting]]
>All funcs → stored

###### Execution Phase: (Execution phase)

1. Execute code line by line
	Variables will be assign when is executed
2. Create a new execution context for each function call

`console.log() will print 150` because `func getSum()` is loaded to memory ↓

```JavaScript
var x = 100;
var y = 50;

console.log(getSum(x, y)); // 150

// func on the back
function getSum(n1, n2) {
	var sum = n1 + n2;
	return sum
}
```

##### Asynchronous

- Blocking refers to operations that block further execution until that operation completes
- Non-Blocking refers to code that does not block execution

`setTimeout()` is not a part of JavaScript, is WEB API

![[js-asynchronous.png]]

##### Stack & Heap

[JavaScript Under The Hood [4] - Memory Storage](https://youtu.be/Hci9Bb4_fkA)


> Anything is not Primitive is Object

> [!info] Primitive Types
> Primitive Types: Stored directly in the ==stack==, where it is accessed from
> String | Number | Boolean | Null | Undefined | Symbol | Bigint

Symbol →用于唯一的标识符。

> [!info] Reference Types
> Reference Types: Stored in the ==heap== and accessed by reference
> Arrays | Functions | Objects
> Date | RegExp

![[js-stack-heap.png]]

`name` & `newName` are stored independent
``` JavaScript
let name = 'John'

let newName = name; 
newName = 'Jonathan';

console.log(name); // John, does not changed
```

newPerson & person are referencing the same object
``` JavaScript
let person = {
	name: 'Brad',
	age: 40
}

let newPerson = person;
newPerson.name = "Bradley"; // changed referencing object.name

console.log(person.name) // Bradley
```

##### Memory

Memory Management Low-level languages like C and C++ require you to allocate and free up memory manually. This is makes them much more difficult to work with. 

Higher level languages like JavaScript, Python and C# automatically allocates memory when objects are created and frees it when they are not used anymore 

This process is called **garbage collection**

---

Chrome -> Heap Snapshot
![[chrome-devtool-memory.png]]

##### JavaScript Engine
Software component that executes JavaScript code. The first engines were simple interpreters, but modern engines are also responsible for optimizations, such as JIT (Just In Time) compilation.

Each Browser uses a specific JavaScript engine

![[js-engines.png]]

WebKit → render engine

JavaScript → interpret language (Python, Ruby)
	↳ JIT (Compilation at runtime)
C / C++ → Compile language (fast!) 
	↳ AOT (Ahead of time)

- Compiled languages are compiled directly to machine code all at once (fast!)
- Interpreted languages are interpreted line by line
- Compiled languages have a slow write-time and fast run-time and interpreted languages have the opposite

![[js-engine-overview.png]]


Abstract Syntax Tree (AST)
![[Abstract-Syntax-Tree.png| 300]]

ByteCode -  Intermediate Representation (IR)

