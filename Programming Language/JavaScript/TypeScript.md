#JavaScript #TypeScript #programming-language #web-dev 

TypeScript, by Microsoft.
Created by Anders Hejlsberg, also the creator of C#

-   JavaScript → Dynamic → types are checked at run time.
-   TypeScript → Static → types are checked at compile time.

TypeScript needs to be complied to JavaScript

```shell
# install TypeScript
npm install -g typescript
# permission add sudo

tsc --version # check TypeScript version
```

``` shell
tsc script.ts #compile to js
tsc script.ts -w #watch - complier will automatically compile after file changed 

tsc -w # all files, no specified file

tsc --noEmitOnError -w # not compile ts file when there are ts errors
```

```shell
tsc --init # to create a tsconfig.json 
```

```json
// source of ts script
"rootDir": "./src"

// out
"outDir": "./build/js"

// compile to target version
"target": ""

// compile even there are ts errors
"noEmitOnError": false
```

```json
// only compiled paths in the list
"include": [ "src" ]
```

``` shell

```


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

<br>

### `.d.ts` file
can only store type, normally for package does not have type 
```ts
// types.d.ts

export type a = {
	b: number
	c:number
}

function multiplyNumbers(x: number, y: number): number
```

```ts
// other files
import { a } from './types'
```