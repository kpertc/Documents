#programming-language

> Stroustrup加入了OOP特性和对C的泛型编程支持，C++ 是C语言的超集，这意味着任何有效的C程序都是有效的C++程序。

### Tutorial
<iframe width="560" height="315" src="https://www.youtube.com/embed/vLnPwxZdW4Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### Windows Installation

### Mac Installation

```
Mac installation:
To Check if has C++ installed 
gcc -v
```

Install Command Line Tool:[[Xcode Command Line Tools]]


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

### Variables

```c++
string name = "John";
char grade = 'A';

int age = 50;

float gpa1 = 4.0;
double gpa2 = 4.0;
bool isMale = true;

cout<<"My Name is "<<name<<"I am "<<age<<" years old."<<endl;
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

```c++
int luckyNums[] = {4, 8, 15, 16, 23, 42};
int luckyNums[20] = {4, 8, 15, 16, 23, 42};
            //create 20 length array
int luckyNums[20]

cout << luckyNums[2]; //read
luckyNums[2] = 20; //set
```

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

### Classes & Objects

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

### Constructor Function

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

### Inheritance

### Comment

```c++
//blablablabla

/*
    blablablabla
*/
```