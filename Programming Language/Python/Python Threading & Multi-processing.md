#python 

# Threading
### Basic Threading
```python
import threading
import time

def do_something():
	time.sleep(1)
	print("111")

t1 = threading.Thread(target=do_something) # target -> function to execute
t1 = threading.Thread(target=do_something, args=[1.5]) # pass arguments as list

t1.start()
```

```python
t1.join() # complete at here

# join multiple threads

threads = []

for _ in range(10):
	t = threading.Thread(target=do_something)
	t.start()
	threads.append(t)

for thread in threads:
	thread.join()
```
### thread pool executor
python 3.2

```python
import concurrent.futures
```

```python
with concurrent.futures.ThreadPoolExecutor() as executor:
	# schedule future object -> can be check isRunning, complete, result
	f1 = executor.submit(do_something, 1)
	print(f1.result()) # print return
```

```python
with concurrent.futures.ThreadPoolExecutor() as executor:
	# schedule future object -> can be check isRunning, complete, result
	f1 = executor.submit(do_something, 1)
	print(f1.result()) # print return
```

```python
with concurrent.futures.ThreadPoolExecutor() as executor:
	secs = [5, 4, 3, 2, 1]

	### 1
	
	results = [executor.submit(do_something, sec) for sec in secs]
	
	for f in concurrent.futures.as_completed(results): # time order
		print(f.result())

	### 2

	results = executor.map(do_something, secs) # first in first out order

	for result in results:
		print(result)
```


---

# Multi-processing

```python
import multiprocessing
```

```python
import time

def do_something():
	print("start")
	time.sleep(1)
	print("end")

if __name__ == '__main__':
	p1 = multiprocessing.Process(target=do_something)
	
	# arguments
	p1 = multiprocessing.Process(target=do_something, args=[arg1, arg2])
	
	p1.start()
	# p1.join() # wait p1 to end, then execute next command
	print('do something later')
```

```python
processes = []

for _ in range(10):
	p = multiprocessing.Process(target=do_something)
	p.start()
	processes.append(p)

for process in processes:
	process.join()
```


### Process Pool Executor

```python
import concurrent.futures
# no need to import multiprocessing
```

``` python
# context manager
with concurrent.futures.ProcessPoolExecutor() as executor:
	f1 = executor.submit(do_something, 1) # argument
	print(f1.result())



```