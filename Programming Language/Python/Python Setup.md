### Install Packages

```bash
# Check version or installed
python --version
python3 --version
Python 3.10.2

# return path
which python3

type python3
```

check version in Python
```python
import sys
import platform

print(sys.version)
```

```shell
# _PATH_ is an environment variable that allows the system to specifically find various executables by pointing them to the right directory.

echo $PATH

# paths are separated by :
# will use the first found path
/Users/USERNAME/.nvm/versions/node/v16.14.2/bin:
/Library/Frameworks/Python.framework/Versions/3.10/bin:
/usr/local/bin: # /usr/local/bin/python3 run Python fron this dir
/System/Cryptexes/App/usr/bin:
/usr/bin:
/bin:
/usr/sbin:
/sbin:
...


```

```
Requests
python -m pip install requests
```



```
# Setting PATH for python 3.7
PATH="/Library/Frameworks/Python.framework/versions/3.7/bin:${PATH}"
export PATH
```

```shell
# set alias
alias python="python3"
alias pip=pip3
```

.bash_profile



> [!NOTE] `python` instead of `python3` in terminal
> `python` instead of `python3` in terminal
>
> https://stackoverflow.com/posts/43354447/timeline
>
>The simplest way would be to add an alias to `python3` to always point to the native `python` installed. Add this line to the `.bash_profile` file in your `$HOME` directory at the last,
>
>```bash
>alias python="python3"
>```


Switch Python interpreter in VSCode

![[Visual Studio Code (VSCode)#Python]]


