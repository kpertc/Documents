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
/** tap vs button: 
	no state, no button animation
*/
```

![[date-flow-primitives.png]]

### @Binding
Parent ← connect @state ← Child 
```swift
struct MainView; View {
	@State var backgroundColor: Color = Color.green
	@State var title: String = "Title"

	var body: some View {
		ChildView(backgroundColor: $backgroundColor)
	}
}

struct ChildView: View {
	@Binding var backgroundColor: Color
	@Binding var title: String

	var body: some View {
		Button(action: {
			backgroundColor = Color.orange
			title = "New Title"
		}, label: {
			Text("Button")
		})		
	}
}
```

### Environment Variable
``` swift
// Environment Variable
@Environment(\.presentationMode) var presentationMode

```

### 
NVVM Architecture
- Model - data point
- View UI
- View Model - manages Model for View

---
### Shortcut
![[Xcode#SwiftUI]]

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

### 

``` swift
height: UIScreen.main.bounds.height * 0.5 // half of screens height
```

```swift
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

.offset(x: 10.0, y: 20.0) // move x 10 y 20

.rotationEffect(Angle(degrees: 30)) // rotation (30)

.fill() // color
.colorMultiply()

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

.zIndex(2.0) // order in ZStack
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

```swift
systemName: "xmark" // x
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

.disabled(true) // disable button

```

<br>

### Toggle
```swift
@State var _bool: Bool = false

Toggle("Label", isOn: $_bool)

Toggle(isOn: $_bool, label: {
	Text("Label")
})
.toggleStyle(SwitchToggleStyle(tint: .red))
```

<br>

### TextField & TextEditor
- TextField: one line
- TextEditor: multiple lines
```swift
@State var _text: String = ""

TextField("Type something here ... ", text: $_text)

TextField("Type something here ... ", text: $_text)
	.textFieldStyle(.roundedBorder)

// decorated
TextField("Type something here ... ", text: $_text)
	.padding()
	.background(Color.gray.opacity(0.3).cornerRadius(10))
	.foregroundColor(.green)
	.font(.headline)

// onEditingChanged
// onCommit
// formatter

TextEditor(text: $_text)
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

### ![[Swift#Condition]]

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

<br>

### Extract Code

Views are lightweight
> extracting a subview has virtually no runtime overhead

```swift
// Extract Code as function
Button(action: {
	buttonPressed()
}, label: {})

func buttonPressed() {
	...
}

// Extract View as variable
// no custom init → static
_view

var _view: some View {
	VStack {
		...
	}
}

// Extract View as Struct
// struct → custom init()
struct _view: View {
	var body: some View {
		VStack {
			...
		}
}
```

<br>

### Animation & Transition

##### Animation
```swift
// Animation Curve
.default
.linear
.easeIn
.easeInOut
.easeOut
.spring
// custom spring
.spring(response: 1.0, dampingFraction: 0.5, blendDuration: 1.0)
```

``` swift
Button("Button"){
	// on action
	withAnimation(.default) {
		// change some properties 
	}
	
	// modifiers
	withAnimation(Animation
		.default 
		// .default(duration: 3.0) // duration
		.delay(2.0) // delay 2 seconds
		.repeatCount(repeatCount: 5, autoreverses: true) // repeat animation 5 times
	) {
		// change some properties 
	}
}

// or on Shape
RoundedRectangle(cornerRadius: 30)
	.anmation(Animation
		.default
		.repeatForever(autoreverses: true)
	)
```

##### Transition
```swift
.transition(.slide) // enter & exit
.move(edge: .bottom) 

.transition(AnyTransition.opacity.animation(.easeInOut)) // opacity
.transition(AnyTransition.scale.animation(.easeInOut)) // scale

// custom in & out transition
.transition(.asymmetric(insertion: , removal: ))
```

<br>

### Sheet

![[sheet.gif | 200]]

![[SwiftUI#Environment Variable]]

```swift
.sheet(isPresented: $booleanVar, content: {
   // View
   Button("return", action: {
	   presentationMode.wrappedValue.dismiss()
   })
})

.fullScreenCover(isPresented: $booleanVar, content: {
	 
})
```

Only one sheet / fullScreencover per view, can not add multiple sheets on one view
Do not add conditional logic in sheet / fullScreencover

##### Ways to create display a new page
1. Sheet
2. Transition
	``` swift
	ZStack {
		if isShow {
			View()
				.padding(.top, 100) // for show top area
				.transition(.move(.bottom))
				.animation(.spring())
		}
	}
	.zIndex(2.0) // prevent disapper immediately
	```
3.  Animation Offset
	``` swift
	View(isShow: $bindingBool)
		.padding(.top, 100)
		.offset(y: bindingBool ? 0 : UIScreen.main.bounds.heights)
		.animation(.spring())
	```

<br>

### `NavigationView()` & `NavigationLink()`

NavigationView -> container include navigation title & bar

Do not nest a NavigationView inside a NavigationView

```swift
.navigationTitle("Navigation Title")
.navigationBarTitleDisplayMode(.automatic) // large | inline
.navigationBarHidden(true) // hide
```

`.automatic`|`.large`|`.inline`
---|---|---
![[navigationBarTitle-automatic.gif \| 200]]|![[navigationBarTitle-Large.png \| 200]]|![[navigationBarTitle-Inline.png \| 200]]

<br>