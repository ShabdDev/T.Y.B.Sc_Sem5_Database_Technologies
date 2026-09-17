# MongoDB Complete Setup Guide — Ubuntu 22.04 to MongoDB Compass

## 1. MongoDB Basics

MongoDB is a document-oriented NoSQL database.

- `mongod` = MongoDB database server/service
- `mongosh` = MongoDB command-line shell
- MongoDB Compass = MongoDB graphical user interface (GUI)
- Database = contains collections
- Collection = contains documents
- Document = JSON-like record
- BSON = binary representation used internally by MongoDB

Conceptual comparison:

| SQL | MongoDB |
|---|---|
| Database | Database |
| Table | Collection |
| Row | Document |
| Column | Field |
| SQL client / GUI | `mongosh` / Compass |

---

## 2. Check Ubuntu Version

```bash
lsb_release -a
```

or:

```bash
cat /etc/os-release
```

This guide uses Ubuntu 22.04 (Jammy).

---

## 3. Update Ubuntu

```bash
sudo apt update
```

Optional:

```bash
sudo apt upgrade -y
```

---

## 4. Install Required Packages

```bash
sudo apt-get install -y gnupg curl
```

---

## 5. Add MongoDB Repository Key

For MongoDB 8.0 on Ubuntu 22.04:

```bash
curl -fsSL https://pgp.mongodb.com/server-8.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg --dearmor
```

---

## 6. Add MongoDB Repository

```bash
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
```

---

## 7. Update Package List

```bash
sudo apt-get update
```

---

## 8. Install MongoDB Community Server

```bash
sudo apt-get install -y mongodb-org
```

---

## 9. Start MongoDB

```bash
sudo systemctl start mongod
```

---

## 10. Check MongoDB Status

```bash
sudo systemctl status mongod
```

Look for:

```text
Active: active (running)
```

If the status opens in a pager, press:

```text
q
```

---

## 11. Enable MongoDB at Startup

```bash
sudo systemctl enable mongod
```

Useful service commands:

```bash
sudo systemctl start mongod
sudo systemctl stop mongod
sudo systemctl restart mongod
sudo systemctl status mongod
```

---

## 12. Open MongoDB Shell

```bash
mongosh
```

The normal local connection is:

```text
mongodb://localhost:27017
```

or:

```text
mongodb://127.0.0.1:27017
```

Exit:

```javascript
exit
```

or:

```javascript
quit()
```

---

## 13. Basic `mongosh` Commands

Show databases:

```javascript
show dbs
```

Select a database:

```javascript
use College
```

Create a collection:

```javascript
db.createCollection("Students")
```

Insert a document:

```javascript
db.Students.insertOne({
  name: "Anushka",
  roll_number: 101,
  age: 20,
  department: "Computer Science"
})
```

Display documents:

```javascript
db.Students.find()
```

Pretty output:

```javascript
db.Students.find().pretty()
```

Show collections:

```javascript
show collections
```

---

# 14. JSON and MongoDB

Example JSON:

```json
{
  "name": "Anushka",
  "roll_number": 101,
  "age": 20,
  "department": "Computer Science",
  "subjects": [
    "DBMS",
    "MongoDB",
    "Python"
  ],
  "address": {
    "city": "Pune",
    "pincode": "411001"
  }
}
```

To store it using `mongosh`:

```javascript
db.Students.insertOne({
  "name": "Anushka",
  "roll_number": 101,
  "age": 20,
  "department": "Computer Science",
  "subjects": [
    "DBMS",
    "MongoDB",
    "Python"
  ],
  "address": {
    "city": "Pune",
    "pincode": "411001"
  }
})
```

MongoDB stores documents internally as BSON.

---

# 15. Install MongoDB Compass

## Important

Download the `.deb` into your home directory, not directly into `/`.

Go home:

```bash
cd ~
```

Check:

```bash
pwd
```

It should look like:

```text
/home/abc
```

Download Compass:

```bash
wget https://downloads.mongodb.com/compass/mongodb-compass_1.50.0_amd64.deb
```

Install:

```bash
sudo apt install ./mongodb-compass_1.50.0_amd64.deb
```

Verify:

```bash
mongodb-compass --version
```

Start:

```bash
mongodb-compass
```

You can also open it from:

**Applications → MongoDB Compass**

---

# 16. If Compass Is Already Installed

If installation output contains:

```text
Setting up mongodb-compass (1.50.0) ...
```

Compass is already installed.

You do not need to download it again.

Run:

```bash
mongodb-compass --version
```

Then:

```bash
mongodb-compass
```

---

# 17. Fix `.deb` Permission Denied

If you run `wget` while the terminal is at:

```text
/
```

you may get:

```text
Permission denied
```

Fix:

```bash
cd ~
```

Then:

```bash
wget https://downloads.mongodb.com/compass/mongodb-compass_1.50.0_amd64.deb
```

Then:

```bash
sudo apt install ./mongodb-compass_1.50.0_amd64.deb
```

If you get:

```text
Unsupported file ./mongodb-compass_1.50.0_amd64.deb
```

check that the file exists:

```bash
ls ~/mongodb-compass_1.50.0_amd64.deb
```

Then:

```bash
cd ~
sudo apt install ./mongodb-compass_1.50.0_amd64.deb
```

---

# 18. Connect Compass to MongoDB

First make sure the server is running:

```bash
sudo systemctl status mongod
```

You want:

```text
Active: active (running)
```

If stopped:

```bash
sudo systemctl start mongod
```

Open Compass.

Connection string:

```text
mongodb://localhost:27017
```

Alternative:

```text
mongodb://127.0.0.1:27017
```

Click **Connect**.

---

# 19. Fix Compass `ECONNREFUSED 127.0.0.1:27017`

If Compass shows:

```text
ECONNREFUSED 127.0.0.1:27017
```

Compass is installed, but it cannot reach the MongoDB server at that address/port.

Check:

```bash
sudo systemctl status mongod
```

If stopped:

```bash
sudo systemctl start mongod
```

Check again:

```bash
sudo systemctl status mongod
```

Then reconnect Compass using:

```text
mongodb://localhost:27017
```

If MongoDB still fails to start:

```bash
sudo journalctl -u mongod --no-pager -n 30
```

---

# 20. Create Database in Compass

After connecting:

1. Click **Create Database**
2. Database Name:

```text
SetA_DB
```

3. Collection Name:

```text
Q1_Student
```

4. Click **Create Database**

You should have:

```text
SetA_DB
└── Q1_Student
```

---

# 21. Insert a Document in Compass

Open:

```text
SetA_DB → Q1_Student
```

Then:

**Add Data → Insert Document**

Paste:

```json
{
  "name": "Anushka",
  "roll_number": 101,
  "age": 20,
  "department": "Computer Science",
  "subjects": [
    "DBMS",
    "MongoDB",
    "Python"
  ],
  "address": {
    "city": "Pune",
    "pincode": "411001"
  }
}
```

Click **Insert**.

---

# 22. Set A Practical Structure

For the Set A practical, create:

```text
localhost:27017
└── SetA_DB
    ├── Q1_Student
    ├── Q2_Employee
    ├── Q3_Library
    ├── Q4_Product
    ├── Q5_Hospital
    ├── Q6_Movie
    ├── Q7_Customer
    ├── Q8_Weather
    ├── Q9_Course
    └── Q10_Quiz
```

---

# 23. Set A — Q1 Student

Collection:

```text
Q1_Student
```

```json
{
  "name": "Anushka",
  "roll_number": 101,
  "age": 20,
  "department": "Computer Science",
  "subjects": [
    "DBMS",
    "MongoDB",
    "Python"
  ],
  "address": {
    "city": "Pune",
    "pincode": "411001"
  }
}
```

Demonstrates arrays and embedded documents.

---

# 24. Set A — Q2 Employee

Collection:

```text
Q2_Employee
```

```json
{
  "empid": 101,
  "name": "Amit",
  "salary": 50000,
  "department": "IT",
  "skills": [
    "Java",
    "SQL",
    "MongoDB"
  ]
}
```

Structured representation:

| Empid | Name | Salary | Department | Skills |
|---|---|---:|---|---|
| 101 | Amit | 50000 | IT | Java, SQL, MongoDB |

---

# 25. Set A — Q3 Library

Collection:

```text
Q3_Library
```

```json
{
  "book_id": 101,
  "title": "Introduction to Database Systems",
  "author": "Raghu Ramakrishnan",
  "price": 550,
  "availability": true,
  "genres": [
    "Database",
    "Computer Science",
    "Technology"
  ]
}
```

---

# 26. Set A — Q4 Product Catalog

Collection:

```text
Q4_Product
```

Insert these as separate MongoDB documents.

Product 1:

```json
{
  "product_id": 101,
  "product_name": "Laptop",
  "category": "Electronics",
  "price": 55000,
  "stock_quantity": 10
}
```

Product 2:

```json
{
  "product_id": 102,
  "product_name": "Mouse",
  "category": "Electronics",
  "price": 800,
  "stock_quantity": 25
}
```

Product 3:

```json
{
  "product_id": 103,
  "product_name": "Keyboard",
  "category": "Electronics",
  "price": 1500,
  "stock_quantity": 15
}
```

---

# 27. Set A — Q5 Hospital Patient

Collection:

```text
Q5_Hospital
```

```json
{
  "patient_id": 501,
  "name": "Rahul Sharma",
  "age": 45,
  "diagnosis": "Diabetes",
  "doctor": {
    "name": "Dr. Priya Deshmukh",
    "specialization": "Endocrinology"
  },
  "prescribed_medicines": [
    "Metformin",
    "Glimepiride",
    "Vitamin D"
  ]
}
```

---

# 28. Set A — Q6 Movie

Collection:

```text
Q6_Movie
```

```json
{
  "movie_id": 101,
  "title": "The Database Journey",
  "release_year": 2025,
  "director": {
    "name": "Raj Mehta",
    "country": "India"
  },
  "runtime": 135,
  "rating": 4.5,
  "cast": [
    {
      "actor_name": "Amit Kumar",
      "character_name": "Arjun"
    },
    {
      "actor_name": "Priya Shah",
      "character_name": "Meera"
    },
    {
      "actor_name": "Rahul Patil",
      "character_name": "Vikram"
    }
  ]
}
```

---

# 29. Set A — Q7 Customer

Collection:

```text
Q7_Customer
```

Customer 1:

```json
{
  "cust_id": 101,
  "fname": "Amit",
  "lname": "Patil",
  "email": "amit@example.com",
  "phone": "9876543210",
  "loyalty_points": 500
}
```

Customer 2:

```json
{
  "cust_id": 102,
  "fname": "Priya",
  "lname": "Shah",
  "email": "priya@example.com",
  "phone": "9876543211"
}
```

Customer 3:

```json
{
  "cust_id": 103,
  "fname": "Rahul",
  "lname": "Joshi",
  "email": "rahul@example.com",
  "phone": "9876543212",
  "loyalty_points": 250
}
```

`loyalty_points` appears only in some documents, demonstrating schema flexibility.

---

# 30. Set A — Q8 Weather

Collection:

```text
Q8_Weather
```

```json
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
      "day": "Day 1",
      "temperature": 29
    },
    {
      "day": "Day 2",
      "temperature": 30
    },
    {
      "day": "Day 3",
      "temperature": 27
    },
    {
      "day": "Day 4",
      "temperature": 26
    },
    {
      "day": "Day 5",
      "temperature": 28
    }
  ]
}
```

---

# 31. Set A — Q9 Course Enrollment

Collection:

```text
Q9_Course
```

```json
{
  "course_id": "CS101",
  "course_name": "Database Technologies",
  "instructor_name": "Dr. Amit Kulkarni",
  "credits": 4,
  "semester": "Semester 5",
  "max_capacity": 60,
  "enrolled_students": [
    {
      "student_name": "Anushka",
      "registration_ids": [
        "REG101",
        "REG102"
      ]
    },
    {
      "student_name": "Rahul",
      "registration_ids": [
        "REG103"
      ]
    },
    {
      "student_name": "Priya",
      "registration_ids": [
        "REG104",
        "REG105"
      ]
    }
  ]
}
```

---

# 32. Set A — Q10 Online Quiz

Collection:

```text
Q10_Quiz
```

```json
{
  "quiz_id": 101,
  "title": "MongoDB Basics Quiz",
  "subject": "Database Technologies",
  "questions": [
    {
      "question_text": "What type of database is MongoDB?",
      "options": [
        "Relational",
        "Document-oriented",
        "Hierarchical",
        "Network"
      ],
      "correct_answer": "Document-oriented",
      "total_marks": 2
    },
    {
      "question_text": "What is a collection in MongoDB?",
      "options": [
        "A group of databases",
        "A group of documents",
        "A single field",
        "A server"
      ],
      "correct_answer": "A group of documents",
      "total_marks": 2
    },
    {
      "question_text": "Which format is commonly used to represent MongoDB documents?",
      "options": [
        "JSON",
        "HTML",
        "CSS",
        "CSV"
      ],
      "correct_answer": "JSON",
      "total_marks": 2
    }
  ]
}
```

---

# 33. Test `mongosh` and Compass Together

In `mongosh`:

```javascript
use SetA_DB
```

Then:

```javascript
db.Test.insertOne({
  name: "MongoDB Test",
  status: "Working"
})
```

Open Compass and navigate to:

```text
localhost:27017
└── SetA_DB
    └── Test
```

You should see:

```json
{
  "name": "MongoDB Test",
  "status": "Working"
}
```

This confirms that `mongosh` and Compass are connected to the same MongoDB server.

---

# 34. Complete Setup Flow

```text
Ubuntu 22.04
     ↓
Update system
     ↓
Add MongoDB repository
     ↓
Install mongodb-org
     ↓
Start mongod
     ↓
Check active (running)
     ↓
Open mongosh
     ↓
Test MongoDB
     ↓
Install MongoDB Compass
     ↓
Open Compass
     ↓
Connect to mongodb://localhost:27017
     ↓
Create database
     ↓
Create collection
     ↓
Insert JSON document
     ↓
View/query documents
```

---

# 35. Final Verification Checklist

- [ ] Ubuntu 22.04 verified
- [ ] MongoDB repository added
- [ ] `mongodb-org` installed
- [ ] `mongod` is active/running
- [ ] `mongosh` opens
- [ ] MongoDB Compass installed
- [ ] Compass opens
- [ ] Compass connects to `mongodb://localhost:27017`
- [ ] Database created
- [ ] Collection created
- [ ] JSON document inserted
- [ ] Document visible in Compass

---

# 36. Practical Notebook / Exam Note

For a practical record, show:

1. MongoDB installation commands
2. MongoDB service status
3. `mongosh` connection
4. Database creation
5. Collection creation
6. JSON document insertion
7. `find()` output
8. Compass connection
9. Database/collection view in Compass
10. Screenshots if required by the teacher

For questions that say “write the JSON structure manually,” the JSON can be written in the notebook. Using Compass demonstrates that the JSON-like document can actually be stored and viewed in MongoDB.

---

# 37. Key Concepts to Remember

```text
mongod   = MongoDB server
mongosh  = command-line interface
Compass  = graphical interface
Database = group of collections
Collection = group of documents
Document = JSON-like record
BSON = Binary JSON representation
```

Local MongoDB connection:

```text
mongodb://localhost:27017
```

Alternative:

```text
mongodb://127.0.0.1:27017
```

# End
