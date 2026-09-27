# Assignment 4 — Set A
## Employee Management System — Aggregation and Indexing

## 1. Create collection and insert 10 employees

```javascript
use EmployeeDB

db.Employee.insertMany([
  {EmpID:"E101",Name:"Amit",Department:"IT",Salary:65000,City:"Pune",Experience:3},
  {EmpID:"E102",Name:"Priya",Department:"HR",Salary:72000,City:"Mumbai",Experience:5},
  {EmpID:"E103",Name:"Rahul",Department:"IT",Salary:90000,City:"Pune",Experience:8},
  {EmpID:"E104",Name:"Sneha",Department:"Finance",Salary:85000,City:"Nashik",Experience:7},
  {EmpID:"E105",Name:"Karan",Department:"HR",Salary:60000,City:"Pune",Experience:4},
  {EmpID:"E106",Name:"Neha",Department:"IT",Salary:78000,City:"Mumbai",Experience:6},
  {EmpID:"E107",Name:"Rohan",Department:"Finance",Salary:95000,City:"Pune",Experience:10},
  {EmpID:"E108",Name:"Pooja",Department:"HR",Salary:68000,City:"Nashik",Experience:3},
  {EmpID:"E109",Name:"Vikas",Department:"IT",Salary:82000,City:"Pune",Experience:5},
  {EmpID:"E110",Name:"Rani",Department:"Finance",Salary:75000,City:"Mumbai",Experience:6}
])
```

## 2. Display all employee records

```javascript
db.Employee.find().pretty()
```

## 3. Salary greater than ₹60,000

```javascript
db.Employee.find({Salary:{$gt:60000}})
```

## 4. Average salary department-wise

```javascript
db.Employee.aggregate([
  {
    $group:{
      _id:"$Department",
      AverageSalary:{$avg:"$Salary"}
    }
  }
])
```

## 5. Highest salary in each department

```javascript
db.Employee.aggregate([
  {
    $group:{
      _id:"$Department",
      HighestSalary:{$max:"$Salary"}
    }
  }
])
```

## 6. Employee count city-wise

```javascript
db.Employee.aggregate([
  {
    $group:{
      _id:"$City",
      EmployeeCount:{$sum:1}
    }
  }
])
```

## 7. Experience greater than 5 years

```javascript
db.Employee.find({Experience:{$gt:5}})
```

## 8. Salary descending

```javascript
db.Employee.find().sort({Salary:-1})
```

## 9. Single-field index on Name

```javascript
db.Employee.createIndex({Name:1})
```

Expected index name:
```text
Name_1
```

## 10. Unique index on EmpID

```javascript
db.Employee.createIndex(
  {EmpID:1},
  {unique:true}
)
```

Expected index name:
```text
EmpID_1
```

## 11. Explain before/after indexing

Before creating an appropriate index, run:

```javascript
db.Employee.find({Name:"Amit"}).explain("executionStats")
```

After creating `Name_1`, run the same query:

```javascript
db.Employee.find({Name:"Amit"}).explain("executionStats")
```

Compare:
- `executionStats.totalDocsExamined`
- `executionStats.totalKeysExamined`
- execution time
- winning plan

> Exact execution statistics depend on the MongoDB version, dataset, hardware, and cache state. Do not copy a fixed timing as a universal result.

## Result
Aggregation operations and single-field/unique indexes were implemented. Query execution statistics can be compared with `explain("executionStats")`.
