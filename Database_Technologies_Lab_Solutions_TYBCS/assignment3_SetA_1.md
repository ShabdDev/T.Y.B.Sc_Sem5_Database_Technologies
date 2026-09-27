# Assignment 3 — Set A
## CRUD Operations and Data Manipulation in MongoDB

## Q1. LibraryDB and books collection

```javascript
use LibraryDB

db.books.insertMany([
  {title:"Clean Code",author:"Robert Martin",year:2008,genre:"Technology",price:550,available:true},
  {title:"The Pragmatic Programmer",author:"Andrew Hunt",year:1999,genre:"Technology",price:650,available:true},
  {title:"Dune",author:"Frank Herbert",year:2015,genre:"Science Fiction",price:450,available:true},
  {title:"Foundation",author:"Isaac Asimov",year:2016,genre:"Science Fiction",price:380,available:false},
  {title:"Atomic Habits",author:"James Clear",year:2018,genre:"Self Help",price:350,available:true},
  {title:"1984",author:"George Orwell",year:2017,genre:"Fiction",price:280,available:false}
])
```

## Q2. READ operations

### a) Display all books
```javascript
db.books.find().pretty()
```

### b) Only title and author
```javascript
db.books.find({}, {_id:0,title:1,author:1})
```

### c) Price greater than 300
```javascript
db.books.find({price:{$gt:300}})
```

### d) Sort by year ascending
```javascript
db.books.find().sort({year:1})
```

## Q3. Update one price and all Fiction books

```javascript
db.books.updateOne(
  {title:"Dune"},
  {$set:{price:500}}
)

db.books.updateMany(
  {genre:"Fiction"},
  {$set:{available:true}}
)
```

## Q4. Add 10% discount to books costing more than 400

```javascript
db.books.updateMany(
  {price:{$gt:400}},
  {$set:{discount:10}}
)
```

## Q5. Delete one title and all unavailable books

```javascript
db.books.deleteOne({title:"1984"})
db.books.deleteMany({available:false})
```

## Q6. Count documents

```javascript
db.books.countDocuments()
db.books.countDocuments({price:{$lt:200}})
db.books.countDocuments({available:true})
```

## Q7. Genre is Science Fiction or Technology

```javascript
db.books.find({
  genre:{$in:["Science Fiction","Technology"]}
})
```

## Q8. Published between 2015 and 2025

```javascript
db.books.find({
  year:{$gte:2015,$lte:2025}
})
```

## Q9. Increase price by 5% for books before 2018

```javascript
db.books.updateMany(
  {year:{$lt:2018}},
  {$mul:{price:1.05}}
)
```

## Q10. Top 3 most expensive books

```javascript
db.books.find().sort({price:-1}).limit(3)
```

## Result
All requested CRUD, filtering, projection, sorting, counting, update operators, and limiting operations were implemented.
