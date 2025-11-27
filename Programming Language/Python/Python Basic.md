#python #programming-language 

Related Package
[[Math]]
[[random]]

[[Python OS, JSON]]
[[Python File]]
[[Python CSV]]
[[Python time]]
[[Python Requests]]

[[Matplotlib]]
[[Pandas]]

[[PyCharm]]

# Basics

### Python Built-in Functions

https://docs.python.org/zh-cn/3.10/library/functions.html?highlight=dir

### Hello World

```python
print("Hello, World!")

#New line
\n

'''
Comment
Multiple
Lines
'''
```

### Print

```python
print ( '', sep = ' ' ) # each seperated by ' ' space
print ( '', end = ' ' ) # overwrite end with new line
```

### Creating Variable

```python
myVariable = 0
myVariable = 0.111
myVariable = “string”
isVariable = True
isVariable = False
```

### String

```python
print ("Hello\nWorld") #new line
print ("hello\"world") #quotation Mark

phrase = "Hello World"
print (phrase.lower()) #all lower case
print (phrase.upper()) #all upper case

print (phrase.islower()) #check if is all lower return True or False
print (phrase.isupper()) #check if is all upper return True or False

print (phrase.upper().isupper()) #two function togethor

print (len(phrase)) #length of the phrase, character numbers
print (phrase[0]) # H, get the first character
print (phrase.index("hel")) #0 location of the string in the phrase
print (phrase.replace("World","Mars")) #replace

my_num = 5 
print (str(my_num)) #convert int/float to string

string.strip() → remove space at begin and end
lstrip() → begin
rstrip() → end

```

Sting.format and f string

### f string

Require py3.6+

### r string regular Expression

```python
print ('111 \n 111')
#111 
# 111

print (r'111 \n 111') # print out 111 \n 111
```

```python
import re

```

### Numbers

```python
print (10 % 3) #mod remainder

my_num = -5 
print (abs(my_num) #absolute value
print (pow(3,2)) #power, 3^2
print (max(4, 6, 3, 8)) #return the biggest number
print (min(4, 6, 3, 8)) #return the smallest number

print (round(3.2)) #3 四舍五入
print (round(3.5)) #4 四舍五入

from math import * #import more math function
print (floor(3.6)) #3 向下取值
print (ceil(3.2)) #4 向上取值
print (sqrt(36)) #6.0 squareroot 开根

my_string = "123"
int(my_string) #convert string to int
float(my_string) #convert string to int
```

### Input

```python
input() #allow to type something as input
input("Hi input something here") #add text to show
```

### List

-   Access the List

```python
friends = ["Kevin","Karen","Jim"]
print (friends[0]) #Kevin, access the first item
print (friends[-1]) #Jim, access the last item
print (friends[1:]) #Karen, Jim, access all after the first item

friends = ["Kevin","Karen","Jim","Oscar","Toby"] #longer list example
print (friends[1:3]) #Karen, Jim 2-3 (before 4)
print (friends.index("Jim")) #return "Jim"'s index number

friends = ["Kevin","Karen","Jim", "Jim"]
print (friends.count("Jim")) #2 -How many times the item appears

len() #items / length of the list
```

-   Modify the list

```python
friends[1] = "Mike" #modify the second item tto Mike 

friends2 = ["John, Lisa"] #List 2 Example
friends.extend(friends2) #Add another list after 
friends.append("John") #Add another item
friends.insert(1,"Kelly") #insert Kelly to 2nd, items after Kelly +1
friends.remove("Jim") #remove Jim, all items after Jim -1
friends.clear() #remove all items
friends.pop() #remove the last item, "Toby"
friends2 = friends.copy() #copy from other list
```

-   Re-order the list

```python
friends.sort() #put list into an ascending or alphabet order
friends.reverse() #reverse of the order of the list
```

### Tupel

Tupel is Immutalable; can not be changed after it created.

```python
coordinates = (4, 5) # Create Tupel
print (coordinates[1]) #5 Access Tupel Infomation
```

### Function

```python
# def -> "Define"
def say_hi():
    print("Hello")

say_hi() # Call Function
```

```python
def say_hi(name): # Input Variable
    print("Hello " + name)

say_hi("Mike") #Hello Mike
```

Positional argument

```python
def say_hi(name, age): #Two Variable
    print("Hello " + name + "You are: " + str(age))

say_hi("Mike", 70) #Hello MikeYou are: 70
```

##### Optional Parameters

```python
def func(x, text='2'): # text -> optional parameter, has a default value

func('tim')
func('tim', '3') # overwrite text

def testFunc (name1="abc", name2="def"): # keyword argument
testFunc(name2="xyz")
```

```python
*args # all positional arguments
**kwargs # keyword arguments

def my_func(*args, **kwargs):
    print (args, kwargs)
    
my_func("abc", "abc", 123, "abc", key=123, abc=123)
（'abc', 'abc', 123, 'abc'）,{'abc':123, 'key': 123}
```

### Return Statement

```python
def cube(num):
    return num * num * num

print(cube(4)) #return 64
```

Return will break the function, not execute code after it.

### If Statement

https://www.w3schools.com/python/python_conditions.asp

```python
if isRed:
    #Do Something
elif myVariable == 1:
    #Do Something
else:
    #Do Something
    
if isRed or isBlue: #meet one requirment

if isRed and isBlue: #meet both requirment

if not(isBlue) #

if myString == theString #can compare string
```

### Dictionary

```python
monthConversions = {
    "Jan": "January",
    "Feb": "February",
    "Mar": "March",
}

print(monthConversions["Jan"]) #January
print(monthConversions.get("Jan")) #January get will not return error when dictionary not found
print(monthConversions.get("notValid", "message leave to users")) #message leave to users, can leave a string
```

### While Loop

```python
i = 1
while i <= 10:
    print(i)
    i += 1

print("Done with loop")
```

https://www.w3schools.com/python/python_while_loops.asp

### For Loop

```python
#String
for letter in "Giraffe Academy":
    print(letter)
    
#List
friends = ["Jim", "Karen", "Kevin"]
for friend in friends:
    print (friend)
    
for index in range(3, 10): #second will not be included in the range
    print(index) #print 3, 4, 5, 6, 7, 8, 9
    if index == 0:
        print("first Iteration") #show during first iteration
        
for index in range(len(friends)):
    print(friends[index])      
    
    
# For Loop Practice: Exponent Function
def raise_to_power(base_num, pow_num):
    result = 1 #declare variable
    for index in range(pow_num):
        result = result * base_num
    return result
    
print(raise_to_power(3,2))

# has index
for i, BSname in enumerate(GAN_BS):
    print (i)
```

https://www.w3schools.com/python/python_for_loops.asp

##### Comprehensions (List, Set, Dict)
[[YouTube] Python Tutorial: Comprehensions - How they work and why you should be using them by Corey Schafer](https://www.youtube.com/watch?v=3dt4OGnU5sM)
```python
nums = [1,2,3,4,5,6,7,8,9,10] # basic comprehension 
my_list = [n for n in nums]
```

```python
thislist = ["apple", "banana", "cherry"]
[print(x) for x in thislist]

[math.degrees(x) for x in xform_mat.rotation().asVector()]
```

List
```python
# traditional way
my_list = []
for n in nums:
	my_list.append(n*n)

# comprehension
my_list = [n*n for n in nums]
my_list = [n for n in nums if n%2 == 0] # comprehensions with condition

# nested
for letter in 'abcd':
	for num in range(4):
		my_list.append((letter, num))

# comprehension - nested 
my_list = [(letter, num) for letter in 'abcd' for num in range(4)]
```

Dict
```python
# comprehension - return dictionary
my_dict = {name: hero for name, hero in zip (name, heros)}
{"Bruce": "Batman", "Wade": "Deadpool"}
```

Set
```python
nums = [1,1,1,1,2,3,3,3,4,4,5,6,7,8,8,9]
my_set = {n for n in nums} # {1, 2, 3, 4, 5, 6, 7, 8, 9}
```

generator??
```python
my_gen = (n*n for n in nums)

for i in my_gen:
	print(i)
```
### 2D Lists & Nested Loops

```python
number_grid = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9],
    [0]
]

print(number_grid[0][0]) #print 1, access the column 1, row 1 

# Nested loops
for row in number_grid: #access all number in the number_grid
    for col in row:
        print(col)
```

### Translator

```python
def translate(phrase):
    translation = ""
    for letter in phrase:
        if letter in "AEIOUaeiou":
            translation = translation + "g"
        else:
            translation = translation + letter
    return translation

print(translate(input("Enter a phrase: ")))
```

### Sets
> Set is one of 4 built-in data types in Python
> unordered , _unchangeable*_, and _unindexed_.

```python

my_set = set() # create an empty set

numebrs = [1, 1, 2, 3, 4] 
_set = set(numebrs)

print(_set) # {1, 2, 3, 4}

_set.add(5)
_set.remove(5)
len(_set)

# check value exist in the set
if 1 in numebrs:
	print("yes")
```

Math operation 
```python
first = {1, 2, 3, 4}
second = {1, 5}

# union
print(first | second) # {1, 2, 3, 4, 5}

# intersection
print(first & second) # {1}

# different
print(first - second) # {2, 3, 4}

# symmetric_difference
print(first ^ second) # {2, 3, 4, 5}

```
[Mathematical Set Operations in Python by Indhumathy Chelliah](https://betterprogramming.pub/mathematical-set-operations-in-python-e065aac07413)

![[Mathematical Set Operations in Python.webp]]
### Try & Except

```python
try:
    number= int(input("Enter a number: "))
    print(number)

except: #catch all errors
    print("Invalid Input") #show Invalid Input when an error happens
```

```python
try:
    value = 10/0
    number= int(input("Enter a number: "))
    print(number)

except ZeroDivisionError: #catch specific error
    print("Divide by Zero")

except ValueError:
    print("Invalid input")
    
pass # continue
continue # enter next loop
break # stop 
```

```python
try:
    value = 10/0

except ZeroDivisionError as err: #stored error as err
    print(err) #print error
```

### Modules & Pip

```python
import useful_tools

print(useful_tools.roll_dice(10))
print(useful_tools.myInt)
```

### Scope

Local Enclosing Global Built-in

```python
x = 'global x'

def doSomthing()
    global x
    x = 'local x'
    
print x 
#'local x'
```

```python
nonlocal x
x = 'local x'
```

### Class & Object (OOP)

##### Create a class

```python
class Employee:
    pass
```

##### `__init__` , regular, class, static method

##### Property, setter, getter, deleter

```python
class Employee:
    raise_amt = 0.05
    
    def __init__(self, first, last, pay):
        self.first = first
        self.last = last
        self.pay = pay
        
    '''
    '''
     
    def regular_method (self): # will automatically pass instance -> self
        self.variable # self -> edit instance variable
        Student.variable # className -> edit class varible
    
    @classmethod
    def class_method (cls, value): # will automatically pass class -> cls
        cls.raise_amt = value
    
    # class constructor
    @classmethod
    def from_string(cls, emp_str):
        name, major, gpa, is_onprobation = emp_str.split('-')
        return cls(name, major, gpa, is_onprobation) # create a new instance
    
    @staticmethod
    def is_workday(day): # not automatically pass anything
    
    '''
    '''
    
    @property
    def fullname(self):
        return f'{first} {last}'

    @fullname.setter # propertyName.setter
    def fullname(self, name): # need to be the same name
        self.first =
        self.last = 
        
    @fullname.deleter
    def fullname(self):
        print ("Delete Name")
        self.first = None
        self.last = None
    
```

```python
# Execute the class function    
instance.fullname() # instance.function()
Class.fullname(instance) # class.function(instance)
    
# class Method
Class.class_method(value) # no need pass cls that will be pass in automatically

# class Method Constructor
new_employee = Employee.from_string("string")    

# static Method
Employee.is_workday(2)

# property
new_employee.fullname # no need for (), access like attribute
# Setter
new_employee.fullname = "John Smith"
# Deleter
del emp_1.fullname
```

##### Inheritance & super()

```python
class Developer(Employee): # inherit
    raise_amt = 0.05

    def __init__(self, first, last, pay, programming_lang):
        
        super().__init__(first, last, pay) # inherit from Employee's __init__
        Employee.__init__(self, first, last, pay)
        
        self.programming_lang = programming_lang
```

Search order: instance -> class -> built-in

### Decorators

```python
def decorator_function(original_function):
    def wrapper
```

### Building a Multiple Choice Quiz

Question Class

```python
class Question:
    def __init__(self, prompt, answer):
        self.prompt = prompt
        self.answer = answer
```

Main

```python
from Question import Question

question_prompts = [
    "What color are apples?\n(a) Red/Green\n(b) Purple\n(c) Orange\n\n",
    "What color are Bananas?\n(a) Teal\n(b) Magenta\n(c) Yellow\n\n",
    "What color are strawberries?\n(a) Yellow\n(b) Red\n(c) Blue\n\n"
]

questions = [
    Question(question_prompts[0], "a"),
    Question(question_prompts[1], "c"),
    Question(question_prompts[2], "b")
]

def run_test(questions):
    score = 0
    for question in questions:
        answer = input(question.prompt)
        if answer == questions.answer:
            score += 1
    print("You got" + str(score) + "/" + str(len(questions)) + "correct")
```

### [Special (Magic/Dunder) Methods](https://www.youtube.com/watch?v=3ohzBxoFHAY)

`_if_` `__name__ == "__main__"`

If the script directly ran by Python, "__name__" == "__main__"

If the script is imported, "__name__" == the title of the script

```python
str()
repr()
dir()

__str__
__repr__

string.__str__ = str(string)
```

### Other Functions

```python
dir() # list out all the function of the variable
help() # detailed help info

instance.__dict__  # Use __dict__ to print all attribute

isinstance() # print to check if it is an instance
isinstance( instance, className ) # return True or False to tell is instance of the class

issubclass() # print to check if it is a subclass
issubclass(Developer, Employee) 
```

### Type Hint
https://docs.python.org/3/library/typing.html

Python 3.5+
python will ignore "types" at runtime, they are just meta data, only for documentation / readability purpose

```python
from typing import List

def myFunc (array: List, device: str) -> List:
    print(array)
```

``` python
user1: string = "111"
```

``` python
from dataclasses import dataclass

@dataclass
class User:
	name: str
	email: str
	account_id: int
```
##### type checking
check type before runtime
VS code `Mypy Type Checker` extension
[ty - Python type checker](https://docs.astral.sh/ty/)
##### Data Validation
valid data at runtime
``` python
# manual type check
if not isinstance(name, str)
	raise TypeError("name must be a string")
```

use [[Pydantic]]

### zip command
return paired tuples
https://www.w3schools.com/python/ref_func_zip.asp
```python
a = ("John", "Charles", "Mike")  
b = ("Jenny", "Christy", "Monica")  
  
x = zip(a, b) 
# [("John","Jenny"), ("Charles","Christy"), ("Mike", "Monica")]
```

# Intermediate & Advanced

### First Class Functions

### [Lambda](https://www.w3schools.com/python/python_lambda.asp)


### Iterators and Iterables
object has `__iter__ ` → Iterables → return Iterators
has a state that remember where it is, what is next value

```python
nums = [1,2,3]
i_nums = nums.__iter__() # get list_iterator object

# iter(nums)

print(i_nums) # iterator object
print(dir(i_nums)) # its functions

# i_nums.__next__() #
# i_nums.__iter__() # return self

# manually next test
print(i_nums.__next__()) # 1
print(i_nums.__next__()) # 2
print(i_nums.__next__()) # 3
print(i_nums.__next__()) # StopIteration exception
```

custom iterator by custom define `__iter__` and `__next__`
```python
class MyRange:

	def __init__(self, start, end):
		self.value = start
		self.end = end
	
	def __iter__(self):
		return self
	
	def __next__(self):
		if self.value >= self.end:
		raise StopIteration
	
	current = self.value
	self.value += 1
	return current

nums = MyRange(1, 10)

# MyRange is iterable, can be used in for-loop
for num in nums:
	print(num)
```
##### Generator
Generator → iterator → PY 3+ new syntax
```python
def my_range(start, end):
	current = start
	while current < end:
		yield current
		current += 1

nums = my_range(1, 10)

for num in nums:
	print(num)

# 1 2 3 4 5 6 7 8 9

# infinite loop
def my_range(start):
	current = start
	while True:
		yield current
		current += 1
```

![[Asyncio in Python - Full Tutorial 1-56 screenshot.png]]
### Asyncio
python version >= 3.4, for tasks less CPU intense
Event loop
``` python
import asyncio #python build-in

async def main():
	# await keyword only in async function
	await
	
# async function() → return a coroutine object

asyncio.run(main())
```

``` python
async def fake_fetch(delay):
	await asyncio.sleep(delay)
```

Task
``` python

```

### [[Python Threading & Multi-processing]]

### [[Python Subprocess]]
