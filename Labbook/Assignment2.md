# Assignment 2 – Set A
```
Aim

To create a MongoDB database named Movie,
create Film and Actor collections,
insert documents, and
perform basic MongoDB queries and CRUD operations.

Create Database

Open mongosh.

use Movie

Expected output:

switched to db Movie
Explanation
use

selects a database.

Movie

is the database name.

MongoDB creates the database physically when we first store data in it.

Check the current database:

db

Expected:

Movie

Create Film Collection

The workbook requires a Film collection with:

Film Id
Title
Year of release
Genre/Category
Actors
Directors
Release details including places, dates and rating.

Create it:

db.createCollection("Film")

Expected:

{ ok: 1 }

Create Actor Collection

The workbook requires an Actor collection containing Actor ID, name, address, contact details and age.

Run:

db.createCollection("Actor")

Expected:

{ ok: 1 }

Check collections:

show collections

Expected:

Actor
Film

Insert 10 Documents into Film

We will use 10 films.

The actors, directors, and releaseDetails fields are represented using arrays and embedded documents.

Insert Films

Copy and run:

db.Film.insertMany([
  {
    FilmId: "F001",
    Title: "Inception",
    YearOfRelease: 2010,
    Genre: ["Sci-Fi", "Action", "Thriller"],
    Actors: [
      { FirstName: "Leonardo", LastName: "DiCaprio" },
      { FirstName: "Joseph", LastName: "Gordon-Levitt" }
    ],
    Directors: [
      { FirstName: "Christopher", LastName: "Nolan" }
    ],
    ReleaseDetails: {
      Places: ["USA", "UK", "India"],
      Dates: [
        new Date("2010-07-16"),
        new Date("2010-07-16"),
        new Date("2010-07-16")
      ],
      Rating: 8.8
    }
  },

  {
    FilmId: "F002",
    Title: "Interstellar",
    YearOfRelease: 2014,
    Genre: ["Sci-Fi", "Adventure", "Drama"],
    Actors: [
      { FirstName: "Matthew", LastName: "McConaughey" },
      { FirstName: "Anne", LastName: "Hathaway" }
    ],
    Directors: [
      { FirstName: "Christopher", LastName: "Nolan" }
    ],
    ReleaseDetails: {
      Places: ["USA", "UK", "India"],
      Dates: [
        new Date("2014-11-07"),
        new Date("2014-11-07"),
        new Date("2014-11-07")
      ],
      Rating: 8.7
    }
  },

  {
    FilmId: "F003",
    Title: "The Dark Knight",
    YearOfRelease: 2008,
    Genre: ["Action", "Crime", "Drama"],
    Actors: [
      { FirstName: "Christian", LastName: "Bale" },
      { FirstName: "Heath", LastName: "Ledger" }
    ],
    Directors: [
      { FirstName: "Christopher", LastName: "Nolan" }
    ],
    ReleaseDetails: {
      Places: ["USA", "UK", "India"],
      Dates: [
        new Date("2008-07-18"),
        new Date("2008-07-25"),
        new Date("2008-07-18")
      ],
      Rating: 9.0
    }
  },

  {
    FilmId: "F004",
    Title: "Titanic",
    YearOfRelease: 1997,
    Genre: ["Romance", "Drama"],
    Actors: [
      { FirstName: "Leonardo", LastName: "DiCaprio" },
      { FirstName: "Kate", LastName: "Winslet" }
    ],
    Directors: [
      { FirstName: "James", LastName: "Cameron" }
    ],
    ReleaseDetails: {
      Places: ["USA", "UK", "India"],
      Dates: [
        new Date("1997-12-19"),
        new Date("1998-01-01"),
        new Date("1997-12-19")
      ],
      Rating: 7.9
    }
  },

  {
    FilmId: "F005",
    Title: "Avatar",
    YearOfRelease: 2009,
    Genre: ["Sci-Fi", "Adventure", "Action"],
    Actors: [
      { FirstName: "Sam", LastName: "Worthington" },
      { FirstName: "Zoe", LastName: "Saldana" }
    ],
    Directors: [
      { FirstName: "James", LastName: "Cameron" }
    ],
    ReleaseDetails: {
      Places: ["USA", "UK", "India"],
      Dates: [
        new Date("2009-12-18"),
        new Date("2009-12-18"),
        new Date("2009-12-18")
      ],
      Rating: 7.8
    }
  },

  {
    FilmId: "F006",
    Title: "The Matrix",
    YearOfRelease: 1999,
    Genre: ["Sci-Fi", "Action"],
    Actors: [
      { FirstName: "Keanu", LastName: "Reeves" },
      { FirstName: "Laurence", LastName: "Fishburne" }
    ],
    Directors: [
      { FirstName: "Lana", LastName: "Wachowski" },
      { FirstName: "Lilly", LastName: "Wachowski" }
    ],
    ReleaseDetails: {
      Places: ["USA", "UK", "India"],
      Dates: [
        new Date("1999-03-31"),
        new Date("1999-04-01"),
        new Date("1999-03-31")
      ],
      Rating: 8.7
    }
  },

  {
    FilmId: "F007",
    Title: "Gladiator",
    YearOfRelease: 2000,
    Genre: ["Action", "Drama", "Adventure"],
    Actors: [
      { FirstName: "Russell", LastName: "Crowe" },
      { FirstName: "Joaquin", LastName: "Phoenix" }
    ],
    Directors: [
      { FirstName: "Ridley", LastName: "Scott" }
    ],
    ReleaseDetails: {
      Places: ["USA", "UK", "India"],
      Dates: [
        new Date("2000-05-05"),
        new Date("2000-05-05"),
        new Date("2000-05-05")
      ],
      Rating: 8.5
    }
  },

  {
    FilmId: "F008",
    Title: "Avengers Endgame",
    YearOfRelease: 2019,
    Genre: ["Action", "Adventure", "Sci-Fi"],
    Actors: [
      { FirstName: "Robert", LastName: "Downey Jr." },
      { FirstName: "Chris", LastName: "Evans" }
    ],
    Directors: [
      { FirstName: "Anthony", LastName: "Russo" },
      { FirstName: "Joe", LastName: "Russo" }
    ],
    ReleaseDetails: {
      Places: ["USA", "UK", "India"],
      Dates: [
        new Date("2019-04-26"),
        new Date("2019-04-26"),
        new Date("2019-04-26")
      ],
      Rating: 8.4
    }
  },

  {
    FilmId: "F009",
    Title: "3 Idiots",
    YearOfRelease: 2009,
    Genre: ["Comedy", "Drama"],
    Actors: [
      { FirstName: "Aamir", LastName: "Khan" },
      { FirstName: "R", LastName: "Madhavan" }
    ],
    Directors: [
      { FirstName: "Rajkumar", LastName: "Hirani" }
    ],
    ReleaseDetails: {
      Places: ["India", "USA", "UK"],
      Dates: [
        new Date("2009-12-25"),
        new Date("2010-01-01"),
        new Date("2009-12-25")
      ],
      Rating: 8.4
    }
  },

  {
    FilmId: "F010",
    Title: "Dangal",
    YearOfRelease: 2016,
    Genre: ["Biography", "Drama", "Sport"],
    Actors: [
      { FirstName: "Aamir", LastName: "Khan" },
      { FirstName: "Fatima", LastName: "Sana Shaikh" }
    ],
    Directors: [
      { FirstName: "Nitesh", LastName: "Tiwari" }
    ],
    ReleaseDetails: {
      Places: ["India", "China", "USA"],
      Dates: [
        new Date("2016-12-23"),
        new Date("2016-12-23"),
        new Date("2016-12-23")
      ],
      Rating: 8.3
    }
  }
])

Expected result will contain:

acknowledged: true
insertedIds: ...

nsert 10 Documents into Actor

The workbook requires Actor documents containing Actor ID, first name, last name, address, contact details and age.

Run:

db.Actor.insertMany([
  {
    ActorId: "A001",
    FirstName: "Leonardo",
    LastName: "DiCaprio",
    Address: {
      Street: "Hollywood Boulevard",
      City: "Los Angeles",
      State: "California",
      Country: "USA",
      PinCode: "90028"
    },
    ContactDetails: {
      EmailId: "leonardo@example.com",
      PhoneNo: "9000000001"
    },
    Age: 51
  },

  {
    ActorId: "A002",
    FirstName: "Joseph",
    LastName: "Gordon-Levitt",
    Address: {
      Street: "Sunset Boulevard",
      City: "Los Angeles",
      State: "California",
      Country: "USA",
      PinCode: "90069"
    },
    ContactDetails: {
      EmailId: "joseph@example.com",
      PhoneNo: "9000000002"
    },
    Age: 45
  },

  {
    ActorId: "A003",
    FirstName: "Matthew",
    LastName: "McConaughey",
    Address: {
      Street: "Main Street",
      City: "Austin",
      State: "Texas",
      Country: "USA",
      PinCode: "73301"
    },
    ContactDetails: {
      EmailId: "matthew@example.com",
      PhoneNo: "9000000003"
    },
    Age: 56
  },

  {
    ActorId: "A004",
    FirstName: "Anne",
    LastName: "Hathaway",
    Address: {
      Street: "Park Avenue",
      City: "New York",
      State: "New York",
      Country: "USA",
      PinCode: "10017"
    },
    ContactDetails: {
      EmailId: "anne@example.com",
      PhoneNo: "9000000004"
    },
    Age: 43
  },

  {
    ActorId: "A005",
    FirstName: "Christian",
    LastName: "Bale",
    Address: {
      Street: "Oxford Street",
      City: "London",
      State: "England",
      Country: "UK",
      PinCode: "W1D"
    },
    ContactDetails: {
      EmailId: "christian@example.com",
      PhoneNo: "9000000005"
    },
    Age: 52
  },

  {
    ActorId: "A006",
    FirstName: "Kate",
    LastName: "Winslet",
    Address: {
      Street: "Baker Street",
      City: "London",
      State: "England",
      Country: "UK",
      PinCode: "NW1"
    },
    ContactDetails: {
      EmailId: "kate@example.com",
      PhoneNo: "9000000006"
    },
    Age: 50
  },

  {
    ActorId: "A007",
    FirstName: "Sam",
    LastName: "Worthington",
    Address: {
      Street: "George Street",
      City: "Sydney",
      State: "New South Wales",
      Country: "Australia",
      PinCode: "2000"
    },
    ContactDetails: {
      EmailId: "sam@example.com",
      PhoneNo: "9000000007"
    },
    Age: 50
  },

  {
    ActorId: "A008",
    FirstName: "Keanu",
    LastName: "Reeves",
    Address: {
      Street: "Rodeo Drive",
      City: "Los Angeles",
      State: "California",
      Country: "USA",
      PinCode: "90210"
    },
    ContactDetails: {
      EmailId: "keanu@example.com",
      PhoneNo: "9000000008"
    },
    Age: 62
  },

  {
    ActorId: "A009",
    FirstName: "Aamir",
    LastName: "Khan",
    Address: {
      Street: "Pali Hill",
      City: "Mumbai",
      State: "Maharashtra",
      Country: "India",
      PinCode: "400050"
    },
    ContactDetails: {
      EmailId: "aamir@example.com",
      PhoneNo: "9000000009"
    },
    Age: 61
  },

  {
    ActorId: "A010",
    FirstName: "Fatima",
    LastName: "Sana Shaikh",
    Address: {
      Street: "Link Road",
      City: "Mumbai",
      State: "Maharashtra",
      Country: "India",
      PinCode: "400053"
    },
    ContactDetails: {
      EmailId: "fatima@example.com",
      PhoneNo: "9000000010"
    },
    Age: 34
  }
])

Query 1 – Insert at Least 10 Documents

Already completed.

Check the count:

db.Film.countDocuments()

Expected:

10

Check Actor:

db.Actor.countDocuments()
Expected:

10

The workbook specifically requires at least 10 documents in both collections.

Query 2 – Display All Documents

The workbook uses find() to display documents.

Display Film
db.Film.find().pretty()

Display Actor
db.Actor.find().pretty()
Explanation
find()

retrieves matching documents.

{}

when used as a filter means "match everything."

pretty() formats the output so it is easier to read.

Query 3 – Find Film by Title

We will search for:

Inception

Command:

db.Film.find({ Title: "Inception" }).pretty()
Explanation
Title

is the field.

"Inception"

is the value we are searching for.

Expected document begins approximately:

{
  FilmId: "F001",
  Title: "Inception",
  YearOfRelease: 2010,
  ...
}

Query 4 – Find Actor by First Name

We will search for:

Aamir

Command:

db.Actor.find({ FirstName: "Aamir" }).pretty()

Expected:

{
  ActorId: "A009",
  FirstName: "Aamir",
  LastName: "Khan",
  ...
}

Query 5 – Display Only Film Titles

The workbook demonstrates projection, where 1 includes a field and 0 excludes a field.

Run:

db.Film.find(
  {},
  {
    Title: 1,
    _id: 0
  }
)

Expected:

{ Title: 'Inception' }
{ Title: 'Interstellar' }
{ Title: 'The Dark Knight' }
{ Title: 'Titanic' }
...

Important
Title: 1

means include Title.

_id: 0

means don't display MongoDB's automatically generated _id.

Query 6 – Delete a Film

We will delete:

Inception

Command:

db.Film.deleteOne({ Title: "Inception" })

Expected:

{
  acknowledged: true,
  deletedCount: 1
}
Explanation

deleteOne() removes one document matching the condition.

The workbook describes deleteOne() as the method used to remove a document based on deletion criteria.

Check:

db.Film.find({ Title: "Inception" })

It should return no document.

Query 7 – Count Total Films

Run:

db.Film.countDocuments()

Originally we inserted 10 films.

After deleting Inception:

Total = 9

The workbook gives countDocuments() for obtaining the document count.

Query 8 – Remove All Documents Whose Film ID Is a Given Value

We will use:

F007

Command:

db.Film.deleteMany({ FilmId: "F007" })

Expected:

{
  acknowledged: true,
  deletedCount: 1
}

Why deleteMany()?

The question says:

Remove all the documents whose Film ID is ...

Therefore, deleteMany() is appropriate.

After this operation:

Film count = 8

because:

10 original
- 1 Inception
- 1 Gladiator
= 8

Query 9 – Remove First Record from Actor

The workbook's older syntax discusses remove() with the justOne parameter for removing only one record.

For your current mongosh, use the modern deleteOne() method.

First see one document:

db.Actor.findOne()

Suppose it returns:

{
  ActorId: "A001",
  FirstName: "Leonardo",
  ...
}

Store that document:

const firstActor = db.Actor.findOne()

Then delete exactly that document:

db.Actor.deleteOne({ _id: firstActor._id })

Expected:

{
  acknowledged: true,
  deletedCount: 1
}

Check:

db.Actor.countDocuments()

Expected:

9
Why use _id?

Every MongoDB document has a unique _id, so deleting using _id identifies exactly the document returned by findOne().

Query 10 – Drop Database Movie

⚠️ Important: Do this only after completing and verifying all other queries.

First check:

db

Expected:

Movie

Then:

db.dropDatabase()

Expected:

{ ok: 1, dropped: 'Movie' }

Check databases:

show dbs

Movie should no longer appear if it contains no remaining data.

The workbook specifies db.dropDatabase() for deleting an existing database.

Complete Query List for Practical

// 1. Create database
use Movie

// 2. Create collections
db.createCollection("Film")
db.createCollection("Actor")

// 3. Display collections
show collections

// 4. Display all Film documents
db.Film.find().pretty()

// 5. Display all Actor documents
db.Actor.find().pretty()

// 6. Find Film by Title
db.Film.find({ Title: "Inception" }).pretty()

// 7. Find Actor by First Name
db.Actor.find({ FirstName: "Aamir" }).pretty()

// 8. Display only Film Titles
db.Film.find({}, { Title: 1, _id: 0 })

// 9. Delete a Film
db.Film.deleteOne({ Title: "Inception" })

// 10. Count Total Films
db.Film.countDocuments()

// 11. Remove all documents with FilmId
db.Film.deleteMany({ FilmId: "F007" })

// 12. Remove first Actor record
const firstActor = db.Actor.findOne()
db.Actor.deleteOne({ _id: firstActor._id })

// 13. Drop Movie database
db.dropDatabase()
```

# Assignment 2 – Set B

```
Assignment 2 – Set B: MongoDB

Aim

To create the Company database, create Employee and Transaction collections, insert at least 10 documents into each, and perform the required queries.

This solution follows the SPPU T.Y.B.Sc. Computer Science Database Technologies workbook, Assignment 2, Set B. The workbook specifies the Company database, the fields for Employee and Transaction, and the ten required queries. fileciteturn1file0L766-L798

1. Create Database

Open mongosh:

use Company

Check:

db

Expected:

Company

2. Create Collections

Employee

db.createCollection("Employee")

Transaction

db.createCollection("Transaction")

Check:

show collections

Expected:

Employee
Transaction

The workbook defines Employee with Employee ID, name, email, phone, address, salary, designation, experience, date of joining and birthdate. It defines Transaction with transaction ID/date, employee name, transaction details and payment details. fileciteturn1file0L766-L787

Query 1 – Insert at Least 10 Employee Documents

db.Employee.insertMany([
  {
    EmployeeId: "E001",
    FirstName: "Amit",
    LastName: "Kulkarni",
    Email: "amit.kulkarni@example.com",
    PhoneNo: "9000000001",
    Address: {
      HouseNo: "101",
      Street: "FC Road",
      City: "Pune",
      State: "Maharashtra",
      Country: "India",
      PinCode: "411004"
    },
    Salary: 65000,
    Designation: "Software Developer",
    Experience: 3,
    DateOfJoining: new Date("2023-06-12"),
    Birthdate: new Date("1998-04-15")
  },
  {
    EmployeeId: "E002",
    FirstName: "Priya",
    LastName: "Sharma",
    Email: "priya.sharma@example.com",
    PhoneNo: "9000000002",
    Address: {
      HouseNo: "202",
      Street: "Baner Road",
      City: "Pune",
      State: "Maharashtra",
      Country: "India",
      PinCode: "411045"
    },
    Salary: 72000,
    Designation: "Senior Developer",
    Experience: 5,
    DateOfJoining: new Date("2021-03-15"),
    Birthdate: new Date("1996-08-22")
  },
  {
    EmployeeId: "E003",
    FirstName: "Rahul",
    LastName: "Patil",
    Email: "rahul.patil@example.com",
    PhoneNo: "9000000003",
    Address: {
      HouseNo: "303",
      Street: "MG Road",
      City: "Mumbai",
      State: "Maharashtra",
      Country: "India",
      PinCode: "400001"
    },
    Salary: 85000,
    Designation: "Team Lead",
    Experience: 7,
    DateOfJoining: new Date("2019-07-01"),
    Birthdate: new Date("1993-11-10")
  },
  {
    EmployeeId: "E004",
    FirstName: "Sneha",
    LastName: "Joshi",
    Email: "sneha.joshi@example.com",
    PhoneNo: "9000000004",
    Address: {
      HouseNo: "404",
      Street: "Kothrud Road",
      City: "Pune",
      State: "Maharashtra",
      Country: "India",
      PinCode: "411038"
    },
    Salary: 60000,
    Designation: "Tester",
    Experience: 3,
    DateOfJoining: new Date("2023-01-09"),
    Birthdate: new Date("1999-02-18")
  },
  {
    EmployeeId: "E005",
    FirstName: "Vikas",
    LastName: "Desai",
    Email: "vikas.desai@example.com",
    PhoneNo: "9000000005",
    Address: {
      HouseNo: "505",
      Street: "Hinjewadi Road",
      City: "Pune",
      State: "Maharashtra",
      Country: "India",
      PinCode: "411057"
    },
    Salary: 95000,
    Designation: "Project Manager",
    Experience: 9,
    DateOfJoining: new Date("2017-09-18"),
    Birthdate: new Date("1990-06-25")
  },
  {
    EmployeeId: "E006",
    FirstName: "Neha",
    LastName: "Shinde",
    Email: "neha.shinde@example.com",
    PhoneNo: "9000000006",
    Address: {
      HouseNo: "606",
      Street: "College Road",
      City: "Nashik",
      State: "Maharashtra",
      Country: "India",
      PinCode: "422005"
    },
    Salary: 68000,
    Designation: "Software Developer",
    Experience: 4,
    DateOfJoining: new Date("2022-02-14"),
    Birthdate: new Date("1997-12-03")
  },
  {
    EmployeeId: "E007",
    FirstName: "Rohit",
    LastName: "Mehta",
    Email: "rohit.mehta@example.com",
    PhoneNo: "9000000007",
    Address: {
      HouseNo: "707",
      Street: "Andheri East",
      City: "Mumbai",
      State: "Maharashtra",
      Country: "India",
      PinCode: "400069"
    },
    Salary: 78000,
    Designation: "DevOps Engineer",
    Experience: 5,
    DateOfJoining: new Date("2021-08-23"),
    Birthdate: new Date("1995-05-17")
  },
  {
    EmployeeId: "E008",
    FirstName: "Pooja",
    LastName: "More",
    Email: "pooja.more@example.com",
    PhoneNo: "9000000008",
    Address: {
      HouseNo: "808",
      Street: "Civil Lines",
      City: "Nagpur",
      State: "Maharashtra",
      Country: "India",
      PinCode: "440001"
    },
    Salary: 58000,
    Designation: "HR Executive",
    Experience: 3,
    DateOfJoining: new Date("2023-04-03"),
    Birthdate: new Date("1999-09-12")
  },
  {
    EmployeeId: "E009",
    FirstName: "Sagar",
    LastName: "Jadhav",
    Email: "sagar.jadhav@example.com",
    PhoneNo: "9000000009",
    Address: {
      HouseNo: "909",
      Street: "Shivaji Nagar",
      City: "Pune",
      State: "Maharashtra",
      Country: "India",
      PinCode: "411005"
    },
    Salary: 74000,
    Designation: "Database Administrator",
    Experience: 6,
    DateOfJoining: new Date("2020-10-19"),
    Birthdate: new Date("1994-03-29")
  },
  {
    EmployeeId: "E010",
    FirstName: "Kavita",
    LastName: "Rane",
    Email: "kavita.rane@example.com",
    PhoneNo: "9000000010",
    Address: {
      HouseNo: "1001",
      Street: "Karve Road",
      City: "Pune",
      State: "Maharashtra",
      Country: "India",
      PinCode: "411052"
    },
    Salary: 82000,
    Designation: "Senior Tester",
    Experience: 6,
    DateOfJoining: new Date("2020-05-11"),
    Birthdate: new Date("1995-10-07")
  }
])

Verify:

db.Employee.countDocuments()

Expected:

10

Query 2 – Insert At Least 10 Transaction Documents

db.Transaction.insertMany([
  {
    TransactionId: "T001",
    TransactionDate: new Date("2026-09-01"),
    Name: "Amit",
    TransactionDetails: {
      ItemId: "I001",
      ItemName: "Laptop",
      Quantity: 1,
      Price: 65000
    },
    Payment: {
      Type: "Credit Card",
      TotalAmountPaid: 65000,
      PaymentSuccessful: true
    }
  },
  {
    TransactionId: "T002",
    TransactionDate: new Date("2026-09-02"),
    Name: "Priya",
    TransactionDetails: {
      ItemId: "I002",
      ItemName: "Monitor",
      Quantity: 2,
      Price: 18000
    },
    Payment: {
      Type: "Debit Card",
      TotalAmountPaid: 36000,
      PaymentSuccessful: true
    }
  },
  {
    TransactionId: "T003",
    TransactionDate: new Date("2026-09-03"),
    Name: "Rahul",
    TransactionDetails: {
      ItemId: "I003",
      ItemName: "Keyboard",
      Quantity: 2,
      Price: 2500
    },
    Payment: {
      Type: "Credit Card",
      TotalAmountPaid: 5000,
      PaymentSuccessful: true
    }
  },
  {
    TransactionId: "T004",
    TransactionDate: new Date("2026-09-04"),
    Name: "Sneha",
    TransactionDetails: {
      ItemId: "I004",
      ItemName: "Mouse",
      Quantity: 3,
      Price: 1200
    },
    Payment: {
      Type: "Cash",
      TotalAmountPaid: 3600,
      PaymentSuccessful: true
    }
  },
  {
    TransactionId: "T005",
    TransactionDate: new Date("2026-09-05"),
    Name: "Vikas",
    TransactionDetails: {
      ItemId: "I005",
      ItemName: "Printer",
      Quantity: 1,
      Price: 15000
    },
    Payment: {
      Type: "Credit Card",
      TotalAmountPaid: 15000,
      PaymentSuccessful: true
    }
  },
  {
    TransactionId: "T006",
    TransactionDate: new Date("2026-09-06"),
    Name: "Neha",
    TransactionDetails: {
      ItemId: "I006",
      ItemName: "Hard Disk",
      Quantity: 2,
      Price: 5500
    },
    Payment: {
      Type: "Debit Card",
      TotalAmountPaid: 11000,
      PaymentSuccessful: true
    }
  },
  {
    TransactionId: "T007",
    TransactionDate: new Date("2026-09-07"),
    Name: "Rohit",
    TransactionDetails: {
      ItemId: "I007",
      ItemName: "SSD",
      Quantity: 1,
      Price: 7000
    },
    Payment: {
      Type: "Credit Card",
      TotalAmountPaid: 7000,
      PaymentSuccessful: true
    }
  },
  {
    TransactionId: "T008",
    TransactionDate: new Date("2026-09-08"),
    Name: "Pooja",
    TransactionDetails: {
      ItemId: "I008",
      ItemName: "Webcam",
      Quantity: 1,
      Price: 4000
    },
    Payment: {
      Type: "Cash",
      TotalAmountPaid: 4000,
      PaymentSuccessful: true
    }
  },
  {
    TransactionId: "T009",
    TransactionDate: new Date("2026-09-09"),
    Name: "Sagar",
    TransactionDetails: {
      ItemId: "I009",
      ItemName: "Router",
      Quantity: 2,
      Price: 3000
    },
    Payment: {
      Type: "Credit Card",
      TotalAmountPaid: 6000,
      PaymentSuccessful: true
    }
  },
  {
    TransactionId: "T010",
    TransactionDate: new Date("2026-09-10"),
    Name: "Kavita",
    TransactionDetails: {
      ItemId: "I010",
      ItemName: "Tablet",
      Quantity: 1,
      Price: 22000
    },
    Payment: {
      Type: "Debit Card",
      TotalAmountPaid: 22000,
      PaymentSuccessful: true
    }
  }
])

Verify:

db.Transaction.countDocuments()

Expected:

10

Query 3 – Display All Documents

Employee

db.Employee.find().pretty()

Transaction

db.Transaction.find().pretty()

Query 4 – Find Employee by Employee ID

Example: find E005.

db.Employee.find({
  EmployeeId: "E005"
}).pretty()

Result:

Vikas Desai

Query 5 – Find Employee by Designation

Example: find all Software Developer employees.

db.Employee.find({
  Designation: "Software Developer"
}).pretty()

This returns:

Amit Kulkarni
Neha Shinde

Query 6 – Delete Only One Transaction

Delete transaction T004:

db.Transaction.deleteOne({
  TransactionId: "T004"
})

Expected:

{
  acknowledged: true,
  deletedCount: 1
}

Verify:

db.Transaction.find({
  TransactionId: "T004"
})

Query 7 – Count Transactions and Employees

Transactions

db.Transaction.countDocuments()

After deleting T004:

9

Employees

db.Employee.countDocuments()

Before employee deletions:

10

Query 8 – Find Credit Card Payments

Payment is an embedded document, so use dot notation:

db.Transaction.find({
  "Payment.Type": "Credit Card"
}).pretty()

The query searches:

Payment
   └── Type
        └── "Credit Card"

Query 9 – Delete Employee by First Name and Last Name

Example:

db.Employee.deleteOne({
  FirstName: "Vikas",
  LastName: "Desai"
})

Verify:

db.Employee.find({
  FirstName: "Vikas",
  LastName: "Desai"
})

No matching document should remain.

Query 10 – Remove First Employee Record

First retrieve one employee:

const firstEmployee = db.Employee.findOne()

Delete exactly that document:

db.Employee.deleteOne({
  _id: firstEmployee._id
})

Verify:

db.Employee.countDocuments()

After deleting Vikas Desai and the first employee:

8

Final Verification

db.Employee.countDocuments()
db.Transaction.countDocuments()

Expected final counts:

Collection

Initial

Deleted

Final

Employee

10

2

8

Transaction

10

1

9

Complete Query Sheet

use Company

db.createCollection("Employee")
db.createCollection("Transaction")

show collections

// Display all
db.Employee.find().pretty()
db.Transaction.find().pretty()

// Find Employee by ID
db.Employee.find({ EmployeeId: "E005" }).pretty()

// Find Employee by Designation
db.Employee.find({
  Designation: "Software Developer"
}).pretty()

// Delete one Transaction
db.Transaction.deleteOne({
  TransactionId: "T004"
})

// Count Transactions
db.Transaction.countDocuments()

// Count Employees
db.Employee.countDocuments()

// Find Credit Card Payments
db.Transaction.find({
  "Payment.Type": "Credit Card"
}).pretty()

// Delete Employee by First and Last Name
db.Employee.deleteOne({
  FirstName: "Vikas",
  LastName: "Desai"
})

// Remove first Employee
const firstEmployee = db.Employee.findOne()
db.Employee.deleteOne({
  _id: firstEmployee._id
})

// Final counts
db.Employee.countDocuments()
db.Transaction.countDocuments()

```
Assignment 2 - Set C

```

Assignment 2 – Set C

Installation and Configuration of MongoDB with Database and Collection Creation

Aim

To create a MongoDB database named Hotel, create Customer, Room, and Booking collections, insert documents, and perform the required MongoDB queries.

This solution follows the SPPU T.Y.B.Sc. Computer Science Database Technologies workbook, Assignment 2, Set C. The workbook specifies the Hotel database, the three collections and their fields, and the 15 required queries. fileciteturn1file0L800-L836

1. Create Database Hotel

Open MongoDB Shell (mongosh) and run:

use Hotel

Check the current database:

db

Expected:

Hotel

2. Create the Customer Collection

The Customer collection contains:

Customer ID

Name

Contact Number

Email

Address

Create it:

db.createCollection("Customer")

Expected:

{ ok: 1 }

3. Create the Room Collection

The Room collection contains:

Room Number

Room Type

Rent Per Day

Availability Status

Create it:

db.createCollection("Room")

Expected:

{ ok: 1 }

4. Create the Booking Collection

The Booking collection contains:

Booking ID

Customer Name

Room Number

Check-In Date

Check-Out Date

Total Bill

Create it:

db.createCollection("Booking")

Check all collections:

show collections

Expected:

Booking
Customer
Room

Query 1 – Insert at Least 10 Documents

The workbook requires at least 10 documents in each of the Customer, Room, and Booking collections. fileciteturn1file0L821-L823

1.1 Insert 10 Customer Documents

db.Customer.insertMany([
  {
    CustomerId: "101",
    Name: "Amit Patil",
    ContactNumber: "9845671231",
    Email: "amit@example.com",
    Address: "Shivaji Nagar, Pune"
  },
  {
    CustomerId: "102",
    Name: "Rani Deshmukh",
    ContactNumber: "9845671237",
    Email: "rani@example.com",
    Address: "Satara Road, Satara"
  },
  {
    CustomerId: "103",
    Name: "Rahul Jadhav",
    ContactNumber: "9845671233",
    Email: "rahul@example.com",
    Address: "FC Road, Pune"
  },
  {
    CustomerId: "104",
    Name: "Sneha Joshi",
    ContactNumber: "9845671234",
    Email: "sneha@example.com",
    Address: "College Road, Nashik"
  },
  {
    CustomerId: "105",
    Name: "Vikas Shinde",
    ContactNumber: "9845671235",
    Email: "vikas@example.com",
    Address: "MG Road, Mumbai"
  },
  {
    CustomerId: "106",
    Name: "Pooja More",
    ContactNumber: "9845671236",
    Email: "pooja@example.com",
    Address: "Main Road, Satara"
  },
  {
    CustomerId: "107",
    Name: "Sagar Kulkarni",
    ContactNumber: "9845671238",
    Email: "sagar@example.com",
    Address: "Kothrud, Pune"
  },
  {
    CustomerId: "108",
    Name: "Neha Pawar",
    ContactNumber: "9845671239",
    Email: "neha@example.com",
    Address: "Camp, Pune"
  },
  {
    CustomerId: "109",
    Name: "Rohit Mehta",
    ContactNumber: "9845671240",
    Email: "rohit@example.com",
    Address: "Andheri, Mumbai"
  },
  {
    CustomerId: "110",
    Name: "Kavita Rane",
    ContactNumber: "9845671241",
    Email: "kavita@example.com",
    Address: "Karve Road, Pune"
  }
])

Verify:

db.Customer.countDocuments()

Expected:

10

1.2 Insert 10 Room Documents

db.Room.insertMany([
  {
    RoomNumber: "101",
    RoomType: "Deluxe",
    RentPerDay: 3500,
    AvailabilityStatus: "Available"
  },
  {
    RoomNumber: "102",
    RoomType: "Standard",
    RentPerDay: 2000,
    AvailabilityStatus: "Booked"
  },
  {
    RoomNumber: "103",
    RoomType: "Suite",
    RentPerDay: 5000,
    AvailabilityStatus: "Available"
  },
  {
    RoomNumber: "104",
    RoomType: "Deluxe",
    RentPerDay: 3500,
    AvailabilityStatus: "Available"
  },
  {
    RoomNumber: "105",
    RoomType: "Standard",
    RentPerDay: 2200,
    AvailabilityStatus: "Booked"
  },
  {
    RoomNumber: "106",
    RoomType: "Suite",
    RentPerDay: 5500,
    AvailabilityStatus: "Available"
  },
  {
    RoomNumber: "107",
    RoomType: "Deluxe",
    RentPerDay: 4000,
    AvailabilityStatus: "Maintenance"
  },
  {
    RoomNumber: "108",
    RoomType: "Standard",
    RentPerDay: 2100,
    AvailabilityStatus: "Available"
  },
  {
    RoomNumber: "109",
    RoomType: "Deluxe",
    RentPerDay: 3800,
    AvailabilityStatus: "Booked"
  },
  {
    RoomNumber: "110",
    RoomType: "Suite",
    RentPerDay: 6000,
    AvailabilityStatus: "Available"
  }
])

Verify:

db.Room.countDocuments()

Expected:

10

1.3 Insert 10 Booking Documents

db.Booking.insertMany([
  {
    BookingId: "B001",
    CustomerName: "Amit Patil",
    RoomNumber: "102",
    CheckInDate: new Date("2026-09-01"),
    CheckOutDate: new Date("2026-09-03"),
    TotalBill: 4000
  },
  {
    BookingId: "B002",
    CustomerName: "Rani Deshmukh",
    RoomNumber: "105",
    CheckInDate: new Date("2026-09-02"),
    CheckOutDate: new Date("2026-09-05"),
    TotalBill: 6600
  },
  {
    BookingId: "B003",
    CustomerName: "Rahul Jadhav",
    RoomNumber: "109",
    CheckInDate: new Date("2026-09-03"),
    CheckOutDate: new Date("2026-09-06"),
    TotalBill: 11400
  },
  {
    BookingId: "B004",
    CustomerName: "Sneha Joshi",
    RoomNumber: "103",
    CheckInDate: new Date("2026-09-04"),
    CheckOutDate: new Date("2026-09-06"),
    TotalBill: 10000
  },
  {
    BookingId: "B005",
    CustomerName: "Vikas Shinde",
    RoomNumber: "101",
    CheckInDate: new Date("2026-09-05"),
    CheckOutDate: new Date("2026-09-08"),
    TotalBill: 10500
  },
  {
    BookingId: "B006",
    CustomerName: "Pooja More",
    RoomNumber: "107",
    CheckInDate: new Date("2026-09-06"),
    CheckOutDate: new Date("2026-09-08"),
    TotalBill: 8000
  },
  {
    BookingId: "B007",
    CustomerName: "Sagar Kulkarni",
    RoomNumber: "102",
    CheckInDate: new Date("2026-09-07"),
    CheckOutDate: new Date("2026-09-09"),
    TotalBill: 4000
  },
  {
    BookingId: "B008",
    CustomerName: "Neha Pawar",
    RoomNumber: "104",
    CheckInDate: new Date("2026-09-08"),
    CheckOutDate: new Date("2026-09-10"),
    TotalBill: 7000
  },
  {
    BookingId: "B009",
    CustomerName: "Rohit Mehta",
    RoomNumber: "106",
    CheckInDate: new Date("2026-09-09"),
    CheckOutDate: new Date("2026-09-11"),
    TotalBill: 11000
  },
  {
    BookingId: "B010",
    CustomerName: "Kavita Rane",
    RoomNumber: "110",
    CheckInDate: new Date("2026-09-10"),
    CheckOutDate: new Date("2026-09-13"),
    TotalBill: 18000
  }
])

Verify:

db.Booking.countDocuments()

Expected:

10

Query 2 – Display All Documents

The workbook asks to display all documents from the three collections. fileciteturn1file0L821-L823

Customer

db.Customer.find().pretty()

Room

db.Room.find().pretty()

Booking

db.Booking.find().pretty()

Query 3 – Delete Customers with IDs 102, 105 and 107

The workbook specifically asks to delete customers whose IDs are 102, 105, and 107. fileciteturn1file0L824-L824

Use $in to match all three IDs:

db.Customer.deleteMany({
  CustomerId: {
    $in: ["102", "105", "107"]
  }
})

Expected:

{
  acknowledged: true,
  deletedCount: 3
}

Verify:

db.Customer.find().pretty()

Customer count:

db.Customer.countDocuments()

Expected:

7

Why $in?

$in: ["102", "105", "107"]

means:

CustomerId = 102
OR
CustomerId = 105
OR
CustomerId = 107

Query 4 – Find Booking by Booking ID

We will search for:

B004

Command:

db.Booking.find({
  BookingId: "B004"
}).pretty()

Expected customer:

Sneha Joshi

Query 5 – Count Customers and Room Collection

The workbook asks to count both Customer and Room collections. fileciteturn1file0L825-L826

Customer count

After Query 3:

db.Customer.countDocuments()

Expected:

7

Room count

db.Room.countDocuments()

Expected:

10

Query 6 – Find Customer from Satara

The workbook asks to find a customer from Satara. fileciteturn1file0L827-L827

Because our address is stored as a single string, use a regular expression:

db.Customer.find({
  Address: /Satara/i
}).pretty()

Expected result includes:

Pooja More

i makes the regular expression case-insensitive.

Query 7 – Remove a Specific Booking ID

We will remove:

B006

Command:

db.Booking.deleteOne({
  BookingId: "B006"
})

Expected:

{
  acknowledged: true,
  deletedCount: 1
}

Verify:

db.Booking.find({
  BookingId: "B006"
})

No document should be returned.

Query 8 – Display Customer Name Rani and Contact Number 9845671237

The workbook specifies the exact customer name and contact number. fileciteturn1file0L828-L829

Run:

db.Customer.find({
  Name: "Rani Deshmukh",
  ContactNumber: "9845671237"
}).pretty()

Expected:

Rani Deshmukh
9845671237

If your teacher expects the name field to contain exactly Rani

You can instead use:

db.Customer.find({
  Name: "Rani",
  ContactNumber: "9845671237"
}).pretty()

However, in our inserted data the complete name is Rani Deshmukh, so the first query matches our data.

Query 9 – Display Room Number and Rent Per Day

We will use:

Room Number = 101
Rent Per Day = 3500

The workbook asks to display the specified room number and rent per day. fileciteturn1file0L829-L830

Run:

db.Room.find({
  RoomNumber: "101",
  RentPerDay: 3500
}).pretty()

Expected:

{
  RoomNumber: "101",
  RoomType: "Deluxe",
  RentPerDay: 3500,
  AvailabilityStatus: "Available"
}

Query 10 – Remove a Specific Booking by Customer Name

We will remove the booking for:

CustomerName = "Rohit Mehta"

Command:

db.Booking.deleteOne({
  CustomerName: "Rohit Mehta"
})

Expected:

{
  acknowledged: true,
  deletedCount: 1
}

Verify:

db.Booking.find({
  CustomerName: "Rohit Mehta"
})

Query 11 – Find Room Availability Status

We will search for:

Available

Command:

db.Room.find({
  AvailabilityStatus: "Available"
}).pretty()

This displays all available rooms.

Query 12 – Find Deluxe Rooms

The workbook specifically asks for rooms where:

Room Type = Deluxe

fileciteturn1file0L832-L833

Run:

db.Room.find({
  RoomType: "Deluxe"
}).pretty()

Expected rooms include:

101
104
107
109

Query 13 – Remove All Documents from Customer Collection

⚠️ This deletes all Customer documents.

The workbook asks to remove all documents from the Customer collection. fileciteturn1file0L833-L835

Run:

db.Customer.deleteMany({})

Expected:

{
  acknowledged: true,
  deletedCount: 7
}

Check:

db.Customer.countDocuments()

Expected:

0

Important

This removes the documents, but the Customer collection itself still exists.

Query 14 – Delete All Documents from Booking Collection

The workbook asks to delete all documents in Booking. fileciteturn1file0L834-L835

Run:

db.Booking.deleteMany({})

Expected:

{
  acknowledged: true,
  deletedCount: 8
}

Check:

db.Booking.countDocuments()

Expected:

0

Important

deleteMany({}) removes all documents but does not drop the collection.

Query 15 – Drop Database Hotel

The workbook specifies dropping the Hotel database as the final operation. fileciteturn1file0L835-L836

First check:

db

Expected:

Hotel

Then:

db.dropDatabase()

Expected:

{
  ok: 1,
  dropped: "Hotel"
}

Check:

show dbs

Hotel should no longer appear once it contains no data.

Complete Query Sheet

// ==========================================
// ASSIGNMENT 2 - SET C
// HOTEL DATABASE
// ==========================================

// 1. Create / select database
use Hotel

// 2. Create collections
db.createCollection("Customer")
db.createCollection("Room")
db.createCollection("Booking")

// 3. Check collections
show collections


// ==========================================
// QUERY 1
// Insert at least 10 documents
// ==========================================

// Customer
db.Customer.insertMany([
  {
    CustomerId: "101",
    Name: "Amit Patil",
    ContactNumber: "9845671231",
    Email: "amit@example.com",
    Address: "Shivaji Nagar, Pune"
  },
  {
    CustomerId: "102",
    Name: "Rani Deshmukh",
    ContactNumber: "9845671237",
    Email: "rani@example.com",
    Address: "Satara Road, Satara"
  },
  {
    CustomerId: "103",
    Name: "Rahul Jadhav",
    ContactNumber: "9845671233",
    Email: "rahul@example.com",
    Address: "FC Road, Pune"
  },
  {
    CustomerId: "104",
    Name: "Sneha Joshi",
    ContactNumber: "9845671234",
    Email: "sneha@example.com",
    Address: "College Road, Nashik"
  },
  {
    CustomerId: "105",
    Name: "Vikas Shinde",
    ContactNumber: "9845671235",
    Email: "vikas@example.com",
    Address: "MG Road, Mumbai"
  },
  {
    CustomerId: "106",
    Name: "Pooja More",
    ContactNumber: "9845671236",
    Email: "pooja@example.com",
    Address: "Main Road, Satara"
  },
  {
    CustomerId: "107",
    Name: "Sagar Kulkarni",
    ContactNumber: "9845671238",
    Email: "sagar@example.com",
    Address: "Kothrud, Pune"
  },
  {
    CustomerId: "108",
    Name: "Neha Pawar",
    ContactNumber: "9845671239",
    Email: "neha@example.com",
    Address: "Camp, Pune"
  },
  {
    CustomerId: "109",
    Name: "Rohit Mehta",
    ContactNumber: "9845671240",
    Email: "rohit@example.com",
    Address: "Andheri, Mumbai"
  },
  {
    CustomerId: "110",
    Name: "Kavita Rane",
    ContactNumber: "9845671241",
    Email: "kavita@example.com",
    Address: "Karve Road, Pune"
  }
])

// Room
db.Room.insertMany([
  { RoomNumber: "101", RoomType: "Deluxe", RentPerDay: 3500, AvailabilityStatus: "Available" },
  { RoomNumber: "102", RoomType: "Standard", RentPerDay: 2000, AvailabilityStatus: "Booked" },
  { RoomNumber: "103", RoomType: "Suite", RentPerDay: 5000, AvailabilityStatus: "Available" },
  { RoomNumber: "104", RoomType: "Deluxe", RentPerDay: 3500, AvailabilityStatus: "Available" },
  { RoomNumber: "105", RoomType: "Standard", RentPerDay: 2200, AvailabilityStatus: "Booked" },
  { RoomNumber: "106", RoomType: "Suite", RentPerDay: 5500, AvailabilityStatus: "Available" },
  { RoomNumber: "107", RoomType: "Deluxe", RentPerDay: 4000, AvailabilityStatus: "Maintenance" },
  { RoomNumber: "108", RoomType: "Standard", RentPerDay: 2100, AvailabilityStatus: "Available" },
  { RoomNumber: "109", RoomType: "Deluxe", RentPerDay: 3800, AvailabilityStatus: "Booked" },
  { RoomNumber: "110", RoomType: "Suite", RentPerDay: 6000, AvailabilityStatus: "Available" }
])

// Booking
db.Booking.insertMany([
  {
    BookingId: "B001",
    CustomerName: "Amit Patil",
    RoomNumber: "102",
    CheckInDate: new Date("2026-09-01"),
    CheckOutDate: new Date("2026-09-03"),
    TotalBill: 4000
  },
  {
    BookingId: "B002",
    CustomerName: "Rani Deshmukh",
    RoomNumber: "105",
    CheckInDate: new Date("2026-09-02"),
    CheckOutDate: new Date("2026-09-05"),
    TotalBill: 6600
  },
  {
    BookingId: "B003",
    CustomerName: "Rahul Jadhav",
    RoomNumber: "109",
    CheckInDate: new Date("2026-09-03"),
    CheckOutDate: new Date("2026-09-06"),
    TotalBill: 11400
  },
  {
    BookingId: "B004",
    CustomerName: "Sneha Joshi",
    RoomNumber: "103",
    CheckInDate: new Date("2026-09-04"),
    CheckOutDate: new Date("2026-09-06"),
    TotalBill: 10000
  },
  {
    BookingId: "B005",
    CustomerName: "Vikas Shinde",
    RoomNumber: "101",
    CheckInDate: new Date("2026-09-05"),
    CheckOutDate: new Date("2026-09-08"),
    TotalBill: 10500
  },
  {
    BookingId: "B006",
    CustomerName: "Pooja More",
    RoomNumber: "107",
    CheckInDate: new Date("2026-09-06"),
    CheckOutDate: new Date("2026-09-08"),
    TotalBill: 8000
  },
  {
    BookingId: "B007",
    CustomerName: "Sagar Kulkarni",
    RoomNumber: "102",
    CheckInDate: new Date("2026-09-07"),
    CheckOutDate: new Date("2026-09-09"),
    TotalBill: 4000
  },
  {
    BookingId: "B008",
    CustomerName: "Neha Pawar",
    RoomNumber: "104",
    CheckInDate: new Date("2026-09-08"),
    CheckOutDate: new Date("2026-09-10"),
    TotalBill: 7000
  },
  {
    BookingId: "B009",
    CustomerName: "Rohit Mehta",
    RoomNumber: "106",
    CheckInDate: new Date("2026-09-09"),
    CheckOutDate: new Date("2026-09-11"),
    TotalBill: 11000
  },
  {
    BookingId: "B010",
    CustomerName: "Kavita Rane",
    RoomNumber: "110",
    CheckInDate: new Date("2026-09-10"),
    CheckOutDate: new Date("2026-09-13"),
    TotalBill: 18000
  }
])

// Verify counts
db.Customer.countDocuments()
db.Room.countDocuments()
db.Booking.countDocuments()


// ==========================================
// QUERY 2
// Display all documents
// ==========================================

db.Customer.find().pretty()
db.Room.find().pretty()
db.Booking.find().pretty()


// ==========================================
// QUERY 3
// Delete Customer IDs 102, 105, 107
// ==========================================

db.Customer.deleteMany({
  CustomerId: {
    $in: ["102", "105", "107"]
  }
})


// ==========================================
// QUERY 4
// Find Booking by Booking ID
// ==========================================

db.Booking.find({
  BookingId: "B004"
}).pretty()


// ==========================================
// QUERY 5
// Count Customers and Rooms
// ==========================================

db.Customer.countDocuments()
db.Room.countDocuments()


// ==========================================
// QUERY 6
// Find Customer from Satara
// ==========================================

db.Customer.find({
  Address: /Satara/i
}).pretty()


// ==========================================
// QUERY 7
// Remove Specific Booking
// ==========================================

db.Booking.deleteOne({
  BookingId: "B006"
})


// ==========================================
// QUERY 8
// Find Rani with specified contact number
// ==========================================

db.Customer.find({
  Name: "Rani Deshmukh",
  ContactNumber: "9845671237"
}).pretty()


// ==========================================
// QUERY 9
// Find Room 101 with Rent 3500
// ==========================================

db.Room.find({
  RoomNumber: "101",
  RentPerDay: 3500
}).pretty()


// ==========================================
// QUERY 10
// Remove Booking by Customer Name
// ==========================================

db.Booking.deleteOne({
  CustomerName: "Rohit Mehta"
})


// ==========================================
// QUERY 11
// Find Available Rooms
// ==========================================

db.Room.find({
  AvailabilityStatus: "Available"
}).pretty()


// ==========================================
// QUERY 12
// Find Deluxe Rooms
// ==========================================

db.Room.find({
  RoomType: "Deluxe"
}).pretty()


// ==========================================
// QUERY 13
// Remove ALL Customer documents
// ==========================================

db.Customer.deleteMany({})


// ==========================================
// QUERY 14
// Remove ALL Booking documents
// ==========================================

db.Booking.deleteMany({})


// ==========================================
// QUERY 15
// Drop Hotel database
// ==========================================

db.dropDatabase()

Important Concepts Used

Concept

Example

Database

Hotel

Collections

Customer, Room, Booking

Insert multiple documents

insertMany()

Display documents

find()

Count documents

countDocuments()

Delete one

deleteOne()

Delete multiple

deleteMany()

Match multiple values

$in

Regular expression

/Satara/i

Date

new Date("2026-09-01")

Embedded/nested data

Not required in this Set C schema

Drop database

db.dropDatabase()

Viva Questions

Q1. How do you create the Hotel database?

use Hotel

Q2. How many collections are required?

Three:

Customer
Room
Booking

Q3. How do you insert multiple documents?

db.Customer.insertMany([...])

Q4. How do you delete customers with IDs 102, 105 and 107?

db.Customer.deleteMany({
  CustomerId: {
    $in: ["102", "105", "107"]
  }
})

Q5. What does $in do?

It matches a field against any value in the specified array.

Q6. How do you find a booking by Booking ID?

db.Booking.find({
  BookingId: "B004"
})

Q7. How do you count documents?

db.Customer.countDocuments()

Q8. How do you find a customer from Satara?

db.Customer.find({
  Address: /Satara/i
})

Q9. What is the difference between deleteMany({}) and drop()?

deleteMany({})
    ↓
Deletes all documents
Collection remains

drop()
    ↓
Deletes the collection itself

Q10. How do you remove all Booking documents?

db.Booking.deleteMany({})

Q11. How do you drop the Hotel database?

db.dropDatabase()

Final Expected State

Before Query 13 and Query 14:

Customer = 7
Room     = 10
Booking  = 8

After Query 13:

Customer = 0

After Query 14:

Booking = 0

Room remains:

Room = 10

Finally, Query 15:

db.dropDatabase()

removes the Hotel database.

```
