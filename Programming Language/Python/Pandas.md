#python #data 

[[../../Software & Tool/Jupyter Notebook]]


Use Jupyter Notebook or Google Collab

```Python
import pandas as pd
df = pd.read_csv('xxx/xxx.csv')
```

![[pandas-intro.png]]

```Python
return (Row, Column)
df.shape # (3000, 9)
```

```python
# read csv line by line
df = pd.read_csv('xxx/xxx.csv')

for index, row in df.iterrows():  
    # print(row)  
    print(row["text"])  
    print(row["embedding"])
```