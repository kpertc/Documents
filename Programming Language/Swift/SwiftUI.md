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
VStack(spacing: 12) 
LazyVStack() // optimiza create when need to LazyHStack

HStack()
ZStack() // front back

List()
Picker() // UI?
ScrollView(.horizontal)
```

<br>

### Enum
```swift
enum Fruit {
	case apple
	case orange
}

fruit: Fruit
fruit = .apple
fruit = .orange
```

<br>

```swift
let count: Int = 5 
Text("\(count)") // convert int to string

// Text
Text("Text".uppercased())
	.font()
	.underline()

// Shapes
Circle()
Ellipse() // 椭圆
Capsule() // 胶囊
Rectangle()
RoundedRectangle(cornerRadius: 50)

// modifier
.padding()
.padding(.horizontal, 20)

.fill() // color

.stroke()
.stroke(Color.gray, lineWidth: 3.0)

.trim()
.frame(width: 200, height: 100)
.cornerRadius(8)

.overlay()

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
Image set / Color set
![[managing-assets-with-asset-catalogs-1~dark@2x.png]]

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
Button("Press me!") {
	 // code
}

Button(
  "Button Title",
  action: {
	// some code
	print("log")
  }
)

Button(action: { // code
}, label: {
	// View Here
	Text("Save")
		.padding()
		.background(
			Color.blue
				.cornerRadius(10)
		)		   
})


```

<br>

### Animation

```swift
.transition(.move(edge: .bottom))
```

<br>

### ScrollView
```swift
ScrollView( 
// content 
) 

ScrollView(.vertical, showIndicators: false, content: { ... })
```

showsIndicators
![[showsIndicators.png | 100]]

<br>

### Grid
```swift
let columns: [GridItems] = [
	GridItem(.fix(50), spacing: nil, alignment: nil),
	// spacing -> horizontal or column spacing
]

// .fix .flexible .adaptive 
GridItem(.flexible(), spacing: nil, alignment: nil),
GridItem(.adaptive(minimum: 50, maximum: 300), spacing: nil, alignment: nil),

LazyVGrid(columns: columns
	spacing: 10 // row spacing or vertical
	pinnedViews: [.sectionHeaders]
) {
	Section: // .header .footer

	// create content
	ForEach(0..<50) {index in 
		Rectangle()
	}
}
```

<br>

### Custom init()
```swift
// normally swiftUI no need to create a init function

let backgroundColor: Color
let count: Int
let title: String

// custom init
init(backgroundColor: Color, count: Int, title: String) {
	self.backgroundColor = backgroundColor

	// ... custom here
}
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

<br>

### ForEach
```swift
ForEach(0..<10, { index in 
	print("\\(index)")
})
// 0, 1, 2, 3 ... 9

// ForEach create Text base on String[]
let data: [String] = ["Hi"]

ForEach(data.indices) { index in 
	Text("\\(data[index])")
}
```

<br>

### safearea

```swift
// .edgesIgnoringSafeArea -> deprecated
.ignoresSafeArea() = .edgesIgnoringSafeArea(.all)

// .edgesIgnoringSafeArea(.top) 
.ignoresSafeArea(edges: .top) //.bottom .all

// practics
// Create a separate view to ignore the safearea by ZStack
ZStack {
	//background
	Color.blue
		.edgesIgnoringSafeArea(.all)

	//foreground
	... content
}

// Set .background to ignore safearea while the main content is in the safeare
Rectangle()
	.background(
		Color.red
			.edgesIgnoringSafeArea(.all)
	)
```
