#programming-language

C++ can natively run on machine → fast
compare to C#, Java → run on virtual machine

Stroustrup加入了OOP特性和对C的泛型编程支持，C++ 是C语言的超集，这意味着任何有效的C程序都是有效的C++程序。

### Tutorial
<iframe width="560" height="315" src="https://www.youtube.com/embed/vLnPwxZdW4Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

[C++ series by The Cherno](https://youtu.be/SfGuIVzE_Os?si=A1NhihRyKfJTlnJW)

### Windows Installation

use Visual Studio

### Mac Installation

```
Mac installation:
To Check if has C++ installed 
gcc -v
```

Install Command Line Tool:[[Env Tools]]

```

![[img/build&run.png]]
Build | Run I Build&Run

### Hello World

```c++
cout -> Console out
endl -> End line
```

```c++
cout << "Hello World!" << endl;
```

### Compile
code to binary executable

##### **Configuration** (a set of rules)
- Release → Optimization for max-speed 
- Debug → Not optimization for max-speed, have extra code for debugging
- ...

##### **Target** (Platform → x86/x64/android)
- Application `.exe`
- Library `.dll`

##### `declaration`
	will not show error in editor but may not exist
	if can not find → linker error: `unresolved external symbol ...`

##### `definition`
	the actual content

##### 1. Compilation (compile)
1. pre-process
	Get evaluated before compile
	preprocess statement begin with `#` 
	`# define if ifdef`
	`#` include (header files)
		↳ header file does not compiled, literally copy the content of header file to the file where is `# include ...`

1. Generate Abstract Syntax Tree (AST) → Machine Code
	Optimization: redebug
		- constant folding → 5 * 2 will be optimized to 10
		- function signature
##### 2. Linking
Linker stitch object files to one .exe by finding symbol and function


##### compile error vs linking error
Compile error, C → compile
`error C2143: syntax errorL missing ‘;’ before ‘}’`

linking error
`fatel error LINK1561: entry point must be defined`


FAQ: at compiling stage: check declaration but not promise definition, if definition is not correct will resolve linking error

### Comment

```c++
//blablablabla

/*
    blablablabla
*/
```

### Variables

```c++
string name = "John";
char grade = 'A';
char a = 50; // if char is number, will be convert to character code

int age = 50;
short
long
long long

float gpa1 = 4.0f; // f lower case, double case doesnt matter
float _double = 4.0; // without ending with f -> is a double
// float 4 bits, double 8 bits

double gpa2 = 4.0;

bool isMale = true;
// 0 -> false; anything number, default 1 -> true

// int range +- 2 billion
// unsigned int range + 4 billion by not storaging the sign (+ -)
unsigned int = 4;

cout<<"My Name is "<<name<<"I am "<<age<<" years old."<<endl;

// memory can not address bits, only address bytes
```

##### size

1 byte = 8 bits
4 byte = 32 bits
1 int → 4 bits
empty Class → 1 byte

```c++
// check variable size
sizeof(_variable)

// can also check size of a object
class Entity {
public:
    int x, y;
};

Entity e;
sizeof(e) // 8
```
<br>

### pointer

pointer is int store memory address address of 1 byte(8 bits) memory

```cpp
void* ptr = 0; // 0 is not a valid address, will crash
void* ptr = NULL;
void* ptr = nullptr; // nullptr is introduced at C++ v11
```

```cpp
int _var = 8; // create a variable
void* ptr = &_var; // use &
// ptr  void *  0x16fdff1ec  0x000000016fdff1ec
```

type does not matter, `int`, `double`, `void` can represent pointer

access/read the pointer 
```c++
int* ptr = &var; 
*ptr = 10; // edit int pointer by int 
// *ptr -> 10 now
```

Edit Memory and check in memory view in Xcode
```cpp
char* buffer = new char[8]; // create a 8-bits memory
memset(buffer, 1, 8); // set value of the address of memory to 1
```
![[cpp_memory_xcode.png]]
##### Reference
```c++
bool* // pointer
bool& // reference

int x = 42;
int& ref = x;  // ref is a reference to x
```
##### Release memory
```cpp
delete ptr; 
delete[] buffer; // release array memory
```
##### Smart Pointer
Pointer wrap to provides automatic memory management. Like stack, deallocation when reach the scope.

1. unique pointer
	can not be shared
```cpp
#include <memory>
std::unique_ptr<Entity> _entity(new Entity());

// prefer way, safer
std::unique_ptr<Entity> _entity = std::make_unique<Entity>();

std::cout << _entity->x << std::endl;
```
2. shared pointer
```cpp

```


need to de-reference before using pointer as variable
```cpp
(*pointer)
```
##### Arrow operator (->)
```cpp
pointer →
pointer → Print()
```



### Header
```c++
#include “file.h”

#pragma once
// prevent declare multiple times, in different files

#ifndef // if not define
#define …

#include "../_header.h" relative path
"" for everything
#include <iostream> in directory

c library usually has extension .h
c++ library usually no extension
e.g. <iostream> has no extension
```

### String

```c++
"\n" //New Line

string phrase = "Giraffe Academy";

phrase.length() //15
phrase[0] //G , the first letter
phrase[0] = 'B'; //Change the first letter to B

phrase.find("Academy") //8, find at 8th
```

### Numbers

```c++
int num;
int num1, num2;
   
10 % 3;

num ++;
num --;

num += 80;
num -= 80;
num *= 80;
num /= 80;

10 / 3; //3
10.0 / 3.0 //3.3333
//integer operation will always get integer back

#include <cmath>
pow(2, 5); //32 
sqrt(36); //6
round(4.3); //4, standard round
ceil(4.1); //5, always round up
floor(4.6); //4, always round down
fmax(3, 10); //10, bigger one
fmin(3, 10); //3, smaller one
```



### Get User Input

```c++
double age;
cout << "Enter your age: ";
cin >> age;

cout << "You are "<< age << " years old";

//string line
string name;
cout << "Enter your name: ";
getline(cin, name);

cout << "Hello "<< name;
```

### Build a Calculator

```c++
int num1, num2;
   
cout << "Enter first number: ";
cin >> num1;

cout << "Enter second number: ";
cin >> num2;

cout << num1 + num2;
```

### Mad Libs Game

```c++
string color, pluralNoun, celebrity;

cout <<"enter a color: ";
getline(cin, color);
cout<<"enter a plural noun: ";
getline(cin, pluralNoun);
cout<<"enter a celebrity: ";
getline(cin, celebrity);

cout << "Rose are " << color << endl;
cout << pluralNoun << " are blue"<<endl;
cout <<"I love "<<celebrity<<endl;
```

### Arrays
raw array
raw array is faster than standard array
array → save the data continuously in memory
```c++
int luckyNums[20] // create 20 array
// first index is 0, last index is 19

int luckyNums[] = {4, 8, 15, 16, 23, 42};
int luckyNums[20] = {4, 8, 15, 16, 23, 42};
            //create 20 length array

cout << luckyNums[2]; //read
luckyNums[2] = 20; //set
```

```cpp
// create on stack
int example[5];
int* ptr = example; // array is pointer

// create on heap
int* another = new int[5];
```

have to maintain the size of length
not reliable
```cpp
int a[5]
int count = sizeof(a) / sizeof(int); // get size of array
// or
int count = sizeof(arr) / sizeof(arr[0]);
```

C++ 11 standard array
```cpp
#include <array>

std::array<int, 5> _newArray;
_newArray.size(); // standard array has size
```
### `int main()`
`int main()` → default entry point
	 entry point can be customized other than named `main()` in setting
- special case, don’t have to return a int
- no return will `return 0`

### Function
```c++
void // <= No return Type Function
//C ++ function need to be on Top

void sayHi(string name, int age); //Function stub/signature

void sayHi()
{
    cout<<"Hello User";
}

void sayHi(string name, int age)
{
    cout<<"Hello "<< name << " you are "<< age; 
}

//Main
sayHi();

sayHi("Mike", 60);
```

Debug must have a return, 
### Return

```c++
double cube(double num)
{  
    return  num * num * num;
}
//return will break/terminated function

//Main
double answer = cube(5.0); 
```

### If

```c++
bool isMale = false;

if(isMale)
{
    cout<<"You are a male";
}
else
{
    cout<<"You are not male";
}
```

```c++
bool isMale = true;
bool isTall = true

if(isMale && isTall) // and operator
{
    cout<<"You are a tall male";
}

if(isMale || isTall) // or operator
! //not, negate operator, reverse
```

```c++
bool isMale = true;
bool isTall = true;

if(isMale && isTall)
{
    cout<<"You are a tall male";
}

else if(isMale && !isTall)
{
    cout<<"You are a short male";
}
else if(!isMale && isTall)
{
    cout<<"You are tall but not male";
}
else
{
    cout<<"You are not male and not tall";
}
```

If (variable) // check variable is 0

### Switch

```c++
int dayNum = 0;
string dayName;

switch(dayNum)
{

case 0:
    dayName = "Sunday";
    break;

case 1:
    dayName = "Monday";
    break;

case 2:
    dayName = "Tuesday";
    break;
    
default:
    dayName = "Invalid Number";
}

cout << dayName;
```

### While Loop

While the condition is true, will loop

```c++
int index = 1;

while(index <= 5)
{
    cout<< index <<endl;
    index ++;
}

//do while loop

int index = 6;

do
{
    cout<< index << endl;
    index ++;
}
while(index <= 5);
```

### Guessing Game

### For Loop

```c++
  for (int i = 1; i <= 5; i++){
    cout << i << endl;
  }
```

### 2d Arrays & Nested Loops

```c++
// 2d Array
int numberGrid[3][2] = {
    {1, 2},
    {3, 4},
    {5, 6}
};

// get value
cout << numberGrid[0][0] << endl;
```

```c++
for (int i = 0; i < 3; i++){
    for (int j = 0; j < 2; j++){
      cout << numberGrid[i][j];
    }
    cout << endl;
}
```

### Pointer

A type of variable, memory address

```c++
int age = 19;
double gpa = 2.7;
string name = "Mike";

cout << &age; // Memory address


// storing pointer
int age = 19;
int *pAge = &age; //p+ Naming convention for pointer

double gpa = 2.7;
double *pGpa = &gpa;

string name = "Mike";
string *pName = &name;

cout << &pAge << endl;
cout << &pGpa << endl;
cout << &pName << endl;

cout << *pAge << endl; //de-referencing the pointer, get the value
```
<br>
### Classes & Objects

property default is private

```c++
class Book {
  public:
    string title;
    string author;
    int pages;
};


//Main
Book book1;
book1.title = "Harry Potter";
book1.author = "JK Rowling";
book1.pages = 500;

Book book2;
book2.title = "Lord of the Rings";
book2.author = "Tolkein";
book2.pages = 700;

cout << book1.pages << endl;
```

can have multiple sections `public` / `private`
```c++
class Log {
	public:
		...
	private:
		int logLevel;
	public:
		void SetLevel() {
			...
		}
		...
}
```

### Struct
class → private by default
struct → public by default

==struct in C# and C++ is different==
![[C＃ Fundamental#Struct vs Class]]

### Constructor

C++ need to be manually init (memory)
without manual init -> un-inited value is what memory left to
```c++
class Entity { 
	public: float X, Y; 
}; 

Entity e;

// X -> float -1.43127687E-34
// Y -> float -6.43330269E+20
```

Other languages, such as Java can automatically init and set the value to 0 / clear the memory

```c++
class Book {
  public:
    string title;
    string author;
    int pages;
 
    //Constructor  
    Book(string aTitle, string aAuthor){
    title = aTitle;
    author = aAuthor;
    }
    
    //can be multiple type of constructor  
    Book(string aTitle, string aAuthor, int aPages){
     
    title = aTitle;
    author = aAuthor;
    pages = aPages;
     
    cout << "Creating Object" << endl;
  }
};


//Main
Book book1("Harry Potter", "JK Rowling", 500);
cout << book1.title << endl;
```

```c++
```
No constructor:
Hide constructor ? -> private

```c++
class Entity { 
	Entity() = delete
}; 

Entity e;
```

### Struct
`struct` for backward compatibility
C does not have `class`, only have `struct`


### Destructor

will be called when the obj destroy, not call to destroy the obj
```c++
// destructor
~Entity() {
	// do something
}

// manually call destructor
e.~Entity();
```

```c++
void test () {
    Entity e;
    // object e will be destroy when get out the scope
}

int main(int argc, const char * argv[]) {
    test();
}
```

### Object Function

```c++
False -> 0
True -> 1 

class Student {
  public:
  string name;
  string major;
  double gpa;
  Student(string aName, string aMajor, double aGpa)
  {
    name = aName;
    major = aMajor;
    gpa = aGpa;
  }

  bool hasHonors()
  {
    if (gpa >= 3.5)
    {
      return true;
    }
    return false;
  }
};

// Main
Student student1("Jim", "Business", 2.4);
Student student2("Pam", "Art", 3.6);

cout << student1.hasHonors() << endl;
cout << student2.hasHonors() << endl;
```
<br>
### Virtual Function and Interfaces

##### Virtual Function
> In C++, a vtable (virtual table) and virtual functions are mechanisms used to implement polymorphism and dynamic dispatch in object-oriented programming. -GPT

Virtual Function have slightly additional memory (for vtable) and performance cost

Base `print()` is overrided by Derived ↓
`virtual` and `override` keyword, `override` is not mandatory, but is recomended
```cpp
class Base {
public:
    virtual void print() {
        cout << "Base class print() called" << endl;
    }
};

class Derived : public Base {
public:
    void print() override {
        cout << "Derived class print() called" << endl;
    }
};
```

##### Interfaces
C++ does not have a built-in Interface. However, C++ provides a way to achieve similar functionality through ==pure virtual functions==.

`virtual ... = 0` → Pure virtual function: no implement in the base class, need to implement in the sub-class. 
- Can not instantiate the class with pure virtual function, become "abstract class".
- Can not instantiate when sub-class not implement the function.

```cpp
class Interface {
public:
    virtual void doSomething() = 0;  // Pure virtual function
    virtual int calculate(int a, int b) = 0;  // Pure virtual function
    virtual ~Interface() {}  // Virtual destructor (for proper cleanup)

    // Non-virtual member function
    void commonFunction() {
        // Implementation shared by derived classes
    }
};

class ConcreteClass : public Interface {
public:
    void doSomething() override {
        // Implementation of doSomething in ConcreteClass
    }

    int calculate(int a, int b) override {
        // Implementation of calculate in ConcreteClass
        return a + b;
    }
};
```

<br>

### Getters & Setters

##### Private / Public

```c++
class Movie {
    private: // can not be accessed
    string rating;
    public: // can be accessed
    string title;
    string director;
     
    Movie(string aTitle, string aDirector, string aRating)
    {
      title = aTitle;
      director = aDirector;
      rating = aRating;
    }
    
    //setter
    void setRating(string aRating)
    {
        if (aRating == "G" || aRating == "PG" || aRating == "PG-13" )
        {
          rating = aRating;
        }
        else
        {
          rating = "NR";
        }
    }
     
     //getter
    string getRating ()
    {
        return rating;
    }
};

int main(int argc, const char * argv[]) {
    Movie avengers ("The Avengers", "Joss Whedon", "PG-13");
    
    cout << avengers.rating << endl; // can not be accessed
    
    avengers.setRating("PG-13"); //setter
    cout << avengers.getRating() << endl; //getter
}
```
<br>

### Stack and Heap

[How to CREATE/INSTANTIATE OBJECTS in C++ by Cherno](https://youtu.be/Ks97R1knQDY?si=M2c5TaE8pL4nAu4T)

##### Two way to create object in C++:

```cpp
// stack way to create object
// use this by default, fast way in C++
Entity entity;

// heap way to create object
new Entity(); // return a pointer
// need to manually free the object, and slower
Entity* entity = new Entity();
delete entity;
```

##### Stack & Heap

stack and the heap are two regions of memory, ultimately in RAM
- stack → automatic (faster)
- heap → dynamic (slower, memory allocation in slow)

main usage different between stack / heap is ==lifetime==
- stack → controlled by scope
```cpp
function () { ... } // function scope

if (...) { ... } // if scope

{ ... } // empty scope
```

- heap → will remain after created

Reason to use heap:
1. Control lifetime: cross the scope
2. Size: stack is small 1~2MB, when you have a large object, need to use heap

![[Miscellaneous#Memory Management in Objective C and C++]]



<br>
### Inheritance
inherit public variable and method
```c++
class Entity {
public:
    int x, y;
    
    Entity () {
        x = 10;
        y = 10;
    }
};

class Player : Entity {
public:
    void logout () {
        std::cout << x << std::endl;
    }
};

Player p;
p.logout(); // Player has attrubute x and logout -> 10

```

### `Static`

- inside the `class` / `struct`
	- Properties / method belong the class / struct
- outside the `class` / `struct`
    - only link in the translation unit (like private in class)

Use `extern` keyword for looking definition at external translation unit
`extern int ...`