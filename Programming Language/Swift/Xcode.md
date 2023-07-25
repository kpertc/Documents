Install Command Line Tool & Multiple Xcodes -> [[Env Tools]]

<br>

Turn on / off Minimap
![[minimap.gif]]

##### Emoji
^(ctrl) + ⌘ + space 
![[emoji.gif]]

<br>

### Simulator

Switch light & dark mode
⌘ + Shift + A

Format code
Ctrl i 
<br>

### SwiftUI
Shortcut| 
---|---
Library|![[Library.gif]]
⌥ (option) + ⌘ (command) + Enter|Toggle preview
⌘  + click|![[menu-of-actions.webp]]
Add Modifiers|![[add-modifiers.gif]]
Extracted Subview

### ![[Swift#Documentation]]
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
