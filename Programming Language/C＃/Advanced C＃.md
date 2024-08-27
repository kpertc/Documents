#C＃ 

> [!tip]
>-   Better code reuse, cleaner code,
>-   Extensibility
>-   Flexibility of design
>-   Easier maintenance of code
>-   Separation of concerns
>-   Enablement of effective unit testing
>-   And the provision for overall better performance and efficiency of our applications

<br>

### Delegate

A delegates is a type safe function pointer, reference type variable, reference to a method.
Action is a delegate type; doesn't return a value
System Action Func
Make sure the delegate isn't null

``` csharp
public delegate void _voidDelegate(); //declare the type -> void

_voidDelegate myfunction; //declare

void Start()
{
    //ways to assign delegate:
    myfunction = beginFunction; 
}

void beginFunction ()
{
    Debug.Log("Begain");
}
```

<br>

### Generics

``` csharp
using System.Collections.Generic;

Dictionary<string, int>
```

Non-Generic **ArrayList**|**Generic List<T/>**
:--|:--
Boxing operation, runtime cost, can add any type of item<br>Microsoft does not recommend using ArrayList or future development|Reusability, type safety, efficiency, only add specified type

> [!example]
IEnumerable vs IEnumerator
IEnumerable : foreach
IEnumerator: Move next ()
IEnumerable use IEnumerator Internally

<br>

### Interface

Naming Convention - beginning with “I”
Inherent only 1, multiple interface

``` csharp
public interface ITaxCalculator
{
    int Calculator(); //do not have access modifier
}

public interface IMyInterface, IMyInterfaceII
{
   
}

public class interfaceTest : MonoBehaviour, IMyInterfaceII
{

}
```

<br>

### Language Integrated Query, LinQ

``` csharp
item i1 = new item("i1", true, 10f);
item i2 = new item("i2", false, 20f);
item i3 = new item("i3", true, 30f);

public static List<item> _list = new List<item>();

_list.Add(i1);
_list.Add(i2);
_list.Add(i3);

var result = _list.Where(t => t.isTrue == true);
// get is item is true i1, i3
```

<br>

### Asynchronous Programming

-   Task-based Asynchronous Pattern (TAP)
-   Legacy - Event-based Asynchronous Pattern (EAP)
-   Legacy - Asynchronous Programming Model (APM)

  

**Two Kinds of Blocking Operations**

-   CPU-bound Operations - Heavy calculation, gaming financial
-   I/O-bound Operations - Internet Data, Copy Paste File