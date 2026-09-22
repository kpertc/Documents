#VR 

[Sample Models](https://developer.apple.com/augmented-reality/quick-look/)


Entity Component System (ECS)
System -> update per frame


```swift
import RealityKit
import RealityKitContent // or ARKit, depending on target
```


```swift
let entity = try await Entity(named: "Scene", in: realityKitContentBundle)
```

[[SwiftUI]]

[Reality Composer Pro](https://developer.apple.com/videos/play/wwdc2023/10273)

SwiftUI
```swift
RealityView ()
```

SwiftUI -> RealityKit
Add SwiftUI to RealityKit entity
```swift
RealityView { _, _ in
	 // 
} update: {_, _ in 
   //
} attachments: { // Attrachments API
	Button { ... }
		.background(.green)
		.tag(" ")
}
```

USD -> 
`.rkassets`