
### [[Houdini Python]]
### [[Houdini Vector Expression Language, VEX]]

---

### (HScript `$`) Expression Function

[Expression cookbook](https://www.sidefx.com/docs/houdini/ref/expression_cookbook.html)
![[Houdini Programming/documentation (4).pdf]]

Use HScript in (Channel) parameter or Hscript Textport

##### Hscript Textport

|Windows/Hscript Textport|Check Variable name by Textport|
|-|-|
|![[Houdini Programming/windows-Hscript-Textport.png]]|![[Houdini Programming/checkNamebyTextPort.gif]]|

https://www.sidefx.com/docs/houdini/ref/expression_cookbook.html

Source [[YouTube] 01 What is HScript and where to use it](https://www.youtube.com/watch?v=VeJrovx2a1k&list=PLSET4TyKEfn9TLeA9wunf_-yEbhg-Rctf)

Custom Interface
![[Houdini Programming/Custom-Interface.png]]


### Access other nodes

```C#
point("node", point number, "attribname", index)
// point(0,"P",0)

prim("node", prim number, "attribname", index)
// prim(0, 0, "attribname", 0)

vertex("node", prim number, vertex number on prim, "attribname", index)
detail("node", "attribname", index)
```

```C#
@primnum // current prim #
@numprim // total # of prim 
```

![[Houdini Programming/HScript-Channel-Reference.png]]

`$T` Time (floating point time in seconds)
`$PR` local Variable for the current Primitive Number

```C#
clamp(value, min, max)
bbox("node", D_YMIN)
bbox("node", D_YMAX)
centroid("node", D_Y)
```

If

```C#
if ( condition, true, false )
```

```Plain
Returns the full path of a node.
opfullpath(' relative path here ')
```

---

### Change Expression Language

**Change default expression Language**: preference > Scripting > Expression Language
Change expression language:
![[Houdini Programming/Change-Expression-Language.png]]