#programming-language 

[[SwiftUI]]

Practicing using Xcode playground

### Tutorial

https://www.youtube.com/watch?v=comQ1-x2a1Q

### Documentation


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

### Array

```swift
array.append(  )
array.append(contentsOf: [ ... items ])

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

### Struct

```swift
struct User {
	let displayName: String
	let userName: String
	let followerCount: Int
}

struct User : Identifiable {
	let id: String = UUID().uuidString // make identifiable
	let displayName: String
	let userName: String
	let followerCount: Int
}

User(displayName: "Nick", userName: "nick123", followerCount: 300)
```

<br>

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
if failed, `text = nil`, and no error back
program can continue to run
no need to place in `do {} catch {}`

```swift
let text = try? ...
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
	
// remove	
FileManager.default.removeItem(at: )
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