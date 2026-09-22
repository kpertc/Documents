Stage > Layer > Shape

``` tsx
import { Stage, Layer } from "react-konva";

const handleMouseDown = (e) => {
	const pos = e.target.getStage().getPointerPosition(); // pointer pos
}

// Stage needs explicit pixel width / height
<Stage
	width={width}
	height={height}
	onMouseDown={handleMouseDown}
>
	<Layer></Layer>
</Stage>
```