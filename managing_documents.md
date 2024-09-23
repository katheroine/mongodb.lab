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
...             login: "pineapple"
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
	"upsertedId" : ObjectId("66f15152134bc0eaaca9c100")
}
> db.user.find();
{ "_id" : ObjectId("66f15133e0d4b8f6440ce96f"), "id" : 1, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66f15133e0d4b8f6440ce970"), "id" : 2, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66f15133e0d4b8f6440ce971"), "id" : 3, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
{ "_id" : ObjectId("66f15152134bc0eaaca9c100"), "login" : "pineapple", "id" : 5 }
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
{ "_id" : ObjectId("66f15133e0d4b8f6440ce96f"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66f15133e0d4b8f6440ce970"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : true }
{ "_id" : ObjectId("66f15133e0d4b8f6440ce971"), "id" : 4, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
{ "_id" : ObjectId("66f15152134bc0eaaca9c100"), "login" : "pineapple", "id" : 6 }
```

#### Update operators

**Fields**

* `$set` - sets the value of a field

**Updating value of the existing field of the existing document**

```
> db.user.updateOne(
...     {
...         login: "carrot"
...     },
...     {
...         $set: {
...             confirmed: false
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.user.find();
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce972"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce973"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : false }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce974"), "id" : 4, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
{ "_id" : ObjectId("66f1599e134bc0eaaca9c12d"), "login" : "pineapple", "id" : 6 }
```

**Adding a new field to the exisiting document**

```
> db.user.updateOne(
...     {
...         login: "pineapple"
...     },
...     {
...         $set: {
...             confirmed: true
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.user.find();
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce972"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce973"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : false }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce974"), "id" : 4, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false }
{ "_id" : ObjectId("66f1599e134bc0eaaca9c12d"), "login" : "pineapple", "id" : 6, "confirmed" : true }
```

**Adding a new field to all documents**

```
> db.user.updateMany(
...     {},
...     {
...         $set: {
...             points: 0
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 4 }
> db.user.find();
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce972"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true, "points" : 0 }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce973"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : false, "points" : 0 }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce974"), "id" : 4, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false, "points" : 0 }
{ "_id" : ObjectId("66f1599e134bc0eaaca9c12d"), "login" : "pineapple", "id" : 6, "confirmed" : true, "points" : 0 }
```

* `$unset` - removes the field from the document

**Removing the field of one document**

```
> db.user.updateOne(
...     {
...         login: "carrot"
...     },
...     {
...         $unset: {
...             points: ""
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.user.find();
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce972"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "confirmed" : true, "points" : 0 }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce973"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ], "confirmed" : false }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce974"), "id" : 4, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "confirmed" : false, "points" : 0 }
{ "_id" : ObjectId("66f1599e134bc0eaaca9c12d"), "login" : "pineapple", "id" : 6, "confirmed" : true, "points" : 0 }
```

**Removing the field of all documents**

```
> db.user.updateMany(
...     {},
...     {
...         $unset: {
...             confirmed: ""
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 4 }
> db.user.find();
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce972"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "points" : 0 }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce973"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ] }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce974"), "id" : 4, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "points" : 0 }
{ "_id" : ObjectId("66f1599e134bc0eaaca9c12d"), "login" : "pineapple", "id" : 6, "points" : 0 }
```

* `$rename` - renames the field

**Renaming the field of one document**

```
> db.user.updateOne(
...     {
...         login: "tigger"
...     },
...     {
...         $rename: {
...             points: "credits"
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.user.find();
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce972"), "id" : 2, "login" : "tigger", "groups" : [ "bloggers", "readers", "hobbysts" ], "credits" : 0 }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce973"), "id" : 3, "login" : "carrot", "groups" : [ "writers", "academics" ] }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce974"), "id" : 4, "login" : "monsterro", "groups" : [ "hobbyst", "readers" ], "points" : 0 }
{ "_id" : ObjectId("66f1599e134bc0eaaca9c12d"), "login" : "pineapple", "id" : 6, "points" : 0 }
```

**Renaming the field of all documents**

```
> db.user.updateMany(
...     {},
...     {
...         $rename: {
...             login: "nick"
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 4 }
>
> db.user.find();
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce972"), "id" : 2, "groups" : [ "bloggers", "readers", "hobbysts" ], "credits" : 0, "nick" : "tigger" }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce973"), "id" : 3, "groups" : [ "writers", "academics" ], "nick" : "carrot" }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce974"), "id" : 4, "groups" : [ "hobbyst", "readers" ], "points" : 0, "nick" : "monsterro" }
{ "_id" : ObjectId("66f1599e134bc0eaaca9c12d"), "id" : 6, "points" : 0, "nick" : "pineapple" }
```

* `$inc` - increments the field value

```
> db.user.updateMany(
...     {},
...     {
...         $inc: {
...             credits: 1,
...             points: 2
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 4 }
> db.user.find();
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce972"), "id" : 2, "groups" : [ "bloggers", "readers", "hobbysts" ], "credits" : 1, "nick" : "tigger", "points" : 2 }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce973"), "id" : 3, "groups" : [ "writers", "academics" ], "nick" : "carrot", "credits" : 1, "points" : 2 }
{ "_id" : ObjectId("66f1599ee0d4b8f6440ce974"), "id" : 4, "groups" : [ "hobbyst", "readers" ], "points" : 2, "nick" : "monsterro", "credits" : 1 }
{ "_id" : ObjectId("66f1599e134bc0eaaca9c12d"), "id" : 6, "points" : 2, "nick" : "pineapple", "credits" : 1 }
```

* `$mul`- multiplies the value of a field by a number

```
> db.user.updateOne(
...     {
...         nick: "monsterro"
...     },
...     {
...         $mul: {
...             points: 3
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.user.find();
{ "_id" : ObjectId("66f19c64e0d4b8f6440ce975"), "id" : 2, "groups" : [ "bloggers", "readers", "hobbysts" ], "credits" : 1, "nick" : "tigger", "points" : 2 }
{ "_id" : ObjectId("66f19c64e0d4b8f6440ce976"), "id" : 3, "groups" : [ "writers", "academics" ], "nick" : "carrot", "credits" : 1, "points" : 2 }
{ "_id" : ObjectId("66f19c64e0d4b8f6440ce977"), "id" : 4, "groups" : [ "hobbyst", "readers" ], "points" : 6, "nick" : "monsterro", "credits" : 1 }
{ "_id" : ObjectId("66f19c64134bc0eaaca9c1bc"), "id" : 6, "points" : 2, "nick" : "pineapple", "credits" : 1 }
```

* `min` - updates the value of the field to a specified value if the specified value is less than the current value of the field

```
> db.user.updateOne(
...     {
...         nick: "monsterro"
...     },
...     {
...         $min: {
...             points: 7
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 0 }
> db.user.find({nick: "monsterro"});
{ "_id" : ObjectId("66f19c64e0d4b8f6440ce977"), "id" : 4, "groups" : [ "hobbyst", "readers" ], "points" : 6, "nick" : "monsterro", "credits" : 1 }
```

```
> db.user.updateOne(
...     {
...         nick: "monsterro"
...     },
...     {
...         $min: {
...             points: 5
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.user.find({nick: "monsterro"});
{ "_id" : ObjectId("66f19c64e0d4b8f6440ce977"), "id" : 4, "groups" : [ "hobbyst", "readers" ], "points" : 5, "nick" : "monsterro", "credits" : 1 }
```

* `max` - updates the value of the field to a specified value if the specified value is greater than the current value of the field

```
> db.user.updateOne(
...     {
...         nick: "monsterro"
...     },
...     {
...         $max: {
...             credits: 1
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 0 }
> db.user.find({nick: "monsterro"});
{ "_id" : ObjectId("66f19c64e0d4b8f6440ce977"), "id" : 4, "groups" : [ "hobbyst", "readers" ], "points" : 5, "nick" : "monsterro", "credits" : 1 }
```

```
> db.user.updateOne(
...     {
...         nick: "monsterro"
...     },
...     {
...         $max: {
...             credits: 2
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.user.find({nick: "monsterro"});
{ "_id" : ObjectId("66f19c64e0d4b8f6440ce977"), "id" : 4, "groups" : [ "hobbyst", "readers" ], "points" : 5, "nick" : "monsterro", "credits" : 2 }
```

* `$currentDate` - sets the field value to the current date

```
> db.user.updateMany(
...     {},
...     {
...         $currentDate: {
...             updated_at: {
...                 $type: "timestamp"
...             },
...             last_access: {
...                 $type: "date"
...             }
...         }
...     }
... );
{ "acknowledged" : true, "matchedCount" : 4, "modifiedCount" : 4 }
> db.user.find().pretty();
{
	"_id" : ObjectId("66f19c64e0d4b8f6440ce975"),
	"id" : 2,
	"groups" : [
		"bloggers",
		"readers",
		"hobbysts"
	],
	"credits" : 1,
	"nick" : "tigger",
	"points" : 2,
	"last_access" : ISODate("2024-09-23T18:10:12.655Z"),
	"updated_at" : Timestamp(1727115012, 1)
}
{
	"_id" : ObjectId("66f19c64e0d4b8f6440ce976"),
	"id" : 3,
	"groups" : [
		"writers",
		"academics"
	],
	"nick" : "carrot",
	"credits" : 1,
	"points" : 2,
	"last_access" : ISODate("2024-09-23T18:10:12.655Z"),
	"updated_at" : Timestamp(1727115012, 2)
}
{
	"_id" : ObjectId("66f19c64e0d4b8f6440ce977"),
	"id" : 4,
	"groups" : [
		"hobbyst",
		"readers"
	],
	"points" : 5,
	"nick" : "monsterro",
	"credits" : 2,
	"last_access" : ISODate("2024-09-23T18:10:12.655Z"),
	"updated_at" : Timestamp(1727115012, 3)
}
{
	"_id" : ObjectId("66f19c64134bc0eaaca9c1bc"),
	"id" : 6,
	"points" : 2,
	"nick" : "pineapple",
	"credits" : 1,
	"last_access" : ISODate("2024-09-23T18:10:12.655Z"),
	"updated_at" : Timestamp(1727115012, 4)
}
```

**Array**

* `$addToSet`: Adds distinct elements to an array
* `$pop`: Removes the first or last element of an array
* `$pull`: Removes all elements from an array that match the query
* `$push`: Adds an element to an array

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
