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

### Deleting documents

**`db.<collection>.deleteOne(<document_contition>)`**

If many documents mets the condition, there will be removed the first of them.

**Deleting single document**

```
> db.user.deleteOne({"id": 3});
{ "acknowledged" : true, "deletedCount" : 1 }
> db.user.find();
{ "_id" : ObjectId("66ec4ea150304329da899db4"), "id" : 1, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66ec4ea150304329da899db5"), "id" : 2, "login" : "pumpkin", "groups" : [ "writers", "academics" ], "confirmed" : true }
```

**Deleting multiple documents**

**`db.<collection>.deleteMany(<documents_contition>)`**

To delete all documents in collection, the condition should be empty.

```
> db.user.deleteMany({});
{ "acknowledged" : true, "deletedCount" : 2 }
> db.user.find();
```
