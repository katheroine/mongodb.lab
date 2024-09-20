[⌂ Home](../../README.md)
[▲ Previous: Installation and running](installation_and_running.md)
[▼ Next: Managing tables](managing_tables.md)

## Managing databases

### Displaying databases

**`show dbs`**

```
> show dbs
admin              0.000GB
config             0.000GB
local              0.000GB
```

### Displaying actually using database

**`db`**

```
> db
test
```

### Creating and choosing databases

**`use <database>`**

```
> use quote_mongodb_lab
switched to db quote_mongodb_lab
```

### Deleting database

**`db.dropDatabase(<database>)`**

```
> db.dropDatabase();
{ "dropped" : "quote_mongodb_lab", "ok" : 1 }
```
