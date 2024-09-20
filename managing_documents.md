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

```
