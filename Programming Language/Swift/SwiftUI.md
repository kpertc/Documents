#UI #design 

Recommend|Resources
---|---
⭐⭐⭐⭐⭐|[Official](https://developer.apple.com/documentation/swiftui)
⭐⭐⭐⭐⭐|[Introduction to SwiftUI](https://developer.apple.com/videos/play/wwdc2020/10119/)
⭐⭐⭐⭐|[Design with SwiftUI](https://developer.apple.com/videos/play/wwdc2023/10115/)
⭐⭐⭐⭐⭐|[Swiftful Thinking](https://www.youtube.com/@SwiftfulThinking)

---

UIKit → 2008
Swift UI → 2019

Declarative Ul
- Identity
- Lifetime
- Dependencies

---

Views are lightweight
> extracting a subview has virtually no runtime overhead

Views are `struct`, only require `body`

```swift
// state changed -> View update
@state var zoomed = false 
@state private var zoomed = false
...
.aspectRatio(contentMode: zoomed ? .fill : .fit)
.onTapGesture { 
	withAnimation { // animation
		zoomed.toggled()
	}
}  
// onLongPressGesture
// onLongTouchGesture
```

![[date-flow-primitives.png]]

---

NVVM Architecture
- Model - data point
- View UI
- View Model - manages Model for View

---
### Shortcut
[[Xcode]]

<br>

Group Preview
![[group-preview.png]]

---

<br>

```swift
struct Sandwich: Identifiable { ... }
```

<br>

```swift
NavigationView {
	List() {
		VStack() {
			...
		}
	}
}
.navigationTitle("Title")


VStack()
HStack()
ZStack() // front back

List()
Picker() // UI?
```


```swift
// Text
Text()
	.font()

@State var TextVariable: String = ""
TextField("Textfield", text: $TextVariable)
Label("Spicy", systemImage: "flame.fill")

// Shapes
Circle()
Ellipse() // 椭圆
Capsule() // 胶囊
Rectangle()
RoundedRectangle(cornerRadius: 50)

// modifier
.padding()
.fill() // color
.stroke()
.trim()
.frame(width: 200, height: 100)
.cornerRadius(8)

// shadow
.shadow(radius: 10)
.shadow(color: Color.red, radius: 10, x: 0, y: 20)
.shadow(color: Color.red.opacity(0.3), radius: 10, x: 0, y: 20) // add opacity

// let UI could show on safe area
.edgesIgnoringSafeArea(.bottom)
```

<br>

### Color

```swift
UIColor // UI Kit
UIColor.systemcolor ?  

// Color Literal
var color = #colorLiteral() // then press enter
var color = Color("CustomColor") // set color in Assets.xcassets
```

![[colorliteral.gif]]
![[assets-color.png]]

##### Gradients
```swift
// Linear gradients
var LinearGradient = LinearGradient(
   gradient: Gradient(colors: [Color.red, Color.blue]), 
   startPoint: .leading,
   endPoint: .trailing
)

// add more color
var LinearGradient = LinearGradient(
   gradient: Gradient(colors: [Color.red, Color.blue, Color.orange, Color.purple]), 
   startPoint: .leading,
   endPoint: .trailing
)

// .top .bottom .topLeading .topTrailing

// Radial gradient
var RadialGradient = RadialGradient(
	colors: [Color.red, Color.blue], center: .center, 
	startRadius: 5, 
	endRadius: 400
)

// Angular gradient
var AngularGradient = AngularGradient(
	  colors: [Color.red, Color.blue], 
	  center: .center, 
	  angle: .degrees(180)
)
```

![[angular-gradient.png | 150]]

<br>

### Image
```swift
Image(systemName: "heart") // heart icon
Image(systemName: "heart.fill") // filled Color
	.resizeable() // -> resize to frame
	.aspectRatio(contentMode: .fit)

	// change font size to change icon size
	.font(.title)
	.font(.caption)
	.font(.system(size: 500)) // custom size

	.foregroundColor(Color.red)
	.background(Color.green)

	.frame(width: 300, height: 100) // require resizeable to match the frame
``` 

<br>

### Button
```swift
Button(
  "Button Title",
  action: {
	// some code
	print("log")
  }
)
```

<br>

### Animation

```swift
.transition(.move(edge: .bottom))
```

<br>

### If
```swift
if sandwich.isSpicy {
	 // UI ...
	 HStack {
		Spacer()
		Label("Spicy", systemImage: "flame.fill")
		Spacer()
	 }
}
```