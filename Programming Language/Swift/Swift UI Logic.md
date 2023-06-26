### NVVM Architecture
- Model - data point
- View UI
- View Model - manages Model for View

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

<br>

### Environment Variable
``` swift
// Environment Variable
@Environment(\.presentationMode) var presentationMode

{
	presentationMode.wrappedValue.dismiss()
}

```

<br>

### `UserDefaults` & `@AppStorage`

for small data

Use@rDefaults

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
