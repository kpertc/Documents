Reading, writing file: [[Python File]]

### OS Module

##### Working directory

```Python
os.getcwd() # get current working directory
os.chdir('') # change directory
```

##### Create folder / directory

```Python
os.mkdir("folder") # 
os.makedirs("folder/sub-folder") # create multiple level of dir
```

##### Delete folder / directory

```Python
os.rmdir() # only for empty dir
os.removedirs()


os.remove() # only for files

s
import shutil
shutil.rmtree('/path/to/your/dir/')

```

##### listdir

```Python
os.listdir() # get list of all files in the directory

# get all .hdr files in the dir
for _file in os.listdir(HDRFolder):
        if _file.endswith('.hdr'):
```

##### Path

```Python
os.path.isfile() # check file exist, return T or F
os.path.exists() # check directory exist, return T or F
os.path.join() # join path

os.path.basename('/tmp/test.txt') # test.txt 
os.path.splitext('/tmp/test.txt') # ('/tmp/test', '.txt') -split extension

os.path.split('/tmp/test.txt') # ('/tmp', 'test.txt')

os.path.dirname('/tmp/test.txt') # /tmp -directory name
```

##### Rename

```C#
os.rename('','')
```

##### os.stat()

```Python
from datatime import datatime

# from timestamp
mod_time = os.stat
```

###### Time of last modification

```Python
os.chdir('/Users/coreyschafer/Desktop/')

mod_time = os.stat('demo.txt').st_mtime # Time of last modification.
print(datetime.fromtimestamp(mod_time))
```

  
##### os.walk()
go thru all files

```Python
for dirpath, dirnames, filenames in os.walk('/Users')
```

##### os.environ

```Python
os.environ
os.environ.get('HOME')
```

<br/>

### Reading Writing Files

###### Read / Load JSON

```Python
import json
# string to dict
json.load(_file)
# dict to string
json.dumps( dictData )
```