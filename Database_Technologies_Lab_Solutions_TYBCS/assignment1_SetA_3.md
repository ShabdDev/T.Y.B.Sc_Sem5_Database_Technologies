# Assignment 1 — Set C
## Advanced MongoDB Data Modeling

## Q1. Social Media application

### Users collection
```json
{
  "_id": "U101",
  "name": "John",
  "email": "john@example.com",
  "profile": {
    "city": "Pune",
    "bio": "Computer Science Student"
  }
}
```

### Posts collection with embedded comments
```json
{
  "_id": "P101",
  "user_id": "U101",
  "content": "Learning MongoDB today.",
  "created_at": "2026-09-25T10:00:00Z",
  "comments": [
    {
      "comment_id": "C101",
      "user_id": "U102",
      "text": "Great!",
      "created_at": "2026-09-25T10:05:00Z"
    }
  ]
}
```

### Comments collection
```json
{
  "_id": "C101",
  "post_id": "P101",
  "user_id": "U102",
  "text": "Great!",
  "created_at": "2026-09-25T10:05:00Z"
}
```

### Modeling decision
- User profile is referenced because a user can create many posts/comments.
- Comments can be embedded in a post when they are normally retrieved with the post.
- A separate Comments collection can also be maintained when comments need independent querying or can become very large.

## Q2. Online Food Delivery System

### Restaurant
```json
{
  "_id": "R101",
  "name": "Pune Spice",
  "address": {"city": "Pune", "area": "Kothrud"},
  "menu": [
    {"item_id": "I101", "name": "Paneer Tikka", "price": 280},
    {"item_id": "I102", "name": "Veg Biryani", "price": 220}
  ]
}
```

### Customer
```json
{
  "_id": "C101",
  "name": "Priya Patil",
  "phone": "9876543210",
  "address": {
    "street": "Karve Road",
    "city": "Pune",
    "pincode": "411038"
  }
}
```

### Order
```json
{
  "_id": "O101",
  "customer_id": "C101",
  "restaurant_id": "R101",
  "ordered_items": [
    {"item_id": "I101", "name": "Paneer Tikka", "quantity": 2, "price": 280},
    {"item_id": "I102", "name": "Veg Biryani", "quantity": 1, "price": 220}
  ],
  "total": 780,
  "status": "Delivered"
}
```

### Justification
- Menu items are embedded in Restaurant because they are commonly read with restaurant details.
- Customer address is embedded because it is part of the customer profile.
- Order references Customer and Restaurant because both can participate in many orders.
- Ordered items are embedded because an order is normally retrieved together with its line items and the historical price should remain with the order.

## Q3. JSON limitations and BSON solutions

| JSON limitation | BSON/MongoDB solution |
|---|---|
| No native ObjectId | BSON `ObjectId` |
| Date often represented as text | BSON `Date` |
| No standard Decimal128 | BSON `Decimal128` |
| Binary data needs text encoding | BSON `Binary` |
| Limited numeric type distinction | BSON numeric types such as Int32, Int64, Double, Decimal128 |

### Example
```javascript
{
  _id: ObjectId("64ab1234ef567890abcd1234"),
  createdAt: ISODate("2026-09-25T10:30:00Z"),
  amount: NumberDecimal("125000.75"),
  document: BinData(0, "SGVsbG8=")
}
```

## Result
The advanced data models demonstrate embedding, referencing, nested structures, arrays, and BSON-specific capabilities.
