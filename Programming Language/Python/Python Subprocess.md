#python 

[Python Tutorial: Calling External Commands Using the Subprocess Module by Corey Schafer](https://youtu.be/2Fp1N6dof0Y?si=VhYhEXaY1rBKIikW)

```python
import subprocess
```

``` python
subprocess.run('ls')
subprocess.run('ls', shell=True) # shell = True for windows ?
```

### `shell=True`
```python
subprocess.run(['ls', '-la']) # can not input string
subprocess.run('ls -la', shell=True)
```

``` python
p1 = subprocess.run(['ls', '-la'])

print(p1.args) # return command: ['ls', '-la']
print(p1.returncode) # return returncode: 0
```

### get output
```python
# will not output to console
p1 = subprocess.run(['ls', '-la'], capture_output=True)
p1 = subprocess.run(['ls', '-la'], stdout=subprocess.PIPE) # same

# error message
p1 = subprocess.run(['ls', '-la'], stderr=subprocess.DEVNULL) # ignore errors

# get byte output
print(p1.stdout) # get output in byte by stdout → standard out

# Get text ouput
# 1 → decode()
print(p1.stdout.decode())

# 2 → text=True
p1 = subprocess.run(['ls', '-la'], capture_output=True, text=True)
print(p1.stdout)

# write output to file
with open('output.txt', 'w') as f:
	p1 = subprocess.run(['ls', '-la'], stdout=f, text=True)
```

### Command Error
```python
p1 = subprocess.run(['ls', '-la', 'dne']) # an error command
print(p1.returncode) # 1 (non-zero return code)
print(p1.stderr) # ls: dne: No such file or directory

if p1.returncode != 0:
	# do something

# check=True → Stop execution
p1 = subprocess.run(['ls', '-la', 'dne'], check=True)
```



```python
pl = subprocess.run('cat test.txt' capture_output=True,_text=True, shell=True)

# use result from another process
subprocess.run(['grep', '-n', 'test'], capture_output=True, text=True, input=p1.stdout)
```