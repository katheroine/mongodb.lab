# MongoDB.lab

Laboratory of MongoDB.

1. [Installation and running databases](installation_and_running.md)
2. [Managing databases](managing_databases.md)
    1. [Displaying databases](managing_databases.md#displaying-databases)
    2. [Displaying actually using database](managing_databases.md#displaying-actually-using-database)
    3. [Creating and choosing databases](managing_databases.md#creating-and-choosing-databases)
    4. [Deleting database](managing_databases.md#deleting-database)
3. [Managing collections](managing_collections.md)
    1. [Displaying collections](managing_collections.md#displaying-collections)
    2. [Creating collections](managing_collections.md#creating-collection)
    3. [Deleting collections](managing_collections.md#deleting-collections)
4. [Managing documents](managing_documents.md)
    1. [Inserting documents](managing_documents.md#inserting-documents)
    2. [Updating documents](managing_documents.md#updating-documents)
    3. [Deleting documents](managing_documents.md#deleting-documents)
5. [Querying database](querying_database.md)
    1. [Queries](querying_database.md#queries)
    2. [Aggregations](querying_database.md#aggregations)

**MongoDB** is a document database. It stores data in a type of **`JSON`** format called **`BSON`**.

-- [W3Schools MongoDB Tutorial](https://www.w3schools.com/mongodb/index.php)

## SQL vs Document Databases

SQL databases are considered relational databases. They store related data in separate tables. When data is needed, it is queried from multiple tables to join the data back together.

MongoDB is a document database which is often referred to as a non-relational database. This does not mean that relational data cannot be stored in document databases. It means that relational data is stored differently. A better way to refer to it is as a non-tabular database.

MongoDB stores data in flexible documents. Instead of having multiple tables you can simply keep all of your related data together. This makes reading your data very fast.

You can still have multiple groups of data too. In MongoDB, instead of tables these are called collections.

-- [W3Schools MongoDB Tutorial](https://www.w3schools.com/mongodb/mongodb_get_started.php)
