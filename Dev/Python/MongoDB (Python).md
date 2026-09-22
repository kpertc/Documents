#python #data 


### Official Websites:

[Official Website](https://www.mongodb.com/)
[PyMongo Documentation](https://pymongo.readthedocs.io/en/stable/)

### Tutorial:

[YouTube - Tech with Tim](https://www.youtube.com/watch?v=rE_bJl2GAY8&t=15s)
[W3School Python MongoDB](https://www.w3schools.com/python/python_mongodb_insert.asp)

  

### About MongoDB

MonogDB is a "Not-Only-SQL" "Non-Relational" Database
storing info by using Json-like document (BSON)


### Use MongoDB with [mongosh (MongoDB Shell)](https://www.mongodb.com/docs/mongodb-shell/)
旧的 `mongo` shell 在 5.0 弃用、6.0 移除

  

### Two ways to use MongoDB with Python

1.  ##### **Online -> Create a free account and create a cluster**
	![[create-account-1.png]]|![[create-account-2.png]]|![[create-account-3.png]]
	---|---|---    
  

2.  ##### **Local ->** **[Community Server](https://www.mongodb.com/try/download/community)**
	or [mac install](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/) -> [Homebrew](https://brew.sh/)

  

### Mongo DB Python

[Mongo Python Driver](https://www.mongodb.com/docs/drivers/python/)

install `pymongo` (dnspython 自 PyMongo 4.0 起已是硬依赖，不用单独装)

```Python
from pymongo import MongoClient

client = MongoClient("mongodb+srv://<user>:<password>@<cluster>.mongodb.net/")
db = client["dbname"]
col = db["collname"]

col.insert_one({"name": "John", "age": 30})
col.find_one({"name": "John"})
```