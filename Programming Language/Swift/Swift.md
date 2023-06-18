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