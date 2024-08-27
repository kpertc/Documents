Groups can act as Binary Masks for SOP nodes.

Selecting - Highlight Flag shows group

```Plain
#-# Select Consecutive geometry elements

* Select all attribute
^ remove from the selection
! negate selection

Vertex
[prim]v[vertex] selects one or more vertex of a primitive

Edge
p#-# select edge by point # 
p#-#-# 
```

```Plain
use attribtue to select group
@P.y>0
@Cd>0.5

use VEX
`nprims('0') -1` last prim number
```

Ways to create group

-   `Group`
    
-   `Group Expression` [Houdini: 10 Useful VEX Snippets for Group Expression Node](https://www.artstation.com/blogs/jorgelega/7m1r/houdini-10-useful-vex-snippets-for-group-expression-node)
    
-   `Attribute Wrangle` `@group_groupName ... ;`
    

  

##### Include by Edges

Edge Depth - Expand|Unshared Edges|
--|--|--
![[img/Houdini Group and VEX/Edge Depth - Expand.png]]|![[img/Houdini Group and VEX/unshared-edge-1.png]]|![[img/Houdini Group and VEX/unshared-edge-2.png]]


### Group by Range

![[img/Houdini Group and VEX/group-by-range.png | 500]]

**Equal Partitions**: Divides geometry into sections and selects a section|**Range** **Filter****:** Select patterns of X out of Y elements
---|---
![[img/Houdini Group and VEX/Equal Partitions.png]]|![[img/Houdini Group and VEX/Range Filter.png]]

### Group Expand

| Require Primitives Share Edge `OFF`            | Require Primitives Share Edge `ON`                           |
| ---------------------------------------------- | ------------------------------------------------------------ |
| ![[img/Houdini Group and VEX/groupExpand.gif]] | ![[img/Houdini Group and VEX/requirePrimitiveShareEdge.gif]] |

Flood Fill to Connected Geometry: allow unbounded growth to connected geometry

  

### Group Promote

### Group Rename

### Group Copy

Copy groups by nums

  

### [VEX](https://www.sidefx.com/docs/houdini/vex/groups.html)

[setpointgroup()](https://www.sidefx.com/docs/houdini/vex/functions/setpointgroup.html)
[setprimgroup()](https://www.sidefx.com/docs/houdini/vex/functions/setprimgroup.html) 
[setvertexgroup()](https://www.sidefx.com/docs/houdini/vex/functions/setvertexgroup.html)

```C#
setpointgroup(0, "groupName", @ptnum, 1); // set to the group
setpointgroup(0, "groupName", @ptnum, 0); // remove from the group
setprimgroup
setvertexgroup
```

Return 1 if in the group

```C#
inpointgroup()
invertexgroup()
inprimgroup()
```

Returns the number of points/vertices/primitives in the group

[npointsgroup()](https://www.sidefx.com/docs/houdini/vex/functions/npointsgroup.html)
[nverticesgroup()](https://www.sidefx.com/docs/houdini/vex/functions/nverticesgroup.html)
[nprimitivesgroup()](https://www.sidefx.com/docs/houdini/vex/functions/nprimitivesgroup.html)

```C#
npointsgroup()
nverticesgroup()
nprimitivesgroup(geometry, "groupname")
```

Return an array of integer

[expandpointgroup()](https://www.sidefx.com/docs/houdini/vex/functions/expandpointgroup.html)
[expandprimgroup()](https://www.sidefx.com/docs/houdini/vex/functions/expandprimgroup.html)
[expandvertexgroup()](https://www.sidefx.com/docs/houdini/vex/functions/expandvertexgroup.html)

```C#
expandpointgroup() // [ 80, 81, 82, 83 ]
expandprimgroup()
expandvertexgroup()
```

##### Create Group

Create new group by VEX `@group_groupName`

Turn on: `@group_groupName = 1`

Turn off: `@group_groupName = 0`

![[img/Houdini Group and VEX/group-enable.png]]

![[img/Houdini Group and VEX/group-VEX.png]]

```C#
if (@primnum % 2 == 0)
{
    @group_group2 = 1;
}
```

##### Mixing group expression with VEX

[setpointgroup](https://www.sidefx.com/docs/houdini/vex/functions/setpointgroup.html)
`setpointgroup(0, "@P.y>0", @ptnum, 0);`