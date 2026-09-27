# Assignment 4 — Set B
## Movie Database Management System — Aggregation and Indexing

## 1. Insert 10 movies

```javascript
use MovieDB

db.Movie.insertMany([
  {MovieID:"M101",MovieName:"Inception",Genre:"Sci-Fi",Rating:8.8,ReleaseYear:2010,Language:"English"},
  {MovieID:"M102",MovieName:"Dune",Genre:"Sci-Fi",Rating:8.7,ReleaseYear:2021,Language:"English"},
  {MovieID:"M103",MovieName:"RRR",Genre:"Action",Rating:8.0,ReleaseYear:2022,Language:"Telugu"},
  {MovieID:"M104",MovieName:"Oppenheimer",Genre:"Drama",Rating:8.9,ReleaseYear:2023,Language:"English"},
  {MovieID:"M105",MovieName:"Dangal",Genre:"Sports",Rating:8.3,ReleaseYear:2016,Language:"Hindi"},
  {MovieID:"M106",MovieName:"3 Idiots",Genre:"Comedy",Rating:8.4,ReleaseYear:2009,Language:"Hindi"},
  {MovieID:"M107",MovieName:"Interstellar",Genre:"Sci-Fi",Rating:8.7,ReleaseYear:2014,Language:"English"},
  {MovieID:"M108",MovieName:"Drishyam",Genre:"Thriller",Rating:8.2,ReleaseYear:2015,Language:"Hindi"},
  {MovieID:"M109",MovieName:"KGF",Genre:"Action",Rating:8.4,ReleaseYear:2018,Language:"Kannada"},
  {MovieID:"M110",MovieName:"Parasite",Genre:"Drama",Rating:8.5,ReleaseYear:2019,Language:"Korean"}
])
```

## 2. Display all movies

```javascript
db.Movie.find().pretty()
```

## 3. Movies after 2020

```javascript
db.Movie.find({ReleaseYear:{$gt:2020}})
```

## 4. Average rating genre-wise

```javascript
db.Movie.aggregate([
  {
    $group:{
      _id:"$Genre",
      AverageRating:{$avg:"$Rating"}
    }
  }
])
```

## 5. Highest-rated movie in each genre

```javascript
db.Movie.aggregate([
  {$sort:{Rating:-1}},
  {
    $group:{
      _id:"$Genre",
      MovieName:{$first:"$MovieName"},
      Rating:{$first:"$Rating"}
    }
  }
])
```

## 6. Count movies language-wise

```javascript
db.Movie.aggregate([
  {
    $group:{
      _id:"$Language",
      TotalMovies:{$sum:1}
    }
  }
])
```

## 7. Ratings greater than 8.5

```javascript
db.Movie.find({Rating:{$gt:8.5}})
```

## 8. Sort by release year ascending

```javascript
db.Movie.find().sort({ReleaseYear:1})
```

## 9. Text index on MovieName

```javascript
db.Movie.createIndex({MovieName:"text"})
```

## 10. Text search

```javascript
db.Movie.find({
  $text:{$search:"Inception"}
})
```

## 11. Compound index on Genre and Rating

```javascript
db.Movie.createIndex({
  Genre:1,
  Rating:-1
})
```

## 12. Analyze query performance

```javascript
db.Movie.find({
  Genre:"Sci-Fi",
  Rating:{$gt:8.5}
}).explain("executionStats")
```

Compare `totalDocsExamined`, `totalKeysExamined`, and the winning execution plan.

## Result
The Movie aggregation queries, text index, compound index, text search, and execution-plan analysis were implemented.
