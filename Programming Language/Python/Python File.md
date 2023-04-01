[[Python CSV]]

Modes:
1.  “ r “, for **reading**.
2.  “ w “, for writing.
3.  “ a “, for appending.
4.  “ r+ “, for both **reading** and writing.

Rb, reading binary (image)

Wb, write binary (image)

Simple open a file

```Python
f = open('test.txt','r') # file path, mode 
    # do something
f.close()
```

Use context manager

```Python
with open('test.txt','r') as f:
    # do something 
# Automatically close the file
```

```Python
f.read() # read all, need seek(0) to reset
f.read(100) # read first 100 letters

f.readable() 

f.readlines() # get a list of lines
f.readline() # get first line
for line in f:
    print(line, end='')

f.tell() # current position
f.seek() # set current position offset

f.mode
f.name
f.closed # return if f is closed
```

```Python
with open('test.txt','r') as f:
    size_to_read = 10
    f_contents = f.read(size_to_read)
    
    #print content
    while len(f_contnets) > 0;
        print(f_contents, end='*')
        f_contents = f.read(size_to_read)
    
    while len(f_contents)
```


##### Read File

```Python
employee_file = open("employees.txt", "r")

print(employee_file.readable()) # return Boolean True or False

filePath = getFiles().get('theARKitJsonPath')        
_file = open(filePath, "r")        
arkitData = json.load(_file)         

employee_file.close()
```

##### Write File

```Python
with open(targetArtistJsonPath, 'w') as fp:        
    fp.write(strData)

fp.close()
```
