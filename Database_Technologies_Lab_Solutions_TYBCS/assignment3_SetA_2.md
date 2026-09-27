# Assignment 3 — Set B
## Advanced CRUD, Embedded Documents, Arrays, Upsert and bulkWrite

## Q1. Hospital database and complete CRUD

```javascript
use hospital

db.patients.insertMany([
  {patientId:"P101",name:"Amit",age:45,disease:"Diabetes",ward:"General Ward",admissionDate:ISODate("2026-09-01")},
  {patientId:"P102",name:"Priya",age:32,disease:"Fever",ward:"General Ward",admissionDate:ISODate("2026-09-02")},
  {patientId:"P103",name:"Rahul",age:55,disease:"Hypertension",ward:"ICU",admissionDate:ISODate("2026-09-03")},
  {patientId:"P104",name:"Sneha",age:42,disease:"Diabetes",ward:"General Ward",admissionDate:ISODate("2026-09-04")},
  {patientId:"P105",name:"Karan",age:29,disease:"Fever",ward:"General Ward",admissionDate:ISODate("2026-09-05")}
])

// READ
db.patients.find().pretty()
db.patients.find({patientId:"P101"})

// UPDATE
db.patients.updateOne(
  {patientId:"P101"},
  {$set:{age:46}}
)

// DELETE
db.patients.deleteOne({patientId:"P105"})
```

## Q2. `$and` and `$or`

### General Ward and age > 40
```javascript
db.patients.find({
  $and:[
    {ward:"General Ward"},
    {age:{$gt:40}}
  ]
})
```

### Diabetes OR Fever
```javascript
db.patients.find({
  $or:[
    {disease:"Diabetes"},
    {disease:"Fever"}
  ]
})
```

## Q3. Embedded address

```javascript
db.students.insertOne({
  studentId:"S101",
  name:"Pooja",
  address:{
    street:"MG Road",
    city:"Pune",
    pincode:"411001"
  }
})

db.students.find({"address.city":"Pune"})

db.students.updateOne(
  {studentId:"S101"},
  {$set:{"address.pincode":"411002"}}
)
```

## Q4. Courses array with `$push` and `$pull`

```javascript
db.students.updateOne(
  {studentId:"S101"},
  {$push:{courses:"MongoDB"}}
)

db.students.updateOne(
  {studentId:"S101"},
  {$pull:{courses:"MongoDB"}}
)

db.students.find({courses:"MongoDB"})
```

## Q5. Upsert employee

```javascript
db.employees.updateOne(
  {employeeId:"E999"},
  {$set:{name:"New Employee",salary:50000,designation:"Developer"}},
  {upsert:true}
)
```

If `E999` does not exist, a new employee is inserted. If it exists, the salary/designation fields are updated.

## Q6. bulkWrite

```javascript
db.products.bulkWrite([
  {
    insertOne:{
      document:{
        productId:"P201",
        name:"Wireless Keyboard",
        stock:50,
        status:"Active"
      }
    }
  },
  {
    updateOne:{
      filter:{productId:"P101"},
      update:{$inc:{stock:10}}
    }
  },
  {
    deleteOne:{
      filter:{productId:"P999",status:"Discontinued"}
    }
  }
])
```

## Q7. Increase age of General Ward patients

```javascript
db.patients.updateMany(
  {ward:"General Ward"},
  {$inc:{age:1}}
)
```

## Q8. Remove ward field

```javascript
db.patients.updateMany(
  {},
  {$unset:{ward:""}}
)
```

## Q9. Skills array operations

```javascript
db.students.insertMany([
  {studentId:"S102",name:"Amit",skills:["Java","SQL"]},
  {studentId:"S103",name:"Priya",skills:["Python","MongoDB"]}
])

// Add
db.students.updateOne(
  {studentId:"S102"},
  {$push:{skills:"Docker"}}
)

// Remove
db.students.updateOne(
  {studentId:"S102"},
  {$pull:{skills:"Java"}}
)

// Search
db.students.find({skills:"MongoDB"})
```

## Result
The hospital, embedded-document, array, upsert, bulk-write, increment, unset, push, pull, and search operations were implemented.
