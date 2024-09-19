[⌂ Home](../../README.md)
[▲ Previous: Managing databases](managing_databases.md)

## Managing collections

### Displaying collections

```
> show collections
```

### Creating collection

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
...     "id": 1,
...     "owner": "Agnes Graham",
...     "author": "Gabriel Gacia Marquez",
...     "source": "One Hundred Years of Solitude",
...     "content": "There is always something left to love.",
...     "rating": 10
... });
{
	"acknowledged" : true,
	"insertedId" : ObjectId("66ec1570dc5bbdfcbff2ddfe")
}
> show collections
cover_type
quote
```

**Creating collection by adding first documents**

**`db.<collection>.inserMany(<documents>)`**

```
> db.cite.insertMany([
...     {
...         "id": 1,
...         "owner": "Magnus Cromwell",
...         "author": "Umberto Eco",
...         "source": "Foucault's Pendulum",
...         "content": "We are formed by little scraps of wisdom.",
...         "rating": 9
...     },
...     {
...         "id": 2,
...         "owner": "Amelia Rosedale",
...         "author": "Gustav Meyrink",
...         "source": "The Golem",
...         "content": "In the darkness, we find our true selves.",
...         "rating": 7
...     }
... ]);
{
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("66ec23ebdc5bbdfcbff2de00"),
		ObjectId("66ec23ebdc5bbdfcbff2de01")
	]
}
> show collections
cite
cover_type
quote
```
