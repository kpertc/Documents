### SF Symbol
> Apple designed SF Symbols to integrate seamlessly with the San Francisco system font

act like font
- changed with font size
- light & dark mode

`Image(systemName: "heart.fill")`

Rendering mode: monochrome / hierarchical / palette / multicolor → `.symbolRenderingMode(.palette)`

Variable value (0 - 1 fill, e.g. wifi, speaker): `Image(systemName: "wifi", variableValue: 0.5)`

Animate (iOS 17+): `.symbolEffect(.bounce)`