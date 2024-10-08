[⌂ Home](../../README.md)
[▲ Previous: Managing documents](managing_documents.md)

## Querying database

**Database preparation**

```javascript
db.createCollection("quote", {
    validator: {
        $jsonSchema: {
            bsonType: "object",
            required: [ "id", "owner_id", "content" ],
            properties: {
                id: {
                    bsonType: "int",
                    description: "'id' must be an integer and is required"
                },
                owner_id: {
                    bsonType: "int",
                    description: "'owner_id' must be an integer and is required"
                },
                content: {
                    bsonType: "string",
                    description: "'content' must be a string and is required"
                },
                author: {
                    bsonType: "string",
                    description: "'author' must be a string"
                },
                source: {
                    bsonType: "string",
                    description: "'source' must be a string"
                },
                rating: {
                    bsonType: "int",
                    description: "'rating' must be a string"
                }
            }
        }
    }
});

db.quote.insertMany([
    {
        id: NumberInt(1),
        owner_id: NumberInt(101),
        content: "Though this be madness, yet there is method in 't.",
        author: "William Shakespeare",
        source: "Hamlet",
        rating: NumberInt(5)
    },
    {
        id: NumberInt(2),
        owner_id: NumberInt(102),
        content: "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
        author: "Jane Austen",
        source: "Pride and Prejudice",
        rating: NumberInt(4)
    },
    {
        id: NumberInt(3),
        owner_id: NumberInt(103),
        content: "All of science is nothing more than the refinement of everyday thinking.",
        author: "Albert Einstein",
        source: "Physics and Reality",
        rating: NumberInt(5)
    },
    {
        id: NumberInt(4),
        owner_id: NumberInt(104),
        content: "There is no greater agony than bearing an untold story inside you.",
        author: "Maya Angelou",
        source: "I Know Why the Caged Bird Sings",
        rating: NumberInt(4)
    },
    {
        id: NumberInt(5),
        owner_id: NumberInt(105),
        content: "The higher we soar the smaller we appear to those who cannot fly.",
        author: "Friedrich Nietzsche",
        source: "Thus Spoke Zarathustra",
        rating: NumberInt(3)
    },
    {
        id: NumberInt(6),
        owner_id: NumberInt(106),
        content: "Nowadays people know the price of everything and the value of nothing.",
        author: "Oscar Wilde",
        source: "The Picture of Dorian Gray",
        rating: NumberInt(4)
    },
    {
        id: NumberInt(7),
        owner_id: NumberInt(107),
        content: "Service without humility is selfishness and egotism.",
        author: "Mahatma Gandhi",
        source: "The Story of My Experiments with Truth",
        rating: NumberInt(5)
    },
    {
        id: NumberInt(8),
        owner_id: NumberInt(108),
        content: "There is no gate, no lock, no bolt that you can set upon the freedom of my mind.",
        author: "Virginia Woolf",
        source: "A Room of One's Own",
        rating: NumberInt(3)
    },
    {
        id: NumberInt(9),
        owner_id: NumberInt(109),
        content: "If you tell the truth you do not need a good memory!",
        author: "Mark Twain",
        source: "The Adventures of Huckleberry Finn",
        rating: NumberInt(3)
    },
    {
        id: NumberInt(10),
        owner_id: NumberInt(110),
        content: "Freedom is obedience to self-formulated rules.",
        author: "Aristotle",
        source: "Nicomachean Ethics",
        rating: NumberInt(5)
    }
]);
```

### Queries

#### Scope

##### Selecting all columns of all records

**Without formatting**

```javascript
db.<collection>.find();
```

```
> db.quote.find();
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce983"), "id" : 1, "owner_id" : 101, "content" : "Though this be madness, yet there is method in 't.", "author" : "William Shakespeare", "source" : "Hamlet", "rating" : 5 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce984"), "id" : 2, "owner_id" : 102, "content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.", "author" : "Jane Austen", "source" : "Pride and Prejudice", "rating" : 4 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce985"), "id" : 3, "owner_id" : 103, "content" : "All of science is nothing more than the refinement of everyday thinking.", "author" : "Albert Einstein", "source" : "Physics and Reality", "rating" : 5 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce986"), "id" : 4, "owner_id" : 104, "content" : "There is no greater agony than bearing an untold story inside you.", "author" : "Maya Angelou", "source" : "I Know Why the Caged Bird Sings", "rating" : 4 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce987"), "id" : 5, "owner_id" : 105, "content" : "The higher we soar the smaller we appear to those who cannot fly.", "author" : "Friedrich Nietzsche", "source" : "Thus Spoke Zarathustra", "rating" : 3 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce988"), "id" : 6, "owner_id" : 106, "content" : "Nowadays people know the price of everything and the value of nothing.", "author" : "Oscar Wilde", "source" : "The Picture of Dorian Gray", "rating" : 4 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce989"), "id" : 7, "owner_id" : 107, "content" : "Service without humility is selfishness and egotism.", "author" : "Mahatma Gandhi", "source" : "The Story of My Experiments with Truth", "rating" : 5 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce98a"), "id" : 8, "owner_id" : 108, "content" : "There is no gate, no lock, no bolt that you can set upon the freedom of my mind.", "author" : "Virginia Woolf", "source" : "A Room of One's Own", "rating" : 3 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce98b"), "id" : 9, "owner_id" : 109, "content" : "If you tell the truth you do not need a good memory!", "author" : "Mark Twain", "source" : "The Adventures of Huckleberry Finn", "rating" : 3 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce98c"), "id" : 10, "owner_id" : 110, "content" : "Freedom is obedience to self-formulated rules.", "author" : "Aristotle", "source" : "Nicomachean Ethics", "rating" : 5 }
```

**With formatting**

```javascript
db.<collection>.find().pretty();
```

```
> db.quote.find().pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"id" : 1,
	"owner_id" : 101,
	"content" : "Though this be madness, yet there is method in 't.",
	"author" : "William Shakespeare",
	"source" : "Hamlet",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"id" : 2,
	"owner_id" : 102,
	"content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"id" : 3,
	"owner_id" : 103,
	"content" : "All of science is nothing more than the refinement of everyday thinking.",
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce986"),
	"id" : 4,
	"owner_id" : 104,
	"content" : "There is no greater agony than bearing an untold story inside you.",
	"author" : "Maya Angelou",
	"source" : "I Know Why the Caged Bird Sings",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce987"),
	"id" : 5,
	"owner_id" : 105,
	"content" : "The higher we soar the smaller we appear to those who cannot fly.",
	"author" : "Friedrich Nietzsche",
	"source" : "Thus Spoke Zarathustra",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"id" : 7,
	"owner_id" : 107,
	"content" : "Service without humility is selfishness and egotism.",
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98a"),
	"id" : 8,
	"owner_id" : 108,
	"content" : "There is no gate, no lock, no bolt that you can set upon the freedom of my mind.",
	"author" : "Virginia Woolf",
	"source" : "A Room of One's Own",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98b"),
	"id" : 9,
	"owner_id" : 109,
	"content" : "If you tell the truth you do not need a good memory!",
	"author" : "Mark Twain",
	"source" : "The Adventures of Huckleberry Finn",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"id" : 10,
	"owner_id" : 110,
	"content" : "Freedom is obedience to self-formulated rules.",
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics",
	"rating" : 5
}
```

##### Selecting chosen columns of all records

**Without formatting**

```javascript
db.<collection>.find(
    {},
    {
        <field_1>: <includion_1>,
        <field_2>: <inclusion_2>,
        <field_3>: <inclusion_3>
    }
);
```

```
> db.quote.find(
...     {},
...     {
...         author: true,
...         source: true
...     }
... );
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce983"), "author" : "William Shakespeare", "source" : "Hamlet" }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce984"), "author" : "Jane Austen", "source" : "Pride and Prejudice" }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce985"), "author" : "Albert Einstein", "source" : "Physics and Reality" }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce986"), "author" : "Maya Angelou", "source" : "I Know Why the Caged Bird Sings" }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce987"), "author" : "Friedrich Nietzsche", "source" : "Thus Spoke Zarathustra" }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce988"), "author" : "Oscar Wilde", "source" : "The Picture of Dorian Gray" }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce989"), "author" : "Mahatma Gandhi", "source" : "The Story of My Experiments with Truth" }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce98a"), "author" : "Virginia Woolf", "source" : "A Room of One's Own" }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce98b"), "author" : "Mark Twain", "source" : "The Adventures of Huckleberry Finn" }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce98c"), "author" : "Aristotle", "source" : "Nicomachean Ethics" }
```

**With formatting**

```javascript
db.<collection>.find(
    {},
    {
        <field_1>: <includion_1>,
        <field_2>: <inclusion_2>,
        <field_3>: <inclusion_3>
    }
).pretty();
```

```
> db.quote.find(
...     {},
...     {
...         author: true,
...         source: true
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"author" : "William Shakespeare",
	"source" : "Hamlet"
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice"
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"author" : "Albert Einstein",
	"source" : "Physics and Reality"
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce986"),
	"author" : "Maya Angelou",
	"source" : "I Know Why the Caged Bird Sings"
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce987"),
	"author" : "Friedrich Nietzsche",
	"source" : "Thus Spoke Zarathustra"
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray"
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth"
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98a"),
	"author" : "Virginia Woolf",
	"source" : "A Room of One's Own"
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98b"),
	"author" : "Mark Twain",
	"source" : "The Adventures of Huckleberry Finn"
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics"
}
```

##### Selecting all columns of chosen records

**Without formatting**

```javascript
db.<collection>.find(
    {
        <field_1>: <value_1>,
        <field_2>: <value_2>,
        <field_3>: <value_3>,
    }
);
```

```
> db.quote.find(
...     {
...         owner_id: 106
...     }
... );
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce988"), "id" : 6, "owner_id" : 106, "content" : "Nowadays people know the price of everything and the value of nothing.", "author" : "Oscar Wilde", "source" : "The Picture of Dorian Gray", "rating" : 4 }
```

**With formatting**

```javascript
db.<collection>.find(
    {
        <field_1>: <value_1>,
        <field_2>: <value_2>,
        <field_3>: <value_3>,
    }
).pretty();
```

```
> db.quote.find(
...     {
...         owner_id: 106
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
```

##### Selecting chosen columns of chosen records

**Without formatting**

```javascript
db.<collection>.find(
    {
        <field_1>: <value_1>,
        <field_2>: <value_2>,
        <field_3>: <value_3>,
    },
    {
        <field_1>: <includion_1>,
        <field_2>: <inclusion_2>,
        <field_3>: <inclusion_3>
    }
);
```

```
> db.quote.find(
...     {
...         rating: {
...             $gt: 4
...         }
...     },
...     {
...         author: true,
...         source: true,
...         rating: true
...     }
... );
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce983"), "author" : "William Shakespeare", "source" : "Hamlet", "rating" : 5 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce985"), "author" : "Albert Einstein", "source" : "Physics and Reality", "rating" : 5 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce989"), "author" : "Mahatma Gandhi", "source" : "The Story of My Experiments with Truth", "rating" : 5 }
{ "_id" : ObjectId("66f57f34e0d4b8f6440ce98c"), "author" : "Aristotle", "source" : "Nicomachean Ethics", "rating" : 5 }
```

**With formatting**

```javascript
db.<collection>.find(
    {
        <field_1>: <value_1>,
        <field_2>: <value_2>,
        <field_3>: <value_3>,
    },
    {
        <field_1>: <includion_1>,
        <field_2>: <inclusion_2>,
        <field_3>: <inclusion_3>
    }
).pretty();
```

```
> db.quote.find(
...     {
...         rating: {
...             $gt: 4
...         }
...     },
...     {
...         author: true,
...         source: true,
...         rating: true
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"author" : "William Shakespeare",
	"source" : "Hamlet",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics",
	"rating" : 5
}
```

#### Column aliases

#### Query operators

##### Relational operators

**Equal `$eq`**

```
> db.quote.find(
...     {
...         rating: {
...             $eq: 5
...         }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"id" : 1,
	"owner_id" : 101,
	"content" : "Though this be madness, yet there is method in 't.",
	"author" : "William Shakespeare",
	"source" : "Hamlet",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"id" : 3,
	"owner_id" : 103,
	"content" : "All of science is nothing more than the refinement of everyday thinking.",
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"id" : 7,
	"owner_id" : 107,
	"content" : "Service without humility is selfishness and egotism.",
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"id" : 10,
	"owner_id" : 110,
	"content" : "Freedom is obedience to self-formulated rules.",
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics",
	"rating" : 5
}
```

**Different `$ne`**

```
> db.quote.find(
...     {
...         rating: {
...             $ne: 5
...         }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"id" : 2,
	"owner_id" : 102,
	"content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce986"),
	"id" : 4,
	"owner_id" : 104,
	"content" : "There is no greater agony than bearing an untold story inside you.",
	"author" : "Maya Angelou",
	"source" : "I Know Why the Caged Bird Sings",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce987"),
	"id" : 5,
	"owner_id" : 105,
	"content" : "The higher we soar the smaller we appear to those who cannot fly.",
	"author" : "Friedrich Nietzsche",
	"source" : "Thus Spoke Zarathustra",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98a"),
	"id" : 8,
	"owner_id" : 108,
	"content" : "There is no gate, no lock, no bolt that you can set upon the freedom of my mind.",
	"author" : "Virginia Woolf",
	"source" : "A Room of One's Own",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98b"),
	"id" : 9,
	"owner_id" : 109,
	"content" : "If you tell the truth you do not need a good memory!",
	"author" : "Mark Twain",
	"source" : "The Adventures of Huckleberry Finn",
	"rating" : 3
}
```

**Smaller than `$lt`**

```
> db.quote.find(
...     {
...         rating: {
...             $lt: 4
...         }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce987"),
	"id" : 5,
	"owner_id" : 105,
	"content" : "The higher we soar the smaller we appear to those who cannot fly.",
	"author" : "Friedrich Nietzsche",
	"source" : "Thus Spoke Zarathustra",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98a"),
	"id" : 8,
	"owner_id" : 108,
	"content" : "There is no gate, no lock, no bolt that you can set upon the freedom of my mind.",
	"author" : "Virginia Woolf",
	"source" : "A Room of One's Own",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98b"),
	"id" : 9,
	"owner_id" : 109,
	"content" : "If you tell the truth you do not need a good memory!",
	"author" : "Mark Twain",
	"source" : "The Adventures of Huckleberry Finn",
	"rating" : 3
}
```

**Smaller than or equals `$lte`**

```
> db.quote.find(
...     {
...         rating: {
...             $lte: 4
...         }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"id" : 2,
	"owner_id" : 102,
	"content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce986"),
	"id" : 4,
	"owner_id" : 104,
	"content" : "There is no greater agony than bearing an untold story inside you.",
	"author" : "Maya Angelou",
	"source" : "I Know Why the Caged Bird Sings",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce987"),
	"id" : 5,
	"owner_id" : 105,
	"content" : "The higher we soar the smaller we appear to those who cannot fly.",
	"author" : "Friedrich Nietzsche",
	"source" : "Thus Spoke Zarathustra",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98a"),
	"id" : 8,
	"owner_id" : 108,
	"content" : "There is no gate, no lock, no bolt that you can set upon the freedom of my mind.",
	"author" : "Virginia Woolf",
	"source" : "A Room of One's Own",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98b"),
	"id" : 9,
	"owner_id" : 109,
	"content" : "If you tell the truth you do not need a good memory!",
	"author" : "Mark Twain",
	"source" : "The Adventures of Huckleberry Finn",
	"rating" : 3
}
```

**Greater than `$gt`**

```
> db.quote.find(
...     {
...         rating: {
...             $gt: 4
...         }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"id" : 1,
	"owner_id" : 101,
	"content" : "Though this be madness, yet there is method in 't.",
	"author" : "William Shakespeare",
	"source" : "Hamlet",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"id" : 3,
	"owner_id" : 103,
	"content" : "All of science is nothing more than the refinement of everyday thinking.",
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"id" : 7,
	"owner_id" : 107,
	"content" : "Service without humility is selfishness and egotism.",
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"id" : 10,
	"owner_id" : 110,
	"content" : "Freedom is obedience to self-formulated rules.",
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics",
	"rating" : 5
}
```

**Greater than or equals `$gte`**

```
> db.quote.find(
...     {
...         rating: {
...             $gte: 4
...         }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"id" : 1,
	"owner_id" : 101,
	"content" : "Though this be madness, yet there is method in 't.",
	"author" : "William Shakespeare",
	"source" : "Hamlet",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"id" : 2,
	"owner_id" : 102,
	"content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"id" : 3,
	"owner_id" : 103,
	"content" : "All of science is nothing more than the refinement of everyday thinking.",
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce986"),
	"id" : 4,
	"owner_id" : 104,
	"content" : "There is no greater agony than bearing an untold story inside you.",
	"author" : "Maya Angelou",
	"source" : "I Know Why the Caged Bird Sings",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"id" : 7,
	"owner_id" : 107,
	"content" : "Service without humility is selfishness and egotism.",
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"id" : 10,
	"owner_id" : 110,
	"content" : "Freedom is obedience to self-formulated rules.",
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics",
	"rating" : 5
}
```

**Inside the set `$in`**

```
> db.quote.find(
...     {
...         rating: {
...             $in: [3, 5]
...         }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"id" : 1,
	"owner_id" : 101,
	"content" : "Though this be madness, yet there is method in 't.",
	"author" : "William Shakespeare",
	"source" : "Hamlet",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"id" : 3,
	"owner_id" : 103,
	"content" : "All of science is nothing more than the refinement of everyday thinking.",
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce987"),
	"id" : 5,
	"owner_id" : 105,
	"content" : "The higher we soar the smaller we appear to those who cannot fly.",
	"author" : "Friedrich Nietzsche",
	"source" : "Thus Spoke Zarathustra",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"id" : 7,
	"owner_id" : 107,
	"content" : "Service without humility is selfishness and egotism.",
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98a"),
	"id" : 8,
	"owner_id" : 108,
	"content" : "There is no gate, no lock, no bolt that you can set upon the freedom of my mind.",
	"author" : "Virginia Woolf",
	"source" : "A Room of One's Own",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98b"),
	"id" : 9,
	"owner_id" : 109,
	"content" : "If you tell the truth you do not need a good memory!",
	"author" : "Mark Twain",
	"source" : "The Adventures of Huckleberry Finn",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"id" : 10,
	"owner_id" : 110,
	"content" : "Freedom is obedience to self-formulated rules.",
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics",
	"rating" : 5
}
```

**Not inside the set `$nin`**

```
> db.quote.find(
...     {
...         rating: {
...             $nin: [3, 5]
...         }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"id" : 2,
	"owner_id" : 102,
	"content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce986"),
	"id" : 4,
	"owner_id" : 104,
	"content" : "There is no greater agony than bearing an untold story inside you.",
	"author" : "Maya Angelou",
	"source" : "I Know Why the Caged Bird Sings",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
```

##### Logical operators

**Logical negation `$not`**

```
> db.quote.find(
...     {
...         rating: {
...             $not:
...             {
...                 $in: [3, 5]
...             }
...         }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"id" : 2,
	"owner_id" : 102,
	"content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce986"),
	"id" : 4,
	"owner_id" : 104,
	"content" : "There is no greater agony than bearing an untold story inside you.",
	"author" : "Maya Angelou",
	"source" : "I Know Why the Caged Bird Sings",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
```

**Logical product `$and`**

```
> db.quote.find(
...     {
...         $and: [
...             {
...                 rating: 3
...             },
...             {
...                 id: {
...                     $lt: 6
...                 }
...             }
...         ]
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce987"),
	"id" : 5,
	"owner_id" : 105,
	"content" : "The higher we soar the smaller we appear to those who cannot fly.",
	"author" : "Friedrich Nietzsche",
	"source" : "Thus Spoke Zarathustra",
	"rating" : 3
}
```

**Logical sum `$or`**

```
> db.quote.find(
...     {
...         $or: [
...             {
...                 rating: 5
...             },
...             {
...                 id: {
...                     $lt: 3
...                 }
...             }
...         ]
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"id" : 1,
	"owner_id" : 101,
	"content" : "Though this be madness, yet there is method in 't.",
	"author" : "William Shakespeare",
	"source" : "Hamlet",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"id" : 2,
	"owner_id" : 102,
	"content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"id" : 3,
	"owner_id" : 103,
	"content" : "All of science is nothing more than the refinement of everyday thinking.",
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"id" : 7,
	"owner_id" : 107,
	"content" : "Service without humility is selfishness and egotism.",
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"id" : 10,
	"owner_id" : 110,
	"content" : "Freedom is obedience to self-formulated rules.",
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics",
	"rating" : 5
}
```

**Negation of logical sum (not or) `$nor`**

```
> db.quote.find(
...     {
...         $nor: [
...             {
...                 rating: 4
...             },
...             {
...                 id: {
...                     $gt: 4
...                 }
...             }
...         ]
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"id" : 1,
	"owner_id" : 101,
	"content" : "Though this be madness, yet there is method in 't.",
	"author" : "William Shakespeare",
	"source" : "Hamlet",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"id" : 3,
	"owner_id" : 103,
	"content" : "All of science is nothing more than the refinement of everyday thinking.",
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
```

##### Element operators

**`$exists`**

```
> db.quote.find(
...     {
...         rating: {
...                 $exists: true
...             }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"id" : 1,
	"owner_id" : 101,
	"content" : "Though this be madness, yet there is method in 't.",
	"author" : "William Shakespeare",
	"source" : "Hamlet",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"id" : 2,
	"owner_id" : 102,
	"content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"id" : 3,
	"owner_id" : 103,
	"content" : "All of science is nothing more than the refinement of everyday thinking.",
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce986"),
	"id" : 4,
	"owner_id" : 104,
	"content" : "There is no greater agony than bearing an untold story inside you.",
	"author" : "Maya Angelou",
	"source" : "I Know Why the Caged Bird Sings",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce987"),
	"id" : 5,
	"owner_id" : 105,
	"content" : "The higher we soar the smaller we appear to those who cannot fly.",
	"author" : "Friedrich Nietzsche",
	"source" : "Thus Spoke Zarathustra",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"id" : 7,
	"owner_id" : 107,
	"content" : "Service without humility is selfishness and egotism.",
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98a"),
	"id" : 8,
	"owner_id" : 108,
	"content" : "There is no gate, no lock, no bolt that you can set upon the freedom of my mind.",
	"author" : "Virginia Woolf",
	"source" : "A Room of One's Own",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98b"),
	"id" : 9,
	"owner_id" : 109,
	"content" : "If you tell the truth you do not need a good memory!",
	"author" : "Mark Twain",
	"source" : "The Adventures of Huckleberry Finn",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"id" : 10,
	"owner_id" : 110,
	"content" : "Freedom is obedience to self-formulated rules.",
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics",
	"rating" : 5
}
```

**`$type`**

```
> db.quote.find(
...     {
...         rating: {
...                 $type: "int"
...             }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce983"),
	"id" : 1,
	"owner_id" : 101,
	"content" : "Though this be madness, yet there is method in 't.",
	"author" : "William Shakespeare",
	"source" : "Hamlet",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"id" : 2,
	"owner_id" : 102,
	"content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"id" : 3,
	"owner_id" : 103,
	"content" : "All of science is nothing more than the refinement of everyday thinking.",
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce986"),
	"id" : 4,
	"owner_id" : 104,
	"content" : "There is no greater agony than bearing an untold story inside you.",
	"author" : "Maya Angelou",
	"source" : "I Know Why the Caged Bird Sings",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce987"),
	"id" : 5,
	"owner_id" : 105,
	"content" : "The higher we soar the smaller we appear to those who cannot fly.",
	"author" : "Friedrich Nietzsche",
	"source" : "Thus Spoke Zarathustra",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"id" : 7,
	"owner_id" : 107,
	"content" : "Service without humility is selfishness and egotism.",
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98a"),
	"id" : 8,
	"owner_id" : 108,
	"content" : "There is no gate, no lock, no bolt that you can set upon the freedom of my mind.",
	"author" : "Virginia Woolf",
	"source" : "A Room of One's Own",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98b"),
	"id" : 9,
	"owner_id" : 109,
	"content" : "If you tell the truth you do not need a good memory!",
	"author" : "Mark Twain",
	"source" : "The Adventures of Huckleberry Finn",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"id" : 10,
	"owner_id" : 110,
	"content" : "Freedom is obedience to self-formulated rules.",
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics",
	"rating" : 5
}
```

##### Evaluation operators

**Modulo `$mod`**

```
> db.quote.find(
...     {
...         rating: {
...                 $mod: [2, 0]
...             }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce984"),
	"id" : 2,
	"owner_id" : 102,
	"content" : "Pride relates more to our opinion of ourselves, vanity to what we would have others think of us.",
	"author" : "Jane Austen",
	"source" : "Pride and Prejudice",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce986"),
	"id" : 4,
	"owner_id" : 104,
	"content" : "There is no greater agony than bearing an untold story inside you.",
	"author" : "Maya Angelou",
	"source" : "I Know Why the Caged Bird Sings",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
```

**Regular expresions `$regex`**

```
> db.quote.find(
...     {
...         content: {
...                 $regex: /ing\./
...             }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce985"),
	"id" : 3,
	"owner_id" : 103,
	"content" : "All of science is nothing more than the refinement of everyday thinking.",
	"author" : "Albert Einstein",
	"source" : "Physics and Reality",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
```

**Query expression `$expr`**

```
> db.quote.find(
...     {
...         $expr: {
...                 $gt: ["$id", "$rating"]
...             }
...     }
... ).pretty();
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce987"),
	"id" : 5,
	"owner_id" : 105,
	"content" : "The higher we soar the smaller we appear to those who cannot fly.",
	"author" : "Friedrich Nietzsche",
	"source" : "Thus Spoke Zarathustra",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce988"),
	"id" : 6,
	"owner_id" : 106,
	"content" : "Nowadays people know the price of everything and the value of nothing.",
	"author" : "Oscar Wilde",
	"source" : "The Picture of Dorian Gray",
	"rating" : 4
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce989"),
	"id" : 7,
	"owner_id" : 107,
	"content" : "Service without humility is selfishness and egotism.",
	"author" : "Mahatma Gandhi",
	"source" : "The Story of My Experiments with Truth",
	"rating" : 5
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98a"),
	"id" : 8,
	"owner_id" : 108,
	"content" : "There is no gate, no lock, no bolt that you can set upon the freedom of my mind.",
	"author" : "Virginia Woolf",
	"source" : "A Room of One's Own",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98b"),
	"id" : 9,
	"owner_id" : 109,
	"content" : "If you tell the truth you do not need a good memory!",
	"author" : "Mark Twain",
	"source" : "The Adventures of Huckleberry Finn",
	"rating" : 3
}
{
	"_id" : ObjectId("66f57f34e0d4b8f6440ce98c"),
	"id" : 10,
	"owner_id" : 110,
	"content" : "Freedom is obedience to self-formulated rules.",
	"author" : "Aristotle",
	"source" : "Nicomachean Ethics",
	"rating" : 5
}
```

### Aggregations

#### Aggregate operators

**Database preparation**

```
db.createCollection("user", {
    validator: {
        $jsonSchema: {
            bsonType: "object",
            required: [ "login" ],
            properties: {
                login: {
                    bsonType: "string",
                    description: "'login' must be a string and is required"
                },
                group_name: {
                    bsonType: "string",
                    description: "'group_name' must be a string"
                },
                credits: {
                    bsonType: "int",
                    description: "'credits' must be a string"
                }
            }
        }
    }
});

db.user.insertMany([
    {
        login: "john_doe",
        group_name: "bloggers"
        credits: NumberInt(100)
    },
    {
        login: "science_gal",
        group_name: "scientists",
        credits: 250
    },
    {
        login: "news_hound",
        group_name: "journalists",
        credits: 150
    },
    {
        login: "study_buddy",
        group_name: "students",
        credits: 50
    },
    {
        login: "data_miner",
        group_name: "researchers",
        credits: 200
    },
    {
        login: "craft_master",
        group_name: "hobbyists",
        credits: 75
    },
    {
        login: "tech_blogger",
        group_name: "bloggers",
        credits: 120
    },
    {
        login: "quantum_guy",
        group_name: "scientists",
        credits: 300
    },
    {
        login: "truth_seeker",
        group_name: "journalists",
        credits: 180
    },
    {
        login: "college_kid",
        group_name: "students",
        credits: 30
    },
    {
        login: "lab_rat",
        group_name: "researchers",
        credits: 220
    },
    {
        login: "diy_enthusiast",
        group_name: "hobbyists",
        credits: 90
    },
    {
        login: "food_critic",
        group_name: "bloggers",
        credits: 80
    },
    {
        login: "rocket_woman",
        group_name: "scientists",
        credits: 280
    },
    {
        login: "roving_reporter",
        group_name: "journalists",
        credits: 160
    },
    {
        login: "grad_student",
        group_name: "students",
        credits: 40
    },
    {
        login: "book_worm",
        group_name: "researchers",
        credits: 240
    },
    {
        login: "stamp_collector",
        group_name: "hobbyists",
        credits: 60
    },
    {
        login: "travel_guru",
        group_name: "bloggers",
        credits: 110
    },
    {
        login: "chem_whiz",
        group_name: "scientists",
        credits: 270
    }
]);
```

**Results count `$count`**

```
> db.user.aggregate([
...     {
...         $match: {}
...     },
...     {
...         $count: "count"
...     }
... ]);
{ "count" : 20 }
```

```
> db.user.aggregate([
...     {
...         $match: {
...             group_name: "researchers"
...         }
...     },
...     {
...         $count: "users number"
...     }
... ]);
{ "users number" : 3 }
```

**Minimum value `$min`**

```
> db.user.aggregate([
...     {
...         $group: {
...             _id: null,
...             minimum_credits: {
...                 $min: "$credits"
...             }
...         }
...     }
... ]);
{ "_id" : null, "minimum_credits" : 30 }
```

**Maximum value `$max`**

```
> db.user.aggregate([
...     {
...         $group: {
...             _id: null,
...             maximum_credits: {
...                 $max: "$credits"
...             }
...         }
...     }
... ]);
{ "_id" : null, "maximum_credits" : 300 }
```

**Total `$sum`**

```
> db.user.aggregate([
...     {
...         $group: {
...             _id: null,
...             total_credits: {
...                 $sum: "$credits"
...             }
...         }
...     }
... ]);
{ "_id" : null, "total_credits" : 3005 }
```

**Average `$avg`**

```
> db.user.aggregate([
...     {
...         $group: {
...             _id: null,
...             average_credits: {
...                 $avg: "$credits"
...             }
...         }
...     }
... ]);
{ "_id" : null, "average_credits" : 150.25 }
```

**Standard deviation `$stdDevPop`**

```
> db.user.aggregate([
...     {
...         $group: {
...             _id: null,
...             standard_deviation_of_credits: {
...                 $stdDevPop: "$credits"
...             }
...         }
...     }
... ]);
{ "_id" : null, "standard_deviation_of_credits" : 84.85981086474327 }S
```

#### Groupings

**Results count**

```
> db.user.aggregate([
...     {
...         $group: {
...             _id: "$group_name",
...             count: {
...                 $sum: 1
...             }
...         },
...
...     }
... ]);
{ "_id" : "hobbyists", "count" : 3 }
{ "_id" : "researchers", "count" : 3 }
{ "_id" : "students", "count" : 3 }
{ "_id" : "journalists", "count" : 3 }
{ "_id" : "scientists", "count" : 4 }
{ "_id" : "bloggers", "count" : 4 }
```

**Minimum value `$min`**

```
> db.user.aggregate([
...     {
...         $group: {
...             _id: "$group_name",
...             minimum_credits: {
...                 $min: "$credits"
...             }
...         }
...     }
... ]);
{ "_id" : "hobbyists", "minimum_credits" : 60 }
{ "_id" : "researchers", "minimum_credits" : 200 }
{ "_id" : "students", "minimum_credits" : 30 }
{ "_id" : "journalists", "minimum_credits" : 150 }
{ "_id" : "scientists", "minimum_credits" : 250 }
{ "_id" : "bloggers", "minimum_credits" : 80 }
```

**Maximum value `$max`**

```
> db.user.aggregate([
...     {
...         $group: {
...             _id: "$group_name",
...             maximum_credits: {
...                 $max: "$credits"
...             }
...         }
...     }
... ]);
{ "_id" : "hobbyists", "maximum_credits" : 90 }
{ "_id" : "researchers", "maximum_credits" : 240 }
{ "_id" : "students", "maximum_credits" : 50 }
{ "_id" : "journalists", "maximum_credits" : 180 }
{ "_id" : "scientists", "maximum_credits" : 300 }
{ "_id" : "bloggers", "maximum_credits" : 120 }
```

**Average `$avg`**

```
> db.user.aggregate([
...     {
...         $group: {
...             _id: "$group_name",
...             average_credits: {
...                 $avg: "$credits"
...             }
...         }
...     }
... ]);
{ "_id" : "hobbyists", "average_credits" : 75 }
{ "_id" : "researchers", "average_credits" : 220 }
{ "_id" : "students", "average_credits" : 40 }
{ "_id" : "journalists", "average_credits" : 163.33333333333334 }
{ "_id" : "scientists", "average_credits" : 275 }
{ "_id" : "bloggers", "average_credits" : 102.5 }
```

**Standard deviation `$stdDevPop`**

```
> db.user.aggregate([
...     {
...         $group: {
...             _id: "$group_name",
...             standard_deviation_of_credits: {
...                 $stdDevPop: "$credits"
...             }
...         }
...     }
... ]);
{ "_id" : "hobbyists", "standard_deviation_of_credits" : 12.24744871391589 }
{ "_id" : "researchers", "standard_deviation_of_credits" : 16.32993161855452 }
{ "_id" : "students", "standard_deviation_of_credits" : 8.16496580927726 }
{ "_id" : "journalists", "standard_deviation_of_credits" : 12.472191289246473 }
{ "_id" : "scientists", "standard_deviation_of_credits" : 18.027756377319946 }
{ "_id" : "bloggers", "standard_deviation_of_credits" : 14.79019945774904 }
```
