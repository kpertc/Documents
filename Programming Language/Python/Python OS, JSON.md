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
os.path.isdir() # check directory exist, return T or F
os.path.exists() # file OR directory exist
os.path.join() # join path

os.path.basename('/tmp/test.txt') # test.txt 
os.path.splitext('/tmp/test.txt') # ('/tmp/test', '.txt') -split extension

os.path.split('/tmp/test.txt') # ('/tmp', 'test.txt')

os.path.dirname('/tmp/test.txt') # /tmp -directory name
```

##### Rename

```Python
os.rename('','') # os.replace() -> atomic overwrite, cross-platform
```

##### os.stat()

###### Time of last modification

```Python
from datetime import datetime

os.chdir('/Users/coreyschafer/Desktop/')

mod_time = os.stat('demo.txt').st_mtime # Time of last modification.
print(datetime.fromtimestamp(mod_time))
```

  
##### os.walk()
go thru all files

```Python
for dirpath, dirnames, filenames in os.walk('/Users'):
	# filenames are bare names, join with dirpath
	...
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
json.load(_file) # file -> dict
json.loads(_str) # string -> dict ("s" = string)
json.dump(dictData, _file) # dict -> file
json.dumps(dictData) # dict -> string
```