
SET A
```
1. Design a JSON document to represent a student record containing name, roll number, age, 
department, list of subjects, and address (city and pincode). Write the JSON structure manually.

{
  "name": "Anushka",
  "roll_number": 101,
  "age": 20,
  "department": "Computer Science",
  "subjects": [
    "DBMS",
    "MongoDB",
    "Operating System",
    "Computer Networks"
  ],
  "address": {
    "city": "Pune",
    "pincode": "411001"
  }
}

```
``` 
2. Compare structured data (table format) and semi-structured data (JSON format) using an 
example of an employee record containing empid, name, salary, department, and skills.

Structured data — Table

| empid | name  | salary | department | skills          |
| ----: | ----- | -----: | ---------- | --------------- |
|   101 | Amit  |  60000 | IT         | Java, SQL       |
|   102 | Priya |  65000 | HR         | Excel, HRMS     |
|   103 | Rahul |  70000 | IT         | Python, MongoDB |

Semi-structured JSON

[
  {
    "empid": 101,
    "name": "Amit",
    "salary": 60000,
    "department": "IT",
    "skills": ["Java", "SQL"]
  },
  {
    "empid": 102,
    "name": "Priya",
    "salary": 65000,
    "department": "HR",
    "skills": ["Excel", "HRMS"],
    "experience": 3
  },
  {
    "empid": 103,
    "name": "Rahul",
    "salary": 70000,
    "department": "IT",
    "skills": ["Python", "MongoDB"]
  }
]

Difference

| Feature     | Structured   | Semi-Structured  |
| ----------- | ------------ | ---------------- |
| Format      | Rows/Columns | JSON/XML         |
| Schema      | Fixed        | Flexible         |
| Nested data | Normally no  | Yes              |
| Arrays      | Not natural  | Supported        |
| Example     | MySQL table  | MongoDB document |

```
```
3. Write a JSON document to represent a library book record containing book_id, title, author, 
price, availability (boolean), and an array of genres.

{
  "book_id": 1001,
  "title": "Introduction to Database Systems",
  "author": "Raghu Ramakrishnan",
  "price": 650,
  "availability": true,
  "genres": [
    "Database",
    "Computer Science",
    "Education"
  ]
}
```
```
4. Represent the following structured table data as a JSON array of objects for a product catalog 
containing product_id, product_name, category, price, and stock_quantity.

[
  {
    "product_id": 101,
    "product_name": "Laptop",
    "category": "Electronics",
    "price": 55000,
    "stock_quantity": 15
  },
  {
    "product_id": 102,
    "product_name": "Wireless Mouse",
    "category": "Accessories",
    "price": 800,
    "stock_quantity": 50
  },
  {
    "product_id": 103,
    "product_name": "Keyboard",
    "category": "Accessories",
    "price": 1200,
    "stock_quantity": 35
  },
  {
    "product_id": 104,
    "product_name": "Monitor",
    "category": "Electronics",
    "price": 15000,
    "stock_quantity": 20
  }
]
```
```
5. Create a JSON document for a hospital patient record using embedded documents. The record 
should include patient_id, name, age, diagnosis, doctor details (name and specialization), and a 
list of prescribed medicines.

{
  "patient_id": 501,
  "name": "Sneha Patil",
  "age": 35,
  "diagnosis": "Fever",
  "doctor": {
    "name": "Dr. Rahul Deshmukh",
    "specialization": "General Physician"
  },
  "prescribed_medicines": [
    {
      "name": "Paracetamol",
      "dosage": "500mg",
      "frequency": "Twice a day"
    },
    {
      "name": "Vitamin C",
      "dosage": "500mg",
      "frequency": "Once a day"
    }
  ]
}
```
```
6. Design a JSON document for a movie record containing movie_id, title, release_year, director 
(name and country), runtime, rating (out of 5), and an array of cast members with their 
character names.

{
  "movie_id": 1001,
  "title": "The Great Adventure",
  "release_year": 2025,
  "director": {
    "name": "Raj Mehta",
    "country": "India"
  },
  "runtime": 145,
  "rating": 4.5,
  "cast": [
    {
      "name": "Amit Sharma",
      "character": "Arjun"
    },
    {
      "name": "Priya Joshi",
      "character": "Meera"
    },
    {
      "name": "Rahul Patil",
      "character": "Vikram"
    }
  ]
}
```
```
7. Convert the following structured table data (Customer: cust_id, fname, lname, email, phone) 
into a JSON array of objects and add an optional "loyalty_points" field to only some records to 
demonstrate schema flexibility.

[
  {
    "cust_id": 101,
    "fname": "Amit",
    "lname": "Sharma",
    "email": "amit@example.com",
    "phone": "9876543210",
    "loyalty_points": 500
  },
  {
    "cust_id": 102,
    "fname": "Priya",
    "lname": "Patil",
    "email": "priya@example.com",
    "phone": "9876543211"
  },
  {
    "cust_id": 103,
    "fname": "Rahul",
    "lname": "Joshi",
    "email": "rahul@example.com",
    "phone": "9876543212",
    "loyalty_points": 250
  }
]
```
``` 
8. Create a JSON document representing a weather record with location (city, country, latitude, 
longitude), current conditions (temperature, humidity, wind_speed), and a 5-day forecast array 
with daily temperatures.

{
  "location": {
    "city": "Pune",
    "country": "India",
    "latitude": 18.5204,
    "longitude": 73.8567
  },
  "current_conditions": {
    "temperature": 28,
    "humidity": 65,
    "wind_speed": 12
  },
  "forecast": [
    {
      "day": "Monday",
      "temperature": 27
    },
    {
      "day": "Tuesday",
      "temperature": 29
    },
    {
      "day": "Wednesday",
      "temperature": 30
    },
    {
      "day": "Thursday",
      "temperature": 28
    },
    {
      "day": "Friday",
      "temperature": 27
    }
  ]
}
```
```
9. Design a JSON structure for a course enrollment record that includes course_id, course_name, 
instructor_name, credits, semester, max_capacity, and an array of enrolled students with their 
registration_ids.

{
  "course_id": "CS301",
  "course_name": "Database Technologies",
  "instructor_name": "Dr. Patil",
  "credits": 4,
  "semester": 5,
  "max_capacity": 60,
  "enrolled_students": [
    {
      "student_name": "Amit",
      "registration_id": "REG101"
    },
    {
      "student_name": "Priya",
      "registration_id": "REG102"
    },
    {
      "student_name": "Rahul",
      "registration_id": "REG103"
    }
  ]
}
```
```
10. Create a JSON document for an online quiz with quiz_id, title, subject, questions array (each 
question containing question_text, options, and correct_answer), and total_marks.

{
  "quiz_id": 501,
  "title": "Database Fundamentals Quiz",
  "subject": "Database Technologies",
  "questions": [
    {
      "question_text": "Which database is a NoSQL database?",
      "options": [
        "MySQL",
        "Oracle",
        "MongoDB",
        "PostgreSQL"
      ],
      "correct_answer": "MongoDB"
    },
    {
      "question_text": "What format is MongoDB data commonly represented as?",
      "options": [
        "JSON",
        "HTML",
        "CSS",
        "CSV"
      ],
      "correct_answer": "JSON"
    }
  ],
  "total_marks": 10
}
```
-------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------

# Set B

```
1. Design a JSON schema for an e-commerce order management system. The document should 
include order_id, customer (with embedded address), list of items (product name, quantity, 
price), order_status, and payment details (method and transaction_id).

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
    {
      "product_name": "Laptop",
      "quantity": 1,
      "price": 55000
    },
    {
      "product_name": "Wireless Mouse",
      "quantity": 2,
      "price": 800
    }
  ],
  "order_status": "Delivered",
  "payment": {
    "method": "Credit Card",
    "transaction_id": "TXN123456"
  }
}
```
```
2. Design two separate JSON documents demonstrating the referencing (normalization) approach 
for a university system where students belong to departments. Show how department_id is 
referenced in the student document.

Department document
{
  "_id": "D101",
  "department_name": "Computer Science",
  "hod": "Dr. Patil"
}

Student document
{
  "_id": "S101",
  "name": "Priya",
  "age": 21,
  "department_id": "D101"
}

```
```
3. Convert the following XML semi-structured data into equivalent JSON format for a company 
employee record containing employee details, projects assigned, and contact information.

{
  "employee": {
    "employee_id": 101,
    "name": "Amit Sharma",
    "designation": "Developer",
    "projects": [
      {
        "project_id": "P101",
        "project_name": "Banking Application"
      },
      {
        "project_id": "P102",
        "project_name": "E-Commerce Application"
      }
    ],
    "contact": {
      "email": "amit@example.com",
      "phone": "9876543210"
    }
  }
}
```
```
4. Create a JSON array with at least 5 documents representing an IPL player dataset. Include 
fields: player_id, name, team, category (Batsman/Bowler/All-rounder), bid_price, runs_scored, 
and wickets_taken. Ensure that different documents have different optional fields to 
demonstrate schema flexibility.

[
  {
    "player_id": 1,
    "name": "Rohit Sharma",
    "team": "Mumbai",
    "category": "Batsman",
    "bid_price": 15000000,
    "runs_scored": 450,
    "wickets_taken": 0
  },
  {
    "player_id": 2,
    "name": "Arjun Patel",
    "team": "Pune",
    "category": "Bowler",
    "bid_price": 9000000,
    "runs_scored": 80,
    "wickets_taken": 18,
    "economy_rate": 7.2
  },
  {
    "player_id": 3,
    "name": "Rahul Verma",
    "team": "Delhi",
    "category": "All-rounder",
    "bid_price": 12000000,
    "runs_scored": 320,
    "wickets_taken": 12,
    "strike_rate": 145.5
  },
  {
    "player_id": 4,
    "name": "Vikas Joshi",
    "team": "Chennai",
    "category": "Batsman",
    "bid_price": 11000000,
    "runs_scored": 390,
    "wickets_taken": 0
  },
  {
    "player_id": 5,
    "name": "Karan Singh",
    "team": "Bangalore",
    "category": "Bowler",
    "bid_price": 8500000,
    "runs_scored": 45,
    "wickets_taken": 20,
    "economy_rate": 6.8,
    "best_bowling": "4/21"
  }
]
```
```
5. Explain with example the difference between BSON and JSON. List at least four additional 
data types that BSON supports which are not available in standard JSON, with examples of 
each.

JSON
{
  "name": "Amit",
  "age": 25,
  "salary": 55000
}

JSON common types:

String
Number
Boolean
Array
Object
Null

BSON additional types
1. ObjectId
ObjectId("64ab1234ef567890abcd1234")

2. Date
ISODate("2026-09-16T10:30:00Z")

3. Decimal128
Decimal128("99999.99")

4. Binary
BinData(0, "...")
```
```
6. Design a MongoDB data model for a Banking System using referencing approach. Create 
separate JSON documents for: Account (account_id, account_type, balance, customer_id), 
Customer (customer_id, name, email), and Branch (branch_id, branch_name, location). Show 
how documents reference each other.

Customer
{
  "_id": "C101",
  "name": "Amit Sharma",
  "email": "amit@example.com"
}

Branch
{
  "_id": "B101",
  "branch_name": "Pune Main Branch",
  "location": "Pune"
}

Account
{
  "_id": "A101",
  "account_type": "Savings",
  "balance": 75000,
  "customer_id": "C101",
  "branch_id": "B101"
}


```
```
7. Create a JSON array representing a real estate property listing dataset with at least 6 
documents. Include fields: property_id, title, location (city, area, latitude, longitude), price, 
property_type, bedrooms, bathrooms, and optional fields like "pool", "garage", "furnished" to 
demonstrate schema flexibility in MongoDB.

[
  {
    "property_id": 101,
    "title": "2 BHK Apartment",
    "location": {
      "city": "Pune",
      "area": "Kothrud",
      "latitude": 18.5074,
      "longitude": 73.8077
    },
    "price": 8500000,
    "property_type": "Apartment",
    "bedrooms": 2,
    "bathrooms": 2,
    "garage": true,
    "furnished": true
  },
  {
    "property_id": 102,
    "title": "3 BHK Flat",
    "location": {
      "city": "Mumbai",
      "area": "Andheri",
      "latitude": 19.1197,
      "longitude": 72.8468
    },
    "price": 15000000,
    "property_type": "Apartment",
    "bedrooms": 3,
    "bathrooms": 3,
    "pool": true,
    "furnished": true
  },
  {
    "property_id": 103,
    "title": "1 BHK Apartment",
    "location": {
      "city": "Pune",
      "area": "Wakad",
      "latitude": 18.5995,
      "longitude": 73.7625
    },
    "price": 5500000,
    "property_type": "Apartment",
    "bedrooms": 1,
    "bathrooms": 1,
    "furnished": false
  },
  {
    "property_id": 104,
    "title": "4 BHK Villa",
    "location": {
      "city": "Pune",
      "area": "Baner",
      "latitude": 18.5590,
      "longitude": 73.7868
    },
    "price": 25000000,
    "property_type": "Villa",
    "bedrooms": 4,
    "bathrooms": 4,
    "pool": true,
    "garage": true
  },
  {
    "property_id": 105,
    "title": "2 BHK House",
    "location": {
      "city": "Nashik",
      "area": "College Road",
      "latitude": 20.0059,
      "longitude": 73.7629
    },
    "price": 6500000,
    "property_type": "House",
    "bedrooms": 2,
    "bathrooms": 2,
    "garage": true
  },
  {
    "property_id": 106,
    "title": "3 BHK Villa",
    "location": {
      "city": "Nagpur",
      "area": "Dharampeth",
      "latitude": 21.1458,
      "longitude": 79.0882
    },
    "price": 12000000,
    "property_type": "Villa",
    "bedrooms": 3,
    "bathrooms": 3,
    "furnished": true
  }
]
```
```
8. Compare BSON and JSON by providing a practical MongoDB scenario.
Show: (1) How ObjectId is used for document identification,
(2) How ISODate handles timestamps better than JSON,
(3) How Decimal128 ensures precision for financial data, and
(4) How Binary data type handles file storage. Provide examples for each.

1. ObjectId
{
  "_id": ObjectId("64ab1234ef567890abcd1234"),
  "name": "Amit"
}
2. ISODate
{
  "created_at": ISODate("2026-09-16T10:30:00Z")
}
3. Decimal128
{
  "amount": Decimal128("99999.99")
}
4. Binary
{
  "file_data": BinData(0, "...")
}

```
```
9. Convert the following XML structure into JSON format for a company's project management 
system: 
<project> 
<project_id>P101</project_id> 
<project_name>AI Implementation</project_name> 
<team_members> 
<member><name>Arun</name><role>Lead</role></member> 
<member><name>Pooja</name><role>Developer</role></member> 
</team_members> 
<milestones> 
<milestone><title>Planning</title><status>Complete</status></milestone> 
</milestones> 
</project>

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

# Set C

```
SET C — Q1: Social Media MongoDB Data Model

Assignment

Design a complete MongoDB data model for a Social Media application. The model should have at least three collections: Users, Posts, and Comments. Demonstrate embedding for comments within posts and referencing for user profiles. Design JSON documents for each collection with appropriate fields.

1. Database Design

Database name:

SocialMediaDB

Collections:

SocialMediaDB
├── Users
├── Posts
└── Comments

The model demonstrates:

Referencing: Posts and Comments store user_id to refer to a user in the Users collection.

Embedding: Comments are stored inside the comments array of a Post document.

2. Users Collection

Collection name:

Users

JSON Document

{
  "user_id": "U101",
  "name": "Anushka Patil",
  "username": "anushka101",
  "email": "anushka@example.com",
  "password": "hashed_password",
  "profile": {
    "bio": "Computer Science Student",
    "city": "Pune"
  },
  "created_at": "2026-09-22"
}

The user_id uniquely identifies the user. Other collections can store user_id instead of storing the complete user profile again. This demonstrates referencing.

3. Posts Collection

Collection name:

Posts

JSON Document

{
  "post_id": "P101",
  "user_id": "U101",
  "content": "Learning MongoDB and MongoDB Compass today!",
  "post_type": "text",
  "likes": 25,
  "created_at": "2026-09-22T09:00:00",
  "comments": [
    {
      "comment_id": "C101",
      "user_id": "U102",
      "text": "Great! Keep learning.",
      "created_at": "2026-09-22T09:10:00"
    },
    {
      "comment_id": "C102",
      "user_id": "U103",
      "text": "MongoDB is interesting!",
      "created_at": "2026-09-22T09:15:00"
    }
  ]
}

The user_id references the user who created the post. The comments array contains comment documents directly inside the Post document, demonstrating embedding.

4. Comments Collection

Collection name:

Comments

JSON Document 1

{
  "comment_id": "C101",
  "post_id": "P101",
  "user_id": "U102",
  "text": "Great! Keep learning.",
  "likes": 3,
  "created_at": "2026-09-22T09:10:00"
}

JSON Document 2

{
  "comment_id": "C102",
  "post_id": "P101",
  "user_id": "U103",
  "text": "MongoDB is interesting!",
  "likes": 5,
  "created_at": "2026-09-22T09:15:00"
}

post_id identifies the post to which the comment belongs, and user_id identifies the user who created the comment.

5. Embedding Demonstration

Comments are embedded inside the Post document:

{
  "post_id": "P101",
  "user_id": "U101",
  "content": "Learning MongoDB!",
  "comments": [
    {
      "comment_id": "C101",
      "user_id": "U102",
      "text": "Great! Keep learning."
    },
    {
      "comment_id": "C102",
      "user_id": "U103",
      "text": "MongoDB is interesting!"
    }
  ]
}

Structure:

Post P101
│
├── post_id
├── user_id
├── content
├── likes
└── comments[]
      ├── Comment C101
      └── Comment C102

This is embedding because the comment information is stored inside the Post document.

6. Referencing Demonstration

The Post stores the user's ID instead of the complete user information:

{
  "post_id": "P101",
  "user_id": "U101"
}

The user_id refers to a document in the Users collection:

{
  "user_id": "U101",
  "name": "Anushka Patil",
  "username": "anushka101"
}

Therefore:

Posts.user_id → Users.user_id
Comments.post_id → Posts.post_id
Comments.user_id → Users.user_id

7. Complete Data Model

SocialMediaDB
│
├── Users
│   ├── U101
│   ├── U102
│   └── U103
│
├── Posts
│   └── P101
│       ├── user_id → U101
│       └── comments[]
│           ├── C101 → U102
│           └── C102 → U103
│
└── Comments
    ├── C101
    │   ├── post_id → P101
    │   └── user_id → U102
    │
    └── C102
        ├── post_id → P101
        └── user_id → U103

8. MongoDB Compass Setup

Connect MongoDB Compass to:

mongodb://localhost:27017

Create database:

SocialMediaDB

Create these three collections:

Users
Posts
Comments

Compass should show:

localhost:27017
└── SocialMediaDB
    ├── Users
    ├── Posts
    └── Comments

9. Insert Users in Compass

Open:

SocialMediaDB → Users

Select Add Data → Insert Document and insert:

{
  "user_id": "U101",
  "name": "Anushka Patil",
  "username": "anushka101",
  "email": "anushka@example.com",
  "password": "hashed_password",
  "profile": {
    "bio": "Computer Science Student",
    "city": "Pune"
  },
  "created_at": "2026-09-22"
}

Additional users:

{
  "user_id": "U102",
  "name": "Rahul Sharma",
  "username": "rahul102",
  "email": "rahul@example.com",
  "password": "hashed_password",
  "profile": {
    "bio": "Technology Enthusiast",
    "city": "Mumbai"
  },
  "created_at": "2026-09-22"
}

{
  "user_id": "U103",
  "name": "Priya Shah",
  "username": "priya103",
  "email": "priya@example.com",
  "password": "hashed_password",
  "profile": {
    "bio": "Student",
    "city": "Pune"
  },
  "created_at": "2026-09-22"
}

10. Insert Post in Compass

Open:

SocialMediaDB → Posts

Select Add Data → Insert Document and insert:

{
  "post_id": "P101",
  "user_id": "U101",
  "content": "Learning MongoDB and MongoDB Compass today!",
  "post_type": "text",
  "likes": 25,
  "created_at": "2026-09-22T09:00:00",
  "comments": [
    {
      "comment_id": "C101",
      "user_id": "U102",
      "text": "Great! Keep learning.",
      "created_at": "2026-09-22T09:10:00"
    },
    {
      "comment_id": "C102",
      "user_id": "U103",
      "text": "MongoDB is interesting!",
      "created_at": "2026-09-22T09:15:00"
    }
  ]
}

11. Insert Comments in Compass

Open:

SocialMediaDB → Comments

Insert:

{
  "comment_id": "C101",
  "post_id": "P101",
  "user_id": "U102",
  "text": "Great! Keep learning.",
  "likes": 3,
  "created_at": "2026-09-22T09:10:00"
}

Then insert:

{
  "comment_id": "C102",
  "post_id": "P101",
  "user_id": "U103",
  "text": "MongoDB is interesting!",
  "likes": 5,
  "created_at": "2026-09-22T09:15:00"
}

12. Optional mongosh Implementation

Select the database:

use SocialMediaDB

Create collections:

db.createCollection("Users")
db.createCollection("Posts")
db.createCollection("Comments")

Insert a user:

db.Users.insertOne({
  user_id: "U101",
  name: "Anushka Patil",
  username: "anushka101",
  email: "anushka@example.com",
  password: "hashed_password",
  profile: {
    bio: "Computer Science Student",
    city: "Pune"
  },
  created_at: "2026-09-22"
})

Insert a post with embedded comments:

db.Posts.insertOne({
  post_id: "P101",
  user_id: "U101",
  content: "Learning MongoDB and MongoDB Compass today!",
  post_type: "text",
  likes: 25,
  created_at: "2026-09-22T09:00:00",
  comments: [
    {
      comment_id: "C101",
      user_id: "U102",
      text: "Great! Keep learning.",
      created_at: "2026-09-22T09:10:00"
    },
    {
      comment_id: "C102",
      user_id: "U103",
      text: "MongoDB is interesting!",
      created_at: "2026-09-22T09:15:00"
    }
  ]
})

Insert comments:

db.Comments.insertMany([
  {
    comment_id: "C101",
    post_id: "P101",
    user_id: "U102",
    text: "Great! Keep learning.",
    likes: 3,
    created_at: "2026-09-22T09:10:00"
  },
  {
    comment_id: "C102",
    post_id: "P101",
    user_id: "U103",
    text: "MongoDB is interesting!",
    likes: 5,
    created_at: "2026-09-22T09:15:00"
  }
])

Display the data:

db.Users.find().pretty()
db.Posts.find().pretty()
db.Comments.find().pretty()

13. Embedding vs Referencing

Concept                 Implementation                                       Example

Embedding               Comments are stored inside Posts                     Posts.comments[]

Referencing             User ID is stored instead of full profile            Posts.user_id

Referencing             Comment identifies its Post                          Comments.post_id

Referencing             Comment identifies its User                          Comments.user_id

14. Result

A complete MongoDB data model for a Social Media application was designed using three collections: Users, Posts, and Comments.

The Users collection stores user profiles.

The Posts collection stores posts and embeds comments inside each post.

The Comments collection stores comment records separately.

user_id is used to reference users.

post_id is used to reference posts from comments.

The comments array inside Posts demonstrates MongoDB embedding.

Conclusion

The Social Media model successfully demonstrates both embedding and referencing in MongoDB. Embedding keeps comments together with their related post, while referencing avoids repeating complete user profile information in posts and comments.
```

```
SET C — Q2: Online Food Delivery System

Case Study

Design a complete JSON-based data representation for an Online Food Delivery System.

The system contains:

Restaurant with embedded menu items

Customer with address

Order referencing restaurant and customer IDs

Order with embedded ordered items

1. Database Design

Database name:

FoodDeliveryDB

Collections:

FoodDeliveryDB
├── Restaurants
├── Customers
└── Orders

Relationships:

Restaurants
    │
    │ restaurant_id
    ↓
  Orders
    ↑
    │ customer_id
Customers

Inside a Restaurant:

Restaurant
└── menu_items[]
      ├── Item 1
      ├── Item 2
      ├── Item 3
      └── Item 4

Inside an Order:

Order
└── ordered_items[]
      ├── Item 1
      ├── Item 2
      └── Item 3

2. Restaurant Collection

Collection name:

Restaurants

JSON Document

{
  "restaurant_id": "R101",
  "restaurant_name": "Spice Garden",
  "cuisine": ["Indian", "Chinese"],
  "location": {
    "city": "Pune",
    "area": "Kothrud",
    "pincode": "411038"
  },
  "rating": 4.5,
  "contact": "9876543210",
  "menu_items": [
    {
      "item_id": "I101",
      "item_name": "Paneer Tikka",
      "category": "Starter",
      "price": 250,
      "is_available": true
    },
    {
      "item_id": "I102",
      "item_name": "Veg Biryani",
      "category": "Main Course",
      "price": 220,
      "is_available": true
    },
    {
      "item_id": "I103",
      "item_name": "Butter Naan",
      "category": "Bread",
      "price": 60,
      "is_available": true
    },
    {
      "item_id": "I104",
      "item_name": "Masala Dosa",
      "category": "South Indian",
      "price": 120,
      "is_available": false
    }
  ]
}

Why Embed Menu Items?

Menu items are embedded inside the Restaurant because they are closely related to that restaurant and are commonly retrieved along with its menu.

Choice: Embedding

3. Customer Collection

Collection name:

Customers

JSON Document

{
  "customer_id": "C101",
  "name": "Anushka Patil",
  "email": "anushka@example.com",
  "phone": "9876543210",
  "address": {
    "house_no": "12",
    "street": "Karve Road",
    "area": "Kothrud",
    "city": "Pune",
    "state": "Maharashtra",
    "pincode": "411038"
  }
}

Why Embed the Address?

The address is part of the customer's information and is normally retrieved with the customer.

Choice: Embedding

4. Order Collection

Collection name:

Orders

JSON Document

{
  "order_id": "O101",
  "customer_id": "C101",
  "restaurant_id": "R101",
  "order_date": "2026-09-22T12:30:00",
  "delivery_address": {
    "house_no": "12",
    "street": "Karve Road",
    "area": "Kothrud",
    "city": "Pune",
    "state": "Maharashtra",
    "pincode": "411038"
  },
  "ordered_items": [
    {
      "item_id": "I101",
      "item_name": "Paneer Tikka",
      "quantity": 2,
      "price": 250
    },
    {
      "item_id": "I102",
      "item_name": "Veg Biryani",
      "quantity": 1,
      "price": 220
    },
    {
      "item_id": "I103",
      "item_name": "Butter Naan",
      "quantity": 2,
      "price": 60
    }
  ],
  "subtotal": 840,
  "delivery_fee": 40,
  "total_amount": 880,
  "payment_method": "UPI",
  "payment_status": "Paid",
  "order_status": "Preparing"
}

5. Referencing Restaurant and Customer

The Order contains:

{
  "customer_id": "C101",
  "restaurant_id": "R101"
}

These IDs refer to documents in the respective collections.

Orders.customer_id → Customers.customer_id
Orders.restaurant_id → Restaurants.restaurant_id

Why Use Referencing?

A customer can place many orders:

Customer C101
    ├── Order O101
    ├── Order O105
    └── Order O110

A restaurant can receive many orders:

Restaurant R101
    ├── Order O101
    ├── Order O102
    ├── Order O103
    └── Order O104

Storing the complete customer or restaurant document inside every order would duplicate data.

Choice: Referencing

6. Why Embed Ordered Items?

Ordered items represent the specific items purchased in a particular order.

{
  "ordered_items": [
    {
      "item_id": "I101",
      "item_name": "Paneer Tikka",
      "quantity": 2,
      "price": 250
    },
    {
      "item_id": "I102",
      "item_name": "Veg Biryani",
      "quantity": 1,
      "price": 220
    }
  ]
}

An order and its ordered items are normally retrieved together.

Choice: Embedding

7. Why Store Item Name and Price in the Order?

Restaurant menu prices can change.

For example:

Current menu:
Paneer Tikka = ₹250

Later:

Paneer Tikka = ₹300

An old order should still preserve the price paid when the order was placed.

Therefore, the order stores:

{
  "item_id": "I101",
  "item_name": "Paneer Tikka",
  "quantity": 2,
  "price": 250
}

This preserves historical order information.

8. Embedding vs Referencing

Relationship                     Choice                                 Reason

Restaurant → Menu Items          Embedding            Menu belongs to restaurant and is commonly retrieved with it

Customer → Address               Embedding            Address is part of customer information

Order → Customer                 Referencing          One customer can have many orders

Order → Restaurant               Referencing          One restaurant can receive many orders

Order → Ordered Items            Embedding            Items belong to a particular order and are retrieved with it

9. Complete Data Model

FoodDeliveryDB
│
├── Restaurants
│     └── R101
│          ├── restaurant_name
│          ├── cuisine[]
│          ├── location
│          └── menu_items[]
│                ├── I101
│                ├── I102
│                ├── I103
│                └── I104
│
├── Customers
│     └── C101
│          ├── name
│          ├── email
│          ├── phone
│          └── address
│
└── Orders
      └── O101
           ├── customer_id → C101
           ├── restaurant_id → R101
           ├── order_date
           ├── delivery_address
           └── ordered_items[]
                 ├── I101
                 ├── I102
                 └── I103

10. MongoDB Compass Implementation

Connect MongoDB Compass to:

mongodb://localhost:27017

Create database:

FoodDeliveryDB

Create these collections:

Restaurants
Customers
Orders

Compass structure:

localhost:27017
└── FoodDeliveryDB
    ├── Restaurants
    ├── Customers
    └── Orders

Insert Restaurant

Open:

Restaurants → Add Data → Insert Document

Paste the Restaurant JSON from Section 2.

Insert Customer

Open:

Customers → Add Data → Insert Document

Paste the Customer JSON from Section 3.

Insert Order

Open:

Orders → Add Data → Insert Document

Paste the Order JSON from Section 4.

11. Optional mongosh Implementation

Select the database:

use FoodDeliveryDB

Create collections:

db.createCollection("Restaurants")
db.createCollection("Customers")
db.createCollection("Orders")

Insert Restaurant

db.Restaurants.insertOne({
  restaurant_id: "R101",
  restaurant_name: "Spice Garden",
  cuisine: ["Indian", "Chinese"],
  location: {
    city: "Pune",
    area: "Kothrud",
    pincode: "411038"
  },
  rating: 4.5,
  contact: "9876543210",
  menu_items: [
    {
      item_id: "I101",
      item_name: "Paneer Tikka",
      category: "Starter",
      price: 250,
      is_available: true
    },
    {
      item_id: "I102",
      item_name: "Veg Biryani",
      category: "Main Course",
      price: 220,
      is_available: true
    },
    {
      item_id: "I103",
      item_name: "Butter Naan",
      category: "Bread",
      price: 60,
      is_available: true
    },
    {
      item_id: "I104",
      item_name: "Masala Dosa",
      category: "South Indian",
      price: 120,
      is_available: false
    }
  ]
})

Insert Customer

db.Customers.insertOne({
  customer_id: "C101",
  name: "Anushka Patil",
  email: "anushka@example.com",
  phone: "9876543210",
  address: {
    house_no: "12",
    street: "Karve Road",
    area: "Kothrud",
    city: "Pune",
    state: "Maharashtra",
    pincode: "411038"
  }
})

Insert Order

db.Orders.insertOne({
  order_id: "O101",
  customer_id: "C101",
  restaurant_id: "R101",
  order_date: "2026-09-22T12:30:00",
  delivery_address: {
    house_no: "12",
    street: "Karve Road",
    area: "Kothrud",
    city: "Pune",
    state: "Maharashtra",
    pincode: "411038"
  },
  ordered_items: [
    {
      item_id: "I101",
      item_name: "Paneer Tikka",
      quantity: 2,
      price: 250
    },
    {
      item_id: "I102",
      item_name: "Veg Biryani",
      quantity: 1,
      price: 220
    },
    {
      item_id: "I103",
      item_name: "Butter Naan",
      quantity: 2,
      price: 60
    }
  ],
  subtotal: 840,
  delivery_fee: 40,
  total_amount: 880,
  payment_method: "UPI",
  payment_status: "Paid",
  order_status: "Preparing"
})

Check the data:

db.Restaurants.find().pretty()
db.Customers.find().pretty()
db.Orders.find().pretty()

12. Result

A complete JSON-based data model for an Online Food Delivery System was designed using three collections:

Restaurants

Customers

Orders

The model demonstrates:

Embedded menu items inside Restaurants.

Embedded address inside Customers.

Referenced customer using customer_id in Orders.

Referenced restaurant using restaurant_id in Orders.

Embedded ordered items inside Orders.

Historical item price preservation inside an Order.

Conclusion

The model uses embedding for closely related data that is normally accessed together and referencing for entities that are shared across many documents. This provides a practical MongoDB design for an online food delivery application.
```
-------

```
Set C
Q3. Limitations of JSON and How BSON Overcomes Them in MongoDB
Question

Research and document the limitations of JSON format and how BSON overcomes those limitations in MongoDB. Provide concrete examples showing where standard JSON would fail and how BSON handles the same scenario correctly.

1. Introduction
What is JSON?

JSON (JavaScript Object Notation) is a text-based data format commonly used for storing and exchanging data.

Example:

{
  "name": "Ramesh",
  "age": 25,
  "active": true
}

Standard JSON supports a limited set of data types:

String
Number
Boolean
Object
Array
Null
What is BSON?

BSON (Binary JSON) is the binary-encoded document format used by MongoDB.

BSON provides additional data types that are not available as native types in standard JSON, such as:

ObjectId
Date
Binary data
Int32
Int64
Decimal128
Regular Expression
Timestamp

Therefore, BSON allows MongoDB to represent data more precisely than standard JSON.

2. Limitations of Standard JSON
Limitation 1 – JSON does not have a native ObjectId type

MongoDB commonly uses ObjectId for the _id field.

Standard JSON

JSON cannot represent an ObjectId as a native JSON data type.

We would have to store it as a string:

{
  "_id": "68c123456789abcdef123456"
}

MongoDB would treat this as a String, not as an ObjectId.

BSON

BSON supports ObjectId directly:

{
  _id: ObjectId("68c123456789abcdef123456")
}

Here:

ObjectId(...)

is a BSON type.

Advantage

MongoDB can efficiently use ObjectId for document identifiers and indexes.

3. Limitation 2 – JSON has no native Date/DateTime type

Standard JSON does not have a dedicated Date data type.

For example:

{
  "createdAt": "2026-09-22T18:30:00Z"
}

The value is simply a string.

An application must interpret that string as a date.

BSON

BSON provides a native Date type.

In mongosh:

{
  createdAt: new Date()
}

Example:

db.users.insertOne({
  name: "Ramesh",
  createdAt: new Date()
})

MongoDB stores the value as a BSON Date rather than an ordinary string.

Checking the type
db.users.aggregate([
  {
    $project: {
      createdAtType: { $type: "$createdAt" }
    }
  }
])

Output will identify the field as:

date
Advantage

MongoDB can perform date-related operations such as:

Date comparisons
Sorting by date
Date aggregation
Date range queries
4. Limitation 3 – JSON has no native Binary Data type

Standard JSON cannot directly represent arbitrary binary data.

For example, suppose we want to store a PDF or image.

We might convert the binary data into Base64:

{
  "file": "JVBERi0xLjQKJc..."
}

The problem is that this is now a string containing Base64 data, not a native binary value.

It also increases the size of the data because binary data has been encoded into text.

BSON

BSON supports a dedicated Binary data type.

Conceptually:

{
  fileData: <BSON Binary Data>
}

MongoDB can therefore distinguish binary data from normal text.

Advantage

BSON can represent binary data directly, which is useful for applications dealing with:

Files
Images
Encryption data
Binary identifiers
Other raw binary information
5. Limitation 4 – JSON does not distinguish different integer sizes

JSON has a general Number type.

For example:

{
  "age": 25,
  "population": 10000000000
}

JSON does not provide separate standard types such as:

Int32
Int64
BSON

BSON provides multiple numeric types.

For example:

{
  age: NumberInt(25),
  population: NumberLong("10000000000")
}

Here:

NumberInt(25)

represents a 32-bit integer.

And:

NumberLong("10000000000")

represents a 64-bit integer.

Advantage

MongoDB can preserve the intended numeric representation and range.

6. Limitation 5 – JSON does not have Decimal128

This is particularly important for financial and monetary calculations.

A normal JSON number might look like:

{
  "price": 999.99
}

JSON does not have a native Decimal128 data type.

For applications requiring exact decimal precision, such as:

Banking
Accounting
Payments
Financial transactions

a dedicated decimal type is useful.

BSON

MongoDB supports Decimal128.

Example:

{
  price: Decimal128("999.99")
}

For example:

db.products.insertOne({
  name: "Laptop",
  price: Decimal128("99999.99")
})
Advantage

Decimal128 provides high-precision decimal arithmetic and is designed for use cases where exact decimal representation is important.

7. Limitation 6 – JSON does not preserve MongoDB-specific BSON types

Consider this JSON:

{
  "_id": "68c123456789abcdef123456",
  "createdAt": "2026-09-22T18:30:00Z",
  "price": "999.99"
}

Everything here is represented as strings.

MongoDB cannot know from ordinary JSON alone that:

_id       → ObjectId
createdAt → Date
price     → Decimal128

was intended.

BSON can store the actual types:

{
  _id: ObjectId("68c123456789abcdef123456"),
  createdAt: new Date(),
  price: Decimal128("999.99")
}

Thus, BSON preserves the type information.

Concrete Example – Student Record

Suppose we want to store a student's information.

Standard JSON
{
  "studentId": "68c123456789abcdef123456",
  "name": "Sneha",
  "age": 21,
  "fees": "25000.50",
  "admissionDate": "2026-06-15T10:30:00Z"
}

Problems:

studentId      → String
fees           → String
admissionDate  → String
age            → generic JSON Number

The application has to interpret these strings and numbers correctly.

BSON representation in MongoDB
{
  _id: ObjectId("68c123456789abcdef123456"),
  name: "Sneha",
  age: NumberInt(21),
  fees: Decimal128("25000.50"),
  admissionDate: new Date("2026-06-15T10:30:00Z")
}

Now MongoDB has explicit BSON types:

_id            → ObjectId
age            → Int32
fees           → Decimal128
admissionDate  → Date

This preserves the meaning of the data.

8. Practical MongoDB Demonstration

We can demonstrate BSON types using mongosh.

Step 1 – Create database
use bson_demo
Step 2 – Insert different BSON types
db.types.insertOne({
  name: "Ramesh",
  age: NumberInt(25),
  population: NumberLong("10000000000"),
  price: Decimal128("999.99"),
  userId: ObjectId(),
  createdAt: new Date()
})
Step 3 – Display the document
db.types.find()

You can see values such as:

age          → 25
population   → 10000000000
price        → 999.99
userId       → ObjectId(...)
createdAt    → ISODate(...)
```
