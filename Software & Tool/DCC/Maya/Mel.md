**Maya Embedded Language**
|Python|MEL|
|------------ | ------------|
|(Generalist)|(specialist)|
| - cross DCCs<br/> - most maya functions<br/> - extern| - only in maya<br/> - (all maya functions<br/> - feedback & help)|


```python
print "Hello World"

polyCube //create a cube

help polyCube //Open Help
```

```python
polyCube

setAttr pCube1.translateX 20
```

```python
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

```python
//Comment

/*
Multi-lines
Comment
*/
```

### Using Python in MEL

```python
python("print min(3, 4)");
python("print 'Hello World'");
```

### Using MEL in Python

```python
import maya.mel as mel
mel.eval('select -r pSphere 3;')
```

# [Communicating between Python and MEL](https://download.autodesk.com/us/maya/maya2013_getting_started/index.html?url=files/Using_Python_in_Maya_Communicating_between_Python_and_MEL.htm,topicNumber=d30e45784)