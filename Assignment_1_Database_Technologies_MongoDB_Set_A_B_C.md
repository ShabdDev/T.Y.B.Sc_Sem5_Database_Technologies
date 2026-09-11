# Assignment 1 — Design and Representation of Data using Structured, Semi-Structured, and JSON Formats

**Course:** T.Y.B.Sc. Computer Science — Database Technologies  
**Practical:** Assignment 1  
**Total Slots:** 2  
**Topics:** Structured Data, Semi-Structured Data, JSON, BSON, MongoDB Data Modeling

---

## 1. Aim

To design and represent data using:

1. Structured data
2. Semi-structured data
3. JSON format
4. MongoDB/BSON documents
5. Embedding and referencing

The assignment also introduces practical MongoDB data-modeling concepts.

---

# 2. Theory Required Before the Practical

## 2.1 Structured Data

Structured data has a **fixed and predefined schema**.

Example:

| Student_ID | Name | Age | Marks | Department |
|---|---|---:|---:|---|
| 101 | Anushka | 20 | 85 | Computer Science |
| 102 | Rahul | 21 | 78 | Information Technology |

### Key points

- Stored in rows and columns.
- Fixed schema.
- Data types are predefined.
- Commonly stored in relational databases.
- Queried using SQL.

**Examples:** MySQL, PostgreSQL, Oracle.

### Advantages

- Easy to query using SQL.
- Strong consistency and integrity.
- Good for transactions.
- Suitable for banking, payroll, ERP, etc.

### Limitations

- Rigid schema.
- Difficult to handle changing fields.
- Not suitable for complex/semi-structured data such as JSON documents and multimedia.
- Horizontal scaling can be difficult.

---

# 2.2 Semi-Structured Data

Semi-structured data does not follow a rigid table structure but contains organizational information such as **keys, tags, attributes or nested objects**.

Examples:

- JSON
- XML
- YAML
- HTML
- Email headers

Example:

```xml
<student>
    <student_id>101</student_id>
    <name>Anushka</name>
    <age>20</age>
    <department>Computer Science</department>
    <marks>85</marks>
</student>
```

Another document can contain an additional field:

```xml
<student>
    <student_id>102</student_id>
    <name>Rahul</name>
    <age>21</age>
    <department>Information Technology</department>
    <marks>78</marks>
    <hostel>Yes</hostel>
</student>
```

The second record has `hostel`, while the first does not.

### Key points

- No rigid schema.
- Records may contain different fields.
- Supports nested structures.
- More flexible than relational tables.
- Useful for web applications, APIs and IoT data.

---

# 2.3 JSON

**JSON = JavaScript Object Notation**

JSON is a lightweight, text-based format commonly used to represent semi-structured data.

### JSON object

```json
{
  "student_id": 101,
  "name": "Anushka",
  "age": 20,
  "department": "Computer Science"
}
```

### JSON rules

| Rule | Meaning |
|---|---|
| `{ }` | Object |
| `[ ]` | Array |
| `"key": value` | Key-value pair |
| `,` | Separates items |
| Strings | Use double quotes |
| `true/false` | Boolean |
| `null` | Empty/missing value |

### JSON data types

- String
- Number
- Boolean
- Array
- Object
- Null

Example:

```json
{
  "name": "Anushka",
  "age": 20,
  "is_active": true,
  "subjects": ["Python", "MongoDB"],
  "address": {
    "city": "Pune"
  },
  "middle_name": null
}
```

---

# 2.4 BSON

**BSON = Binary JSON**

MongoDB stores documents internally in BSON.

BSON extends JSON-like documents with additional data types such as:

- ObjectId
- Date
- Binary
- Decimal128
- Int32 / Int64

### Why MongoDB uses BSON

- Efficient encoding/decoding.
- Supports additional data types.
- Supports embedded documents and arrays.
- Provides MongoDB-specific types such as `ObjectId`.

### Example

```javascript
{
  _id: ObjectId("64ab1234ef567890abcd1234"),
  name: "Anushka",
  dob: ISODate("2005-06-15"),
  marks: 85
}
```

---

# 2.5 JSON vs BSON

| Feature | JSON | BSON |
|---|---|---|
| Format | Text | Binary |
| Used for | Data exchange | MongoDB internal document storage |
| ObjectId | No native type | Yes |
| Date | No native date type | Yes |
| Binary data | Limited | Supported |
| Decimal128 | No | Yes |
| Human-readable | Yes | Not directly |
| MongoDB | Input/representation | Internal storage format |

---

# 2.6 MongoDB Basic Structure

Remember:

```text
MongoDB
   |
   +-- Database
         |
         +-- Collection
                |
                +-- Document
                       |
                       +-- Fields
```

### Relational comparison

```text
RDBMS                 MongoDB
--------------------------------------
Database          →   Database
Table             →   Collection
Row               →   Document
Column            →   Field
Primary Key       →   _id
```

---

# 2.7 Embedding vs Referencing

## Embedding

Related data is stored inside the same document.

Use when data is:

- Frequently accessed together.
- Usually read together.
- Relatively small.

Example:

```javascript
{
  order_id: 501,
  customer: "Rahul",
  items: [
    { product: "Laptop", qty: 1, price: 55000 },
    { product: "Mouse", qty: 2, price: 500 }
  ],
  total: 56000
}
```

## Referencing

Related data is stored in separate collections and connected using identifiers.

Use when:

- Data is large.
- Data is shared by many documents.
- There are many-to-many relationships.

Example:

```javascript
// Student
{
  _id: ObjectId("abc"),
  name: "Priya",
  dept_id: ObjectId("xyz")
}

// Department
{
  _id: ObjectId("xyz"),
  dept_name: "Computer Science",
  hod: "Dr. Mulay"
}
```

### Simple rule

```text
Read together frequently → EMBEDDING

Large/shared/many-to-many → REFERENCING
```

---

# 3. Software Required

For this practical, use:

1. **MongoDB Community Server**
2. **MongoDB Compass**
3. **MongoDB Shell (`mongosh`)** — useful for command-line practice
4. Optional: **VS Code** for writing/saving JSON files

MongoDB provides Community Server for local/self-managed use, and Compass provides a graphical interface for querying and managing MongoDB. urlMongoDB Community Server Downloadhttps://www.mongodb.com/try/download/community urlMongoDB Compass Installation Guidehttps://www.mongodb.com/docs/compass/install/

> **Recommended for students:** MongoDB Community Server + MongoDB Compass. You can perform most of this assignment through Compass, while also learning the MongoDB shell commands.

---

# 4. Installation — Windows

## Step 1 — Download MongoDB Community Server

Open:

urlMongoDB Community Server Downloadhttps://www.mongodb.com/try/download/community

Select:

```text
Version   → 8.0.x (stable/LTS line)
Platform  → Windows
Package   → MSI
```

MongoDB's official download page currently lists Community releases including the 8.0 release line. citeturn0search4

---

## Step 2 — Install MongoDB

Run the downloaded `.msi` file.

During installation:

1. Accept the license agreement.
2. Choose **Complete** installation.
3. Keep MongoDB Server as a Windows Service.
4. Keep the default service configuration.
5. Install Compass if the installer offers the option.
6. Finish installation.

The official Windows installer can install MongoDB Server as a Windows service and can also install Compass. citeturn0search3turn0search6

---

# 5. Verify MongoDB Installation

Open **PowerShell** or **Command Prompt**.

Run:

```powershell
mongod --version
```

Expected result:

```text
db version: 8.0.x
```

Then:

```powershell
mongosh --version
```

Expected result:

```text
2.x.x
```

If `mongosh` is not recognized, install MongoDB Shell separately from the official MongoDB downloads.

---

# 6. Check MongoDB Service

Open:

```text
Services
```

in Windows.

Find:

```text
MongoDB Server
```

Its status should be:

```text
Running
```

If it is stopped:

1. Right-click **MongoDB Server**.
2. Select **Start**.

---

# 7. Connect Using MongoDB Shell

Open PowerShell:

```powershell
mongosh
```

You should see a MongoDB shell prompt similar to:

```text
test>
```

Check the current database:

```javascript
db
```

Output:

```text
test
```

---

# 8. Connect Using MongoDB Compass

Open **MongoDB Compass**.

Use:

```text
mongodb://localhost:27017
```

Click:

```text
Connect
```

If connected successfully, Compass will show the local MongoDB deployment.

Compass can connect to a MongoDB deployment running locally on your machine and lets you visually explore and modify data. citeturn0search16turn0search17

---

# 9. Create the Practical Database

We will use:

```text
Database: TYCSE_DB
```

In `mongosh`:

```javascript
use TYCSE_DB
```

Create the first collection:

```javascript
db.students.insertOne({
  student_id: 101,
  name: "Anushka",
  age: 20,
  department: "Computer Science",
  marks: 85
})
```

MongoDB creates the collection automatically when the first document is inserted. citeturn0search2turn0search1

Check:

```javascript
show dbs
```

Check collections:

```javascript
show collections
```

Check the inserted document:

```javascript
db.students.find()
```

---

# 10. Practical Workflow

For every question:

```text
1. Understand the data requirement
        ↓
2. Decide structured / semi-structured / JSON
        ↓
3. Design the document
        ↓
4. Create/select MongoDB database
        ↓
5. Create collection
        ↓
6. Insert document(s)
        ↓
7. Display/query the document
        ↓
8. Verify output in Compass
        ↓
9. Take screenshot for journal
```

---

# SET A — Solutions

---

## A1. Student JSON Document

### Requirement

Create a student record containing:

- Name
- Roll number
- Age
- Department
- List of subjects
- Address with city and pincode

### MongoDB Command

```javascript
use TYCSE_DB

db.students.insertOne({
  roll_no: 101,
  name: "Anushka",
  age: 20,
  department: "Computer Science",
  subjects: [
    "Database Technologies",
    "DSA",
    "Operating Systems"
  ],
  address: {
    city: "Pune",
    pincode: "411001"
  }
})
```

### Check Output

```javascript
db.students.findOne({ roll_no: 101 })
```

Expected structure:

```text
students
   |
   +-- roll_no
   +-- name
   +-- age
   +-- department
   +-- subjects[]
   +-- address
         +-- city
         +-- pincode
```

---

# A2. Structured vs Semi-Structured Data

## Structured

```text
Student_ID | Name     | Age | Department
101        | Anushka  | 20  | Computer Science
102        | Rahul    | 21  | Information Technology
```

Fixed columns are required.

## Semi-Structured JSON

```json
{
  "student_id": 101,
  "name": "Anushka",
  "age": 20,
  "department": "Computer Science"
}
```

Another document can contain extra fields:

```json
{
  "student_id": 102,
  "name": "Rahul",
  "age": 21,
  "department": "Information Technology",
  "hostel": true
}
```

### Main Difference

| Structured | Semi-Structured |
|---|---|
| Fixed schema | Flexible schema |
| Rows/columns | Documents/keys |
| SQL | JSON/XML etc. |
| Less flexible | More flexible |

---

# A3. Library Book JSON

### Requirement

Fields:

- book_id
- title
- author
- price
- availability
- genres array

### Command

```javascript
db.library.insertOne({
  book_id: "B101",
  title: "Database Systems",
  author: "Ramakrishnan",
  price: 650,
  availability: true,
  genres: [
    "Database",
    "Computer Science",
    "Education"
  ]
})
```

### Check

```javascript
db.library.findOne({ book_id: "B101" })
```

---

# A4. Product Catalog JSON Array

### Requirement

Create product documents containing:

- product_id
- product_name
- category
- price
- stock_quantity

### Command

```javascript
db.products.insertMany([
  {
    product_id: "P101",
    product_name: "Laptop",
    category: "Electronics",
    price: 55000,
    stock_quantity: 10
  },
  {
    product_id: "P102",
    product_name: "Mouse",
    category: "Accessories",
    price: 500,
    stock_quantity: 50
  },
  {
    product_id: "P103",
    product_name: "Keyboard",
    category: "Accessories",
    price: 1200,
    stock_quantity: 25
  }
])
```

### Check

```javascript
db.products.find()
```

---

# A5. Hospital Patient — Embedded Documents

### Requirement

Create a patient record with:

- patient_id
- name
- age
- diagnosis
- doctor details
- specialization
- prescribed medicines

### Command

```javascript
db.patients.insertOne({
  patient_id: "P001",
  name: "Priya",
  age: 35,
  diagnosis: "Fever",
  doctor: {
    name: "Dr. Mehta",
    specialization: "General Medicine"
  },
  medicines: [
    {
      name: "Paracetamol",
      dosage: "500mg",
      frequency: "Twice a day"
    },
    {
      name: "Vitamin C",
      dosage: "500mg",
      frequency: "Once a day"
    }
  ]
})
```

### Why embedding?

Doctor details and medicines are represented as nested data belonging to the patient record.

---

# A6. Movie JSON Document

### Requirement

Fields:

- movie_id
- title
- release_year
- director name/country
- runtime
- rating
- cast array with character names

### Command

```javascript
db.movies.insertOne({
  movie_id: "M101",
  title: "Database World",
  release_year: 2026,
  director: {
    name: "Raj Mehta",
    country: "India"
  },
  runtime: 140,
  rating: 4.5,
  cast: [
    {
      actor: "Amit",
      character: "Professor"
    },
    {
      actor: "Priya",
      character: "Student"
    }
  ]
})
```

### Check

```javascript
db.movies.findOne({ movie_id: "M101" })
```

---

# A7. Convert Structured Customer Table to JSON

### Original structured data

```text
cust_id | fname | lname | email | phone
```

### JSON

```javascript
db.customers.insertMany([
  {
    cust_id: 101,
    fname: "Rahul",
    lname: "Sharma",
    email: "rahul@example.com",
    phone: "9876543210",
    loyalty_points: 120
  },
  {
    cust_id: 102,
    fname: "Priya",
    lname: "Patil",
    email: "priya@example.com",
    phone: "9876501234"
  },
  {
    cust_id: 103,
    fname: "Amit",
    lname: "Joshi",
    email: "amit@example.com",
    phone: "9876512345",
    loyalty_points: 250
  }
])
```

### Important Observation

`loyalty_points` exists only in some documents.

This demonstrates **schema flexibility**.

---

# A8. Weather JSON

### Requirement

Include:

- city
- country
- latitude
- longitude
- temperature
- humidity
- wind_speed
- 5-day forecast array

### Command

```javascript
db.weather.insertOne({
  location: {
    city: "Pune",
    country: "India",
    latitude: 18.5204,
    longitude: 73.8567
  },
  current_conditions: {
    temperature: 28,
    humidity: 65,
    wind_speed: 12
  },
  forecast: [
    { day: "Monday", temperature: 29 },
    { day: "Tuesday", temperature: 30 },
    { day: "Wednesday", temperature: 28 },
    { day: "Thursday", temperature: 27 },
    { day: "Friday", temperature: 29 }
  ]
})
```

### Check

```javascript
db.weather.findOne()
```

---

# A9. Course Enrollment

### Requirement

Include:

- course_id
- course_name
- instructor_name
- credits
- semester
- max_capacity
- enrolled students
- registration_ids

### Command

```javascript
db.courses.insertOne({
  course_id: "CS501",
  course_name: "Database Technologies",
  instructor_name: "Dr. Sharma",
  credits: 4,
  semester: 5,
  max_capacity: 60,
  enrolled_students: [
    {
      student_id: 101,
      name: "Anushka",
      registration_id: "REG101"
    },
    {
      student_id: 102,
      name: "Rahul",
      registration_id: "REG102"
    }
  ]
})
```

### Check

```javascript
db.courses.findOne({ course_id: "CS501" })
```

---

# A10. Online Quiz

### Requirement

Include:

- quiz_id
- title
- subject
- questions array
- question_text
- options
- correct_answer
- total_marks

### Command

```javascript
db.quizzes.insertOne({
  quiz_id: "Q101",
  title: "MongoDB Basics",
  subject: "Database Technologies",
  questions: [
    {
      question_text: "What is MongoDB?",
      options: [
        "Relational Database",
        "Document Database",
        "Operating System",
        "Compiler"
      ],
      correct_answer: "Document Database"
    },
    {
      question_text: "What format is MongoDB data represented as?",
      options: [
        "JSON-like documents",
        "CSV only",
        "HTML only",
        "Plain text only"
      ],
      correct_answer: "JSON-like documents"
    }
  ],
  total_marks: 10
})
```

### Check

```javascript
db.quizzes.findOne({ quiz_id: "Q101" })
```

---

# SET B — Solutions

---

# B1. E-Commerce Order Management

### Requirement

Create a JSON schema/document containing:

- order_id
- customer details with embedded address
- items array
- product name
- quantity
- price
- order_status
- payment method
- transaction_id

### Command

```javascript
db.orders.insertOne({
  order_id: "ORD101",
  customer: {
    customer_id: "C101",
    name: "Rahul",
    address: {
      street: "MG Road",
      city: "Pune",
      pincode: "411001"
    }
  },
  items: [
    {
      product_name: "Laptop",
      quantity: 1,
      price: 55000
    },
    {
      product_name: "Mouse",
      quantity: 2,
      price: 500
    }
  ],
  order_status: "Confirmed",
  payment: {
    method: "UPI",
    transaction_id: "TXN12345"
  }
})
```

### Check

```javascript
db.orders.findOne({ order_id: "ORD101" })
```

---

# B2. University — Referencing / Normalization

### Requirement

Create separate documents for:

- Account
- Customer
- Branch

and reference them.

### Account

```javascript
db.accounts.insertOne({
  account_id: "A101",
  account_type: "Savings",
  balance: 50000,
  customer_id: "C101"
})
```

### Customer

```javascript
db.customers_banking.insertOne({
  customer_id: "C101",
  name: "Priya",
  email: "priya@example.com",
  branch_id: "B101"
})
```

### Branch

```javascript
db.branches.insertOne({
  branch_id: "B101",
  branch_name: "Pune Main Branch",
  location: "Pune"
})
```

### Relationship

```text
Account
   |
   | customer_id
   ↓
Customer
   |
   | branch_id
   ↓
Branch
```

### Why referencing?

The same customer or branch can be related to many other records without duplicating the complete information.

---

# B3. XML to JSON Conversion

### XML idea

```xml
<employee>
    <employee_id>101</employee_id>
    <name>Rahul</name>
    <department>IT</department>
    <projects>
        <project>AI System</project>
        <project>Database Migration</project>
    </projects>
    <contact>
        <email>rahul@example.com</email>
        <phone>9876543210</phone>
    </contact>
</employee>
```

### Equivalent JSON

```json
{
  "employee_id": 101,
  "name": "Rahul",
  "department": "IT",
  "projects": [
    "AI System",
    "Database Migration"
  ],
  "contact": {
    "email": "rahul@example.com",
    "phone": "9876543210"
  }
}
```

---

# B4. IPL Player Dataset

### Requirement

At least 5 documents with:

- player_id
- name
- team
- category
- bid_price
- runs_scored
- wickets_taken
- different optional fields

### Command

```javascript
db.ipl_players.insertMany([
  {
    player_id: 1,
    name: "Player One",
    team: "Team A",
    category: "Batsman",
    bid_price: 5000000,
    runs_scored: 450,
    wickets_taken: 2
  },
  {
    player_id: 2,
    name: "Player Two",
    team: "Team B",
    category: "Bowler",
    bid_price: 4000000,
    runs_scored: 80,
    wickets_taken: 18,
    captain: true
  },
  {
    player_id: 3,
    name: "Player Three",
    team: "Team C",
    category: "All-rounder",
    bid_price: 7000000,
    runs_scored: 320,
    wickets_taken: 12,
    strike_rate: 145.2
  },
  {
    player_id: 4,
    name: "Player Four",
    team: "Team D",
    category: "Batsman",
    bid_price: 3500000,
    runs_scored: 280,
    wickets_taken: 0
  },
  {
    player_id: 5,
    name: "Player Five",
    team: "Team E",
    category: "Wicketkeeper",
    bid_price: 4500000,
    runs_scored: 390,
    wickets_taken: 0,
    dismissals: 15
  }
])
```

### Demonstrate schema flexibility

Notice:

- `captain` appears only in one document.
- `strike_rate` appears only in one document.
- `dismissals` appears only in one document.

Check:

```javascript
db.ipl_players.find()
```

---

# B5. BSON vs JSON

### BSON Types

At least five additional BSON types:

1. ObjectId
2. Date
3. Binary
4. Decimal128
5. Int32 / Int64

### Examples

```javascript
{
  _id: ObjectId("64ab1234ef567890abcd1234"),
  created_at: ISODate("2026-01-01T00:00:00Z"),
  amount: NumberDecimal("99.99"),
  quantity: NumberInt(10)
}
```

### Why BSON?

- Efficient encoding/decoding.
- Additional data types.
- Native MongoDB document representation.
- Embedded documents and arrays.
- ObjectId for unique document identification.

---

# B6. Banking System — Referencing

### Account

```javascript
db.bank_accounts.insertOne({
  account_id: "A101",
  account_type: "Savings",
  customer_id: "C101"
})
```

### Customer

```javascript
db.bank_customers.insertOne({
  customer_id: "C101",
  name: "Anushka",
  email: "anushka@example.com"
})
```

### Branch

```javascript
db.bank_branches.insertOne({
  branch_id: "B101",
  branch_name: "Pune Branch",
  location: "Pune"
})
```

### Relationship

```text
Account
  |
  | customer_id
  ↓
Customer
  |
  | branch_id
  ↓
Branch
```

---

# B7. Real Estate Property Dataset

At least 6 documents.

### Command

```javascript
db.properties.insertMany([
  {
    property_id: "P101",
    title: "2 BHK Apartment",
    type: "Apartment",
    area: 1100,
    latitude: 18.5204,
    longitude: 73.8567,
    price: 7500000,
    bedrooms: 2,
    bathrooms: 2,
    pool: false,
    furnished: true
  },
  {
    property_id: "P102",
    title: "3 BHK Villa",
    type: "Villa",
    area: 2200,
    latitude: 18.5404,
    longitude: 73.8767,
    price: 15000000,
    bedrooms: 3,
    bathrooms: 3,
    garage: true,
    furnished: true
  },
  {
    property_id: "P103",
    title: "1 BHK Flat",
    type: "Apartment",
    area: 700,
    latitude: 18.5104,
    longitude: 73.8467,
    price: 4500000,
    bedrooms: 1,
    bathrooms: 1
  },
  {
    property_id: "P104",
    title: "4 BHK Villa",
    type: "Villa",
    area: 3000,
    latitude: 18.5604,
    longitude: 73.8967,
    price: 22000000,
    bedrooms: 4,
    bathrooms: 4,
    pool: true,
    garage: true
  },
  {
    property_id: "P105",
    title: "Office Space",
    type: "Commercial",
    area: 1800,
    latitude: 18.5304,
    longitude: 73.8667,
    price: 12000000,
    furnished: false
  },
  {
    property_id: "P106",
    title: "3 BHK Apartment",
    type: "Apartment",
    area: 1600,
    latitude: 18.5504,
    longitude: 73.8867,
    price: 10500000,
    bedrooms: 3,
    bathrooms: 3,
    furnished: true
  }
])
```

### Check

```javascript
db.properties.find()
```

---

# B8. Practical BSON vs JSON Scenario

## 1. ObjectId

MongoDB uses `_id` to uniquely identify documents.

Example:

```javascript
{
  _id: ObjectId("64ab1234ef567890abcd1234")
}
```

Check:

```javascript
db.students.findOne()
```

---

## 2. ISODate

MongoDB supports a native date/time representation.

Example:

```javascript
{
  created_at: ISODate("2026-01-01T10:30:00Z")
}
```

---

## 3. Decimal128

Useful when exact decimal precision is important.

Example:

```javascript
{
  price: NumberDecimal("99999.99")
}
```

---

## 4. Binary

Used for binary data.

Example:

```javascript
{
  file_data: BinData(0, "...")
}
```

---

# B9. Project Management XML → JSON

### Given XML

```xml
<project>
    <project_id>P101</project_id>
    <project_name>AI Implementation</project_name>

    <team_members>
        <member>
            <name>Arun</name>
            <role>Lead</role>
        </member>
        <member>
            <name>Pooja</name>
            <role>Developer</role>
        </member>
    </team_members>

    <milestones>
        <milestone>
            <title>Planning</title>
            <status>Complete</status>
        </milestone>
    </milestones>
</project>
```

### JSON

```json
{
  "project_id": "P101",
  "project_name": "AI Implementation",
  "team_members": [
    {
      "name": "Arun",
      "role": "Lead"
    },
    {
      "name": "Pooja",
      "role": "Developer"
    }
  ],
  "milestones": [
    {
      "title": "Planning",
      "status": "Complete"
    }
  ]
}
```

### MongoDB

```javascript
db.projects.insertOne({
  project_id: "P101",
  project_name: "AI Implementation",
  team_members: [
    { name: "Arun", role: "Lead" },
    { name: "Pooja", role: "Developer" }
  ],
  milestones: [
    { title: "Planning", status: "Complete" }
  ]
})
```

---

# SET C — Solutions

---

# C1. Social Media MongoDB Data Model

### Requirement

At least three collections:

1. Users
2. Posts
3. Comments

Need to demonstrate:

- Embedding comments
- Referencing users

---

## Users Collection

```javascript
db.social_users.insertOne({
  user_id: "U101",
  name: "Anushka",
  email: "anushka@example.com",
  profile: {
    city: "Pune",
    bio: "Computer Science student"
  }
})
```

---

## Posts Collection

```javascript
db.social_posts.insertOne({
  post_id: "POST101",
  user_id: "U101",
  content: "Learning MongoDB today!",
  created_at: ISODate("2026-01-10T10:00:00Z"),
  likes: 25,
  comments: [
    {
      comment_id: "C101",
      user_id: "U102",
      text: "Great!",
      created_at: ISODate("2026-01-10T10:10:00Z")
    },
    {
      comment_id: "C102",
      user_id: "U103",
      text: "Very useful.",
      created_at: ISODate("2026-01-10T10:15:00Z")
    }
  ]
})
```

Here:

```text
Post → user_id → Users
Post → embedded comments
```

This demonstrates both **referencing and embedding**.

---

## Comments Collection

If comments need independent management, create:

```javascript
db.social_comments.insertMany([
  {
    comment_id: "C201",
    post_id: "POST101",
    user_id: "U104",
    text: "Excellent post!"
  },
  {
    comment_id: "C202",
    post_id: "POST101",
    user_id: "U105",
    text: "Thanks for sharing."
  }
])
```

### Check

```javascript
db.social_users.find()
db.social_posts.find()
db.social_comments.find()
```

---

# C2. Online Food Delivery System

### Requirement

Create JSON data for:

- Restaurant
- Embedded menu items
- Customer with address
- Order
- Reference restaurant and customer

---

## Restaurant

```javascript
db.restaurants.insertOne({
  restaurant_id: "R101",
  name: "Pune Spice",
  address: {
    street: "FC Road",
    city: "Pune",
    pincode: "411004"
  },
  menu: [
    {
      item_id: "M101",
      name: "Paneer Biryani",
      price: 250
    },
    {
      item_id: "M102",
      name: "Veg Biryani",
      price: 200
    }
  ]
})
```

---

## Customer

```javascript
db.food_customers.insertOne({
  customer_id: "C101",
  name: "Rahul",
  phone: "9876543210",
  address: {
    street: "MG Road",
    city: "Pune",
    pincode: "411001"
  }
})
```

---

## Order

```javascript
db.food_orders.insertOne({
  order_id: "ORD101",
  restaurant_id: "R101",
  customer_id: "C101",
  items: [
    {
      item_id: "M101",
      name: "Paneer Biryani",
      quantity: 2,
      price: 250
    },
    {
      item_id: "M102",
      name: "Veg Biryani",
      quantity: 1,
      price: 200
    }
  ],
  total_amount: 700,
  order_status: "Preparing",
  payment: {
    method: "UPI",
    transaction_id: "TXN9001"
  }
})
```

### Relationships

```text
Restaurant
    ↑
    |
restaurant_id
    |
Order
    |
customer_id
    ↓
Customer
```

### Why this model?

- Restaurant menu is embedded because it belongs closely to the restaurant.
- Customer is referenced because the same customer can place many orders.
- Restaurant is referenced because one restaurant can receive many orders.

---

# C3. JSON Limitations and How BSON Helps

## Limitation 1 — Limited Native Data Types

Standard JSON supports:

- String
- Number
- Boolean
- Array
- Object
- Null

MongoDB BSON adds:

- ObjectId
- Date
- Binary
- Decimal128
- Int32
- Int64

---

## Limitation 2 — Date Handling

JSON does not have a dedicated native date type.

BSON:

```javascript
{
  created_at: ISODate("2026-01-01T10:30:00Z")
}
```

---

## Limitation 3 — Exact Decimal Values

JSON numbers do not provide a dedicated Decimal128 type.

BSON:

```javascript
{
  amount: NumberDecimal("999999.99")
}
```

Useful for financial values where precision matters.

---

## Limitation 4 — Binary Data

Standard JSON is text-based.

BSON supports binary data:

```javascript
{
  file_data: BinData(0, "...")
}
```

Useful for binary files/data.

---

## Limitation 5 — Document Identification

JSON has no built-in MongoDB-specific identifier.

MongoDB BSON supports:

```javascript
_id: ObjectId("64ab1234ef567890abcd1234")
```

This uniquely identifies a document.

---

## Summary

```text
JSON
 ↓
Simple + human-readable
 ↓
Limited native data types
 ↓
BSON
 ↓
Binary + richer MongoDB data types
 ↓
Better suited to MongoDB storage
```

---

# 11. How to Perform the Practical in MongoDB Compass

You can perform the assignment either through **mongosh** or **Compass**.

## Method 1 — mongosh

Open:

```powershell
mongosh
```

Then:

```javascript
use TYCSE_DB
```

Run the commands from each question.

Example:

```javascript
db.products.insertMany([
  {
    product_id: "P101",
    product_name: "Laptop",
    category: "Electronics",
    price: 55000,
    stock_quantity: 10
  },
  {
    product_id: "P102",
    product_name: "Mouse",
    category: "Accessories",
    price: 500,
    stock_quantity: 50
  }
])
```

Check:

```javascript
db.products.find()
```

---

# 12. Performing the Same Work in Compass

## Step 1

Open **MongoDB Compass**.

## Step 2

Connect:

```text
mongodb://localhost:27017
```

## Step 3

Click:

```text
Create Database
```

Enter:

```text
Database Name: TYCSE_DB
Collection Name: students
```

## Step 4

Open the collection.

## Step 5

Click:

```text
Add Data
```

Choose:

```text
Insert Document
```

## Step 6

Paste a document:

```json
{
  "roll_no": 101,
  "name": "Anushka",
  "age": 20,
  "department": "Computer Science",
  "subjects": [
    "Database Technologies",
    "DSA"
  ],
  "address": {
    "city": "Pune",
    "pincode": "411001"
  }
}
```

Click:

```text
Insert
```

## Step 7 — Verify

The document should appear inside the collection.

You can use the Compass filter:

```json
{ "roll_no": 101 }
```

Click:

```text
Find
```

---

# 13. How to Check Whether the Practical Worked

For every question, verify three things.

## Check 1 — Collection

In Compass:

```text
TYCSE_DB
   ↓
collection
```

Example:

```text
TYCSE_DB
 ├── students
 ├── products
 ├── movies
 ├── customers
 └── orders
```

---

## Check 2 — Document

Open the collection and confirm that the fields are present.

For example:

```text
student
 ├── roll_no
 ├── name
 ├── age
 ├── department
 ├── subjects
 └── address
```

---

## Check 3 — Query

Use:

```javascript
db.students.find()
```

or:

```javascript
db.students.findOne({ roll_no: 101 })
```

A successful query should display the inserted document.

MongoDB's CRUD API includes `insertOne()`, `insertMany()`, `find()`, `updateOne()`, `deleteOne()` and related methods. citeturn0search2turn0search7

---

# 14. Useful Commands for This Practical

## Select database

```javascript
use TYCSE_DB
```

## Show databases

```javascript
show dbs
```

## Show collections

```javascript
show collections
```

## Insert one

```javascript
db.collection.insertOne({
  name: "Anushka"
})
```

## Insert many

```javascript
db.collection.insertMany([
  { name: "Anushka" },
  { name: "Rahul" }
])
```

## Display all documents

```javascript
db.collection.find()
```

## Display one document

```javascript
db.collection.findOne()
```

## Search using a field

```javascript
db.students.find({
  department: "Computer Science"
})
```

## Count documents

```javascript
db.students.countDocuments()
```

## Delete one document

```javascript
db.students.deleteOne({
  roll_no: 101
})
```

> For the first practical, deletion is mainly useful for correcting test data. Avoid deleting your entire collection accidentally.

MongoDB documents these CRUD operations as the standard create, read, update and delete operations. citeturn0search2turn0search11

---

# 15. Recommended Practical Screenshot Checklist

For the practical journal, capture screenshots showing:

### Installation

- MongoDB installation completed
- MongoDB service running
- `mongod --version`
- `mongosh --version`

### Connection

- Compass connected to `localhost:27017`
- `TYCSE_DB` database

### Each Assignment

For each question:

1. Command/document entered
2. Collection created
3. Inserted document
4. Query/filter
5. Output in Compass

---

# 16. Viva / Oral Questions

## Basic

1. What is structured data?
2. What is semi-structured data?
3. What is JSON?
4. What is BSON?
5. Why does MongoDB use BSON?
6. What is a MongoDB document?
7. What is a collection?
8. What is the difference between a collection and a table?
9. What is `_id`?
10. What is ObjectId?

## Modeling

11. What is embedding?
12. What is referencing?
13. When should embedding be used?
14. When should referencing be used?
15. Why is MongoDB called schema-flexible?
16. Can two MongoDB documents in the same collection have different fields?

## Practical

17. How do you create/select a database?
18. How do you insert one document?
19. How do you insert multiple documents?
20. How do you display documents?
21. How do you filter documents?
22. How do you check the number of documents?
23. How do you connect Compass to local MongoDB?
24. What is `mongodb://localhost:27017`?
25. What happens when you insert into a collection that does not yet exist?

---

# 17. Final Practical Flow

Remember this sequence:

```text
Install MongoDB
      ↓
Install/Use Compass
      ↓
Start MongoDB Service
      ↓
Connect to localhost:27017
      ↓
Create TYCSE_DB
      ↓
Create Collections
      ↓
Design JSON Documents
      ↓
Insert Documents
      ↓
Query Documents
      ↓
Verify in Compass
      ↓
Take Screenshots
      ↓
Complete Journal
```

---

# 18. Important Student Notes

### Structured

```text
Fixed schema
Rows + Columns
SQL
RDBMS
```

### Semi-Structured

```text
Flexible structure
Keys/Tags
Nested data
JSON/XML
```

### MongoDB

```text
Database
   ↓
Collection
   ↓
Document
   ↓
Fields
```

### BSON

```text
JSON-like
+
ObjectId
+
Date
+
Binary
+
Decimal128
+
Integer types
```

### Data Modeling

```text
Frequently together → Embed

Large/shared/many-to-many → Reference
```

---

# 19. Practical Completion Criteria

The practical is considered complete when students can:

- Explain structured and semi-structured data.
- Create valid JSON documents.
- Explain JSON syntax and data types.
- Explain JSON vs BSON.
- Install MongoDB Community Server.
- Connect using Compass.
- Create a database and collections.
- Insert single and multiple documents.
- Represent nested objects and arrays.
- Demonstrate schema flexibility.
- Demonstrate embedding.
- Demonstrate referencing.
- Verify documents using queries.
- Complete **Set A, Set B and Set C**.

---

## Official MongoDB References

- urlMongoDB Community Serverhttps://www.mongodb.com/try/download/community
- urlMongoDB Compasshttps://www.mongodb.com/docs/compass/
- urlMongoDB CRUD Operationshttps://www.mongodb.com/docs/manual/crud/
- urlMongoDB insertOne()https://www.mongodb.com/docs/manual/reference/method/db.collection.insertOne/
- urlMongoDB insertMany()https://www.mongodb.com/docs/manual/reference/method/db.collection.insertMany/
- urlMongoDB updateOne()https://www.mongodb.com/docs/manual/reference/method/db.collection.updateOne/
- urlMongoDB deleteOne()https://www.mongodb.com/docs/manual/reference/method/db.collection.deleteOne/
