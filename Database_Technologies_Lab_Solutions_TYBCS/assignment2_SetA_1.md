# Assignment 2 — Set A
## Installation and Configuration of MongoDB with Database and Collection Creation

> The workbook's Set A requires a `Movie` database, `Film` and `Actor` collections, at least 10 documents in each, and the listed CRUD/database queries.

## 1. Create database

Run in `mongosh`:

```javascript
use Movie
```

Expected:
```text
switched to db Movie
```

## 2. Create Film and Actor collections

```javascript
db.createCollection("Film")
db.createCollection("Actor")
```

## 3. Insert 10 Film documents

```javascript
db.Film.insertMany([
  {
    filmId: "F101",
    title: "Inception",
    year: 2010,
    genres: ["Action", "Sci-Fi", "Thriller"],
    actors: [
      {firstName: "Leonardo", lastName: "DiCaprio"},
      {firstName: "Joseph", lastName: "Gordon-Levitt"}
    ],
    directors: [
      {firstName: "Christopher", lastName: "Nolan"}
    ],
    releaseDetails: [
      {place: "USA", date: ISODate("2010-07-16"), rating: 4.7},
      {place: "India", date: ISODate("2010-07-16"), rating: 4.6}
    ]
  },
  {
    filmId: "F102", title: "Interstellar", year: 2014,
    genres: ["Sci-Fi", "Drama"],
    actors: [{firstName: "Matthew", lastName: "McConaughey"}],
    directors: [{firstName: "Christopher", lastName: "Nolan"}],
    releaseDetails: [{place: "India", date: ISODate("2014-11-07"), rating: 4.8}]
  },
  {
    filmId: "F103", title: "The Matrix", year: 1999,
    genres: ["Action", "Sci-Fi"],
    actors: [{firstName: "Keanu", lastName: "Reeves"}],
    directors: [{firstName: "Lana", lastName: "Wachowski"}, {firstName: "Lilly", lastName: "Wachowski"}],
    releaseDetails: [{place: "USA", date: ISODate("1999-03-31"), rating: 4.6}]
  },
  {
    filmId: "F104", title: "Titanic", year: 1997,
    genres: ["Romantic", "Drama"],
    actors: [{firstName: "Leonardo", lastName: "DiCaprio"}],
    directors: [{firstName: "James", lastName: "Cameron"}],
    releaseDetails: [{place: "USA", date: ISODate("1997-12-19"), rating: 4.5}]
  },
  {
    filmId: "F105", title: "Avatar", year: 2009,
    genres: ["Action", "Sci-Fi"],
    actors: [{firstName: "Sam", lastName: "Worthington"}],
    directors: [{firstName: "James", lastName: "Cameron"}],
    releaseDetails: [{place: "USA", date: ISODate("2009-12-18"), rating: 4.4}]
  },
  {
    filmId: "F106", title: "The Dark Knight", year: 2008,
    genres: ["Action", "Crime"],
    actors: [{firstName: "Christian", lastName: "Bale"}],
    directors: [{firstName: "Christopher", lastName: "Nolan"}],
    releaseDetails: [{place: "USA", date: ISODate("2008-07-18"), rating: 4.9}]
  },
  {
    filmId: "F107", title: "Dangal", year: 2016,
    genres: ["Sports", "Drama"],
    actors: [{firstName: "Aamir", lastName: "Khan"}],
    directors: [{firstName: "Nitesh", lastName: "Tiwari"}],
    releaseDetails: [{place: "India", date: ISODate("2016-12-23"), rating: 4.5}]
  },
  {
    filmId: "F108", title: "3 Idiots", year: 2009,
    genres: ["Comedy", "Drama"],
    actors: [{firstName: "Aamir", lastName: "Khan"}],
    directors: [{firstName: "Rajkumar", lastName: "Hirani"}],
    releaseDetails: [{place: "India", date: ISODate("2009-12-25"), rating: 4.8}]
  },
  {
    filmId: "F109", title: "RRR", year: 2022,
    genres: ["Action", "Drama"],
    actors: [{firstName: "Ram", lastName: "Charan"}],
    directors: [{firstName: "S. S.", lastName: "Rajamouli"}],
    releaseDetails: [{place: "India", date: ISODate("2022-03-25"), rating: 4.6}]
  },
  {
    filmId: "F110", title: "Oppenheimer", year: 2023,
    genres: ["Drama", "History"],
    actors: [{firstName: "Cillian", lastName: "Murphy"}],
    directors: [{firstName: "Christopher", lastName: "Nolan"}],
    releaseDetails: [{place: "India", date: ISODate("2023-07-21"), rating: 4.7}]
  }
])
```

## 4. Insert 10 Actor documents

```javascript
db.Actor.insertMany([
  {actorId:"A101", firstName:"Leonardo", lastName:"DiCaprio", address:{street:"MG Road",city:"Pune",state:"Maharashtra",country:"India",pincode:"411001"}, contact:{email:"leo@example.com",phone:"9000000001"}, age:51},
  {actorId:"A102", firstName:"Joseph", lastName:"Gordon-Levitt", address:{street:"Main Street",city:"Los Angeles",state:"California",country:"USA",pincode:"90001"}, contact:{email:"joseph@example.com",phone:"9000000002"}, age:45},
  {actorId:"A103", firstName:"Matthew", lastName:"McConaughey", address:{street:"Lake Road",city:"Austin",state:"Texas",country:"USA",pincode:"73301"}, contact:{email:"matthew@example.com",phone:"9000000003"}, age:56},
  {actorId:"A104", firstName:"Keanu", lastName:"Reeves", address:{street:"Sunset Blvd",city:"Los Angeles",state:"California",country:"USA",pincode:"90001"}, contact:{email:"keanu@example.com",phone:"9000000004"}, age:62},
  {actorId:"A105", firstName:"James", lastName:"Cameron", address:{street:"King Road",city:"Toronto",state:"Ontario",country:"Canada",pincode:"M5H1A1"}, contact:{email:"james@example.com",phone:"9000000005"}, age:72},
  {actorId:"A106", firstName:"Sam", lastName:"Worthington", address:{street:"Park Road",city:"Perth",state:"WA",country:"Australia",pincode:"6000"}, contact:{email:"sam@example.com",phone:"9000000006"}, age:50},
  {actorId:"A107", firstName:"Christian", lastName:"Bale", address:{street:"Oxford Road",city:"Haverfordwest",state:"Wales",country:"UK",pincode:"SA61"}, contact:{email:"christian@example.com",phone:"9000000007"}, age:52},
  {actorId:"A108", firstName:"Aamir", lastName:"Khan", address:{street:"Hill Road",city:"Mumbai",state:"Maharashtra",country:"India",pincode:"400050"}, contact:{email:"aamir@example.com",phone:"9000000008"}, age:61},
  {actorId:"A109", firstName:"Ram", lastName:"Charan", address:{street:"Film Nagar",city:"Hyderabad",state:"Telangana",country:"India",pincode:"500033"}, contact:{email:"ram@example.com",phone:"9000000009"}, age:41},
  {actorId:"A110", firstName:"Cillian", lastName:"Murphy", address:{street:"Cork Road",city:"Cork",state:"Munster",country:"Ireland",pincode:"T12"}, contact:{email:"cillian@example.com",phone:"9000000010"}, age:50}
])
```

## 5. Display all documents

```javascript
db.Film.find().pretty()
db.Actor.find().pretty()
```

## 6. Find Film by title

```javascript
db.Film.find({ title: "Inception" }).pretty()
```

## 7. Find Actor by first name

```javascript
db.Actor.find({ firstName: "Aamir" }).pretty()
```

## 8. Display only Film titles

```javascript
db.Film.find({}, { _id: 0, title: 1 })
```

## 9. Delete a Film

```javascript
db.Film.deleteOne({ title: "Titanic" })
```

## 10. Count total Films

```javascript
db.Film.countDocuments()
```

## 11. Remove all documents with a specific Film ID

Example:

```javascript
db.Film.deleteMany({ filmId: "F110" })
```

## 12. Remove first Actor record

The workbook describes removing the first record. MongoDB's `deleteOne()` does not guarantee insertion-order selection without a sort. A deterministic approach is:

```javascript
const firstActor = db.Actor.find().sort({ _id: 1 }).limit(1).next()
db.Actor.deleteOne({ _id: firstActor._id })
```

## 13. Drop Movie database

```javascript
db.dropDatabase()
```

## Result
The `Movie` database, `Film` and `Actor` collections, sample records, retrieval, deletion, counting, and database-drop operations were implemented.
