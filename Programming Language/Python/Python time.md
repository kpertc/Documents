#python
### time
``` python
import time

start = time.perf_counter()  # start time
 
def do_something():  
    time.sleep(1)  
  
do_something()  

end = time.perf_counter()  # end time
  
print ( round(end - start, 2)) # duration
```

### Datetime

```Python
from datetime import date

date(2016, 7, 24) #2016-7-24 
```