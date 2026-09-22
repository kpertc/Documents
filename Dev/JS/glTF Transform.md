#JavaScript #CG #web-dev #TypeScript 

`@gltf-transform/core` v4.x
```ts
import { Document, NodeIO, copyToDocument } from '@gltf-transform/core'
```

##### List Material
```ts
doc
    .getRoot()
    .listMaterials()
    .forEach((material) => { })
```

##### List objects
```ts
doc
    .getRoot() // listNodes() is on Root, not Document
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
await MeshoptEncoder.ready; // reorder() needs the WASM module initialized

await doc.transform( // transform() is async
	palette({ min: 5 }),
	flatten(),
	dequantize(),
	join(),
	reorder({ encoder: MeshoptEncoder, target: 'size' }),
	dedup(),
	prune()
)
```

### Calculate new local matrix after move to new hierarchy
```JavaScript
import { mat4 } from 'gl-matrix'

function calculateLocalMatrix(node, parent) {
  const nodeWorldMatrix = node.getWorldMatrix()
  const parentWorldMatrix = parent.getWorldMatrix()

  const parentWorldInverse = mat4.create()
  mat4.invert(parentWorldInverse, parentWorldMatrix)

  const localMatrix = mat4.create()
  mat4.multiply(localMatrix, parentWorldInverse, nodeWorldMatrix)

  return localMatrix
}
```

### KTX

- [[KTX Format]]

Convert gltf model's texture tp ktx2 within gltf model
``` bash
gltf-transform uastc /Users/xxx/Downloads/xxx.glb /Users/xxx/Downloads/xxx-uastc.glb --verbose

gltf-transform etc1s /Users/xxx/Downloads/xxx.glb /Users/xxx/Downloads/xxx-etc1s.glb --verbose

# verbose will list the detail
```

Tutorial: https://www.youtube.com/watch?v=Wt3iEenj_Xw&t=2s

online tools
online convert glb model texture to ktx2
- https://glb.babylonpress.org/