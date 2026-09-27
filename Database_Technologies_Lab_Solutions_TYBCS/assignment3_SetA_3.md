# Assignment 3 — Set C
## E-commerce CRUD and Conditional Updates

## Q1. E-commerce products and orders

```javascript
use ecommerce

db.products.insertMany([
  {productId:"P101",name:"Laptop",category:"Electronics",price:65000,stock:10},
  {productId:"P102",name:"Mouse",category:"Accessories",price:900,stock:40},
  {productId:"P103",name:"Keyboard",category:"Accessories",price:1500,stock:25}
])

db.orders.insertMany([
  {
    orderId:"O101",
    customerId:"C101",
    items:[
      {productId:"P101",name:"Laptop",quantity:1,price:65000},
      {productId:"P102",name:"Mouse",quantity:2,price:900}
    ],
    total:66800,
    status:"Confirmed"
  },
  {
    orderId:"O102",
    customerId:"C102",
    items:[
      {productId:"P103",name:"Keyboard",quantity:1,price:1500}
    ],
    total:1500,
    status:"Delivered"
  }
])
```

### CREATE
```javascript
db.products.insertOne({
  productId:"P104",
  name:"Monitor",
  category:"Electronics",
  price:18000,
  stock:8
})
```

### READ
```javascript
db.products.find().pretty()
db.orders.find({customerId:"C101"}).pretty()
```

### UPDATE
```javascript
db.products.updateOne(
  {productId:"P102"},
  {$inc:{stock:5}}
)
```

### DELETE
```javascript
db.products.deleteOne({productId:"P104"})
```

## Q2. `$rename` and `$mul`

```javascript
db.products.updateMany(
  {},
  {$rename:{stock:"stock_quantity"}}
)

db.products.updateMany(
  {},
  {$mul:{price:1.18}}
)
```

The first operation renames the field; the second multiplies every price by `1.18`.

## Q3. `$min` and `$max`

```javascript
db.employees.insertMany([
  {employeeId:"E101",name:"Amit",salary:65000},
  {employeeId:"E102",name:"Priya",salary:72000}
])

// Update salary only when the new value is lower.
db.employees.updateOne(
  {employeeId:"E101"},
  {$min:{salary:60000}}
)

// Update salary only when the new value is higher.
db.employees.updateOne(
  {employeeId:"E102"},
  {$max:{salary:80000}}
)
```

## Result
The e-commerce CRUD operations and conditional update operators required by Set C were demonstrated.
