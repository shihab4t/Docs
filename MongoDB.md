# MongoDB

# MongoDB Notes

- Create

```sql
db.products.insertOne({name: "iphone 10", price: 100000, category: "smartphone", active: true})
db.student.insertMany([{name:"Ajay",age:20}, {name:"Bina",age:24},{name:"Ram",age:23}])
```

- Read

```sql
db.products.find({}, {active: 0})
db.products.find({category: "smartphone"}).limit(1).pretty()
db.products.find({category: "smartphone"}).limit(1).skip(1).pretty()
```

- Update

```sql
db.products.updateOne({name: "iphone 10", active: true}, {$set: {price: 120000}})
db.products.updateMany({}, {$set: {active: true}})
```

- Delete

```sql
db.products.deleteOne({name: "iphone 10"})
db.products.deleteMany({active: false})
```

# Docs

## Import / Export in Mongodb

- Export as bson
  - `mongodump --uri "mongodb+srv://sandbox.<altes url>.mongodb.net/sample_supplies" --username shihab4t`
- Export as json
  - `mongoexport --uri "mongodb+srv://sandbox.<altes url>.mongodb.net/sample_supplies" --username shihab4t --collection=sales --out=sales.json`
- Import bson
  - `mongorestore --uri "mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies" --drop dump`
- import json/csv
  - `mongoimport --uri="mongodb+srv://<your username>:<your password>@<your cluster>.mongodb.net/sample_supplies" --drop sales.json`

## Utilities Commands

- Clear the shell
  - `cls`
- Show current database
  - `db`
- Show databases
  - `show dbs`
- Use a database
  - `use <db name>`
  - `use sample_training`
- Show all collection on current database
  - `show collections`

## Read Operations

- Getting All documents
  - `db.<collection name>.find()`
  - `db.zips.find()`
- Finding documents
  - `db.<collection name>.find( {"field": "value"} )`
  - `db.zips.find( {"state": "NY"} )`
- Count documents
  - `db.<collection name>.find( {"field": "value"} ).count()`
  - `db.zips.find( {"state": "NY"} ).count()`
  - `db.zips.find( {"state": "NY", "city": "ALBANY"} ).count()`
- Show documents data good format
  - `db.<collection name>.find( {"field": "value"} ).pretty()`
  - `db.zips.find( {"state": "NY", "city": "ALBANY"} ).pretty()`
