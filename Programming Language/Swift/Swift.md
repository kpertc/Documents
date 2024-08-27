#programming-language 

[[SwiftUI]]

Practicing using Xcode playground

### Tutorial

https://www.youtube.com/watch?v=comQ1-x2a1Q

### Documentation


### Stack & Heap

https://github.com/SwiftfulThinking/Swift-Basics/blob/main/SwiftfulThinkingBasicsBootcamp.playground/Pages/ObjectOrientedProgramming.xcplaygroundpage/Contents.swift

https://youtu.be/-JLenSTKEcA

##### Objects in the Stack
Most basic types: 
- String
- Bool
- Int
- Struct
- Enum
- Array

Objects in the Stack are ==Value== types. 
When you edit a Value type, you create a copy of it with new data.
 
\+ Each threads has a Stack, Stack is faster, lower memory footprint, preferable

##### Objects in the Heap 
Functions, Class, Actors
Objects in the Heap are ==Reference== types.
When you edit a Reference type, you edit the object that you are referencing. This "reference" is called "pointer" because it "points" to an object in the Heap (in memory).

\- There is only 1 Heap for all threads, Heap is slower, higher memory footprint, risk of threading issues

Memory need to create a reference is almost the same as the object

##### ==Automatic Reference Counting (ARC)==
is **a memory management attribute used to monitor and manage an application's memory usage**

Not affect value type

`ARC` is used ()[https://stackoverflow.com/questions/24217586/structure-vs-class-in-swift-language]

- When you assign or pass `reference type` a **new reference** to original instance will be created(the address of instance is copied).

- When you **modify** an instance it has a **global** effect because the instance is shared and accessible by any reference that points on it.

- Usually The **Heap Memory** is used

https://medium.com/doyeona/automatic-reference-counting-in-swift-arc-weak-strong-unowned-925f802c1b99
**Automatic Reference Counting (ARC)** ==is to track and== ==_manage the app’s memory usage_====. ==ARC== ==**automatically frees up the memory**== used by class instances **when those instances are** ==**no longer needed.**==

**So how is it going to keep track of the instances?**

==Every instance of a class has a property called== ==**_reference count_**== so if reference count is ==greater than== ==**0, the instance is still kept in memory**== otherwise, **_it will be removed from the memory._**

Strong / weak reference
Is the class still there after async function？

<br>

### Hello World

```Swift
var greeting = "Hello, playground"
print(greeting)
```

  
### Variable vs Constant

`var` -> declare a variable
`let` -> declare a constant
	= `const` in JavaScript
  

### Data Types

String, Int, Float, Double, Bool

-   Float -> 32-bit floating point number
-   Double -> 64-bit floating point number

```Swift
var language: String = "swift" // specify the type "String"
print (language) // swift

print (type(of: language)) // print type var "language" -> String

Int() // Convert variable to Int 
round() //

// convert int to string
let count: Int = 5 
Text("\(count)")
```

<br>

### String

##### Multiline String

```swift
let lorem = """
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Integer nec odio.
Praesent libero.
Sed cursus ante dapibus diam.
Sed nisi.
Nulla quis sem at nibh elementum imperdiet.
Duis sagittis ipsum.
Praesent mauris.
"""
```

```swift
let multilineString = """
Start

End
"""
```

Use a backslash (\\) to omits the following line break.
```swift
let softWrapped = """
This is just \\
one wrong sentence.

This is another one\\
.
"""
```

<br>

### Tuple

```swift
// tuple can combine multiple pieces of data
func getUserInfo2() -> (String, Bool){
	let name = getUserName()
	let isPremium = getUserIsPremium()

	return (name, isPremium)
}

var userData1: String = userName
var userData2: (String, Bool, Bool) = (userName, userIsPremium, userIsNew)
var userData2: (name: String, isPremium: Bool) = ...

let name = getUserInfo2().0 // access tuple by index
```

<br>

### Array

```swift
// Generic 
let fruit: Array<String> = ["apple", "orange"]

array.count
array.indices // range 0,1,2,3
array.indices.first // 0
array.indices.last // last index

array.first
array.last

array.append("apple") // append an item
array.append(contentsOf: ["apple", "Mango"]) // append a list

array.insert("Watermelon", at: 2) // insert item to at index 2
array.insert(contentsOf: ["Watermelon", "Tangerine"], at: 2) // insert a list

array.remove(at: 3) // remove item
array.removeAll()
array.append(  )
array.append(contentsOf: [ ... items ])
```

##### Set
```swift
// Set can not have the same item
// Set does not have order
var fruitsSet: Set<String> = ["apple", "orange"]
```


##### Sorted
``` swift
// sort
let sortedArray = dataArray.sorted { (user1, user2) -> Bool in 
	return user1.points > user2.points
} 
// sortedArray user with greater points have lower index of array 
// short version
let sortedArray = dataArray.sorted(by: { $0.points > $1.points })
```

##### Filter

```swift
let filteredArray = dataArray.filter({ (user) -> Bool in 
	return user.points > 50 // only points > 50
	return user.name.contains("i")
})

// short version
filteredArray = dataArray.filter({ $0.isVerified })
```

##### Map

```swift
// convert to other type, for example, convert to String
mappedArray = dataArray.map({ (user) -> String in
	return user.name
	return user.name ?? "default name" // user.name optional
})

// short version
mappedArray = dataArray.map({ $0.name })

/* 
for optional property use compactMap,
if the item does not have the property it will not be included into the array
*/
mappedArray = dataArray.compactMap({ (user) -> String? in
	return user.name
})

// short version
mappedArray = dataArray.compactMap({ $0.name })
```

##### mix use

```swift
mappedArray = dataArray
	.sorted(by: { $0.points > $1.points })
	.filter({$0.isVerified})
	.compactMap({$0.name})
```

<br>

### Enum
```swift
enum Fruit {
	case apple
	case orange
}

enum Fruit {
	case apple, orange, ...

	var title: String = {
		self // enum value 
		return
	}
}

fruit: Fruit
fruit = .apple
fruit = .orange
```

```swift
// use name instead of index
func getUserInfo2() -> (name: String, isPremium: Bool){
	...
}

let name = getUserInfo2().name
```

Recommend to create custom type → struct / class if too long
can not mutate later

<br>


###  for & ForEach Loops

```swift
while (condition) {
	...
}

repeat {
		
} while
```

```swift
// for can not use in view? 
for item in 0...<10 {
  ...
}

for item in _array {
	... 
}

for (index, item) in array.enumerated() {
	...
}
```

```swift
break // exit loop

continue // next loop
```

```swift
ForEach(0..<10, { index in 
	print("\\(index)")
})
// 0, 1, 2, 3 ... 9

// ForEach create Text base on String[]
let data: [String] = ["Hi"]

// index
ForEach(data.indices) { index in 
	Text("\\(data[index])")
}


ForEach(data, id: \.self) { item in 
	... item
}
```

<br>

### Struct

Value types are copied & mutated
Create a new

```swift
let user // can not change
var user 
```

```swift
struct User {
	let displayName: String
	let userName: String
	let followerCount: Int
}

User(displayName: "Nick", userName: "nick123", followerCount: 300)
// Structs have an implicit init -> no need to write init() manually
```

change struct value = recreate & reassign object

"Immutable struct" = all "let" constants = NOT mutable = "cannot mutate it!"
```swift
struct UserModel {
    let name: String
    let isPremium: Bool
}

var user1: UserModel = UserModel(name: "Nick", isPremium: false)
user1 = UserModel(name: user1.name, isPremium: true)

```

"mutable struct"
```swift
struct UserModel2 {
    let name: String
    var isPremium: Bool
}

var user2 = UserModel2(name: "Nick", isPremium: false)
user2.isPremium = true
```

```swift
struct UserModel4 {
    let name: String
    private(set) var isPremium: Bool
    // private(set) can only set from inside
    // can not e.g. user.isPremium = true
    
    mutating func markUserAsPremium() {
        isPremium = true
    }
    
    mutating func updateIsPremium(newValue: Bool) {
        isPremium = newValue
    }
}

var user4 = UserModel4(name: "Nick", isPremium: false)
user4.markUserAsPremium()
user4.updateIsPremium(newValue: true)
```

struct do not have `deinit()`

```swift
struct User : Identifiable {
	let id: String = UUID().uuidString // make identifiable
	let displayName: String
	let userName: String
	let followerCount: Int
}
```
<br>

### Class

```swift
init()
```

##### `deinit`
```swift
deinit { 
	...
}
```

```swift
let user = User()
User.name = "new name"
/**
	class can be changed even on let, because class is reference, 
	object itself is not changing
	data inside object is changing
*/
```


### Access Control
```swift
public

private

private(set) // read is public, set is private
```


### ![[SwiftUI#Enum]]

### Condition

```swift
@State var isShow: Bool = false
isShow.toggle() // isShow = !isShow
print(isShow.description) // true or false
```

```Swift
var a = 5

if a == 5 {
    print ("1")
}
else if a == 6 {
    print ("2")
}
else {

}

&&  // and
||  // or
```

Ternary Operator
```swift
@var isState: Bool = false
...
Rectangle()
	// .fill(condition ? true : false)
	.fill(isState ? Color.red : Color. blue)
```

<br>

### ![[SwiftUI#ForEach]]

<br>

### Function
```swift
func _funcname() -> Bool {
	
}

// calculated variable
func calculatedNumber: Int {
	return number1 + number2
}
```

##### internal & external name
```swift
func doSomething (externalName InternalName: String) {
	print(InternalName)
}

doSomething(externalName: "Hello")
```

<br>

### @escaping - Async function return

```swift
@Published var text: String = ""

// sync
func downloadData(completionHandler: (_ data: String) -> Void) {
	completionHandler("New Data") // return String: "NewData"
}

downloadData{ (returnData) in 
	print(returnData)
}
```

``` swift
// async
func downloadDataAsync(completionHandler: @escaping (_ data: String) -> ()) {
	// some async logic
	DispatchQueue.main.asyncAfter(deadline: .now() + 2.0) {
		completionhandler("New Data")
	}
}

downloadDataAsync{ (returnData) in 
	self.text = returnedData // strong reference
}
```

``` swift
downloadDataAsync{ [weak self] (returnData) in 
	self?.text = returnedData // weak reference, ok to de-initialize
}
```

<br>

### `if-let` and `guard`

```swift
@State var text:String? = nil // optional

// if text has a value, then create displayText, then use displayText
if let displayText = text {
	Text(displayText)
}
else { ... }
```

```swift
guard let displayText = text else {
	...
	return
}

// if true, will execute the remain ↓
Text(displayText)
```

```swift
text! // force to wrap value
```


```swift
@State var value: String? 
Text(value!) // may crash 
Text(value ?? "default Value" ) // default value
```

Swift does execute the body of the IF only if all the optional bindings are properly completed.

```swift
if let a = optA, let b = optB, let c = optC {
    
}

// or

if 
	let a = optA, 
	let b = optB, 
	let c = optC {
    
}
```

### do { … } catch { … } throw

```swift
func getTitle() -> (title: String?, error: Error?) {
	if isActive {
		return ("New Text!", nil)
	} else {
		return (nil, URLError(.badURL))
	}
}

let returnedValue = manager.getTitle()
if let newTitle = returnedValue.title {
	self.text = newTitle
} else if let error = returnedValue.error {
	self.text = error.localizedDescription
}
```

##### Use `Result`

```swift
func getTitle2() -> Result<String, Error> {
	if isActive {
		return .success("Text")
	} else {
		return .failure(URLError(.badURL))	
	}
}

let result = manager.getTitle2()
switch result {
	case .success(let newTitle):
		self.text = newTitle
	case .failure (let error)
		self.text = error.localizedDescription
}
```

##### throw

```swift
func getTitle3() throws -> String { // require try
	if isActive {
		return "Text"
	} else {
		throw URLError(.badURL)
	}
}

do { // put can throw error in do
	let newTitle = try manager.getTitle3() // if failed, immediately to error
	let newTitle = try manager.getTitle3() 
	... // can put multiple
} catch { // or let customeErrorName
	print(error.localizedDescription)
}
```

##### Optional `try`?

optional → value or `nil`

if failed, `text = nil`, and no error back
program can continue to run
no need to place in `do {} catch {}`

```swift
let text = try? ...
```

<br>

### Protocol

Protocol → set of requirements

```swift
// object must have name:String to conform
struct EmployeeModel: EmployeeHasAName {
	let title:String
	let name: String
}

protocol EmployeeHasAName {
	?? let name: String
}
```

only var in protocol, no `let`
will get error if not conform to the protocol
After comfort to a protocol, only protocol part can be used

```swift
protocol ColorThemeProtocol {
	var primary: Color { get } // read only
	var secondary: Color { get }
	var tertiary: Color { get }

	func someFunc () { }
}

// a struct conform to ColorThemeProtocol
struct ColorTheme: ColorThemeProtocol {
	let primary: Color = .red
	let secondary: Color = .white
	let tertiary: Color = .green
}

// initial a ColorTheme conform ColorThemeProtocol
let colorTheme: ColorThemeProtocol = ColorTheme()
```

##### Combine Protocol
```swift
protocol ButtonTextProtocol { // text only
	var buttonText: String { get }
}

protocol ButtonPressedProtocol { // func only
	func buttonPressed()
}

// text & func
class CombinedClass: ButtonTextProtocol, ButtonPressedProtocol {
	var buttonText: String = "Protocol are awesome!"

	func buttonPressed () {
		print ("Button Pressed")
	}
}

// or create a combined protocol
protocol CombinedProtocol: ButtonTextProtocol, ButtonPressedProtocol {
	// can leave blank
}

class CombinedClass: CombinedProtocol { ... } 
```

```swift
protocol DataServiceProtocol {
	func getData() -> AnyPublisher<[PostsModel], Error>
}
```
<br>

### File

![[xcassets.png]]

``` swift
Image("steve-jobs")
```

##### FileManager

```swift
// image.jpegData(compressionQuality: 1.0)

let directory = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)
let directory = FileManager.default.urls(for: .cachesDirectory, in: .userDomainMask)
let directory = FileManager.default.temporaryDirectory

let path = directory?.appendingPathComponent("\\(name).jpg").first //array.first → [0] 

// save data
data.write(to: path)

// check exists
FileManager.default.fileExists(atPath: path), 
	
// remove file or path
FileManager.default.removeItem(at: )

// create path (Folder)
FileManager.default.createDirectory(atPath: path, withIntermediateDirectories: true, attributes: nil)

```
<br>

### Documentation

![[Mark.png]]
``` swift
// MARK: PROPERTIES

/// Summary

/// Gets an alert with a specified title.
/// This function creates and returns an alert immediately. The alert will have a title based on the text parameter but it will NOT have a message.
/// ```
///getAlert(text: "Hi") -> Alert(title: Text("Hi")
/// ```
/// - Warning: There is no additional message in this Alert.
/// - Parameter text: This is the title for the alert.
/// - Returns: Returns an alert with a title.
func getAlert(text: String) -> Alert {
	return Alert(title: Text(text))
}
```

add documentation
⌘ + click variable
![[add-documentation.gif]]


Code Folding
⌥ ⌘ ←
![[code-folding.gif]]