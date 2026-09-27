# Assignment 1 — Set B
## JSON Design, BSON, Referencing, and Larger Semi-Structured Datasets

## Q1. E-commerce order JSON

```json
{
  "order_id": "ORD1001",
  "customer": {
    "customer_id": "C101",
    "name": "Amit Sharma",
    "address": {
      "street": "MG Road",
      "city": "Pune",
      "pincode": "411001"
    }
  },
  "items": [
    {"product_name": "Laptop", "quantity": 1, "price": 65000},
    {"product_name": "Mouse", "quantity": 2, "price": 900}
  ],
  "order_status": "Confirmed",
  "payment": {
    "method": "UPI",
    "transaction_id": "TXN9001"
  }
}
```

## Q2. University referencing model

### Student document
```json
{
  "_id": "S101",
  "name": "Priya Patil",
  "department_id": "D01"
}
```

### Department document
```json
{
  "_id": "D01",
  "department_name": "Computer Science",
  "hod": "Dr. Mulay"
}
```

`department_id` is the reference from the student document to the department document.

## Q3. XML employee record converted to JSON

```json
{
  "employee": {
    "employee_id": "E101",
    "name": "Rahul Patil",
    "designation": "Developer"
  },
  "projects": [
    {
      "project_id": "P101",
      "project_name": "Banking App",
      "role": "Developer"
    },
    {
      "project_id": "P102",
      "project_name": "CRM System",
      "role": "Tester"
    }
  ],
  "contact": {
    "email": "rahul@example.com",
    "phone": "9876543210"
  }
}
```

## Q4. IPL player dataset

```json
[
  {
    "player_id": "IPL001",
    "name": "Aarav Singh",
    "team": "Mumbai",
    "category": "Batsman",
    "bid_price": 8500000,
    "runs_scored": 520,
    "wickets_taken": 0
  },
  {
    "player_id": "IPL002",
    "name": "Rohan Kumar",
    "team": "Chennai",
    "category": "Bowler",
    "bid_price": 7000000,
    "runs_scored": 90,
    "wickets_taken": 18
  },
  {
    "player_id": "IPL003",
    "name": "Priya Shah",
    "team": "Delhi",
    "category": "All-rounder",
    "bid_price": 11000000,
    "runs_scored": 410,
    "wickets_taken": 12,
    "captain": true
  },
  {
    "player_id": "IPL004",
    "name": "Karan Joshi",
    "team": "Pune",
    "category": "Batsman",
    "bid_price": 6000000,
    "runs_scored": 365
  },
  {
    "player_id": "IPL005",
    "name": "Neha Verma",
    "team": "Bengaluru",
    "category": "Bowler",
    "bid_price": 9000000,
    "runs_scored": 70,
    "wickets_taken": 21,
    "economy": 7.4
  }
]
```

The optional fields `captain` and `economy` demonstrate schema flexibility.

## Q5. BSON vs JSON

| Feature | JSON | BSON |
|---|---|---|
| Representation | Text | Binary encoded |
| ObjectId | Not a standard JSON type | Supported |
| Date | Usually represented as string | Native Date type |
| Binary | Requires encoding such as Base64 | Native Binary type |
| Decimal128 | Not a standard JSON type | Supported |
| MongoDB internal format | No | Yes |

Examples of BSON-specific/additional types:

```javascript
ObjectId("64ab1234ef567890abcd1234")
ISODate("2025-01-01T00:00:00Z")
NumberDecimal("99999.99")
BinData(0, "SGVsbG8=")
```

## Q6. Banking system using references

### Customer
```json
{
  "_id": "C101",
  "name": "Amit Sharma",
  "email": "amit@example.com"
}
```

### Branch
```json
{
  "_id": "B01",
  "branch_name": "Pune Main",
  "location": "Pune"
}
```

### Account
```json
{
  "_id": "A101",
  "account_id": "A101",
  "account_type": "Savings",
  "balance": 85000,
  "customer_id": "C101",
  "branch_id": "B01"
}
```

## Q7. Real-estate property dataset

```json
[
  {
    "property_id": "PR101",
    "title": "2BHK Apartment",
    "location": {"city": "Pune", "area": "Baner", "latitude": 18.559, "longitude": 73.786},
    "price": 8500000,
    "property_type": "Apartment",
    "bedrooms": 2,
    "bathrooms": 2,
    "furnished": true
  },
  {
    "property_id": "PR102",
    "title": "3BHK Villa",
    "location": {"city": "Pune", "area": "Wakad", "latitude": 18.598, "longitude": 73.764},
    "price": 14500000,
    "property_type": "Villa",
    "bedrooms": 3,
    "bathrooms": 3,
    "pool": true,
    "garage": true
  },
  {
    "property_id": "PR103",
    "title": "1BHK Flat",
    "location": {"city": "Mumbai", "area": "Andheri", "latitude": 19.119, "longitude": 72.846},
    "price": 11000000,
    "property_type": "Apartment",
    "bedrooms": 1,
    "bathrooms": 1
  },
  {
    "property_id": "PR104",
    "title": "4BHK Villa",
    "location": {"city": "Nashik", "area": "Gangapur", "latitude": 20.007, "longitude": 73.773},
    "price": 12000000,
    "property_type": "Villa",
    "bedrooms": 4,
    "bathrooms": 4,
    "garage": true
  },
  {
    "property_id": "PR105",
    "title": "2BHK Furnished Flat",
    "location": {"city": "Nagpur", "area": "Dharampeth", "latitude": 21.143, "longitude": 79.073},
    "price": 5500000,
    "property_type": "Apartment",
    "bedrooms": 2,
    "bathrooms": 2,
    "furnished": true
  },
  {
    "property_id": "PR106",
    "title": "3BHK Premium Apartment",
    "location": {"city": "Bengaluru", "area": "Whitefield", "latitude": 12.969, "longitude": 77.750},
    "price": 13500000,
    "property_type": "Apartment",
    "bedrooms": 3,
    "bathrooms": 3,
    "pool": true,
    "furnished": true
  }
]
```

## Q8. Practical BSON scenario

### ObjectId
```javascript
{ _id: ObjectId("64ab1234ef567890abcd1234") }
```
Used as a unique document identifier.

### Date
```javascript
{ createdAt: ISODate("2026-01-10T10:30:00Z") }
```
Represents a real date/time rather than an arbitrary text string.

### Decimal128
```javascript
{ amount: NumberDecimal("125000.75") }
```
Useful for precise financial values.

### Binary
```javascript
{ fileData: BinData(0, "SGVsbG8=") }
```
Represents binary data.

## Q9. Project management XML converted to JSON

```json
{
  "project_id": "P101",
  "project_name": "AI Implementation",
  "team_members": [
    {"name": "Arun", "role": "Lead"},
    {"name": "Pooja", "role": "Developer"}
  ],
  "milestones": [
    {"title": "Planning", "status": "Complete"}
  ]
}
```

## Result
All Set B JSON design, conversion, referencing, BSON, and dataset exercises are completed.
