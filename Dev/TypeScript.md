#JavaScript #TypeScript #programming-language #web-dev 

TypeScript, by Microsoft.

-   JavaScript -> Dynamic
    
-   TypeScript -> Static

TypeScript needs to be complied to JavaScript

  

Check TypeScript installed: `tsc --version`

Install TypeScript `npm install -g typescript`

Convert TypeScript to JavaScript `tsc name.tx`

  

`tsc --init` to create a tsconfig.json

  

Watch -> complier will automatcially comple after file changed

Problem
https://blog.csdn.net/dujyong/article/details/106359483


### Type

Variables

```TypeScript
let variable: number;

let variableArray: number[];

// union types
var variable: (string | number | boolean )  = "s";
variable = 1;
variable = true;
```

Object

```TypeScript
let variable: object;
variable = { name: "John", age: 30 };

let variable: { name: string, age: number, info: string };
variable = { "John", 30, "123456" };
```

### Type Aliases

```TypeScript
type StringOrNum = string | number;

const variable: StringOrNum;
```

### Function

```TypeScript
let logDetails: (obj: {name: string, age: number}) => void;

type person = {name: string, age: number};

logDetails = (ninja: person) => {
    console.log(`${ninja.name} is ${ninja.age} years old`);
}
```

```TypeScript
function functionName (): void {};

type person = {name: string, id: number};
var FuncVariable : (obj: person) => void;
```

### Optional / default parameter

```TypeScript
// c? optional, c will be undefined if not input
const add = (a: number, b: number, c?: number | string ) => {}

// set a default value
const add = (a: number, b: number, c: number | string = 10 ) => {}
```

### Access Modifer

```TypeScript
readonly variable;
private variable;
protected variable;
public variable;
static variable;
```

Shortcut for Class Constructor by using access modifer

```TypeScript
class Invoice {
    constructor (
        readonly variable1;
        private variable2;
        public variable3;
    ) {}
}
```

### Enum

```TypeScript
enum ResourceType { Book, AUTHOR, FILM, DIRECTOR, PERSON }

resourceType = ResourceType.Book;
```

Internally use a int

Namespace

```TypeScript
namespace name {
    ...
}
```