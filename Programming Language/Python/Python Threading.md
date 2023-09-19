#python 

multi-processing

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

python 3.2
thread pool executor

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


