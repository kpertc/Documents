#C＃ #programming-language #Unity 

### Tutorial
[菜鸟教程（功能：字典）](https://www.cainiaojc.com/csharp/csharp-string.html)

[Untiy官方中级编程](https://learn.unity.com/project/zhong-ji-bian-cheng)

### C# Coding Conventions

https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions

[Capitalization Conventions](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/capitalization-conventions)

Related C# Docs
[[C＃ Fundamental]]
[[Advanced C＃]]


Common Language Runtime (CLR)
> .NET provides a run-time environment called the common language runtime that runs the code and provides services that make the development process easier.
> https://learn.microsoft.com/en-us/dotnet/standard/clr

### Hello World

```c#
Console.WriteLine("Hello World!");

Console.ReadLine();
```

### Comments

``` csharp
// Comments

/*
Comments
Comments
Comments
*/
```

``` csharp
string myString; //no info
string myString = "Hello";

char grade = 'A'; //single quotation mark

int age = 30;

float gpa = 3.0f;
double gpa = 3.0;
decimal

bool isMale = true;

//Convert
double num = Convert.ToDouble(Console.ReadLine());
```

### String

``` csharp
"\n" "One line\nNew line!" //New Line
"\"" //print quotation mark

@"c:\Program Files\Microsoft Visual Studio 9.0"  //a verbatim string literal

string phrase = "Giraffe Academy";
Console.WriteLine(phrase.Length); //get length of the string

Console.WriteLine(phrase.ToUpper()); //ALl Upper Case
Console.WriteLine(phrase.ToLower()); //ALl Lower Case

Console.WriteLine(phrase.Contains("Academy")); //Return Bool if contain

Console.WriteLine(phrase[0]); // Return G, Access the letter of the index number
Console.WriteLine(phrase[1]); // Return i

Console.WriteLine(phrase.IndexOf("Academy")); //8, Check if the string exist and also return the index
Console.WriteLine(phrase.IndexOf("z")); //-1, not exist

Console.WriteLine(phrase.Substring(8, 3)); //Aca return from 8th character & next 3
```

https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/tokens/interpolated

### Numbers

``` csharp
5 % 2 //return 1, 5 mod 2, get remainder

5 / 2 //return 2, int divided by int get int
5 / 2.0 //return 2.5, int divided by decimal number get decimal number

num++ //num + 1
num-- //num - 1

Math.Abs(-30) //return 30, Absolute Value
Math.Pow(3, 2) //return 9, 3^2
Math.Sqrt(36) //return 6, squareroot

Math.Max(3, 20) //return 20, return the bigger one
Math.Min(3, 20) //return 3, return the smaller one

Math.Round(3.14) //return 3, round
Math.Round(3.5) //return 4
```

### Constants

``` csharp
//constant can not be changed, can not contain variable

const int pi = 3.14;
const double = 65 / 2;
const string format = ".mp4";
```

### [Nullable Value](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/nullable-value-types) -> T?

``` csharp
Bool? _bool;

print(_bool.HasValue); // false
```

### Getting User's Input

``` csharp
Console.Write("Enter your name: "); //Write -> single line, WriteLine -> New line
string name = Console.ReadLine(); //Store the variable
Console.WriteLine("Hello " + name);

Console.ReadLine(); //Pause the program
```

### Basic Calculator

``` csharp
Console.Write("Enter a number: ");
double num1 = Convert.ToDouble(Console.ReadLine());
Console.Write("Enter another number: ");
double num2 = Convert.ToDouble(Console.ReadLine());

Console.WriteLine(num1 + num2);

Console.ReadLine();
```

### Mad Libs Game

``` csharp
string color, pluralNoun, celebrity;

Console.Write("Enter a color: ");
color = Console.ReadLine();

Console.Write("Enter a plural noun: ");
pluralNoun = Console.ReadLine();

Console.Write("Enter a celebrity: ");
celebrity = Console.ReadLine();

Console.WriteLine("Roses are " + color);
Console.WriteLine(pluralNoun + " are blue");
Console.WriteLine("I Love " + celebrity);

Console.ReadLine();
```

### Arrays

``` csharp
int [] LuckyNumbers = { 4, 8, 15, 16, 23, 42};

luckyNumbers[2] //return 15, Access info
luckyNumbers[2] = 100; //modify thrid value to 100

string[] friends = new string[3]; //create a new array need to specify the length
friends[1] = "JIm";
```

### Enums

``` csharp
enum Breed { bulldog, Boxer, Chihuahua, Briard };

Breed.Chihuahua;
```

![[img/Unity/enum.png | 300]]

``` csharp
public enum Month : 1
{
    Jan = 1,
    Feb = 2,
    Mar = 4,
    Apr = 8
}
```

### Method (Function)

``` csharp
SayHi();

static void SayHi()
{
    Console.WriteLine("Hello");
}

static void sayHi() => Console.WriteLine("Hello World!");

in // not modifable
out // create new variable
ref // use existing variable and make change
```

``` csharp
SayHi("Mike");

static void SayHi(string name)
{
    Console.WriteLine("Hello " + name);
}
```

### Lambda

``` csharp
testDelegateFunction = () => {Debug.Log("Lambas Expression")};
                 // take no input
```

### Func<T/>

``` csharp
// can declare within a method 
Func<string> funcName = () => { return "Hello World"; };
// or written short
Func<string> funcName = () => "Hello World";

print(funcName());
```

### Return Statement

``` csharp
cube(5) //return 125

static int cube (int num)
{
    int result = num * num * num;
    return result;
}
```

### Modifiers

``` csharp
Access modifier
internal // accessible only within files in the same assembly
protected // accessible within its class and by derived class instances
private // accessible only within the body of the class or the struct 

Modifier
abstract

virtual 
override

const // not change
readonly // changeable by setter

sealed // the sealed modifier prevents other classes from inheriting from it 
```

### If Statements

``` csharp
&& // and
|| // or

! //Not
```

``` csharp
if ()
{

}

else if ()
{

}

else
{

}
```

https://learn.unity.com/tutorial/san-yuan-yun-suan-fu#5e3b299cedbc2a2fad38a4ee

### Switch Statements

Switch statement can be achieved by "IF" statement, switch statement is much simpler to use

``` csharp
getDay(0);

static string getDay(int dayNum)
{
    string dayName;

    switch (dayNum)
    {
        case 0:
            dayName = "Sunday";
            break; //if dont break, will keep check

        case 1:
            dayName = "Monday";
            break;

        case 2:
            dayName = "Tuesday";
            break;

        default: //if none of case met, get default
            dayName = "Invalid Day Number";
            break;
    }
    return dayName;
}
```

### While Loop

``` csharp
int index = 1;

while (index <= 5)
{
    Console.WriteLine(index);
    index++;
}

Console.ReadLine();

//
for ( int i = 0; i < numEnemies; i++)
{

}

//do while loop, execute the once before loop
do
{
    Console.WriteLine(index);
    index ++;
} while (index <= 5);
```

### Guessing Gam

``` csharp
static void Main(string[] args)
{
    string secretWord = "giraffe";
    string guess = "";
    int guessCount = 0;
    int guessLimit = 3;
    bool outOfGuesses = false;

    while(guess != secretWord && !outOfGuesses)
    {
        if (guessCount < guessLimit)
        {
            Console.Write("Enter guess； ");
            guess = Console.ReadLine();
            guessCount++;
        }
        else
        {
            outOfGuesses = true;
        }
    }

    if (outOfGuesses)
    {
        Console.Write("You Lose!");
    }
    else
    {
        Console.Write("You Win!");
    }

    Console.ReadLine();
}
```

### For Loop

``` csharp
//declare value i;
//create a condition;
//increment;

for (int i = 1; i <= 5; i++)
{
    Console.WriteLine(i);
}

//Access Array
int[] luckyNumbers = { 4, 8, 15, 16, 23, 42 };

for (int i = 0; i < luckyNumbers.Length; i++)
{
    Console.WriteLine(luckyNumbers[i]);
}

foreach ( in ) // use IEnumerator backend, before Unity 5.5 cause Garbage Collection Problem has been solved
```

### Exponent Function

``` csharp
Console.WriteLine(GetPow(2, 3));

static int GetPow(int baseNum, int powNum)
{
    int result = 1;
    
    for(int i = 0; i < powNum; i++)
    {
        result = result * baseNum;
    }
    
    return result;
}
```

### 2D Array

``` csharp
int[,] numberGrid = {
    {1, 2},
    {3, 4},
    {5, 6}
}

int[,,,] numberGrid = 

int[,] myArray = new int [2,3];

Console.WriteLine(numberGrid[0,0]); //1
Console.WriteLine(numberGrid[1,1]); //4
```

### Exception Handling

``` csharp
try
{

}

catch
{

} 

//get more information
catch(exception e)
{
    Console.WriteLine(e.Message);
} 

//catch one type of error
catch(DivideByZeroException e)
{
    Console.WriteLine(e.Message);
}

catch(FormatException e)
{
    Console.WriteLine(e.Message);
}

//will exectue no matter what
finally 
{

}
```

### Classes & Objects

Class -> create new data type

``` csharp
class Book
{
    public string title;
    public string author;
    public int pages;
}

//Main
Book Book1 = new Book();

Book1.title = "Harry Potter";
Book1.author = "JK Rowling";
Book1.pages = 400;
```

### Struct (Data structure)

``` csharp
struct Car
{
    public string brand;
    public int year;
    public float price;
}

Car car1;
car1.brand = "Toyota";
```

### Constructors

``` csharp
class Book
{
    public string title;
    public string author;
    public int pages;
    
    //Constructor
    public Book(string aTitle, string aAuthor, int aPages) //public + class name
    {
        title = aTitle;
        author = aAuthor;
        pages = aPages;
    }
    
    //can have multiple contructors
    public Book() //this one with no parameters
    {

    }
}

//Main
Book Book1 = new Book("Harry Potter", "JK Rowling", 400);
Book Book2 = new Book();
```

### Deconstructor

``` csharp
~
```

### this

``` csharp
//static does not have this.

public class Employee
{
    private string alias;
    private string name;

    public Employee(string name, string alias)
    {
        // Use this to qualify the members of the class
        // instead of the constructor parameters.
        this.name = name;
        this.alias = alias;
    }
}
```

### Object Methods

``` csharp
class Student
{
    public string name;
    public string major;
    public double gpa;

    public Student(string aName, string aMajor, double aGpa) //Constructor,  public + class name
    {
        name = aName;
        major = aMajor;
        gpa = aGpa;
    }

    public bool HasHonors()
    {
        if (gpa >= 3.5)
        {
            return true;
        }
        return false;
    }    
}
```

``` csharp
//Main
Student student1 = new Student("Jim", "Business", 2.8);

Console.WriteLine(student1.HasHonors());
```

### Getters & Setters

``` csharp
public var myVariable; //can be accessed by outside
private var myVariable; //can not be accessed by outside

public string Rating
{
    get { return rating; }
    set {
        if (value == "G" || value == "PG" || value == "PG-13")
        {
            rating = value;
        }
        else
        {
            rating == "NR";
        }
    }
}
```

### Static Attributes

### Static Class

### [Partial Class](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)

### NameSpace

`::` only works for namespaces (and namespace aliases)

`.` works for both namespaces and subclasses.

``` csharp
namespace xxxx {

}

using o = System;
o.
```


<br>

# Quick Tips

### `#region`

``` csharp
#region regionName

#endregion
```

### TernaryOperator

``` csharp
message = health > 0 ? "Player is Alive" : "Player is Dead";
```