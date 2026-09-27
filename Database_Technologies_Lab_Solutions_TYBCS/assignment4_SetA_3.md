# Assignment 4 — Set C
## Product Inventory Management System

## 1. Insert 10 products

```javascript
use ProductDB

db.Product.insertMany([
  {ProductID:"P101",ProductName:"Laptop",Category:"Electronics",Price:65000,Quantity:10,Supplier:"TechCorp"},
  {ProductID:"P102",ProductName:"Mouse",Category:"Accessories",Price:900,Quantity:50,Supplier:"CompWorld"},
  {ProductID:"P103",ProductName:"Keyboard",Category:"Accessories",Price:1500,Quantity:25,Supplier:"CompWorld"},
  {ProductID:"P104",ProductName:"Monitor",Category:"Electronics",Price:18000,Quantity:15,Supplier:"TechCorp"},
  {ProductID:"P105",ProductName:"Printer",Category:"Office",Price:12000,Quantity:8,Supplier:"OfficeHub"},
  {ProductID:"P106",ProductName:"SSD",Category:"Storage",Price:7000,Quantity:30,Supplier:"TechCorp"},
  {ProductID:"P107",ProductName:"HDD",Category:"Storage",Price:5000,Quantity:18,Supplier:"DataStore"},
  {ProductID:"P108",ProductName:"Webcam",Category:"Accessories",Price:3500,Quantity:12,Supplier:"CompWorld"},
  {ProductID:"P109",ProductName:"Tablet",Category:"Electronics",Price:30000,Quantity:20,Supplier:"TechCorp"},
  {ProductID:"P110",ProductName:"Chair",Category:"Office",Price:8000,Quantity:22,Supplier:"OfficeHub"}
])
```

## 2. Display all products

```javascript
db.Product.find().pretty()
```

## 3. Quantity less than 20

```javascript
db.Product.find({Quantity:{$lt:20}})
```

## 4. Total quantity category-wise

```javascript
db.Product.aggregate([
  {
    $group:{
      _id:"$Category",
      TotalQuantity:{$sum:"$Quantity"}
    }
  }
])
```

## 5. Average price category-wise

```javascript
db.Product.aggregate([
  {
    $group:{
      _id:"$Category",
      AveragePrice:{$avg:"$Price"}
    }
  }
])
```

## 6. Most expensive product in each category

```javascript
db.Product.aggregate([
  {$sort:{Price:-1}},
  {
    $group:{
      _id:"$Category",
      ProductName:{$first:"$ProductName"},
      Price:{$first:"$Price"}
    }
  }
])
```

## 7. Count products by supplier

```javascript
db.Product.aggregate([
  {
    $group:{
      _id:"$Supplier",
      ProductCount:{$sum:1}
    }
  }
])
```

## 8. Sort products by price descending

```javascript
db.Product.find().sort({Price:-1})
```

## 9. Single-field index on ProductName

```javascript
db.Product.createIndex({ProductName:1})
```

## 10. Compound index on Category and Price

```javascript
db.Product.createIndex({
  Category:1,
  Price:-1
})
```

## 11. Unique index on ProductID

```javascript
db.Product.createIndex(
  {ProductID:1},
  {unique:true}
)
```

## 12. Compare query execution statistics

```javascript
db.Product.find({ProductID:"P101"}).explain("executionStats")
```

Check:
- `executionStats.totalDocsExamined`
- `executionStats.totalKeysExamined`
- `executionStats.executionTimeMillis`
- winning plan

## Result
Product inventory aggregation, sorting, and all required index types were implemented.
