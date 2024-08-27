
### VAT Vertex Animation Texture

[Texture Animation: Applying Morphing and Vertex Animation Techniques](https://medium.com/tech-at-wildlife-studios/texture-animation-techniques-1daecb316657)

<iframe width="560" height="315" src="https://www.youtube.com/embed/NQ5Dllbxbz4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

##### Unity #Unity 

<iframe width="560" height="315" src="https://www.youtube.com/embed/SSOpaVp7RW4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

![[img/Houdini VAT Vertex Animation Texture/image (11).png]]

Houdini Unity Package Path: 
`C:\Program Files\Side Effects Software\sidefx_packages\SideFXLabs18.5\unity\shaders`

Add package in Unity

![[img/Houdini VAT Vertex Animation Texture/unity-add-package-1.png]]|![[img/Houdini VAT Vertex Animation Texture/unity-add-package-2.png]]
---|---

选择对应的VATUnity包，导入
![[img/Houdini VAT Vertex Animation Texture/选择对应的VATUnity包-导入.png]]

FBX, Texture应用 Houdini带的preset，材质使用导入的VAT的shader

![[img/Houdini VAT Vertex Animation Texture/选择present-1.png]]|![[img/Houdini VAT Vertex Animation Texture/选择present-2.png]]
---|---

Frame Range -> End - Start
60-1=59

![[img/Houdini VAT Vertex Animation Texture/frame-range.png]]