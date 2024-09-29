### Blender

export data to `.gltf`

### UserData
three.js → `object.userdata`
Blender → `custom properties`

| ![[DCC-threejs-userdata.png]] | ![[DCC-blender-userdata.png]] | ![[DCC-blender-userdata-export-setting.png]] |
| ----------------------------- | ----------------------------- | -------------------------------------------- |

### Attributes

> Export Attributes with meshes, when the name starts with underscore. '_'
> https://docs.blender.org/manual/en/latest/addons/import_export/scene_gltf2.html#data-mesh

![[DCC-threejs-geo-attribute.png]]|![[DCC-blender-attribute.png]]|![[DCC-blender-attribute-export-setting.png]]
---|---|---

`Store Named Attribute` Node to create attribute

![[Blender Geometry Nodes#View Value]]

Set per-face attributes to vertexs
![[DCC-blender-setFaceAttributes.png]]
### Material
##### MeshBasicMaterial
texture or color node connect to Material Output
![[DCC-blender-meshBasiicMaterial.jpeg]]

### Camera Path
- [[Blender Best Practice#Camera follow curve path]]
- 