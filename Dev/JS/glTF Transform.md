#JavaScript #CG #web-dev #TypeScript 
##### List Material
```ts
doc
    .getRoot()
    .listMaterials()
    .forEach((material) => { }
```

##### List objects
```ts
doc
    .listNodes()
    .forEach((node) => {
        // get basic info
        const name = node.getName()
        const translation = node.getTranslation()
        const rotation = node.getRotation()
        const scale = node.getScale()
    })
```

##### Check Type
``` ts
_node.propertyType // PropertyType.NODE
```

##### Load .`glb` and save as `.glb`
```ts
const io = new NodeIO(); 

const document = await io.read(path);

await io.write(path, document);
```

##### Copy nodes to a new document
``` ts
const _wheelDocument = new Document(); // create new document

const wheelList: Node[] = [];

document
	.getRoot()
	.listNodes()
	.forEach((node: Node) => {
		if (node.getName() === "Car_Wheel") {
			wheelList.push(node);
		}
	});

copyToDocument(_wheelDocument, document, wheelList);
```

Using Blender to automatically load the model → [[Blender Scripting Basics#Command line]]

### Transform

``` js
doc.transform(
	palette({ min: 5 }),
	flatten(),
	dequantize(),
	join(),
	reorder({ encoder: MeshoptEncoder, target: 'size' }),
	dedup(),
	prune()
)
```