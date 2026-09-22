#JavaScript 

- reactFlow shadcn https://reactflow.dev/ui

v12+: `npm i @xyflow/react`
```tsx
import { ReactFlow, Handle, Position, Background, Controls, MiniMap, Panel, useReactFlow } from "@xyflow/react";
import "@xyflow/react/dist/style.css";
```
v11 (legacy): package is `reactflow`

``` tsx
const CustomNode = () => {
  return (
    <>
      <div className="text-updater-node">
        <div>Custom Node Content</div>
        <Handle type="target" position={Position.Top} />
        <Handle type="source" position={Position.Bottom} />
      </div>
    </>
  );
};

const nodeTypes = { textUpdater: CustomNode };

const initialNodes = [
  { id: "n1", position: { x: 0, y: 0 }, data: { label: "Node 1" } },
  {
    id: "n2",
    position: { x: 0, y: 100 },
    data: { label: "Node 2" },
    type: "textUpdater", // specify t
  },
  // hidden: keeps the node in state but unrendered, its edges must be hidden separately
  { id: "n3", position: { x: 0, y: 200 }, data: { label: "Node 3" }, hidden: true },
];
```

```tsx
<ReactFlow
	nodes={nodes}
	edges={edges}
	nodeTypes={nodeTypes} // pass node type
	onNodesChange={onNodesChange}
	onEdgesChange={onEdgesChange}
	onConnect={onConnect}
	fitView
>
	<Background />
	<Controls />
	<MiniMap />
	{/* overlay UI */}
	<Panel position="top-left">
		...
	</Panel>
</ReactFlow>
```

add new node on flow
```tsx
const { screenToFlowPosition } = useReactFlow();

const position = screenToFlowPosition({
	x: event.clientX,
	y: event.clientY,
});

// add new node
const newNode = { id: crypto.randomUUID(), position, data: { label: "New" } };
setNodes((nds) => [...nds, newNode]);
```

edge
``` tsx
{ id: "e1-2", source: "n1", target: "n2", animated: true }
```


check node
``` tsx
const { getNode, getNodes } = useReactFlow();
const node = getNode("n1"); // read once
const data = useNodesData("n1"); // subscribe to its data
```