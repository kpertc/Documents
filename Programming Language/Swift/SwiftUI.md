#UI #design 

Recommend|Resources
---|---
⭐⭐⭐⭐⭐|[Official](https://developer.apple.com/documentation/swiftui)
⭐⭐⭐⭐⭐|[Introduction to SwiftUI](https://developer.apple.com/videos/play/wwdc2020/10119/)
⭐⭐⭐⭐|[Design with SwiftUI](https://developer.apple.com/videos/play/wwdc2023/10115/)
⭐⭐⭐⭐⭐|[Swiftful Thinking](https://www.youtube.com/@SwiftfulThinking)

---

[[Swift UI Logic]]

---

UIKit → 2008
Swift UI → 2019

Declarative Ul
- Identity
- Lifetime
- Dependencies


---


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


// shadow
.shadow(radius: 10)
.shadow(color: Color.red, radius: 10, x: 0, y: 20)
.shadow(color: Color.red.opacity(0.3), radius: 10, x: 0, y: 20) // add opacity

// let UI could show on safe area
.edgesIgnoringSafeArea(.bottom)

.zIndex(2.0) // order in ZStack
```

<br>

# UI Elements

### Background & Overlay
a element can have multiple background and overlay
```swift
.background()

.overlay()
.overlay(view, alignment: .center) // .topLeading ...
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
"checkmark.seal.fill"
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

### Gesture

##### TapGesture
```swift
/** tap vs button: 
	no state, no button animation
*/

.onTapGesture { 
	withAnimation { // animation
		zoomed.toggled()
	}
} 
```

##### `.onLongPressGesture()`
```swift
// onLongPressGesture
// onLongTouchGesture

.onLongPressGesture {
	isComplete.toggle()
}

.onLongPressGesture (
	minimumDuration: 5.0,
	maxmiumDistance: 50 // distance for touching while moving
) { 
	isComplete.toggle()
}
```

##### DragGesture
```swift
@State var offset: CGSize = .zero // CGSize(width: 0, height: 0)

RoundedRectangle(cornerRadius: 20)
	.offset(offset)
	.gesture(
		DragGesture()
			.onChange {value in 
				withAnimation(.spring()) {
					offset = value.translation
				}
			}
			.onEnded { value in
				withAnimation(.spring()) {
					offset = .zero // 
				}
			}
	)
```

##### MagnificationGesture
```swift
// zoom gesture

@State var currentAmount: CGFloat = 0

...
.scaleEffect(1 + currentAmount)
.gesture(
	MagnificationGesture()
		.onChanged{ value in
			currentAmount = value - 1
		}
		.onEnded { value in
			withAnimation(.spring()) { 
				currentAmount = 0
			}
		}
)
```

<br>

### Slider

![[slider.png | 200]]

```swift
@State var _value: Double = 10

Slider(value: $_value)
Slider(value: $_value, in: -10...10)
Slider(value: $_value, in: -10...10, step: 1.0)

Slider(value: $_value,
       in: -10...10,
       step: 1.0,
       onEditingChanged: { (_) in },
       minimumValueLabel: Text("min"),
       maximumValueLabel: Text("max"),
       label:{Text("Label")}
)
```

<br>

### Stepper

![[stepper.png | 200]]

```swift
@State var stepperValue: Int = 10
    
Stepper("Title", value: $stepperValue)

// custom +- 10
Stepper("Title"){ // increment
    stepperValue += 10
} onDecrement: {
    stepperValue -= 10
}
```

```swift
// String format
Text(String(format: "%.2f", _value)) // 0.00
Text(String(format: "%.1f", _value)) // 0.0
Text(String(format: "%.0f", _value)) // 0
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

##### ScrollViewReader

```swift
@State var 

ScrollView {
	ScrollViewReader { proxy in 
	
	// change proxy inside ScrollViewReader
	Button("Click to scoll") {
			proxy.scrollTo(49, anchor: nil)
			//  anchor -> .top .center .bottom
			// better to work with withAnimation(.spring())
	}
		...
	
	Text("dummy text")
	.id(index)
	
	}
	// change proxy by outside by @State var and .onChange()
	.onChange(of: scrollToIndex, perform: { value in
		proxy.scrollTo(value, anchor: nil)
	}
}
```

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

### List

similar to `VStack()`, can move, add, delete items

```swift
List {
	Text("Text")
	Text("Text")
	Text("Text")
}

// Section
List {
  Section(header: Text("Fruits")) {
    Text("Text")
    Text("Text")
    Text("Text")
  }
}

// Delete
@State var fruits: [String] = [ "apple", "orange", "banana" ]

List {
	ForEach(fruits, id: \.self) { fruit in
      Text(fruit)
  }
  .onDelete(perform: { indexSet in
      print(indexSet)
      fruits.remove(atOffsets: indexSet)
  })
  // or extract in function
  .onDelete(perform: delete) 
}

func delete(indexSet: IndexSet) {
	 fruits.remove(atOffsets: indexSet)
}

```

![[list-delete.gif | 300]]

##### swipeActions

![[List-swipeActions.gif]]

```swift
List {
    Text("ListItem")
        .swipeActions(edge: .trailing, // .leading
                      allowsFullSwipe: true // allow swipe to execute
        ) {
            Button("Function") {
                print("execute")
            }
            .tint(Color.green)
        }
}
```

<br>

### Picker

```swift
Picker(
	selection: $selection,
	label: Text("Picker")
	content: {
		Text("1").tag("1")
		Text("2").tag("2")
		})
	}
	// Text("1") -> UI
	// .tag("1") -> value
	
)

Picker(
	selection: $selection,
	label: Text("Picker")
	content: {
		Text("1").tag("1")
		Text("2").tag("2")
		// or
		ForEach(18 ..< 100 { number in
			Text("\\(number)")
				.font( ... )
				.foregroundColor( ... )
			.tag("\\(number)")
		})
	}
)
	.background( ... )
	.pickerStyle(WheelPickerStyle()) 
	// MenuPickerStyle() Dropdown, will show label
	// SegmentedPickerStyle()
```

```jsx
init() {
	// UIKit
	UISegmentedControl.appearance().selectedSegmentTintColor = UI.Color.red
}
```

<br>

### Menu

```swift
Menu("Click Me") {
	Button ("Button 1") {}
	Button ("Button 2") {}
	Button ("Button 3") {}
}
```

<br>

### ColorPicker

```swift
@State var color: Color = Color.red

ColorPicker("Select Color",
	selection: $color,
	supportsOpacity: true
)
	.datePickerStyle(
		// WheelDatePickerStyle()
		// GraphicalDatePickerStyle()
	)
```

<br>

### DatePicker

[https://developer.apple.com/documentation/swiftui/datepicker](https://developer.apple.com/documentation/swiftui/datepicker)

```swift
var startingDate: Date = Date()
var endingDate: Date = Date()

DatePicker("title",
   selection: $date,
   displayedComponents: [.date, .hourAndMinute]
   in: startingDate...endingDate // range
)
```

```swift
var dataFormatter: DateFormatter{
    let formatter = DateFormatter()
    // formatter.timeStyle = .medium
    formatter.dateStyle = .medium // short | long
    return formatter
}

Text(date.description)
Text(dataFormatter.string(from: date))
```

![[dateFormatter.png]]

```swift
// adding 1 day
Calendar.current.date(byAdding: .day, value: 1, to: Date() )
```

```swift
let remaining = Calendar.current.dateComponents([.hour, .minute, .second], from: Date(), to: futureDate)

let hour = remaining.hour ?? 0
let minute = remaining.minute ?? 0
let second = remaining.second ?? 0
```

<br>

### Badges

> Badges appear only in list rows, tab bars, and menus.

[https://developer.apple.com/documentation/swiftui/view/badge(_:)-84e43](https://developer.apple.com/documentation/swiftui/view/badge(_:)-84e43)

```swift
tabItem{ ... }
	.badge(2)
	.badge("NEW")

List {
	Text("")
		.badge("New Item!")
}
```


<br>

### Alerts

![[aliert.gif]]

```swift
@State var showAlert: Bool = false

Button ("Click") { ... }
	.alert(isPresented: $showAlert, content: {
		Alert(title: Text("Title"))
	}
```

<br>

### `.onAppear()` & `.onDisappear()`

```swift
.onAppear(perform: {
	myText = "New Text"
})

.onDisappear()
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
`NavigationView` is deprecated now use `NavigationStack`
- `NavigationView` is lazy
- `NavigationStack` not lazy

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

### TabView

![[tabview.png | 200]]

```swift
// view ↓
// Tab Button
TabView {
	ZStack {
		Color.red.ignoresSafeArea()
	}
		.tabItem {
		    Image(systemName: "house.fill")
		    Text("title")
		}
	
	Text("aaa")
		.tabItem {
		    Image(systemName: "house.fill")
		    Text("title")
		}
	
	HomeView()
		.tabItem {
		    Image(systemName: "house.fill")
		    Text("title")
		} 
}
```

```swift
@State var _selection : Int = 1

// init to view2
TabView (selection: $_selection) {
	view1()
		.tag(0)
	
	view2()
		.tag(1)
}
```

##### PageTabViewStyle

![[tabview-PageTabViewStyle.gif]]

```swift
TabView {
  RoundedRectangle(cornerRadius: 25.0)
      .frame(height: 200)
      .padding(30)
  RoundedRectangle(cornerRadius: 25.0)
      .frame(height: 200)
      .padding(30)
  RoundedRectangle(cornerRadius: 25.0)
      .frame(height: 200)
      .padding(30)
}
.frame(height: 200)
.tabViewStyle(PageTabViewStyle())
```

<br>

### ActionSheet

![[actionSheet.gif]]|![[actionSheet-2.gif]]
---|---

```swift
Button("Click") {
	showActionSheet.toggle()
}
.actionSheet(isPresented: $showActionSheet) {
	ActionSheet(
		title: Text("title"),
		message: Text("message"),
		buttons: [
			.default(Text("default")),
			.destructive(Text("destructive")),
			.cancel()
		]
	)
}
```

### Group
apply modifiers
no change to layout
```swift
Group {
   ...
}
```

<br>

### MatchedGeometryEffect

Animate object, for geometry shapes

```swift
@Namespace private var namespace

// view
if !Clicked {
	Rectangle()
		.matchedGeometryEffect(id: "rectangle", in: namespace)
		.frame(width: 100, height: 200)
}

Spacer()

if !Clicked {
	Rectangle()
		.matchedGeometryEffect(id: "rectangle", in: namespace)
		.frame(width: 300, height: 200)
}
```

![[matchedGeometryEffect_bar_from_SwitfulThinking.gif]]
<br>

# Swift UI Logic

### NVVM Architecture
- Model - data point
- View UI
- View Model - manages Model for View

Struct → Class → View
Model → ModelView → View


Views are `struct`, only require `body`

```swift
// state changed -> View update
// @State -> only in struct : View
@state var zoomed = false 
@state private var zoomed = false
...
.aspectRatio(contentMode: zoomed ? .fill : .fit)

.onTapGesture { 
	withAnimation { // animation
		zoomed.toggled()
	}
} 
```



![[date-flow-primitives.png]]

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

### `weak self`

strong reference → will not `deinit()`
```swift
DispatchQueue.main.asyncAfter(deadline: .now() + 500) {
	self.data = "New Data"
}
```

`weak self`
weak reference → will `deinit()` → more efficient
Its ok for the class (self) to `deinit()`
```swift
DispatchQueue.main.asyncAfter(deadline: .now() + 500) { [weak self] in
	self?.data = "New Data" // weak is optional
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

### ![[Swift#Condition]]
<br>

### Generics

create for all types

```swift
struct GenericModel<T> {
	let info: T?
	func removeInfo() -> T {
		// return GenericModel(info: nil)
		// one line no need for return
		GenericModel(info: nil)
	}
}
```

View → protocol not type

```swift
struct GenericView<T:View> : View { // type only conform to View
	let content: T
	var body: some View {
		content
	}
}

// in view
GenericView(content: Text("text"))
```
<br>

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

<br>

### @ObservedObject & @Published

```swift
 class MyClass : ObservableObject { 
	@Published var fruitArray: [Fruit] = []
}

// when @Publish variabale changed, view will be upated

struct View: View {
	// When View reload, @ObservedObject → reload
	// @ObservedObject var myModel: MyClass = MyClass()

	// When View reload, @StateObject will not reload
	@StateObject var myModel: MyClass = MyClass()

	// Use on creation / init -> @StateObject
	// Use for subview -> @ObservedObject

	SecondView(myModel)
} 

struct SecondView: View {
	@ObservedObject var myModel: MyClass
}
```

init @StateObject
```swift
@StateObject private var object: MyObject

init(id: Int = 1) {
    _object = StateObject(wrappedValue: MyObject(id: id))
}
```
<br>

### Environment Variable
``` swift
// Environment Variable
@Environment(\.presentationMode) var presentationMode

{
	presentationMode.wrappedValue.dismiss()
}

```


### @EnvironmentObject

`.environmentObject` similar to `useContext()` in React

```swift
var viewModel: ViewModelObject = ViewModelObject()

View: View {
	SecondView { ... }
		.environmentObject(viewModel)
}

SecondView: View {
	@EnvironmentObject var viewModel: ViewModelObject
}
```

<br>

### PlayAudio and Singleton

```swift
import AVKit

class SoundManager { // singleton
	static let instance = SoundManager() 

	var player: AVAudioPlayer?

	func playSound() {

		guard let url = Bundle.main.url(forResources: "", withExtension: ".mp3") else {return}

		do {
			player = try AVAudioPlayer(contentsOf: url )
			player?.play()
		} catch let error {
			print("Error\\(error.localizedDescription)")
		}
	}
}
```

```swift
SoundManager.instance.playSound()
```

```swift
private init() {
	
}
```


<br>

### `UserDefaults` & `@AppStorage`

for small data

UserDefaults

```swift
@State var cuurentUserName: String?

// save 
UserDefaults.standard.set(value: "Nick", forKey: "name" )

// .onAppear() fetch
name = UserDefaults.standard.string(forKey: "name")
// name = "Nick"
```

@AppStorage

```swift
@AppStorage("name") var currentUserName: String?
// will save automatically
```


### Download

##### Original
```swift
func downloadData(fromURL url: URL, completionHandler: @escaping (_ data: Data?) -> ()) {

	URLSession.shared.dataTask(with: url){ (data, response, error)in
	guard
		let data = data,
		error == nil,
		let response = response as? HTTPURLResponse
		response.statusCode >= 200 & response.statusCode < 300 else {
			print("Error downloading data.")
			completionHandler(nil)
			return
		}
		completionHandler(data)
		}.resume()
}
```

```swift
downloadData(fromURL: url) { (returnedData) in
	if let data = returnedData {
		guard let newPosts = try? JSONDecoder().decode([PostModel].self, from: data) else { return }
		DispatchQueue.main.async { [weak self] in
		self?.posts=newPosts
	}else{
		print("No data returned.")
	}
}
```

```swift
// "_" just mean that when you call, you don't pass the label.

// call the function without name
(completionHandler(image, nil))
```

##### Combine
require \>= iOS 13


<br>

### Identifiable & Hashable

|Identifiable|Hashable|
|---|---|
|explicit ID|no explicit ID|
|ForEach(_array)|ForEach(_array, id: \.self)|

##### Identifiable

```swift
struct MyCustomModel: Identifiable {
	let id = UUID.uuidString
	...
}

let _array: [MyCustomModel] = [ ... ]

// Identifiable use array
ForEach(_array) {
	
}
```

##### Hashable

similar to C# `IEnumerable`?

```swift
// stirng conforms hashable
let _array [String] = ["ONE", "TWO", ... ]

ForEach(_array, id: \\.self) { item in 
	item.hashValue.description 
}
```

```swift
struct MyCustomModel: Hashable {
	let title: String

	func hash(into hasher: inout Hasher) {
		hasher.combine(title)
	}
}
```

<br>

### Typealias

```swift
struct MovieModel {
	let title: String
	let director: String
	let count: Int
}

typealias TVModel = MovieModel
```

<br>

### Timer & `.onReceive`

timer → Publisher

```swift
// on -> thread
// autoconnected -> start
let timer = Timer.publish(every: 1.0, on: .main, in: .common).autoconnected()

Timer
	.publish(every: 1.0, on: .main, in: .common)
	.autoconnected()

// view
view {
	...
}
.onReceive(timer, perform: { value in
	// value -> Date()
})
```

<br>

### Multi-threading

```swift
DispatchQueue.global().async { // to background thread
DispatchQueue.global(qos: .background).async { // select a qos

	let newData = self.dataFunc() // strong	

	DispatchQueue.main.async { // back to main thread
		self.dataArray = newData
	}
}

Thread.isMainThread // Bool
Thread.current // Thread

// CPU page
```

<br>

### DispatchQueue

```swift
DispatchQueue.main.asyncAfter(deadline: .now() + 5) { // delay 5 seconds
	myText = "New Text"
}	
```

<br>

### UIViewRepresentable

UIKit → SwiftUI
UIViewRepresentable: A wrapper for a UIKit view that you use to integrate that view into your SwiftUI view hierarchy

```swift
// example of using UIKit Textfield

struct WebView: UIViewRepresentable {
  
    // 2 -> init
    func makeUIView(context: Context) -> WKWebView {
			let view = UIView() // basic UI View
			view.backgroundColor = .red
			return view
    }
    
    // From SwiftUI to UIKit
    func updateUIView(_ webView: WKWebView, context: Context) {

    }

	// from UIKit to SwiftUI
	// Creates the custom instance that you use to communicate changes from your view to other parts of your SwiftUI interface
	func makeCoordinator () {
		return Coordinator()
	}

	class Coordinator: NSObject, UITextField {
		func textFieldDidChangeSelection() {
		
		}
	}
}
```

##### WebView to SwiftUI
[https://sarunw.com/posts/swiftui-webview/](https://sarunw.com/posts/swiftui-webview/)

```swift
import WebKit
```

View
```swift
let website : String = "<https://www.youtube.com/>"

// open the link in Safari
Link("Sarunw", destination: URL(string: "<https://sarunw.com>")!)

// open the link in view
if let websiteURL = URL(string: website) {
	WebView(url: websiteURL)
}
```

```swift
// open  
struct WebView: UIViewRepresentable {
    // 1
    let url: URL
    
    // 2
    func makeUIView(context: Context) -> WKWebView {
        return WKWebView()
    }
    
    // 3
    func updateUIView(_ webView: WKWebView, context: Context) {

        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

<br>

### Parsing JSON Data

##### Swift object → (JSON) data
```swift
data // swift object 
let jsonData = try? JSONSerialization.data(with: data, options: [])
```
Encodable
```swift
let customer = CustomerModel(id: "", name: "", points: 100, isPremium: false)
let jsonData = try? JSONEncoder().encode(customer) ↓
```


##### data → JSON Object

Manual
```swift
data
if // make sure both jsonObject & result is ok
	let jsonObject = try? JSONSerialization.jsonObject(with: data, options: []),
	let result = jsonObject as? [String: Any] { // try to convert to a type
		... 
		let id = result["id"] as? String 
		// try to get a value with default value 
		let _var = dictionary["_category"] as? String ?? "default value"
		...
	}
```

`Decodable`
```swift
data
self.customer = try ? JSONDecoder().decode(CustomerModel.self, from: data) 

do { 
	self.customer = try JSONDecoder().decode(CustomerModel.self, from: data) 
} catch let error { 
	print("\(error)") 
}
```

```swift
// Decodable -> data to swift object
// Encodable -> swift object to data
// Codable -> Decodable & Encodable
// no need to explicitly write 

struct CustomerModel: Codable { 	
	let id: String
	let name: String
	let points: Int
	let isPremium: Bool
}

struct CustomerModel: Decodable, Encodable { 
	
	// 2 add CodingKeys, parse data to keys
	enum CodingKeys: String, CodingKeys {
		case id
		case name
		case points
		case isPremium = "is_premium" // if property name is differ from json
	}

	// 1 add custom init
	init(from decoder: Decoder) throws {
		let container = try decoder.container(keyedBy: CodingKeys.self)
		
		// get value from keys
		self.id = try container.decode(String.self, forKey: .id)
		...
	}

	// for Encodable
	func encode(to encoder: Encoder) throws {
		var container = encoder.container(keyedBy: CodingKeys.self)
		try container.encode(id, forKey: .id)
		...
	}
}
```

##### Preview data 
```swift
let jsonString = String(data: _data, encoding: .utf8) 
print(jsonString)
```



# Custom

### Custom view modifier

take current content and return new view

re-usable

```swift
struct DefaultButtonViewModifier: ViewModifier {
	func body(content: Content) -> some View {
		content
			// add some modifiers
			.font(.headline)
			.foregroundColor(.white)
			...
	}
}
```

```swift
Text("Hello")
	.modifier(DefaultButtonViewModifier())
```

without modifier

```swift
extension View {
	func withDefaultButtonFormatting() -> some View {
		// self.modifier(DefaultButtonViewModifier())
		modifier(DefaultButtonViewModifier())
	}
}
```

```swift
Text("Hello")
	.withDefaultButtonFormatting()
```


### Custom Button Style

```swift
struct CustomButtonStyle: ButtonStyle {

	let scaleAmount: CGFloat // custom input optional

	func makeBody(configuration: Configuration) -> some View {
		configuration.label
			.scaleEffect(configuration.isPressed ? scaleAmount : 1.0)
			.brightness(configuration.isPressed ? 0.05 : 0)
			.opacity(configuration.isPressed ? 0.8 : 1.0) // opacity to 0.8 when pressed
	}
}

extension View {
	func _CustomButtonStyle() -> some View {
		buttonStyle(CustomButtonStyle())
	}
}

// view
Button(action: { ... }, label: { ... })
	.buttonStyle(CustomButtonStyle())
	.buttonStyle(CustomButtonStyle(scaleAmount: 0.5))
	._CustomButtonStyle() // use with extension part
```
<br>

### Detect app lifecycle
[https://prafullkumar77.medium.com/swiftui-how-to-detect-if-the-application-in-background-or-foreground-20bc4c8d18a](https://prafullkumar77.medium.com/swiftui-how-to-detect-if-the-application-in-background-or-foreground-20bc4c8d18a)

```swift
@main
struct testApp: App {
    @Environment(\\.scenePhase) var scenePhase

    var body: some Scene {
        WindowGroup {
            ContentView()
        }.onChange(of: scenePhase) { phase in
            print("changed")
            switch phase {
            case .background:
                print("App is in background")
            case .active:
                print("App is Active")
            case .inactive:
                print("App is Inactive")
            @unknown default:
                print("New App state not yet introduced")
            }
        }
    }
}
```