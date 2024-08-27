#programming-language 

### Basics

> [!note] Similar to C# syntax

VEX ⇆ VOPs are interchangeable
![[Houdini-Vector-Expression Language-VEX-img/VEX-VOPs-are-interchangeable.png | 300]]

View VEX code from VOP node: RMB > VEX/VOP Options > View VEX Code

---

Change VEX Precision: Binding > VEX Precision 32 || 64 bit

---

Create Spare Parameters
![[Houdini-Vector-Expression Language-VEX-img/Create-Spare Parameters.gif | 300]]

Data Type

|![[Houdini-Vector-Expression Language-VEX-img/data-type-snippets-1.png \| 300]]|![[Houdini-Vector-Expression Language-VEX-img/data-type-snippets-2.png]]|
|-|-|

### Related Topics:
[[Houdini VEX Math]]

### Variables
  
```C#
@Time
```

[VEX Attribute Glossary From kunz](https://wiki.johnkunz.com/index.php?title=VEX_Attribute_Glossary)

### Channel

```C#
ch()
chf() // channel reference float
chv() // channel reference vector

// get channel data
float width = ch('../width');
```

### Variable

```C#
string myString = "Hello World";
float x = 3;
vector vec1 = (0,1,1);
vector vec2 = set(0,1,1);
vector vec3 = {1,1,1};
```

### String
[join](https://www.sidefx.com/docs/houdini/vex/functions/join.html)

```C#
`  ... ` // String to code
\n // new Line
" \" ... \"" // type " 

itoa ( intValue ); // convert int to string
sprintf("%f", floatValue ); // convert float to string

sprintf("%f %f %s", floatValue, floatValue, stringValue ); // sprintf formatting

// Accessing Letter
string _string = "Hello Houdini";
_string[2]; // l
_string[6:9]; // Hou
string vals[] = { "A", "B", "C", "D", "E" };

// Join
string joinVal = join(vals, ","); // A,B,C,D,E

// Get # of letters in a string
int lengthOfString = len(joinVal); // 9

// Find
int index = find(joinVal, "B"); // 2 third place
// if return negative value means con not find

// Split
string splitStringArray[] = split(joinVal, ","); // [ A, B, C, D, E ]
```

### [Array](https://www.sidefx.com/docs/houdini/vex/arrays.html)

Create an array

```C#
float fArray[] = array() // init an empty array

// use vector set an array
v@vec1 = (1, 2, 4);
f[]@values = set( v@vec1 );
```

[append()](https://www.sidefx.com/docs/houdini/vex/functions/append.html)
[pop()](https://www.sidefx.com/docs/houdini/vex/functions/pop.html)
[removeindex()](https://www.sidefx.com/docs/houdini/vex/functions/removeindex.html)
[removevalue()](https://www.sidefx.com/docs/houdini/vex/functions/removevalue.html)
[isvalidindex()](https://www.sidefx.com/docs/houdini/vex/functions/isvalidindex.html)

```C#
// cannot include variables, only literal arrays
float fArray[] = { 2.5, 1.6, 9.3 };
string sArray[] = {"A", "B", "C", "D"};
vector vArray[] = {{0,1,2}, {3,4,5}};

// can use variable in array()
float fArray[] = array( fval, 1.6, 9.3 );
string sArray[] = array( sval, "B", "C", "D" );
vector vArray[] = array( vval, {3,4,5} );

// adding an item
push() // both push and append add variable to the end of the array 
append()

// remove
pop() // remove the last one or remove by specific index
removeindex() // remove by specific index
removevalue() // remove the first matched value

float nums[] = {0, 1, 2, 3, 1, 2, 3};
removevalue(nums; 2);  // == 1// nums == {0, 1, 3, 1, 2, 3}

// get length of an array
int length = len( array );

// check
isvalidindex()
```

### [Dictionary](https://www.sidefx.com/docs/houdini/vex/dicts.html)

[removeindex()](https://www.sidefx.com/docs/houdini/vex/functions/removeindex.html)
[getcomp()](https://www.sidefx.com/docs/houdini/vex/functions/getcomp.html)
[insert()](https://www.sidefx.com/docs/houdini/vex/functions/insert.html)
[json_loads()](https://www.sidefx.com/docs/houdini/vex/functions/json_loads.html)
[json_dumps()](https://www.sidefx.com/docs/houdini/vex/functions/json_dumps.html)

```C#
// init a dictionary
dict myDict = {};
dict myDict = set("a", 3.0);

// can set different type of data
myDict["a"] = 4;
myDict["b"] = "aaaa";
myDict["c"] = (1,2,3);
myDict["d"] = set("a", 3.0);

d@myDict = myDict;

// remove
int result = removeindex() // return 0 or 1; 1 -> successfully removed

isvalidindex() // check, return 0 or 1; 1 -> is valid
getcomp( dict, "key", defaultValue ); // get default value when extracting fail
insert( dict , dict ); // combine dictionaries

json_loads() // JSON string to dict
json_dumps() // dict to JSON string
```

### Attribtue

Init @Attribute

```C#
@myAttribute = 5; //deflaut is float
f@myAttribute = 5; //deflaut is float
i@myAttribute = x; // int
s@myAttribute = x; // string
v@myAttribute = x; // vector
d@myAttribute = set{ ... } // dictionary

f[]@farray = { 1.0, 2.0, 3.0 }; // float array
s[]@ ... // string array
v[]@ ... // vector array
```

```C#
//access diffuse color
v@cd.r = 1; //red value to 1 

v@P // position
v@Cd // color
v@v // Velocity

v@scale //scale
@pScale //uniform scale

@ptnum // point index
@pnum // total amount of number
@primnum // primnum

@id = @ptnum
```

### Get and set attributes

[getattribute()](https://www.sidefx.com/docs/houdini/vex/functions/getattribute.html)
[setattrib()](https://www.sidefx.com/docs/houdini/vex/functions/setattrib.html)
[setvertexattrib()](https://www.sidefx.com/docs/houdini/vex/functions/setvertexattrib.html)
[setpointattrib()](https://www.sidefx.com/docs/houdini/vex/functions/setpointattrib.html)
[setprimattrib()](https://www.sidefx.com/docs/houdini/vex/functions/setprimattrib.html)
[setdetailattrib()](https://www.sidefx.com/docs/houdini/vex/functions/setdetailattrib.html)

```C#
getattribute() // Get attribute
point() // get point attribute
vector PT_pos = point(0, "P", 0);

setattrib() // Set attribute
setvertexattrib()
setpointattrib()
setprimattrib()
setdetailattrib()
"set", "append"
```

```C#
// Intrinsic Attributes
float area = primintrinsic(0,'measuredarea',@primnum);
```

### [Houdini Group and VEX](https://bytedance.feishu.cn/docx/HmzRd8bBMoqfyXxQLvwcaoEhnld?from=create_suite)

### Geometry Functions

Frequent use functions

[nearpoint()](https://www.sidefx.com/docs/houdini/vex/functions/nearpoint.html)
[getbbox()](https://www.sidefx.com/docs/houdini/vex/functions/getbbox.html)

```C#
nearpoint() // return closest point number
also can use group as filter 

getbbox()
neighbours()
```

```C#
distance()
```

##### Add

[addpoint()](https://www.sidefx.com/docs/houdini/vex/functions/addpoint.html)
[addprim()](https://www.sidefx.com/docs/houdini/vex/functions/addprim.html)

```C#
addpoint(0, )
addprim(0, "polyline", 0,4); // add a line
addprim(0, "poly", 0,1,5,3); // add a face
```

##### Remove point

```C#
removepoint(0, @ptnum); // will change point # after removal
removeprim();
```

##### Intrinsic attributes
Primitive / Global
![[Houdini-Vector-Expression Language-VEX-img/Intrinsic-attributes.png | 500]]

Retrieve read-only intrinsic attribute

[primintrinsic()](https://www.sidefx.com/docs/houdini/vex/functions/primintrinsic.html)
[detailintrinsic()](https://www.sidefx.com/docs/houdini/vex/functions/primintrinsic.html)

```C#
primintrinsic()
detailintrinsic()
```

### Logging

`printf("Hello World")`
![[Houdini-Vector-Expression Language-VEX-img/print-hello-world.png]]

疑难杂症
https://www.sidefx.com/forum/topic/58449/?page=1#post-262195
https://www.youtube.com/watch?v=jxW1gDeAKiI

### [Condition](https://www.sidefx.com/docs/houdini/vex/statement.html#if) (If)
Comparison Operator
œ
\>|>=|!=|&&
:-|:-|:-|:-
Greater Than|Greater Than or Equal To|Is Not Equal To|And

<|<=|\=\=|II
:-|:-|:-|:-
Less Than|Less Than or Equal To|Is Equal to|Or


```C#
float yPos = v@P.y;

if () {
    v@Cd.x = 0;
    v@Cd.y = 0;
    v@Cd.z = 1;
}

else{
    v@Cd.x = 1;
    v@Cd.y = 0;
    v@Cd.z = 0;
}

// one line condition, no need { }
if () v@Cd.x = 1;
else v@Cd.x = 0;

// Logical Sets
if (yPos >= 0 && xPos >= 0)
if ( (value < 0.2 || value > 0.8) || (value > 0.4 && value < 0.6) )

// ternary operator
value < 1 ? "yes" ; "no";  

// use return to end process
return
```

##### String comparison

```C#
~= // string match operator

? any one letter "ABXD" ~= "AB?D"; // matched
* any length letters "AB123D" ~= "AB*D"; // matched
[] selected letters "ABCD" or "ABcD" ~= "AB[Cc]D"; // matched

^ exclude 
"AB*D, ^AB[Cc]D" // any AB*D exclude ABCD and ABcD
```
### Function
[length()](https://www.sidefx.com/docs/houdini/vex/functions/length.html)
```C#
// output parameter
export vector

length(vector v); // Returns the distance of the vector or vector4 from the origin.
```

### Loop

##### Foreach

```C#
float sunOfArray = 0;

foreach (float currentLoopValue; myArray) {
    sumOfArray += currentLoopValue;
}
```

##### For

```C#
for (int iteration = 0; iteration < 8; iteration++) {
    sum += 1;
}
```

##### While

```C#
while () { // condition

}
```

![[Houdini-Vector-Expression Language-VEX-img/whileloop.png | 300]]

##### Break & Continue

```C#
for (int i=0; i<10; i++) {
    if (... ) {
        break; // End the loop
    }
}

for (int i=0; i<10; i++) {
    if (... ) {
        continue; // skip the rest of current loop; to next iteration 
    }
}
```

### Implementation Examples

[rand()](https://www.sidefx.com/docs/houdini/vex/functions/rand.html)

```C#
float seed = chf("seed"); // create spare parameter
float randomResult = rand(seed);
```

```C#
rint() // round to closest whole number
```

Probability control by rand

```C#
// in Detail
for(int i=0; i < len(pts); i++) {
    float value = rand(i); // get a random value between 0 and 1
    if (val < threshold) {
      ...        
    }
}
 
threshold = 0.1 // 10% probability
threshold = 0.5 // 50% probability
```

  

Create cone surface

```C#
// in Detail
for(int i=0; i < len(pts); i++) {
    int pt1 = pts[i];
    int pt2 = pts[(i + 1) % len(pts)]; // get point # on looped Geo
    
    int tri = addprim(0, "poly", cpt, pt1, pt2)
}
```


`if (@P.y < 0) @P.y = 0;`

```C#
@P.y = max(@P.y, 0);
```


Force (implement in solver)

```C#
vector gravity = set(0, -0.05, 0);
v@velocity += gravity;
@P += v@velocity;
```

Other Topics:

[[../Houdini Noise]]