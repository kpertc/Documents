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
    @Environment(\.scenePhase) var scenePhase

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