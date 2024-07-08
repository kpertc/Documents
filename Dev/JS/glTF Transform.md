
List Material
```ts
doc
    .getRoot()
    .listMaterials()
    .forEach((material) => { }
```

List object
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