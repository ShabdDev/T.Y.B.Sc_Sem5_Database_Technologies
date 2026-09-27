# Assignment 2 — Set B
## Company Database: Employee and Transaction Collections

## 1. Create database

```javascript
use Company
```

## 2. Create collections

```javascript
db.createCollection("Employee")
db.createCollection("Transaction")
```

## 3. Insert 10 Employees

```javascript
db.Employee.insertMany([
  {employeeId:"E101",firstName:"Amit",lastName:"Sharma",email:"amit@example.com",phone:"9000000101",address:{houseNo:101,street:"MG Road",city:"Pune",state:"Maharashtra",country:"India",pincode:"411001"},salary:65000,designation:"Developer",experience:3,dateOfJoining:ISODate("2023-06-01"),birthdate:ISODate("1998-04-10")},
  {employeeId:"E102",firstName:"Priya",lastName:"Patil",email:"priya@example.com",phone:"9000000102",address:{houseNo:102,street:"FC Road",city:"Pune",state:"Maharashtra",country:"India",pincode:"411004"},salary:72000,designation:"Tester",experience:4,dateOfJoining:ISODate("2022-07-01"),birthdate:ISODate("1997-08-12")},
  {employeeId:"E103",firstName:"Rahul",lastName:"Desai",email:"rahul@example.com",phone:"9000000103",address:{houseNo:103,street:"Park Road",city:"Mumbai",state:"Maharashtra",country:"India",pincode:"400001"},salary:90000,designation:"Manager",experience:8,dateOfJoining:ISODate("2018-03-15"),birthdate:ISODate("1992-02-20")},
  {employeeId:"E104",firstName:"Sneha",lastName:"Joshi",email:"sneha@example.com",phone:"9000000104",address:{houseNo:104,street:"College Road",city:"Nashik",state:"Maharashtra",country:"India",pincode:"422005"},salary:68000,designation:"Developer",experience:5,dateOfJoining:ISODate("2021-01-10"),birthdate:ISODate("1996-05-05")},
  {employeeId:"E105",firstName:"Karan",lastName:"Mehta",email:"karan@example.com",phone:"9000000105",address:{houseNo:105,street:"Ring Road",city:"Nagpur",state:"Maharashtra",country:"India",pincode:"440001"},salary:55000,designation:"Support Engineer",experience:2,dateOfJoining:ISODate("2024-01-10"),birthdate:ISODate("2000-01-15")},
  {employeeId:"E106",firstName:"Neha",lastName:"Verma",email:"neha@example.com",phone:"9000000106",address:{houseNo:106,street:"Station Road",city:"Pune",state:"Maharashtra",country:"India",pincode:"411005"},salary:78000,designation:"Developer",experience:6,dateOfJoining:ISODate("2020-05-10"),birthdate:ISODate("1995-03-22")},
  {employeeId:"E107",firstName:"Rohan",lastName:"Kulkarni",email:"rohan@example.com",phone:"9000000107",address:{houseNo:107,street:"Main Road",city:"Kolhapur",state:"Maharashtra",country:"India",pincode:"416001"},salary:62000,designation:"Analyst",experience:4,dateOfJoining:ISODate("2022-04-01"),birthdate:ISODate("1997-12-11")},
  {employeeId:"E108",firstName:"Pooja",lastName:"Nair",email:"pooja@example.com",phone:"9000000108",address:{houseNo:108,street:"Beach Road",city:"Kochi",state:"Kerala",country:"India",pincode:"682001"},salary:85000,designation:"Manager",experience:7,dateOfJoining:ISODate("2019-04-01"),birthdate:ISODate("1993-11-10")},
  {employeeId:"E109",firstName:"Vikas",lastName:"Shah",email:"vikas@example.com",phone:"9000000109",address:{houseNo:109,street:"Law College Road",city:"Pune",state:"Maharashtra",country:"India",pincode:"411004"},salary:74000,designation:"Developer",experience:5,dateOfJoining:ISODate("2021-06-01"),birthdate:ISODate("1996-09-18")},
  {employeeId:"E110",firstName:"Rani",lastName:"Deshmukh",email:"rani@example.com",phone:"9000000110",address:{houseNo:110,street:"Civil Lines",city:"Nagpur",state:"Maharashtra",country:"India",pincode:"440001"},salary:58000,designation:"HR Executive",experience:3,dateOfJoining:ISODate("2023-01-01"),birthdate:ISODate("1999-07-19")}
])
```

## 4. Insert 10 Transactions

```javascript
db.Transaction.insertMany([
  {transactionId:"T101",transactionDate:ISODate("2026-09-01"),employeeName:{firstName:"Amit",lastName:"Sharma"},details:{itemId:"I101",itemName:"Laptop",quantity:1,price:65000},payment:{type:"Credit Card",totalAmount:65000,successful:true}},
  {transactionId:"T102",transactionDate:ISODate("2026-09-02"),employeeName:{firstName:"Priya",lastName:"Patil"},details:{itemId:"I102",itemName:"Mouse",quantity:2,price:1800},payment:{type:"Cash",totalAmount:1800,successful:true}},
  {transactionId:"T103",transactionDate:ISODate("2026-09-03"),employeeName:{firstName:"Rahul",lastName:"Desai"},details:{itemId:"I103",itemName:"Monitor",quantity:1,price:18000},payment:{type:"Debit Card",totalAmount:18000,successful:true}},
  {transactionId:"T104",transactionDate:ISODate("2026-09-04"),employeeName:{firstName:"Sneha",lastName:"Joshi"},details:{itemId:"I104",itemName:"Keyboard",quantity:3,price:4500},payment:{type:"Credit Card",totalAmount:4500,successful:true}},
  {transactionId:"T105",transactionDate:ISODate("2026-09-05"),employeeName:{firstName:"Karan",lastName:"Mehta"},details:{itemId:"I105",itemName:"Printer",quantity:1,price:12000},payment:{type:"Cash",totalAmount:12000,successful:true}},
  {transactionId:"T106",transactionDate:ISODate("2026-09-06"),employeeName:{firstName:"Neha",lastName:"Verma"},details:{itemId:"I106",itemName:"SSD",quantity:2,price:10000},payment:{type:"Credit Card",totalAmount:20000,successful:true}},
  {transactionId:"T107",transactionDate:ISODate("2026-09-07"),employeeName:{firstName:"Rohan",lastName:"Kulkarni"},details:{itemId:"I107",itemName:"Router",quantity:1,price:3500},payment:{type:"Debit Card",totalAmount:3500,successful:true}},
  {transactionId:"T108",transactionDate:ISODate("2026-09-08"),employeeName:{firstName:"Pooja",lastName:"Nair"},details:{itemId:"I108",itemName:"Tablet",quantity:1,price:30000},payment:{type:"Credit Card",totalAmount:30000,successful:true}},
  {transactionId:"T109",transactionDate:ISODate("2026-09-09"),employeeName:{firstName:"Vikas",lastName:"Shah"},details:{itemId:"I109",itemName:"Webcam",quantity:2,price:5000},payment:{type:"Cash",totalAmount:10000,successful:true}},
  {transactionId:"T110",transactionDate:ISODate("2026-09-10"),employeeName:{firstName:"Rani",lastName:"Deshmukh"},details:{itemId:"I110",itemName:"Headset",quantity:2,price:3000},payment:{type:"Credit Card",totalAmount:6000,successful:true}}
])
```

## 5. Display all documents

```javascript
db.Employee.find().pretty()
db.Transaction.find().pretty()
```

## 6. Find employee by Employee ID

```javascript
db.Employee.find({ employeeId: "E103" })
```

## 7. Find employee by designation

```javascript
db.Employee.find({ designation: "Developer" })
```

## 8. Delete one transaction

```javascript
db.Transaction.deleteOne({ transactionId: "T110" })
```

## 9. Count transactions and employees

```javascript
db.Transaction.countDocuments()
db.Employee.countDocuments()
```

## 10. Find Credit Card payments

```javascript
db.Transaction.find({ "payment.type": "Credit Card" }).pretty()
```

## 11. Delete employee by first and last name

```javascript
db.Employee.deleteOne({ firstName: "Rani", lastName: "Deshmukh" })
```

## 12. Remove first Employee record

```javascript
const firstEmployee = db.Employee.find().sort({ _id: 1 }).limit(1).next()
db.Employee.deleteOne({ _id: firstEmployee._id })
```

## Result
The Company database, Employee and Transaction collections, 10+ records, searches, deletes, and counts were implemented.
