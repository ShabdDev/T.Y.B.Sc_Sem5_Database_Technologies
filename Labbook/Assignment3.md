```
Assignment 3 – SET A – Question 1

The workbook specifies: create a database named LibraryDB, a collection named books, and insert at least 5 book documents with title, author, year, genre, price, and boolean available.

1. Create Database

Open MongoDB Shell (mongosh):

use LibraryDB

Check the current database:

db

Expected:

LibraryDB
2. Create books Collection
db.createCollection("books")

Expected:

{ ok: 1 }

Check:

show collections

Expected:

books
3. Insert 5 Book Documents

Run:

db.books.insertMany([
  {
    title: "The Alchemist",
    author: "Paulo Coelho",
    year: 1988,
    genre: "Fiction",
    price: 250,
    available: true
  },
  {
    title: "Clean Code",
    author: "Robert C. Martin",
    year: 2008,
    genre: "Technology",
    price: 450,
    available: true
  },
  {
    title: "The Hobbit",
    author: "J.R.R. Tolkien",
    year: 1937,
    genre: "Fantasy",
    price: 350,
    available: false
  },
  {
    title: "The Pragmatic Programmer",
    author: "Andrew Hunt",
    year: 1999,
    genre: "Technology",
    price: 550,
    available: true
  },
  {
    title: "Dune",
    author: "Frank Herbert",
    year: 1965,
    genre: "Science Fiction",
    price: 400,
    available: true
  }
])

Expected:

{
  acknowledged: true,
  insertedIds: {
    ...
  }
}
4. Display All Books
db.books.find().pretty()

You should see all 5 documents.

5. Verify Number of Books
db.books.countDocuments()

Expected:

5
Final Collection Structure

Your documents will have this structure:

books
 ├── title
 ├── author
 ├── year
 ├── genre
 ├── price
 └── available

Example:

{
  title: "Clean Code",
  author: "Robert C. Martin",
  year: 2008,
  genre: "Technology",
  price: 450,
  available: true
}
Important concept

available is a Boolean field:

available: true

or

available: false

Do not write:

available: "true"

because "true" is a String, not a Boolean.

Complete Copy-Paste Solution
use LibraryDB

db.createCollection("books")

db.books.insertMany([
  {
    title: "The Alchemist",
    author: "Paulo Coelho",
    year: 1988,
    genre: "Fiction",
    price: 250,
    available: true
  },
  {
    title: "Clean Code",
    author: "Robert C. Martin",
    year: 2008,
    genre: "Technology",
    price: 450,
    available: true
  },
  {
    title: "The Hobbit",
    author: "J.R.R. Tolkien",
    year: 1937,
    genre: "Fantasy",
    price: 350,
    available: false
  },
  {
    title: "The Pragmatic Programmer",
    author: "Andrew Hunt",
    year: 1999,
    genre: "Technology",
    price: 550,
    available: true
  },
  {
    title: "Dune",
    author: "Frank Herbert",
    year: 1965,
    genre: "Science Fiction",
    price: 400,
    available: true
  }
])

db.books.find().pretty()

db.books.countDocuments()
Expected final count
5
```
---
```
Assignment 3 – Set A

Q2. READ Operations on the books Collection

Aim

To perform READ operations on the MongoDB books collection:

Display all books.

Display only the title and author fields.

Find all books with price greater than Rs. 300.

Find books sorted by year in ascending order.

The workbook specifies these four READ operations for the books collection. fileciteturn2file7L1-L4

Prerequisite

Use the database created in Assignment 3 – Set A – Question 1.

use LibraryDB

Check the collection:

show collections

Expected:

books

The examples below assume the 5 books inserted in Q1.

Title                      Author                Year         Genre               Price         Available

The Alchemist              Paulo Coelho          1988         Fiction             250           true

Clean Code                 Robert C. Martin      2008         Technology          450           true

The Hobbit                 J.R.R. Tolkien        1937         Fantasy             350           false

The Pragmatic Programmer   Andrew Hunt           1999         Technology          550           true

Dune                       Frank Herbert         1965         Science Fiction     400           true

a) Display All Books

Command

db.books.find().pretty()

Explanation

db → current database, LibraryDB.

books → the books collection.

find() → retrieves documents.

pretty() → formats the output for readability.

Expected Result

All 5 book documents are displayed.

b) Display Only the Title and Author Fields

Command

db.books.find(
  {},
  {
    title: 1,
    author: 1,
    _id: 0
  }
).pretty()

Explanation

The first {} means all documents are matched.

The second object is a projection:

{
  title: 1,
  author: 1,
  _id: 0
}

title: 1 → include title.

author: 1 → include author.

_id: 0 → hide MongoDB's automatically generated _id.

Expected Result

{
  title: 'The Alchemist',
  author: 'Paulo Coelho'
}
{
  title: 'Clean Code',
  author: 'Robert C. Martin'
}
{
  title: 'The Hobbit',
  author: 'J.R.R. Tolkien'
}
{
  title: 'The Pragmatic Programmer',
  author: 'Andrew Hunt'
}
{
  title: 'Dune',
  author: 'Frank Herbert'
}

c) Find All Books with Price Greater Than Rs. 300

Command

db.books.find({
  price: {
    $gt: 300
  }
}).pretty()

Explanation

$gt means greater than.

price: { $gt: 300 }

means:

price > 300

Expected Books

Clean Code                  Rs. 450
The Hobbit                  Rs. 350
The Pragmatic Programmer    Rs. 550
Dune                        Rs. 400

The Alchemist is not displayed because its price is Rs. 250.

d) Find Books Sorted by Year in Ascending Order

Command

db.books.find().sort({
  year: 1
}).pretty()

Explanation

sort() arranges the returned documents.

year: 1

means ascending order.

Expected Order

Year   Book

1937   The Hobbit

1965   Dune

1988   The Alchemist

1999   The Pragmatic Programmer

2008   Clean Code


Sorting Values

year: 1

→ Ascending

year: -1

→ Descending

Complete Copy-Paste Command Sheet

// Select database
use LibraryDB

// a) Display all books
db.books.find().pretty()

// b) Display only title and author
db.books.find(
  {},
  {
    title: 1,
    author: 1,
    _id: 0
  }
).pretty()

// c) Find books with price greater than Rs. 300
db.books.find({
  price: {
    $gt: 300
  }
}).pretty()

// d) Find books sorted by year in ascending order
db.books.find().sort({
  year: 1
}).pretty()


```
----

```
Assignment 3 - Set A - 3
// Select database
use LibraryDB

// Check existing books
db.books.find().pretty()


// ==========================================
// Q3(a) Update price of a specific book
// ==========================================

db.books.updateOne(
  { title: "The Alchemist" },
  { $set: { price: 300 } }
)


// Verify price update
db.books.find(
  { title: "The Alchemist" }
).pretty()


// ==========================================
// Q3(b) Make all Fiction books available
// ==========================================

db.books.updateMany(
  { genre: "Fiction" },
  { $set: { available: true } }
)


// Verify Fiction books
db.books.find(
  { genre: "Fiction" }
).pretty()
```
-----

```
# Assignment 3 – Set A – Q4

## Add a new field "discount" (10%) to all books with price > 400 using updateMany() and $set

```javascript
// Select the LibraryDB database
use LibraryDB

// Display all books before updating
// find() displays documents from the books collection
// pretty() formats the output in a readable way
db.books.find().pretty()

// Add a new field "discount" with value "10%" 
// to all books whose price is greater than 400
//
// updateMany() updates ALL documents that match the condition
// { price: { $gt: 400 } } means price greater than 400
// $gt = greater than
// $set adds a new field or updates an existing field
db.books.updateMany(
  { price: { $gt: 400 } },
  { $set: { discount: "10%" } }
)

// Display the books whose price is greater than 400
// This verifies that the discount field was added
db.books.find(
  { price: { $gt: 400 } }
).pretty()

// Display all books that contain the discount field
// $exists: true checks whether the discount field exists
db.books.find(
  { discount: { $exists: true } }
).pretty()
```
----------
```
# Assignment 3 – Set A – Q5 

## MongoDB – Books Collection

---

## Q5. Delete one book by its title using deleteOne(). Then delete all books with available: false using deleteMany()

```javascript
// Select the LibraryDB database
use LibraryDB

// Display all books before deletion
db.books.find().pretty()

// Delete one book by its title
// deleteOne() deletes only ONE document that matches the condition
// Here, the book "The Hobbit" will be deleted
db.books.deleteOne(
  { title: "The Hobbit" }
)

// Display books after deleting "The Hobbit"
db.books.find().pretty()

// Delete all books whose available field is false
// deleteMany() deletes ALL documents matching the condition
// false is a Boolean value, so do not write it as "false"
db.books.deleteMany(
  { available: false }
)

// Display the remaining books after deletion
db.books.find().pretty()
```
-----

```

Q6. Use countDocuments() to count total books, books with price < 200, and available books

// Select the LibraryDB database
use LibraryDB

// Count the total number of books
// countDocuments({}) counts all documents in the books collection
db.books.countDocuments({})

// Count books whose price is less than 200
// $lt means "less than"
// This finds books where price < 200
db.books.countDocuments(
  { price: { $lt: 200 } }
)

// Count books that are available
// available: true selects only books whose available field is true
db.books.countDocuments(
  { available: true }
)

```
------------

```
Q7. Find all books whose genre is either "Science Fiction" or "Technology" using $in
// Select the LibraryDB database
use LibraryDB

// Find books whose genre is either Science Fiction or Technology
// $in checks whether the field value matches ANY value in the given array
// Therefore, this query finds:
// genre = "Science Fiction"
// OR
// genre = "Technology"
db.books.find(
  {
    genre: {
      $in: ["Science Fiction", "Technology"]
    }
  }
).pretty()
```

----------------

```
Q8. Display books published between 2015 and 2025 using $gte and $lte

// Select the LibraryDB database
use LibraryDB

// Find books published between 2015 and 2025
// $gte means "greater than or equal to"
// $lte means "less than or equal to"
// Therefore, this condition means:
// year >= 2015 AND year <= 2025
db.books.find(
  {
    year: {
      $gte: 2015,
      $lte: 2025
    }
  }
).pretty()
```
----------

```
Q9. Increase the price of all books published before 2018 by 5% using $mul

// Select the LibraryDB database
use LibraryDB

// Display books before changing their prices
db.books.find().pretty()

// Increase the price of all books published before 2018 by 5%
//
// $lt: 2018 means the book was published before 2018
// $mul multiplies the existing value by the specified number
//
// Multiplying by 1.05 increases the price by 5%
// Example:
// 400 × 1.05 = 420
//
// Therefore, price: 1.05 means:
// New Price = Old Price × 1.05
db.books.updateMany(
  { year: { $lt: 2018 } },
  { $mul: { price: 1.05 } }
)

// Display the books after the price update
db.books.find().pretty()
```
-----------
```
Q10. Find the top 3 most expensive books using sort() and limit()

// Select the LibraryDB database
use LibraryDB

// Find all books and sort them by price in descending order
// sort({ price: -1 }) sorts prices from highest to lowest
// -1 means descending order
db.books.find()
  .sort({ price: -1 })
  .pretty()

// Find the top 3 most expensive books
// sort({ price: -1 }) puts the most expensive book first
// limit(3) restricts the result to only 3 documents
db.books.find()
  .sort({ price: -1 })
  .limit(3)
  .pretty()
```
