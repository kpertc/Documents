**Maya Embedded Language**
|Python|MEL|
|------------ | ------------|
|(Generalist)|(specialist)|
| - cross DCCs<br/> - most maya functions<br/> - extern| - only in maya<br/> - (all maya functions<br/> - feedback & help)|


```mel
print "Hello World"

polyCube //create a cube

help polyCube //Open Help
```

```mel
polyCube

setAttr pCube1.translateX 20
```

```mel
string $myString = "Hello World";
print $myString;

string $usernames[] = {"David", "John", "Luke"};
print $usernames; //print all
print $usernames[0]; //print the first one
$usernames[0] = "Linda"; //edit the first item from David to Linda
print (size($usernames)) //print how many items in the array


int $myInt = 2;
print $myInt;
```

### Comments

```mel
//Comment

/*
Multi-lines
Comment
*/
```

### Using Python in MEL

```mel
python("print(min(3, 4))");
python("print('Hello World')");
```

Maya 2022+ embeds Python 3, so `print` needs the parentheses
The MEL string uses double quotes, so the Python string inside has to use single quotes

### Using MEL in Python

```python
import maya.mel as mel
mel.eval('select -r pSphere3;')
```

### Communicating between Python and MEL

[Maya 2013 getting started](https://download.autodesk.com/us/maya/maya2013_getting_started/index.html?url=files/Using_Python_in_Maya_Communicating_between_Python_and_MEL.htm,topicNumber=d30e45784) (old, current docs: https://help.autodesk.com/view/MAYAUL/ENU/)