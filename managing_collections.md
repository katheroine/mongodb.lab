[⌂ Home](../../README.md)
[▲ Previous: Managing databases](managing_databases.md)
[▼ Next: Managing documents](managing_documents.md)

## Managing collections

### Displaying collections

```
> show collections
```

### Creating collection

#### Data types

* **String** − This is the most commonly used datatype to store the data. String in MongoDB must be UTF-8 valid.
* **Integer** − This type is used to store a numerical value. Integer can be 32 bit or 64 bit depending upon your server.
* **Boolean** − This type is used to store a boolean (true/ false) value.
* **Double** − This type is used to store floating point values.
* **Min/ Max keys** − This type is used to compare a value against the lowest and highest BSON elements.
* **Arrays** − This type is used to store arrays or list or multiple values into one key.
* **Timestamp** − ctimestamp. This can be handy for recording when a document has been modified or added.
* **Object** − This datatype is used for embedded documents.
* **Null** − This type is used to store a Null value.
* **Symbol** − This datatype is used identically to a string; however, it's generally reserved for languages that use a specific symbol type.
* **Date** − This datatype is used to store the current date or time in UNIX time format. You can specify your own date time by creating object of Date and passing day, month, year into it.
* **Object ID** − This datatype is used to store the document’s ID.
* **Binary data** − This datatype is used to store binary data.
* **Code** − This datatype is used to store JavaScript code into the document.
* **Regular expression** − This datatype is used to store regular expression.

-- [Tutorialspoint MongoDB Tutorial](https://www.tutorialspoint.com/mongodb/mongodb_datatype.htm)

**Creating collection explicitly**

**`db.createCollection`**

```
> db.createCollection("cover_type")
{ "ok" : 1 }
> show collections
cover_type
```

**Creating collection by adding first document**

**`db.<collection>.insertOne(<document>)`**

```
> db.quote.insertOne({
...     id: 1,
...     owner: "Agnes Graham",
...     author: "Gabriel Gacia Marquez",
...     source: "One Hundred Years of Solitude",
...     content: "There is always something left to love.",
...     rating: 10
... });
{
	"acknowledged" : true,
	"insertedId" : ObjectId("66edd44a50304329da899dba")
}
> show collections
cover_type
quote
```

**Creating collection by adding first documents**

**`db.<collection>.inserMany(<documents>)`**

```
> show collections
cover_type
quote
> db.cite.insertMany([
...     {
...         id: 1,
...         owner: "Magnus Cromwell",
...         author: "Umberto Eco",
...         source: "Foucault's Pendulum",
...         content: "We are formed by little scraps of wisdom.",
...         rating: 9
...     },
...     {
...         id: 2,
...         owner: "Amelia Rosedale",
...         author: "Gustav Meyrink",
...         source: "The Golem",
...         content: "In the darkness, we find our true selves.",
...         rating: 7
...     }
... ]);
{
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("66f1453ce0d4b8f6440ce966"),
		ObjectId("66f1453ce0d4b8f6440ce967")
	]
}
> show collections
cite
cover_type
quote
```

#### Validation

```
> db.createCollection("quote", {
...     validator: {
...         $jsonSchema: {
...             bsonType: "object",
...             required: [ "id", "owner_id", "content" ],
...             properties: {
...                 id: {
...                     bsonType: "int",
...                     description: "'id' must be an integer and is required"
...                 },
...                 owner_id: {
...                     bsonType: "int",
...                     description: "'owner_id' must be an integer and is required"
...                 },
...                 content: {
...                     bsonType: "string",
...                     description: "'content' must be a string and is required"
...                 },
...                 author: {
...                     bsonType: "string",
...                     description: "'author' must be a string"
...                 },
...                 source: {
...                     bsonType: "string",
...                     description: "'source' must be a string"
...                 },
...                 rating: {
...                     bsonType: "int",
...                     description: "'rating' must be a string"
...                 }
...             }
...         }
...     }
... });
{ "ok" : 1 }
> db.quote.insertOne({
...     id: NumberInt(1),
...     owner_id: NumberInt(11),
...     content: "Though this be madness, yet there is method in 't.",
...     author: "William Shakespeare",
...     source: "Hamlet",
...     rating: NumberInt(5)
... });
{
	"acknowledged" : true,
	"insertedId" : ObjectId("66f553e7e0d4b8f6440ce982")
}
> db.quote.find();
{ "_id" : ObjectId("66f553e7e0d4b8f6440ce982"), "id" : 1, "owner_id" : 11, "content" : "Though this be madness, yet there is method in 't.", "author" : "William Shakespeare", "source" : "Hamlet", "rating" : 5 }
```

### Deleting collections

**`db.<collection>.drop()`**

```
> show collections
cite
cover_type
quote
> db.cover_type.drop();
true
> show collections
cite
quote
```
