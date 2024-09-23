[⌂ Home](../../README.md)
[▲ Previous: Managing collections](managing_collections.md)

## Managing documents

### Inserting documents

**Inserting single document**

**`db.<collection>.insertOne(<document>)`**

```
> db.medium_type.insertOne({
...     codename: "BOOK",
...     description: "A book"
... });
{
	"acknowledged" : true,
	"insertedId" : ObjectId("66f145f9e0d4b8f6440ce968")
}
> db.medium_type.find();
{ "_id" : ObjectId("66f145f9e0d4b8f6440ce968"), "codename" : "BOOK", "description" : "A book" }
```

**Inserting multiple documents**

**`db.<collection>.inserMany(<documents>)`**

```
> db.user.insertMany([
...     {
...         id: 1,
...         login: "tigger",
...         groups: [
...             "bloggers",
...             "readers",
...             "hobbysts"
...         ],
...         confirmed: true
...     },
...     {
...         id: 2,
...         login: "pumpkin",
...         groups: [
...             "writers",
...             "academics"
...         ],
...         confirmed: true
...     },
...     {
...         id: 3,
...         login: "monsterro",
...         groups: [
...             "hobbyst",
...             "readers"
...         ],
...         confirmed: false
...     }
... ]);
{
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("66f1462ae0d4b8f6440ce969"),
		ObjectId("66f1462ae0d4b8f6440ce96a"),
		ObjectId("66f1462ae0d4b8f6440ce96b")
	]
}
> db.user.find();
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce969"), "id" : 1, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce96a"), "id" : 2, "login" : "pumpkin", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce96b"), "id" : 3, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
```

### Updating documents

**Updating single document**

**`db.<collection>.updateOne(<document_contition>, <changes>)`**

If many documents mets the condition, there will be updated only first of them.

```
> db.user.updateOne(
...     {
...         login: "pumpkin"
...     },
...     {
...         $set: {
...             login: "carrot"
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.user.find();
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce969"), "id" : 1, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce96a"), "id" : 2, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce96b"), "id" : 3, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
```

*Upsert*

If the document with the given condition cannot be found, it can be created instead of updated. It requires using the `upsert` flag argument.

```
> db.user.updateOne(
...     {
...         login: "pinecone"
...     },
...     {
...         $set: {
...             id: 5,
...             login: "carrot"
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
	"upsertedId" : ObjectId("66f1473b134bc0eaaca9c0c4")
}
> db.user.find();
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce969"), "id" : 1, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce96a"), "id" : 2, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce96b"), "id" : 3, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
{ "_id" : ObjectId("66f1473b134bc0eaaca9c0c4"), "login" : "carrot", "id" : 5 }
```

**Updating multiple documents**

**`db.<collection>.updateMany(<documents_contition>, <changes>)`**

```
> db.user.updateMany(
...     {},
...     {
...         $inc: {
...             id: 1
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 4 }
> db.user.find();
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce969"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce96a"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce96b"), "id" : 4, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
{ "_id" : ObjectId("66f1473b134bc0eaaca9c0c4"), "login" : "carrot", "id" : 6 }
```

### Deleting documents

**Deleting single document**

**`db.<collection>.deleteOne(<document_contition>)`**

If many documents mets the condition, there will be deleted only first of them.

```
> db.user.deleteOne({id: 4});
{ "acknowledged" : true, "deletedCount" : 1 }
> db.user.find();
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce969"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66f1462ae0d4b8f6440ce96a"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66f1473b134bc0eaaca9c0c4"), "login" : "carrot", "id" : 6 }
```

**Deleting multiple documents**

**`db.<collection>.deleteMany(<documents_contition>)`**

To delete all documents in collection, the condition should be empty.

```
> db.user.deleteMany({});
{ "acknowledged" : true, "deletedCount" : 3 }
> db.user.find();
```
