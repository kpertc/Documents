#C＃  #programming-language 

[[Advanced C＃]]

### Data Type & Variables

==Value types== differ from ==reference types== in that variables of the value types directly contain their data, whereas variables of the reference types store _references_ to their data, the latter being known as _objects_.

![[valuetype-referencetype.png]]

![[type-inherit.png]]

All types in C# ultimately inherit from `System.Object` class.

Value Type is a type in C# that inherits from the "Value Type" base class

-   Value Type variable stores its value ==directly in memory==.
    
-   Reference Type stores a ==pointer== to its data, not data.
    
   ![[stack-heap.png]]
    


##### Stack

is a fixed length location in memory. Fixed length value types are stored one on top of the other on the stack while a sequence of instructions is executed for a thread. These values are processed on a LIFO (last in first out)


##### Heap

is a location in memory that is not constrained by a fixed length. Data is stored in a more haphazard way on the heap when compared to the orderly way that data is stored on the stack. As a result, memory management applied to the heap is more complex and therefore less efficient than memory management applied to the stack. The size of the object data stored on the heap is only constrained by the physical resources of the computer.
  
### Variables

Variables simply represent a storage location in memory where data is stored. The data stored for a particular variable can be changed.

  

String stores a read-only sequence of char objects

  

Main object-oriented principles: Encapsulation, Polymorphism, Inheritance, Abstraction

  

### Struct vs Class
struct -> value type
class -> reference type

`MyStruct myStruct;`

The new keyword is constructor, stuct can be instantiated with new keyword or without
Struct can implement interface

Instantiate class needs new keyword
`MyClass myclass = new MyClass();`


> [!NOTE] Class and Struct is different in C# than C++
> Struct → stack
> Class → heap

Default Values
![[Default Values.png]]