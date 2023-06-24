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

```swift
array.append(  )
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