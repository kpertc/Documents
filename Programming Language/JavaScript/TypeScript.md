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
// 以下都写在 "compilerOptions" 里面
// source of ts script
"rootDir": "./src"

// out
"outDir": "./build/js"

// compile to target version
"target": "ES2022"

// compile even there are ts errors
"noEmitOnError": false
```

```json
// 顶层，和 "compilerOptions" 平级
// only compiled paths in the list
"include": [ "src" ]
```


Problem
https://blog.csdn.net/dujyong/article/details/106359483


---
Run TypeScript directly in node.js
`node test.ts` → Node 22.18+ / 23.6+ 原生 strip types，==不做类型检查==
`npx tsx test.ts`
`npx ts-node test.ts` → legacy

Run `npm link` if can not find typescript (on Windows)
![[node.js#`npm link`]]

---

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

`unknown` vs `any`
  
`any` → can use directly
`unknown` → have to cast type before using (safer any)

``` ts
var _var: any = 1;
_var++; // ok

var _unk: unknown = 1;
_unk++; // error
```

``` ts
var _var: unknown = 1;
// have unwrap type before use
if (typeof _var === 'number') _var++;
```



Object

```TypeScript
let variable: object;
variable = { name: "John", age: 30 };

let typedObj: { name: string, age: number, info: string };
typedObj = { name: "John", age: 30, info: "123456" };
```

### Type Aliases

```TypeScript
type StringOrNum = string | number;

let variable: StringOrNum;
```

### Type Assertion - Type casting

```ts
const canvas = document.getElementById("main_canvas") as HTMLCanvasElement;

// One is a type
let d = <One>'world';
// Bracket type can not be used in tsx file
```

`satisfies` (TS 4.9) → 按类型检查但不 widen；`as` 只是编译期断言（无运行时转换，还会掩盖真实错误）
```ts
const config = { host: 'a', port: 1 } satisfies Config; // 保留字面量类型
```


### `&` intersect type
``` ts
interface Person {
  name: string;
  age: number;
}

interface Employee {
  companyId: number;
  department: string;
}

type EmployeePerson = Person & Employee;

const employee: EmployeePerson = {
  name: "John Doe",
  age: 30,
  companyId: 12345,
  department: "Engineering"
};
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

Function overloading 函数重载
allows you to define ==multiple overload signatures== with the ==same name== but ==different parameters or argument types==, plus ==exactly one implementation==.

``` ts
function pad(v: string, n: number): string;
function pad(v: number, n: number): number;
function pad(v: any, n: number): any { /* single body */ }
```

implementation 的签名本身不能被外部调用


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
        readonly variable1: string,
        private variable2: number,
        public variable3: boolean
    ) {}
}
```

### Class
``` ts
class dog {
    public readonly name: string;
    readonly id: number;
    age: number;

    constructor(){}
}

class dog {
    constructor(
	    // can declare public / readonly in constructor
        public readonly name: string,
        readonly id: number,
        age: number
    ){}
}
```

##### Singleton
``` ts
// one way to create singleton
class DogManager {
    public _num: number = 1;
    static instance: DogManager = new DogManager();

    // make constructor private to prevent create instance
    private constructor() { };

    public add() {
        this._num++;
    }
}

const manager = DogManager.instance;
manager.add();

const fake_manager = DogManager.instance;
console.log(fake_manager._num); // 2 -> same instance as manager
```

### Enum

```TypeScript
enum ResourceType { Book, AUTHOR, FILM, DIRECTOR, PERSON }

const resourceType = ResourceType.Book;
```

Numeric enum internally use a int → 反向映射 `ResourceType[0] === 'Book'`（string enum 没有）
`const enum` 在 `isolatedModules`（Vite / esbuild / SWC）下不跨文件内联（`declare const enum` 直接报错）；`erasableSyntaxOnly` / node 原生 strip types 下，`enum` 和 constructor 参数属性都会报错

Namespace

```TypeScript
namespace name {
    ...
}
```

<br>
### Tuples
(TypeScript only，JS 没有 tuple 类型，只有 array)
a typed array with a pre-defined length and types for each index

```ts
type coord = [x: number, y: number, z:number];
```

```ts 
// state -> tuple
const [count, setCount] = useState(0);
```

<br>
### Interface
define the structure of an object to be complied

```ts
interface IsPerson {
	name: string;
	age: number;
	speak(a: string): void;
	spend(a: number): number;
}

// example object
const me: IsPerson = {
	name: 'shuan',
	age: 30,
	speak(text: string): void { console.log('...') },
	spend(amount: number): number { console.log('...'); return amount; }
	// excess property check: object literal 直接写多余属性会报错；先赋给变量再传则允许（结构化类型）
	// will raise alert if object is not matched with interface
};

let someone: IsPerson; // set interface when define the object

// use interface in
class myClass implements myInterface {
	...
} 

```

<br>
### Generics

```ts
function _func<T>(arg: T): T { // T -> any type
	return arg;
}

// declare generic types in < >, type name can be separated by , 
// <type1, type2>
```

work with interface

``` ts
interface Box<T> { value: T }

function unwrap<T>(b: Box<T>): T {
	return b.value;
}
```

##### keyof
key of the generic type
[No BS TS #8 - Generics with keyof in Typescript by Jack Herrington](https://youtu.be/4XTj6sIGTdc?si=jIOWJjZOVUpcCb0u)
``` ts
function pluck<DataType, KeyType extends keyof DataType>(
	item: DataType[],
	key: KeyType
): DataType[KeyType][] {
	return item.map(item => item[key]);
}

const dogs = [
	{ name: "Mimi", age: 12 },
	{ name: "LG", age: 13 }
]

console.log(pluck(dogs, "name")); // [ 'Mimi', 'LG' ]
```

 <br>

### Abstract Class

[# No BS TS #16 - Abstract Classes in Typescript](https://youtu.be/iFEOdoHp19U?si=mCZOypw2QO8kVkc8)

can not instantiate directly,  act as a template.
Other class inherit from the abstract class

``` ts
abstract class StreetFighter {
	constructor() { }
	move() { }
	fight() { }
	
	abstract getSpecialAttack(): string;
}

// const _fighter = new StreetFighter(); // can not instantiate directly

class Ryu extends StreetFighter { // StreetFighter Class act as a template  
	// abstract method need to be implemented
	getSpecialAttack(): string {
		return "Hello";
	}
}

const _fighter = new Ryu();
const msg = _fighter.getSpecialAttack();
console.log(msg); // "Hello"
```

<br>

### Utility Types

> [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)

``` ts
interface MyUser {
	name: string,
	id: string,
	email?: string;
}
```

##### Partial
> Constructs a type with all properties of `Type` set to ==optional==
``` ts
type MyUserOptionals = Partial<MyUser>;

/*
MyUserOptionals => {
	name?: string,
	id?: string,
	email?: string;
}
*/
```

##### Required
> RequiredConstructs a type consisting of all properties of `Type` set to ==required==. The opposite of ==Partial==.
``` ts
type RequiredMyUser = Required<MyUser>;

/*
RequiredMyUser => {
	name: string,
	id: string,
	email: string;
}
*/
```

##### Pick
> Constructs a type by picking the set of properties `Keys`.

create a type by selecting some properties from a type. 
``` ts
type JustEmailAndName = Pick<MyUser, "email" | "name">;

/*
JustEmailAndName => {
	name: string,
	email?: string;
}
*/
```

##### Omit
> Constructs a type by picking all properties from `Type` and then ==removing `Keys`==

``` ts
type removeEmail = Omit<MyUser, "email">;
/*
removeEmail => {
	name: string,
	id: string,
}
*/

type removeEmailandID = Omit<MyUser, "email" | "id">;
/*
removeEmailandID => {
	name: string,
}
*/
```

##### Record
从两个type创建一个新type的object

``` ts
type UserRoles = Record<"admin" | "guest", MyUser>;
/*
UserRoles => {
	admin: MyUser,
	guest: MyUser
}
*/
```

##### Indexed access types
``` ts
// use the type of MyUser.id -> more dynamic
const _obj : MyUser["id"] = "1111";
```

##### Readonly
``` ts
type ReadOnlyUser = Readonly<MyUser>;
/*
ReadOnlyUser => {
	readonly name: string;
	readonly id: string;
	readonly email?: string; // Readonly 不会去掉 optional
}
*/

// mapped type modifiers: -readonly / -? 去掉修饰符（Required 就是用 -? 实现）
```

``` ts
// set immutable array
const reallyConst = [1,2,3] as const;
// or
const reallyConst: readonly [number, number, number] = [1, 2, 3];

// try to modify
reallyConst[0] = 50; // error
```
<br>
### `.d.ts` file
只放类型声明（含 `declare const` / `declare function` / `declare module` 这类 ambient 声明），不产出 JS，normally for package does not have type 
```ts
// types.d.ts

export type a = {
	b: number
	c:number
}

export declare function multiplyNumbers(x: number, y: number): number;
```

```ts
// other files
import { a } from './types'
```
