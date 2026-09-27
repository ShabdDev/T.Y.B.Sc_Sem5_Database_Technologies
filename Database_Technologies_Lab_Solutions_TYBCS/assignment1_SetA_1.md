# Assignment 1 — Set A
## Design and Representation of Data using Structured, Semi-Structured, and JSON Formats

> Source: T.Y.B.Sc. Computer Science, CS-3010-MJ-P Database Technologies Workbook, Assignment 1, Set A.
> The workbook asks for JSON representations of student, library, product, hospital, movie, customer, weather, course-enrollment, and quiz data.

## Q1. Student JSON document

### Solution
```json
{
  "name": "Anushka Patil",
  "roll_number": "TYBSC101",
  "age": 20,
  "department": "Computer Science",
  "subjects": ["DBMS", "Python", "MongoDB", "Operating Systems"],
  "address": {
    "city": "Pune",
    "pincode": "411001"
  }
}
```

### Key point
`subjects` is an array and `address` is an embedded object, demonstrating nested JSON.

## Q2. Structured table vs semi-structured JSON

### Structured representation
| EmpID | Name | Salary | Department | Skills |
|---|---|---:|---|---|
| E101 | Amit | 65000 | IT | Java, SQL |
| E102 | Priya | 72000 | HR | Excel, Payroll |
| E103 | Rahul | 80000 | IT | Python, MongoDB |

A relational table has a fixed schema: every row is expected to use the same columns.

### Semi-structured representation
```json
[
  {
    "empid": "E101",
    "name": "Amit",
    "salary": 65000,
    "department": "IT",
    "skills": ["Java", "SQL"]
  },
  {
    "empid": "E102",
    "name": "Priya",
    "salary": 72000,
    "department": "HR",
    "skills": ["Excel", "Payroll"],
    "location": "Pune"
  },
  {
    "empid": "E103",
    "name": "Rahul",
    "salary": 80000,
    "department": "IT",
    "skills": ["Python", "MongoDB"]
  }
]
```

The second JSON document has an additional `location` field, showing schema flexibility.

## Q3. Library book JSON

```json
{
  "book_id": "B101",
  "title": "Database System Concepts",
  "author": "Abraham Silberschatz",
  "price": 650,
  "availability": true,
  "genres": ["Database", "Computer Science", "Education"]
}
```

## Q4. Product catalog as JSON array

```json
[
  {
    "product_id": "P101",
    "product_name": "Laptop",
    "category": "Electronics",
    "price": 65000,
    "stock_quantity": 12
  },
  {
    "product_id": "P102",
    "product_name": "Wireless Mouse",
    "category": "Accessories",
    "price": 900,
    "stock_quantity": 50
  },
  {
    "product_id": "P103",
    "product_name": "Keyboard",
    "category": "Accessories",
    "price": 1500,
    "stock_quantity": 35
  }
]
```

## Q5. Hospital patient with embedded doctor details

```json
{
  "patient_id": "PT101",
  "name": "Riya Sharma",
  "age": 35,
  "diagnosis": "Viral Fever",
  "doctor": {
    "name": "Dr. Neha Kulkarni",
    "specialization": "General Medicine"
  },
  "prescribed_medicines": [
    {
      "name": "Paracetamol",
      "dosage": "500 mg",
      "frequency": "Twice daily"
    },
    {
      "name": "ORS",
      "dosage": "1 sachet",
      "frequency": "As required"
    }
  ]
}
```

## Q6. Movie JSON

```json
{
  "movie_id": "M101",
  "title": "Interstellar",
  "release_year": 2014,
  "director": {
    "name": "Christopher Nolan",
    "country": "United Kingdom"
  },
  "runtime": 169,
  "rating": 4.8,
  "cast": [
    {
      "name": "Matthew McConaughey",
      "character": "Cooper"
    },
    {
      "name": "Anne Hathaway",
      "character": "Amelia Brand"
    }
  ]
}
```

## Q7. Customer records with optional loyalty points

```json
[
  {
    "cust_id": "C101",
    "fname": "Amit",
    "lname": "Sharma",
    "email": "amit@example.com",
    "phone": "9876543210",
    "loyalty_points": 450
  },
  {
    "cust_id": "C102",
    "fname": "Priya",
    "lname": "Patil",
    "email": "priya@example.com",
    "phone": "9876543211"
  },
  {
    "cust_id": "C103",
    "fname": "Rahul",
    "lname": "Desai",
    "email": "rahul@example.com",
    "phone": "9876543212",
    "loyalty_points": 220
  }
]
```

## Q8. Weather JSON

```json
{
  "location": {
    "city": "Pune",
    "country": "India",
    "latitude": 18.5204,
    "longitude": 73.8567
  },
  "current_conditions": {
    "temperature": 27.5,
    "humidity": 68,
    "wind_speed": 12.4
  },
  "forecast": [
    {"day": "Day 1", "temperature": 28},
    {"day": "Day 2", "temperature": 29},
    {"day": "Day 3", "temperature": 27},
    {"day": "Day 4", "temperature": 26},
    {"day": "Day 5", "temperature": 28}
  ]
}
```

## Q9. Course enrollment JSON

```json
{
  "course_id": "CS501",
  "course_name": "Database Technologies",
  "instructor_name": "Dr. Sharma",
  "credits": 4,
  "semester": "V",
  "max_capacity": 60,
  "enrolled_students": [
    {"registration_id": "REG001", "student_id": "TY101"},
    {"registration_id": "REG002", "student_id": "TY102"},
    {"registration_id": "REG003", "student_id": "TY103"}
  ]
}
```

## Q10. Online quiz JSON

```json
{
  "quiz_id": "QZ101",
  "title": "MongoDB Basics",
  "subject": "Database Technologies",
  "questions": [
    {
      "question_text": "MongoDB stores documents internally in which format?",
      "options": ["XML", "BSON", "CSV", "HTML"],
      "correct_answer": "BSON"
    },
    {
      "question_text": "Which MongoDB method inserts one document?",
      "options": ["findOne", "insertOne", "updateOne", "deleteOne"],
      "correct_answer": "insertOne"
    }
  ],
  "total_marks": 10
}
```

## Result
The requested structured, semi-structured, and JSON representations were designed successfully. The examples demonstrate objects, arrays, nested objects, booleans, numbers, strings, and optional fields.
