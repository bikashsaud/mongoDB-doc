# mongoDB-doc

## MongoDB

#### What is MongoDB?
```
- Database
-  Features:
    - High performance
    - High Availability
    - Easy Saclability
    
```
#### Collection
```commandline
- Collection is group of MongoDB Documents.
- Equivalent ti RDBMS
- Collection exist in same Documents
- Document in collection have different fields
- 
```

#### Documents

```commandline
- Set  of key value pair
- Have dynamic schemas.
- 
```
## MongoDB

#### What is MongoDB?
```
- Database
-  Features:
    - High performance
    - High Availability
    - Easy Saclability
    
```
#### Collection
```commandline
- Collection is group of MongoDB Documents.
- Equivalent ti RDBMS
- Collection exist in same Documents
- Document in collection have different fields
- 
```

#### Documents

```commandline
- Set  of key value pair
- Have dynamic schemas.
- it store different type of data
- It is like one row or object of tany table(collection).
- Field in MongoDB is like one column
```
![](../../../../../Pictures/Screenshot from 2022-10-08 09-00-55.png)

#### Field (_id)
```commandline
- Unique identifier
- Default by mongo db
- facility to give you also
- Created in following structire
- Total bytes = 12
    - $ bytes current timestamp
    - next3 bytes for machine id
    - next 2 bytes is for MongoDB server
    - last 3 bytes for increammental value
     
```
#### MongoDB vs Relational DB
```commandline
No relationship concept in MongoDB but concept is in RDBMS. 
```
#### Installation
```commandline
https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-20-04
```

#### Considerations while design Schema in MongoDB
```commandline
- design as user requirements
- combile object if they used togather
- Duplicate the data is perfer if computation time is reduceing
- join while write not in read
- optimize schema in case of frequent uses
- do complex aggregation in the schema.

```

#### Terminal
- goto mongoDB terminal enter
```commandline
mongo
```

#### Create DB
```commandline
use <db_name>
```
- current db use : ```db```
- 
- Show list of dbs : ```show dbs``` # Note that until you not create document it cannot show in db list.
## For more CRUD Operations follow link:
```https://www.mongodb.com/docs/manual/crud/#std-label-crud```

### 1. Create Operations

- create document : ```db.<doc_name>.insert({key: value})```
- eg : ```db.post.insert({key:})```
- delete db :
1. switch database: ```use <dbname>```
2. db.dropDatabase()
3. check listof db ```show dbs```
Examples:
```commandline
db.post.insert({"title" : "Post 2","likes" : 1332,"dislikes" : 12,"comments" : ["Nice wow 2!!!","Looking Beautiful2.","Not satisfied."] } )
db.post.insert({"title" : "Post 3","likes" : 232,"dislikes" : 21,"comments" : ["Nice wow 3!!!","Looking Beautiful3.","Not satisfied3."] } )

```
### 2. Find or gET Operation
1. ```find()```
 -```db.collection_name.find()```
 - ```db.collection_name.find().pretty()``` # to show pretty results.
2. ```findOne()  ``` 
3. filters
![](../../../../../Pictures/Screenshot from 2022-10-08 10-23-26.png)

- Equal Case
```  db.post.find({"title": "Post 1"}).pretty()
```
- For less than for integer values, you can use mostly
- ``` db.post.find({" likes":{$lt:200} }).pretty()```

- For more than integer values, you can use integer values
``` db.post.find({" likes":{$gt:200} }).pretty()```
- For more than or equal t0 integer values, you can use integer values
``` db.post.find({" likes":{$gte:200} }).pretty()```
- in shorts
```commandline
- {$gte:200} = greater than equal to
- {$gt:200} = greater than
- {$lte:200} = less than equal to
- {$lt:200} = less than
- equal = {key:value}
- {$ne:200} = not equal to
- 
```
#### AND operator

- find() : in this, if you use " , "  Mongo treats it as AND operator
- eg 
```commandline
db.post.find(
  {
    $AND:[{k1:v1}, {k2:v2}, {"likes":{$gt:30}}]
  }
)
```
#### OR operator
- find() : in this OR, is used as $or in Mongo- eg 
```commandline
db.post.find(
  {
    $or:[{"dislikes":{$lt:5}}, {"likes":{$gt:100}}}]
  }
).pritty()

- Example follows
 db.post.find({$or:[{"dislikes":{$lt:5}}, {" likes":{$gt:100}}]}).pretty()
{
        "_id" : ObjectId("6340fe25720fd8563dc3143c"),
        "title" : "Post 1",
        " likes" : 120,
        "dislikes" : 12,
        "comments" : [
                "Nice wow!!!",
                "Looking Beautiful.",
                "Not satisfied."
        ]
}

--------------------------------
> db.post.find({})
{ "_id" : ObjectId("6340fe25720fd8563dc3143c"), "title" : "Post 1", " likes" : 120, "dislikes" : 12, "comments" : [ "Nice wow!!!", "Looking Beautiful.", "Not satisfied." ], "likes" : 130 }
{ "_id" : ObjectId("63414a67720fd8563dc3143d"), "title" : "Post 2", "likes" : 1332, "dislikes" : 12, "comments" : [ "Nice wow 2!!!", "Looking Beautiful2.", "Not satisfied." ] }
--------------------------------------------------------
```

### 3. Update Documents

- by default update single document 
```db.post.update({"title": "Post 1"}, {$set: {"likes": 130}})```

- multi: true if you want oto changes multiple document once
- ```db.post.update({"title": "Post 1"}, {$set: {"likes": 130}}, {'multi': true})```


### Delete Documents

- remove() methods to remove data from collection
- two parameters 
  - deletion criteria 
  - justOne parameter flag - to delete only one document
  - 
```
db.post.remove({"title": "Post 1"})
WriteResult({ "nRemoved" : 1 })
```

### Projection 
- Selecting only required data rather than selecting all
- use find() method to select only required data. for this use 1 for show data of field else use 0
- eg
- 
```commandline
db.post.find({}--> this means select all data,{"title":1} )

to exclude
db.post.find({}--> this means select all data,{"title":0} )

db.post.find({},{title:1})
{ "_id" : ObjectId("63414a67720fd8563dc3143d"), "title" : "Post 2" }
{ "_id" : ObjectId("63414a87720fd8563dc3143e"), "title" : "Post 3" }

```

### Limit Methods
- Use limit() method
- set only limited number of data show
- ```db.COLLECTION_NAME.fond().limit(MAX_NUMBER_TO_SHOW)```
```commandline
 db.post.find().limit(1)
{ "_id" : ObjectId("63414a67720fd8563dc3143d"), "title" : "Post 2", "likes" : 1332, "dislikes" : 12, "comments" : [ "Nice wow 2!!!", "Looking Beautiful2.", "Not satisfied." ] }
 
 db.post.find({},{"title":1}).limit(1)
{ "_id" : ObjectId("63414a67720fd8563dc3143d"), "title" : "Post 2" }

```

### Sort

- to sort to specific order
- sort() method
- sort(1) = ascending order
- sort(-1) = descending order
- eg
```commandline

> db.post.find().sort({"likes": -1})
{ "_id" : ObjectId("63414a67720fd8563dc3143d"), "title" : "Post 2", "likes" : 1332, "dislikes" : 12, "comments" : [ "Nice wow 2!!!", "Looking Beautiful2.", "Not satisfied." ] }
{ "_id" : ObjectId("63414a87720fd8563dc3143e"), "title" : "Post 3", "likes" : 232, "dislikes" : 21, "comments" : [ "Nice wow 3!!!", "Looking Beautiful3.", "Not satisfied3." ]
```
