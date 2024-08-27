#programming-language 

[Basic Design Patterns in C++ by Larry | Peng Yang](https://medium.com/must-know-computer-science/basic-design-patterns-in-c-39bd3d477a5c)
[Design Patterns](https://www.oodesign.com/)

[[SOLID Principles]]
[[System Design]]

<br>

Terms | | 
:--|:--|:--
Data Concurrency|并发|The ability to allow multiple parts of your application to affect multiple transactions within a single database
Refactoring|重构|
Spaghetti Code||Code that lacks the structure that's required to be maintained and scaled effectively

<br>
### Architectural Patterns

##### Entity-Component-System (ECS)

<br>

### Design Patterns

##### Repository
-   Unit of Work
      Unit of work is referred to as a single transaction that involves multiple operations of insert / update / delete and so on.

<br>

##### Singleton
A design pattern that describes a class that is both globally accessible and can only be instantiated once.

<br>

##### Dependency Injection
An implementation of the inversion of control design principle

<br>

##### Observer Pattern
[Maintains a list of its dependents, called observers, and notifies them automatically of any state changes, usually by calling one of their methods.](https://en.wikipedia.org/wiki/Observer_pattern)

<br>

##### Humble Object (For Unit Test)
[We extract the logic into a separate easy-to-test component that is decoupled from its environment.](http://xunitpatterns.com/Humble%20Object.html) (Isolated from MonoBehavour)