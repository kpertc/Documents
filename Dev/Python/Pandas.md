#python #data 

[[Jupyter Notebook]]


Use Jupyter Notebook or Google Colab

```Python
import pandas as pd
df = pd.read_csv('xxx/xxx.csv')
```

![[pandas-intro.png]]

```Python
# df.shape returns (rows, columns)
df.shape # (3000, 9)
```

```python
# read csv line by line
import json
df = pd.read_csv('xxx/xxx.csv')

# iterrows() boxes each row into a Series (mixed dtypes upcast to object) and is slow
# itertuples() is much faster, vectorized column ops beat both
for index, row in df.iterrows():  
    # print(row)  
    print(row["text"])  
    # CSV can not round-trip a list, row["embedding"] comes back as a str
    print(json.loads(row["embedding"]))
```

store embeddings as `.parquet` / `.npy`, not CSV