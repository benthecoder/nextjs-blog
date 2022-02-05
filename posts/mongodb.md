---
title: 'MongoDB notes'
date: '2022-02-05'
---

## Terms

- *Document* - a way to organize and store data as a set of field-value pairs.
- *Field* - a unique identifier for a datapoint.
- *Value* - data related to a given identifier.
- *Collection* - an organized store of documents in MongoDB, usually with common fields between documents. There can be many collections per database and many documents per collection.
- *Replica Set* - a few connected machines that store the same data to ensure that if something happens to one of the machines the data will remain intact. Comes from the word replicate - to copy something.
- *Instance* - a single machine locally or in the cloud, running a certain software, in our case it is the MongoDB database.
- *Cluster* - group of servers that store your data.

## Cheatsheet

```bash
# show all databases
show dbs 

# drop database
db.dropDatabase()

# switching to database
use <db_name>

# show collections in database
show collections


# =====================
# FIND

# return all matches
db.<collection_name>.find( {"key" : "value" } )

# iterate through cursor
it 

# count total matches
db.<collection_name>.find( {"key" : "value" }).count()

# prettify result
db.<collection_name>.find( {"key" : "value" }).pretty()

# limit n result 
db.<collection_name>.find( {"key" : "value" }).limit(n)

# show random 20 result
db.<collection_name>.find()

# show any random one result
db.<collection_name>.findOne({})

# SORT
# 1 is ascending
db.<collection_name>.find().sort({"key": 1 })
# -1 is ascending
db.<collection_name>.find().sort({"key": -1 })

# SELECT
# 1 means only returning "key"
db.<collection_name>.find({"key": 1 })
# 0 means exclude "key"
db.<collection_name>.find({"key": 1 })

# FILTER
# $eq = equal
db.<collection_name>.find({"name": {$eq: "Sally"} })
# $neq = not equal
db.<collection_name>.find({"name": {$neq: "Sally"} })

# $in = in
db.<collection_name>.find({"name": {$in: ["Ben", "Sally"]} })
# $nin = not in
db.<collection_name>.find({"name": {$nin: ["Ben", "Sally"]} })

# $exists
db.<collection_name>.find({"age": {$exists: true} })
db.<collection_name>.find({"age": {$exists: false} })

# greater than / less than
db.<collection_name>.find({"age": {$gte: 20, $lte: 40} })

# AND OR
db.<collection_name>.find({$or: [{"age": {$gte: 20, $lte: 40}}, {"name" : "Kyle"}] })

# NOT
db.<collection_name>.find({ "age" : { $not { $lte : 20 }}})

# Compare two key values
# below compares whether debt is greater than balance
db.<collection_name>.find({$expr : { $gt : ["$debt", "$balance"]} })

# access nested values
db.<collection_name>.find({"address.street" : "123 Main St"})


# count documents
db.<collection_name>.countDocuments(<query>)


# =====================
# UPDATE
db.<collection_name>.updateOne({"age":27}, {$set: {"age" : 28}})



# =====================
# INSERT

# inserting 
db.<collection_name>.insertOne(<Document>)

# insert many
db.<collection_name>.insertMany([<Document>, <Document>, <Document>])
```
