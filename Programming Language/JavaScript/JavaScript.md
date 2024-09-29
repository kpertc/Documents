w#JavaScript #programming-language #web-dev 

JavaScript Background knowledge: [[JavaScript Overview]]
JavaScript Browser Functions: [[JavaScript API]]

### HTML Template & Hello World

Javascript can be inserted between HTML content

`defer` attribute: execute after page has finished parsing

```HTML
<html>
<head>
  <meta charset="utf-8">
  <title>JavaScript Tutorial</title> 
  <script src="Script.js"></script> 
  
  <script defer src="Script.js"></script>
</head>
<body>
  <script type="text/javascript">
      document.write("Hello World");
  </script> 
</body>
</html>
```

```JavaScript
alert("This is an alert");
```

[[YouTube] What is the Fastest Way to Load JavaScript by Web Dev Simplified](https://www.youtube.com/watch?v=BMuFBYw91UQ)

![[image-3.png]]

### `use strict`

Strict Mode
Safer code
```JavaScript
'use strict' // at first line

// Inside a function
function strict_function() {
  'use strict'; // rest of the function
}

```


``` js
// this[] 任意类型
// this.property
this.aabb = this[aabb]
```

### Comments

```JavaScript
// Comment

/*
    comments
    comments
*/
```

### Accessing HTML Elements

```JavaScript
var header = document.getElementById("header")

header.innerHTML = "Mike's new H1" // change the content of header to custom string

header.style.color = "red";
header.style.background = "red";

var link = document.getElementById("Link");
link.href = "https://amazon.com";
link.style = "color:red;"

// Writing HTML
document.write("<h2>Javascript rules</h2>");
document.write("<hr/>");
```

##### Query Selector

```JavaScript
// Query Selector lets you find the first Element that matches the CSS selector
var element = document.querySelector("h1");
var element = document.querySelector(".class");
var element = document.querySelector("#id");

document.querySelectorAll()
```

### [DOM Manipulate](https://youtu.be/y17RuWkWdn8)

Document Object Model (_DOM_)

```JavaScript
// add Element
document.body.append() // more versatile, appned multiple item, string directly
document.body.appendChild()

// create Element
const div = document.createElement('div'); // CSS selector
document.body.append(div);
// add text to the div
div.innerText = "Hello World"; // visible text contained in a node
div.textContext = "Hello World"; // the full text, with style

// Modify Element
div.innerHTML = "<strong>Hello World</strong>" 

const strong = document.createElement("Strong")
strong.innerText = "Hello World"
div.append(strong)

// Remove Element
element.remove();
element.removeChild(element);

// Element Attribute
element.getAttribute('id');
element.id; // if the attribute has the function, most of attrs does

element.setAttribute('id', 'valueToSet');
element.id = 'valueToSet';

element.removeAttribute('id'); // remove Attribute

// DataSet
<span> data-custom-attr = "value" </span>
element.dataset.customAttr = 'value';

// Classes
element.classList.add('hi1'); // add a class
element.classList.remove('hi1'); // remove a class
element.classList.toggle('hi1'); // remove if it exist; add if it not exist
element.classList.toggle('hi1', true); // add/remove depending on conditional

// Style
element.style.color = "red";
element.style.backgroundColor = "red"; // background-color in HTML
```

[[Require vs Import]]


```JavaScript
 var
 let // in the scope, can be redeclared value
 const // can not be redeclared value
```

### `var` `let` `const`
[https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/](https://www.freecodecamp.org/news/var-let-and-const-whats-the-difference/)

`let` & `const` -> ES6

`var` declarations are globally scoped or function/locally scoped.
`var` can be redeclared, can be reassigned, even function scope can overwrite global scope

```js
// can be redeclared & reassigned
var greeter = "hey hi";
var greeter = "say Hello";
greeter = "say Hello instead";
```

```js
var greeter = "hey hi";

if (true) {
	var greeter = "say Hello";
}

console.log(greeter); // "say Hello" ← May cause problem
```

`let` can not be redeclared, can be reassigned

can not overwrite, function scope can not overwrite global scope

```js
// can not be redeclared
let greeter = "hey hi";
let greeter = "say Hello"; // error

greeter = "say Hello"; // can be reassigned
```

```js
let greeter = "hey hi"

if (true) {
	// different greeter
	let greeter = "say Hello";
}

console.log(greeter); // "hey hi"
```

`const`
can not be redeclared & reassigned

`const`所保证的应该是变量指向的内存地址不能够被改变，也就是保存的指针, 并不是保证变量的值不可以被改变。实际上是可以被改变的。如果需要保证原本的对象本身不被改变，我们可以使用`Object.freeze()`来冻结所声明的对象变量。

##### Hoisting

Hoisting is a JavaScript mechanism where variables and function declarations are moved to the top of their scope before code execution. 

This means that if we do this:

`var`
```js
console.log(greeter); // undefined
var greeter = "hey hi";
```

`let` & `const`
```js
console.log(greeter); // error
let greeter = "hey hi";
```

`let` & `const` are actually `undefined` but scope is not accessible, in "Temporal Dead Zone"

![[var-let-lifecycle.png]]

Related to: [[JavaScript Overview#Memory Creation Phase (Creation Phase)]]
<br>

### `Null` & `undefined`


undefined 不是 undeclared
undeclared 是指变量从未在代码中出现.使用未声明的变量就会报错：”ReferenceError: cat is not defined“。
undefined 则是声明了但是值是 undefined 或者值并不存在。

---

nullish coalescing operator → the double question mark `??`

```jsx
const foo = null ?? 'default value';
console.log(foo); // Output: 'default value'
```

`??` checks for `null` or `undefined` values

`||` accepts for falsy values (`null`, `undefined`, `false`, `0`, `''`, or `NaN`).

```jsx
const bar = '' || 'default value'; // 'default value'
const baz = '' ?? 'default value'; // ''
```

`??=`
 Assign a default value to a variable if it is `null` or `undefined`.
``` Javascript
let firstName = null;
firstName ??= 'yangyang'
console.log(firstName); // 'yangyang'

let lastName = 'name';
lastName ??= 'yangyang'
console.log(lastName); // 'name'
```

---

`null` 是基本数据类型 但是`typeof null` 是 `object` → bug 是 JavaScript 第一版的遗留物

<br>
### Variables & Data Types

```JavaScript
var phrase = "To be or not to be"; //string can use both single or double quotation marks
document.write(phrase);

var age = 23; //int
var gpa = 3.1; //decimal
var isMale = true; //boolean

var flaws = null; //null, no value
var description = undefined; //variable does not have a value yet, open to possibility to have a value
```

symbol (ES6): new primitive data type in ES6

immutable, unique, will not equal
```JavaScript
let symbol1 = Symbol('symbol1')

// to string
symbol1.toString()
```

Assign undeclared variable -> automatically global variable

```JavaScript
function app() {
    l = 'local';
}

console.log(l); // print out 'local' at global scope
```


Get type

```JavaScript
console.log(typeof var);
console.log(typeof "23");
```

<br>

### Working with Strings

```JavaScript
phrase.length
phrase.toUpperCase()
phrase.toLowerCase()

phrase.charAt() //phrase.charAt(2) find the third letter
phrase.indexOf() //phrase.indexOf('a') return letter'a' index
phrase.lastIndexOf() //phrase.lastIndexOf('a') return the last letter 'a' 's index

phrase.substring(0, 3) //return the part of the string, get letters of index between 0 - 3

phrase.endsWith('cool') //return boolean base on if the phrase end with 'cool'
phrase.includes('') //return boolean if the phrase include ''
```

##### Template literals (Template strings)

```JavaScript
const variable1 = "A";
const variable2 = "B";

console.log(`text ${variable1} ${variable2} text`); // text A B text
```

### Math & Numbers

```TypeScript
11 % 3 //mod
Math.abs(number) //absolute value

Math.max(number1, number2) //return the bigger number
Math.min(number1, number2) //return the smaller number

Math.round(number) //round
Math.pow（number, 3）//power number³
Math.sqrt(36) //square root → 6 

Math.random()
```

##### BigInt

**`BigInt`** values represent numeric values which are [too large](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER) to be represented by the `number` [primitive](https://developer.mozilla.org/en-US/docs/Glossary/Primitive). from [Mozilla BigInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)

```js
const _bigint = 1234n; // A bigint is created by appending n 
console.log(typeof _bigint); // bigint

// math
console.log(1n + 2n); // 3
```

> [!NOTE]
> ```
> 0.1 + 0.2 === 0.3; // false -> 0.30000000000000004
> ```
> 这是和 JavaScript 采用“遵循 IEEE 754 标准的双精度 64 位格式”有关。

typeof NaN 返回 'number'

### Getting User Input

```JavaScript
var name = window.prompt("What is your name");
```

### A Basic Calculator

```JavaScript
var num1 = window.prompt("Enter a number: ");
var num2 = window.prompt("Enter another number: ");

num1 = parseInt(num1); //convert string to int
num2 = parseInt(num2);
//num2 = parseFloat(num2);

document.write(num1 + num2);
```

### Array

```JavaScript
// Create an array
var fruits = new Array("Apples", "Oranges", "Peaches");
var fruits = ["Apples", "Oranges", "Peaches"];
var fruits = ["Apples", 24, false]; //can store multiple type of variables

document.write(fruits)
fruits.length //return the length of the array

var fruits = new Array("Apples", "Oranges", "Peaches");
fruits = fruits.split(",") //convert string to array, split by ","
document.write(fruits[0]);

array.unshift(object) // add object the position of first, index 0
```

##### [Array/Object Destructuring](https://www.youtube.com/watch?v=NIq3qLaHCIs)

Array
```JavaScript
const alphabet = ['A', 'B', 'C', 'D', 'E', 'F']
const numbers = ['1', '2', '3', '4', '5', '6']

const [a, b, c] = alphabet // a = 'A', b= 'B', c = 'C'
const [a,,c] = alphabet // a = 'A', c = 'C'
const [a,,c ...rest] = alphabet 
// a = 'A', c = 'C', rest = ['D', 'E', 'F']

// concatenate two array
const newArray = [...alphabet, ...numbers] 
// ['A', 'B', 'C', 'D', 'E', 'F', '1', '2', '3', '4', '5', '6']
const newArray = alphabet.concat(numbers)
// ['A', 'B', 'C', 'D', 'E', 'F', '1', '2', '3', '4', '5', '6']
```

```jsx
const items = [
	{ name: 'Bike', price : 100 },
	{ name: 'TV', price : 200 },
	{ name: 'Album', price : 10 },
	{ name: 'Book', price : 5 },
	{ name: 'Phone', price : 500 },
	{ name: 'Computer', price : 1000 },
	{ name: 'Keyboard', price : 25 },
]
```

##### filter
```jsx
const filteredItems = items.filter((item) => {
	// return Bool	
	return item.price <= 100
})
```

##### map
```jsx
// convert to a new type of array
const itemsNames = items.map((item) => {
	return item.price
})

// { 100, 200, 10, 5, ... }
```

##### find
```jsx
const foundItem = items.find((item) => {
	return item.name === "Book"
})

// return the first item found in array
```

##### forEach, no return

##### some
```jsx
// check entire array if one item meets the condition 
const hasInexpensiveItems = items.some((item) => {
	return item.price <= 100 // Bool
})

// hasInexpensiveItems -> true
```

##### every
```jsx
// check entire array if every items meet the condition
const hasInexpensiveItems = items.every((item) => {
	return item.price <= 1000 // Bool
})

// hasInexpensiveItems -> true
```

##### reduce
```jsx
// calculate total
const total = items.reduce((currentTotal, item) => {
	return item.price + currentTotal
}, 0) // 0 -> initial value
```

Object
```JavaScript
function sumAndMultuply(a, b) { return [a+b, a*b] }

const [sum, multiply, division = 'no division'] = sumAndMultuply(2,3)
// sum = 5, multiply = 6

const personTwo = {
    name: 'Sally',
    age: 32,
    address: {
        city: 'Somewhere else',
        state: 'Another one of them'
    }
}

// access base on object name
const { name, age } = personTwo // name = 'Sally', age = '32'
const { name: firstName, age, favoriteFood = 'Rice' }  = personTwo
// firstName = 'Sally', age = 32, favoirte = 'Rice' -> default value

const { name: firstName, ...rest } = personTwo
// rest = [ age, address ]

// use spread deconstruct in nested obect
const { name: firstName, address: { city } } = personTwo // city = 'Somewhere else'
```

```JavaScript
const personThree = { ...personOne, ...personTwo } 
// later object with same property will overwrite the first one
```

```JavaScript
function printUser ({ name, age, favoriteFood = 'Watermelon' }) { ... }
```

<br>

### Getter & Setter

getter → access like property

```jsx
const person = {
	firstName: 'Mosh',
	lastName: 'Hamedani',
	get fullName(){
		return `${person.firstName} ${person.lastName}`
	},
	set fullName(value){
		const parts = value.split(' ');
		this.firstName = parts[0];
		this.lastName = parts[1];
	}
};

console.log(person.fullName); // get
person.fullName = "John Smith"; // set
```

Overwritten by getter
![[overwritten-by-getter.png]]

<br>

### Function

```JavaScript
function sayHi(){
    document.write("<h1>Hello</h1>")
}

sayHi(John)

function sayHi(name){
    document.write("<h1>Hello" + name + "</h1>")
}

function addition(num1, num2){
  return num1 + num2
}
```

Functions are objects in JavaScript
Anonymous Function
`function () {...}`

Arrow Function (ES6 later)
`() => {...}`

arrow function -> variable must be declared before use
`function` can be hoisted

```JavaScript
function sum(a, b) {
    return a + b
}

let sum = (a, b) => a + b // directly return, no curly braces {}

let isPositive = number => number >= 0 // only one parameter, no need parentheses 

let randomNumber = () => Math.random // no parameter ()
```
##### [Arrow Function Scope](https://blog.webdevsimplified.com/2020-09/arrow-functions/)
``` javascript
	const parentFunction = () => {
		// local
	}
```

Lexical Scope defines how variable names are resolved in nested functions

```JavaScript
class Person {
  constructor(name) {
    this.name = name
  }

  printNameArrow() {
    setTimeout(() => {
      console.log(`Arrow: ${this.name}`)
    }, 100)
  }

  printNameFunction() {
    setTimeout(function() {
      console.log(`Function: ${this.name}`)
    }, 100)
  }
}

const person = new Person('Kyle')
person.printNameArrow()  // Arrow: Kyle
person.printNameFunction()  // Function: 
```

##### Static Function

```JavaScript
class Emoji {

    static addOneTo(val) {
        return 1 + val;
    }
}
```

### Event Listeners

`console.log()` to check event listeners on the object

```JavaScript
<button id="button" onclick="alert('you clicked');">Clicked Me</button>
<button id="button" onclick="handleclick()">Clicked Me</button>

//External JavaScript
function handleClick(){
    element.style = "background-color:blue";
}

//this
<button id="button" onclick="handleClick(this)">Clicked Me</button>

function handleClick(element){
    element.style = "background-color:blue";
}

var image = document.getElementById("image")

//javaScript no On
//mouseover
image.addEventListener("mouseover", function(){
    this.style = "box-shadow: 2px 2px 2px grey";
    this.witdth = "110"
});

//mouseout
image.addEventListener("mouseout", function(){
    this.style = "";
    this.witdth = "100"
});

// remove EventListener
element.addEventListener("click", functionName) 
element.removeEventListener("click", functionName)
```

-   Bubbling -> bigger scope 🫧
    
-   Capturing -> smaller scope 📸

![[bubbling-capturing.png | 200]]

```JavaScript
element.addEventListener("click", e => {}, { capture: true }) 

{ once: true } // only run once
e.stopPropagation(); // Stop bubbling or Capturing
e.matches()
```

Order

### [Custom Event](https://youtu.be/DzZXRvk3EGg)

```JavaScript
const myEvent = new Event("myCustomEvent")

document.addEventListener("myCustomEvent", e => {})

document.dispatchEvent(myEvent)
```

### Messaging App

```JavaScript
var messages = document.getElementById("")
var textbox = document.getElementById("")
var button = document.getElementById("")

button.addEventListener("click", function(){
    var newMessage = document.createElement("Li")
    newMessage.innerHTML = textbox.value;
    message.appendChild(newMessage);
    textbox.value = "";
});
```

### If Statement

```JavaScript
var isMale = false

if(isMale){
    document.write("You are male");
}

else if (!isMale) // not the condition
{

}

else
{
    document.write("You are not male");
}

// && -> and
// || -> or 
```

[Conditional (ternary) operator - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

```CSS
condition ？ true ：false
condition && true
```

### Switch

```JavaScript
var day;

switch(dayNum){
    case 0:
        day = "Sunday";
        break;
        
    case 1:
        day = "Monday";
        break;
        
    default:
        day = "Invalid day"
}
```

### Try

```JavaScript
try {}
catch (error) {}
finally {} // finally will execute after a try or catch
```

### Object

```JavaScript
var person {
    name: "Mike",
    age: 23,
    isMale: true,
    occupation: "programmer"
}

document.write(person);
```

### While Loop

### Timing (Delay)

```JavaScript
//HTML
//use once 3000 -> 3 seconds
<button onClick = "setTimeout(sayHi, 3000)">Click Me</button>

//use repeatly
<button onClick = "setInterval(sayHi, 3000)">Click Me</button>
```

### Web Storage

```JavaScript
var textbox = document.getElementById("textbox");
var button = document.getElementById("btn");

button.addEventListener("click", function()){
    localStorage.name = textbox.value;
});
document.write(localStorage.name);
```

<br>

##### Optional chaining (?.)
```js
_object.property?.property
```


### bind & call & apply
> `call()`、`apply()`、`bind()` 三个方法都可以根据指定的 `this` 值调用。
##### bind
[Bind Explained in JavaScript](https://www.youtube.com/watch?v=g2WcckBB_q0)
```js
// 组合函数到object上
// Bind an object to a function
// Reference it using 'this'

let c1 = {x:5, y:10}

function printCoordinates () {
	console.log(this.x + ',' + this.y);
}

let c1_func = printCoordinates.bind(c1);

c1_func(); // output 5,10
```

##### call
call can not set argument array
```js
let foo = {
    value: 1
};

function bar() {
    console.log(this.value); 
}

bar.call(foo); // 1
```

##### apply
The **apply() method** is used to write methods, which can be used on different objects. [https://www.geeksforgeeks.org/javascript-apply-function/](https://www.geeksforgeeks.org/javascript-apply-function/)

```js
function sum(a, b) {
    return a + b;
}

console.log(sum.apply(null, [3, 5])) // 8
```

```js
const student = {
    grade: 5
}

function sum(a, b) {
    return this.grade + a + b;
    // this -> object
}

// object + arguments (any length)
console.log(sum.apply(student, [3, 5])) // 13
```

<br>

### OOP

##### Class

ES6 introduced classes which is the modern way to construct objects.

```JavaScript
class Player {
    constructor(x, y, radius, color) {
        this.x = x
        this.y = y
        this.radius = radius
        this.color = color
    }
}

const player = new Player (100, 100, 30, 'blue')


// extend class
class Motorcycle extends Vehicle {
    constructor() {
        super();
        this.wheels = 2
    }
    
    wheelie() {
        return "On one wheel Now! ";
    }
}
```

##### `__proto__`

```JavaScript
array.sort()
array.__proto__.sort
```

```JavaScript
const person = { alive: true } 
const musician = { plays: true } 

musician.__proto__ = person;

// instead of use "__proto__" directly
Object.setPrototypeOf(musician, person); // child, parent
Object.getPrototypeOf(musician)
console.log(Object.getPrototypeOf(musician)); // {alive: true}

const guitarist = { 
	strings: 6, 
	__proto__: musician 
}
```

If can not find the properties, JavaScript will find through proto chain
proto chain musician -> person -> JavaScript Object

![[proto-chain.png | 300]]

-   No circular references allowed
-   The __proto__ value must be an object or null
-   An object can only directly inherit from one object

Add function outside a class by prototype

![[add-function-outside-a-class-by-prototype.png]]

`Object.keys` to get keys
```JavaScript
Object.keys(luxuryCar)

// loop through each object key
Object.keys(luxuryCar).forEach(key => {
	console.log(key);
}};

// But a for..in loop includes inherited props
for (let key in luxuryCar) {
	console.log(key);
}
```

prototype

`prototype` → object
`__proto__` → instance ?

```js
function Animal() { ... }

// add a function to Animal by prototype
Animal.prototype.walks = function () { return 'walk' }

const Bear = new Animal()
console.log(Bear.walks()) // walk

console.log(Bear.__proto__ === Animal.prototype) // true
// Proved: Bear is inherited from Animal
```

in ES6, a modern way to create inherit is to use Class & Class extends & constructor { super() } 

<br>

### Async

[Async JS Crash Course - Callbacks, Promises, Async Await](https://youtu.be/PoRJizFvM7s?si=igRChHXkcGcd9JLT)

Old fashion way
##### callback 
```js
// callback
function createPost( _arguments, callback) {
	// ... do something 
	callback() // execute the function
}
```


##### Promise
```JavaScript
let p = new Promise((resolve, reject) => { 
    if () {resolve('message')}
    else () {reject('message')}
})

p.then((message) => {console.log(message)}) // successful case
p.catch((message) => {console.log(message)}) // error case
```

```js
// Promise
function createPost() {
	// ... do something
	return new Promise((resolve, reject) => {
		// ... do something
		if () {
			resolve()
		} else {
			reject()
		}
	})
}

createPost()
.then( // success from resolve()
	// ... do something
)
.catch( // error from reject()
	err => {
		// ... do something
	}	
)

// Promise.all -> process multiple Promises
Promise.all([promise1, promise2, promise3]).then(
	values => console.log(values)
)
```

##### async / await
```js
async function init() {
	await ... // some 

	// wait the previous processed ↓ then execute next line

	getPost();
}
```

![[async.png]]

##### Mixins

a function to create a function
``` js
function myFunc() {
    return () => { console.log("hello") };
}

const logger = myFunc();
logger();
```

a function to create a class
``` js
function createLoggerClass() {
    return class MyLoggerClass {
        private msg = "Hello";
        log() {
            console.log(this.msg);
        }
    }
}

const logClass = createLoggerClass();
const logClassInstance = new logClass();

logClassInstance.log();
```

<br>
### [Console](https://www.youtube.com/watch?v=UUoZ_U2_4tA)

```javascript
console.log("Log")
console.debug("Debug")
console.info("Info")
console.warn("Warn")
console.error("Error")
```

![[console-log.png]]

```JavaScript
// For live view
console.log({ ...object }) // clone object: will show log time object info
console.log(JSON.parse(JSON.stringify(object)))

JSON.stringify(api, null, 4); // formatting

// Apply CSS Style
console.log("Normal, %cGreen", "color: green") // %c begin CSS

// print out as JSON object
console.dir(var))
```

`console.table()`

![[console-table.png]]

```JavaScript
const people = [
{ name: "Kyle", age: 27, programmer: true },
{ name: "Sally", age: 15, programmer: false },
{ name: "John", age: 34, programmer: false },
{ name: "Beth", age: 72, programmer: true }
]
console.table(people)
```

![[console-group.png]]  

```javascript
console.group()
console.groupCollapsed("Stats") // optional collapse
console.log('Inside Group')
console.log('Still Inside Group')

console.group() // group can be nested
console.groupEnd()

console.groupEnd()
```

```javascript
console.time()
console.timeLog() // just log the current time length, will not stop the timer
console.timeEnd()

console.time("Name") // can init multple timer
console.timeEnd("Name")
```

Profiler -> `Chrome` / `JavaScript Profiler`

Usage depends on Browser

![[profiler.png]]

```undefined
console.profile("Name")
// do something ...
console.timeStamp("Name")
// do something ...
console.profileEnd("Name")
```

### [JSON](https://youtu.be/B-k76DMOj2k)

-   JavaScript Object Notation
-   Data Representation Format
-   Lightweight and easy to Read/Write

JSON can store types: `String`, `Number`, `Boolean`, `Null`, `Array`, `Object`

```JavaScript
var myJSON = {
    "name": {
        "first": "Beau",
        "last": "Carnes"
    },
    "age":33,
    "skills": [ "juggling", "stiltwalking", "coding" ],
    "married": true,
    "superpowers": null
 }

// stringify method
var stringified = JSON.stringify(myJSON);
console.log(stringified);

// parse method
var stringJSON = '{ "name":"Beau", "kids":2,"state":"Michigan"}';
var myParse = JSON.parse(stringJSON);
console.log(myParse);
```
<br>
### Decorator

Decorators wrap a function in another function

---

### Recursive

```JavaScript
const foo = (n) => {
	if(n<=1)return;
	foo(n-1);
};
```

### Add a Object in Global

```JavaScript
global.effect = {
	Ama: "abc"
};
```

```JavaScript
// at another script file
const Ama = effect.Ama; // will not be undefined
```


---
### Credits

作者：LeetCode
链接：https://leetcode.cn/leetbook/read/javascript-interview-2/7m2yq6/
来源：力扣（LeetCode）
著作权归作者所有。