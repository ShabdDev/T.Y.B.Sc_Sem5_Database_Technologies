
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
