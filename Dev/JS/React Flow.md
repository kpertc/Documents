#JavaScript 

- 
- reactFlow shadcn https://reactflow.dev/ui

``` tsx
const CustomNode = () => {
  return (
    <>
      <div className="text-updater-node">
        <div>Custom Node Content</div>
        <Handle type="source" position={Position.Top} />
        <Handle type="target" position={Position.Bottom} />
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
  // {
  hidden
  }
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
	
	// 
>
	<Background />
	<Controls />
	<MiniMap />
	// overlay UI
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
setNodes((nds) => [...nds, newNode]);s
```

``
```
edge
abunated: true
```


``` check node

```