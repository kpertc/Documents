#python 

1.  Maya Command → work with existing nodes
    [[CMDs]]
    [[PyMel]]
    [[Mel]]
-   UI
    [[UI CMD]]
	[[PyQT-PySide Components]]

  

2.  Maya API (Python / C++) → Create new nodes and commands
	[[Maya Python API]]
  
##### [[../../../Programming Language/Python/Python Basic]]


##### [Maya Setup PyCharm](https://bytedance.feishu.cn/docx/doxcnWgn7FvNe35Lce8f7nUgj8b)

##### [Maya中Python文件加载方法](https://bytedance.feishu.cn/docx/doxcnLy2GiUZ8kOtG06Hfuk3gub)

  

##### Script Editor Debug

Turn on `History` > `Show Stack Trace` for more

1.  `Invalid Syntex`

      Punctuation coma, parenthesis
    
      Refer to the line or the line above (if the end parenthesis on the last line is missing)
    
2.  `TypeError: can only concatenate list (not "str") to list #` or `'list' object has no attribute ''`
    ```Python
  # when object is not string (is a list)
  pm.setAttr( object + '.scale', (1,1,1 ) )
  pm.setAttr( object[0] + '.scale', (1,1,1 ) )
    ```
    
3.  `IndexError: list index out of range #`    
    1.  when not selecting object
    2.  wrong index used in the list

4.  `NameError: name ' ' is not defined #`
    

miss spelled variable name

In maya script editor `1` `l` look same


##### Script Editor Shortcut

Command Document|Shift + ( Ctrl ) + Arrow -> Selection
---|---
![[Maya Python Programming/mayaCheckCommandDocument.gif]]|![[Maya Python Programming/shift+Arrow.gif]]

![[Maya Python Programming/nodeShowAll.gif]]
  

##### Change Maya Language

![[Maya Python Programming/Change Maya Language-1.png \| 500]]|![[Maya Python Programming/Change Maya Language-2.png]]
---|---

![[Maya Python Programming/Change Maya Language-3.png]]|![[Maya Python Programming/Change Maya Language-4.png \| 500]]
---|---
  

### Command line Renderer
[Common flags for the command line renderer](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2020/ENU/Maya-Rendering/files/GUID-0280AB86-8ABE-4F75-B1B9-D5B7DBB7E25A-htm.html)

DG [DAG Hierarchy](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2022/ENU/Maya-Basics/files/GUID-5029CF89-D420-4236-A7CF-884610828B70-htm.html)

DAG → Transform
DG → no Transform

The DAG hierarchy (also known as an object hierarchy) refers to the parent-child relationships of all nodes that make up an object. DAG stands for directed acyclic graph.

DAG path
`DagPath = House|Apartment1|Window1`

[Maya Programming 入门 第六课](https://bytedance.feishu.cn/docx/J8Lkdsot8oBN3CxjxSvc0orXnKg)

Math by Node
![[Maya Python Programming/Math by Node.png]]