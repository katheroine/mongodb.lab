[⌂ Home](../../README.md)
[▲ Previous: Managing collections](managing_collections.md)

## Managing documents

### Inserting documents

**Inserting single document**

**`db.<collection>.insertOne(<document>)`**

```
> db.medium_type.insertOne({
...     "codename": "BOOK",
...     "description": "A book"
... });
{
	"acknowledged" : true,
	"insertedId" : ObjectId("66ec3cf0dc5bbdfcbff2de02")
}
> db.medium_type.find();
{ "_id" : ObjectId("66ec3cf0dc5bbdfcbff2de02"), "codename" : "BOOK", "description" : "A book" }
```

**Inserting multiple documents**

**`db.<collection>.inserMany(<documents>)`**

```
> db.user.insertMany([
...     {
...         "id": 1,
...         "login": "tigger",
...         "groups": [
...             "bloggers",
...             "readers",
...             "hobbysts"
...         ],
...         "confirmed": true
...     },
...     {
...         "id": 2,
...         "login": "pumpkin",
...         "groups": [
...             "writers",
...             "academics"
...         ],
...         "confirmed": true
...     },
...     {
...         "id": 3,
...         "login": "monsterro",
...         "groups": [
...             "hobbyst",
...             "readers"
...         ],
...         "confirmed": false
...     }
... ]);
{
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("66ec4ea150304329da899db4"),
		ObjectId("66ec4ea150304329da899db5"),
		ObjectId("66ec4ea150304329da899db6")
	]
}
> db.user.find();
{ "_id" : ObjectId("66ec4ea150304329da899db4"), "id" : 1, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66ec4ea150304329da899db5"), "id" : 2, "login" : "pumpkin", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66ec4ea150304329da899db6"), "id" : 3, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
```

### Updating documents

**Updating single document**

**`db.<collection>.updateOne(<document_contition>, <changes>)`**

If many documents mets the condition, there will be updated only first of them.

```
> db.user.updateOne(
...     {
...         "login": "pumpkin"
...     },
...     {
...         $set: {
...             "login": "carrot"
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.user.find();
{ "_id" : ObjectId("66eda56150304329da899db7"), "id" : 1, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66eda56150304329da899db8"), "id" : 2, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66eda56150304329da899db9"), "id" : 3, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
```

*Upsert*

If the document with the given condition cannot be found, it can be created instead of updated. It requires using the `upsert` flag argument.

```
> db.user.updateOne(
...     {
...         "login": "pinecone"
...     },
...     {
...         $set: {
...             "id": 4,
...             "login": "carrot"
...         }
...     },
...     {
...         upsert: true
...     }
... );
{
	"acknowledged" : true,
	"matchedCount" : 0,
	"modifiedCount" : 0,
	"upsertedId" : ObjectId("66edbeae75c384a01106c501")
}
> db.user.find();
{ "_id" : ObjectId("66eda56150304329da899db7"), "id" : 1, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66eda56150304329da899db8"), "id" : 2, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66eda56150304329da899db9"), "id" : 3, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
{ "_id" : ObjectId("66edbeae75c384a01106c501"), "login" : "carrot", "id" : 4 }
```

**Updating multiple documents**

**`db.<collection>.updateMany(<documents_contition>, <changes>)`**

```
> db.user.updateMany(
...     {},
...     {
...         $inc: {
...             "id": 1
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 3 }
> db.user.find();
{ "_id" : ObjectId("66eda56150304329da899db7"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66eda56150304329da899db8"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66eda56150304329da899db9"), "id" : 4, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
{ "_id" : ObjectId("66edbeae75c384a01106c501"), "login" : "carrot", "id" : 5 }
```

### Deleting documents

**Deleting single document**

**`db.<collection>.deleteOne(<document_contition>)`**

If many documents mets the condition, there will be deleted only first of them.

```
> db.user.deleteOne({"id": 4});
{ "acknowledged" : true, "deletedCount" : 1 }
> db.user.find();
{ "_id" : ObjectId("66eda56150304329da899db7"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66eda56150304329da899db8"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66edbeae75c384a01106c501"), "login" : "carrot", "id" : 5 }
```

**Deleting multiple documents**

**`db.<collection>.deleteMany(<documents_contition>)`**

To delete all documents in collection, the condition should be empty.

```
> db.user.deleteMany({});
{ "acknowledged" : true, "deletedCount" : 3 }
> db.user.find();
```
