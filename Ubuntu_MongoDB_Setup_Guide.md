# Assignment 1 --- Environment Setup Guide

## Design and Representation of Data using Structured, Semi-Structured, and JSON Formats

This guide prepares the Ubuntu machine for **Assignment 1 -- Set A, Set
B and Set C**.

The goal is to complete the practical using a simple local environment.
Students do **not** need Neo4j, Docker, MongoDB Atlas, or any cloud
service for this assignment.

------------------------------------------------------------------------

## 1. Required Environment

  -----------------------------------------------------------------------
  Component               Required                Purpose
  ----------------------- ----------------------- -----------------------
  Ubuntu 22.04 LTS 64-bit Yes                     Operating system

  MongoDB Community       Yes                     Database server
  Edition                                         

  MongoDB Shell           Yes                     MongoDB command-line
  (`mongosh`)                                     interface

  MongoDB Compass         Yes                     MongoDB graphical
                                                  interface

  Visual Studio Code      Recommended             Create and edit
                                                  JSON/practical files

  Git                     Optional                Clone/push the GitHub
                                                  practical repository

  Neo4j Desktop           No                      Not used in Assignment
                                                  1

  Neo4j Browser           No                      Not used in Assignment
                                                  1

  MongoDB Atlas           No                      Local MongoDB is
                                                  sufficient

  Docker                  No                      Not required
  -----------------------------------------------------------------------

> **Important:** The general laboratory environment may list Neo4j, but
> Set A, Set B and Set C of this Assignment 1 are based on structured
> data, semi-structured data, JSON, BSON and MongoDB. Therefore, Neo4j
> is not required to perform these sets.

------------------------------------------------------------------------

# 2. Before Starting

## 2.1 Open Terminal

Press:

``` text
Ctrl + Alt + T
```

## 2.2 Check Ubuntu Version

Run:

``` bash
lsb_release -a
```

For this guide, students should use:

``` text
Ubuntu 22.04 LTS
Codename: jammy
```

Check the architecture:

``` bash
uname -m
```

Expected:

``` text
x86_64
```

MongoDB 8.0 Community Edition supports 64-bit Ubuntu 22.04 LTS (Jammy).
MongoDB recommends using its official APT repository for installation.

## 2.3 Update Ubuntu

``` bash
sudo apt update
```

Then:

``` bash
sudo apt upgrade -y
```

Install basic tools:

``` bash
sudo apt install -y curl gnupg wget ca-certificates
```

------------------------------------------------------------------------

# 3. Install MongoDB Community Edition

We will use the official MongoDB 8.0 Community Edition APT repository.

## Step 3.1 --- Import MongoDB GPG Key

Run:

``` bash
curl -fsSL https://pgp.mongodb.com/server-8.0.asc | \
sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \
--dearmor
```

## Step 3.2 --- Add MongoDB Repository

Ubuntu 22.04 uses the codename `jammy`.

Run:

``` bash
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/8.0 multiverse" | \
sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
```

Verify:

``` bash
cat /etc/apt/sources.list.d/mongodb-org-8.0.list
```

You should see a repository containing:

``` text
jammy/mongodb-org/8.0
```

## Step 3.3 --- Update Package Information

``` bash
sudo apt update
```

## Step 3.4 --- Install MongoDB

``` bash
sudo apt install -y mongodb-org
```

------------------------------------------------------------------------

# 4. Start MongoDB

Start the MongoDB server:

``` bash
sudo systemctl start mongod
```

Check its status:

``` bash
sudo systemctl status mongod
```

Look for:

``` text
Active: active (running)
```

Press:

``` text
q
```

to exit the status screen.

## 4.1 Enable MongoDB at Startup

``` bash
sudo systemctl enable mongod
```

Verify:

``` bash
sudo systemctl is-enabled mongod
```

Expected:

``` text
enabled
```

## 4.2 Useful MongoDB Service Commands

Start:

``` bash
sudo systemctl start mongod
```

Stop:

``` bash
sudo systemctl stop mongod
```

Restart:

``` bash
sudo systemctl restart mongod
```

Check status:

``` bash
sudo systemctl status mongod
```

------------------------------------------------------------------------

# 5. Verify MongoDB Installation

Check the MongoDB server:

``` bash
mongod --version
```

Check MongoDB Shell:

``` bash
mongosh --version
```

Both commands should display version information.

------------------------------------------------------------------------

# 6. Test MongoDB Using `mongosh`

Start the MongoDB Shell:

``` bash
mongosh
```

You should connect to the local MongoDB server.

Run:

``` javascript
show dbs
```

Then:

``` javascript
db
```

You should initially be connected to:

``` text
test
```

## 6.1 Create a Test Database and Collection

Run:

``` javascript
use TYCSE_DB
```

Insert one document:

``` javascript
db.students.insertOne({
    roll_no: 101,
    name: "Asha",
    department: "Computer Science"
})
```

Expected result contains:

``` text
acknowledged: true
```

Check the collection:

``` javascript
show collections
```

Expected:

``` text
students
```

Display the document:

``` javascript
db.students.find()
```

You should see the student document.

## 6.2 Exit `mongosh`

``` javascript
exit
```

At this point, MongoDB Community Edition and `mongosh` are working.

------------------------------------------------------------------------

# 7. Install MongoDB Compass

MongoDB Compass is the GUI used to visually work with databases,
collections and documents.

MongoDB provides a Linux `.deb` package for Compass.

## Step 7.1 --- Go to Downloads

``` bash
cd ~/Downloads
```

## Step 7.2 --- Download Compass

The MongoDB Compass version can change over time. Use the current `.deb`
download from the official MongoDB Compass installation page.

For the version currently documented:

``` bash
wget https://downloads.mongodb.com/compass/mongodb-compass_1.50.0_amd64.deb
```

## Step 7.3 --- Install Compass

``` bash
sudo apt install ./mongodb-compass_1.50.0_amd64.deb
```

If the package has dependency problems, run:

``` bash
sudo apt --fix-broken install
```

Then repeat the installation command.

## Step 7.4 --- Verify Compass

``` bash
mongodb-compass --version
```

## Step 7.5 --- Start Compass

``` bash
mongodb-compass
```

Compass should open.

------------------------------------------------------------------------

# 8. Connect MongoDB Compass to Local MongoDB

In MongoDB Compass, use this connection string:

``` text
mongodb://localhost:27017
```

Click:

``` text
Connect
```

You should see databases such as:

``` text
admin
config
local
TYCSE_DB
```

Open:

``` text
TYCSE_DB
```

Then open:

``` text
students
```

You should see the test document created earlier.

### Connection Architecture

``` text
MongoDB Compass
       |
       | mongodb://localhost:27017
       |
       v
MongoDB Server (mongod)
       |
       v
TYCSE_DB
       |
       v
students collection
       |
       v
Student document
```

------------------------------------------------------------------------

# 9. Install Visual Studio Code

VS Code is recommended for writing:

-   JSON documents
-   MongoDB query files
-   Markdown practical notes
-   Assignment files

The official VS Code documentation provides a `.deb` package for
Ubuntu/Debian systems.

## Step 9.1 --- Download VS Code

Open the official VS Code download page:

https://code.visualstudio.com/download

Select:

``` text
Linux
→ .deb
→ 64-bit
```

The downloaded file will normally be in:

``` text
~/Downloads
```

## Step 9.2 --- Install the `.deb` Package

Go to Downloads:

``` bash
cd ~/Downloads
```

List the downloaded files:

``` bash
ls
```

You should see a file similar to:

``` text
code_...._amd64.deb
```

Install it:

``` bash
sudo apt install ./code_*.deb
```

## Step 9.3 --- Verify VS Code

``` bash
code --version
```

## Step 9.4 --- Open VS Code

``` bash
code
```

------------------------------------------------------------------------

# 10. Prepare the Assignment Workspace

Create a folder for the database practicals:

``` bash
mkdir -p ~/Database_Practicals/Assignment_1
```

Move into it:

``` bash
cd ~/Database_Practicals/Assignment_1
```

Open the folder in VS Code:

``` bash
code .
```

Create the following structure:

``` text
Assignment_1/
│
├── README.md
│
├── Set-A/
│   ├── set-a.json
│   └── set-a-queries.js
│
├── Set-B/
│   ├── set-b.json
│   └── set-b-queries.js
│
└── Set-C/
    ├── set-c.json
    └── set-c-queries.js
```

Students may create the folders manually in VS Code if preferred.

------------------------------------------------------------------------

# 11. Recommended VS Code Extensions

Open VS Code.

Press:

``` text
Ctrl + Shift + X
```

Search for:

### 1. MongoDB for VS Code

Useful for:

-   connecting to MongoDB
-   browsing databases
-   browsing collections
-   running MongoDB queries

### 2. Prettier

Useful for formatting JSON and other files.

### 3. Markdown All in One

Useful for GitHub Markdown files.

> The extensions are optional. MongoDB Compass and `mongosh` are
> sufficient to perform the database practical.

------------------------------------------------------------------------

# 12. Optional --- Install Git

Git is **not required to execute the MongoDB practical**, but it is
useful if students need to clone or submit the practical through GitHub.

Install:

``` bash
sudo apt install -y git
```

Verify:

``` bash
git --version
```

Configure the student's Git identity:

``` bash
git config --global user.name "Your Name"
```

``` bash
git config --global user.email "your-email@example.com"
```

Check:

``` bash
git config --global --list
```

------------------------------------------------------------------------

# 13. Final Environment Verification

Students should perform all checks below before starting Set A.

## Ubuntu

``` bash
lsb_release -a
```

## Architecture

``` bash
uname -m
```

Expected:

``` text
x86_64
```

## MongoDB Server

``` bash
mongod --version
```

## MongoDB Shell

``` bash
mongosh --version
```

## MongoDB Service

``` bash
sudo systemctl status mongod
```

Expected:

``` text
active (running)
```

## MongoDB Compass

``` bash
mongodb-compass --version
```

## VS Code

``` bash
code --version
```

## Git --- Optional

``` bash
git --version
```

------------------------------------------------------------------------

# 14. Final MongoDB Connection Test

Open Terminal:

``` bash
mongosh
```

Run:

``` javascript
use TYCSE_DB
```

Run:

``` javascript
db.students.find()
```

You should see:

``` text
{
    roll_no: 101,
    name: 'Asha',
    department: 'Computer Science'
}
```

Exit:

``` javascript
exit
```

Now open MongoDB Compass and connect to:

``` text
mongodb://localhost:27017
```

Open:

``` text
TYCSE_DB
→ students
```

The same document should be visible.

If the document appears in both `mongosh` and Compass, the MongoDB setup
is ready.

------------------------------------------------------------------------

# 15. What Students Will Use During the Practical

## Set A

Students will primarily use:

``` text
VS Code
   ↓
Write JSON
   ↓
mongosh / Compass
   ↓
Insert documents
   ↓
Find and verify documents
```

## Set B

Students will use:

``` text
VS Code
   ↓
Design JSON / BSON examples
   ↓
MongoDB
   ↓
Embedding / Referencing
   ↓
Compass / mongosh
   ↓
Verify output
```

## Set C

Students will use:

``` text
VS Code
   ↓
Design MongoDB data model
   ↓
Create collections
   ↓
Insert documents
   ↓
Query documents
   ↓
Verify output in Compass
```

------------------------------------------------------------------------

# 16. Concepts Students Should Know Before Starting

Before performing Set A, students should understand these basic terms:

  -----------------------------------------------------------------------
  Term                                Meaning
  ----------------------------------- -----------------------------------
  Database                            Container for collections

  Collection                          Group of MongoDB documents

  Document                            MongoDB record represented as a
                                      BSON document

  Field                               Key-value pair inside a document

  JSON                                Text-based data interchange format

  BSON                                Binary-encoded JSON-like document
                                      format used by MongoDB

  Structured Data                     Data organized according to a fixed
                                      schema

  Semi-Structured Data                Data with flexible structure and
                                      metadata/tags

  Embedding                           Storing related data inside the
                                      same document

  Referencing                         Connecting documents using
                                      references/IDs
  -----------------------------------------------------------------------

The practical should be performed in this order:

``` text
Structured Data
      ↓
Semi-Structured Data
      ↓
JSON
      ↓
BSON
      ↓
MongoDB
      ↓
Database
      ↓
Collection
      ↓
Document
      ↓
Embedding / Referencing
      ↓
Set A
      ↓
Set B
      ↓
Set C
```

------------------------------------------------------------------------

# 17. Important: Do Not Install Unnecessary Software

For this assignment, students **do not need**:

``` text
❌ Neo4j Desktop
❌ Neo4j Browser
❌ MongoDB Atlas
❌ Docker
❌ Kubernetes
❌ Node.js
❌ Java
❌ MySQL
❌ Oracle Database
```

These may be used in other database/technology practicals, but they are
not necessary for Assignment 1 Set A, Set B and Set C.

------------------------------------------------------------------------

# 18. Troubleshooting

## Problem 1 --- `mongosh: command not found`

Check:

``` bash
mongosh --version
```

If it is not available, verify the MongoDB installation:

``` bash
dpkg -l | grep mongodb
```

Then:

``` bash
sudo apt update
sudo apt install -y mongodb-org
```

------------------------------------------------------------------------

## Problem 2 --- MongoDB service is not running

Check:

``` bash
sudo systemctl status mongod
```

Try:

``` bash
sudo systemctl start mongod
```

Then:

``` bash
sudo systemctl status mongod
```

If it still fails, inspect the log:

``` bash
sudo tail -50 /var/log/mongodb/mongod.log
```

------------------------------------------------------------------------

## Problem 3 --- `mongosh` cannot connect

First check:

``` bash
sudo systemctl status mongod
```

Then try:

``` bash
mongosh
```

The default local connection is:

``` text
mongodb://127.0.0.1:27017
```

------------------------------------------------------------------------

## Problem 4 --- Compass cannot connect

Check that MongoDB is running:

``` bash
sudo systemctl status mongod
```

In Compass use:

``` text
mongodb://localhost:27017
```

Do not use a cloud connection string for this practical.

------------------------------------------------------------------------

## Problem 5 --- VS Code command not found

Try opening VS Code from the Ubuntu application menu.

If VS Code was installed from the `.deb` package, restart the terminal
and test:

``` bash
code --version
```

------------------------------------------------------------------------

# 19. Completion Checklist

Students should tick every item before starting the practical:

-   [ ] Ubuntu 22.04 LTS verified
-   [ ] 64-bit architecture verified
-   [ ] Ubuntu updated
-   [ ] MongoDB Community Edition installed
-   [ ] MongoDB service started
-   [ ] MongoDB enabled at startup
-   [ ] `mongod --version` works
-   [ ] `mongosh --version` works
-   [ ] `mongosh` connects successfully
-   [ ] `TYCSE_DB` created
-   [ ] Test collection created
-   [ ] Test document inserted
-   [ ] `find()` displays the document
-   [ ] MongoDB Compass installed
-   [ ] Compass connects to `localhost:27017`
-   [ ] Test document visible in Compass
-   [ ] VS Code installed
-   [ ] Assignment workspace created
-   [ ] Optional Git installed if using GitHub

------------------------------------------------------------------------

# 20. Ready to Start Assignment 1

Once the checklist is complete, students are ready to perform:

``` text
Assignment 1
│
├── Set A
│   └── JSON design and representation exercises
│
├── Set B
│   └── JSON, BSON, referencing, embedding and data-model exercises
│
└── Set C
    └── MongoDB data-model and case-study exercises
```

The setup is complete when the following statement is true:

> **MongoDB is running, `mongosh` can connect to it, Compass can connect
> to `localhost:27017`, and VS Code is ready for creating JSON and
> practical files.**

------------------------------------------------------------------------

# Official References

-   MongoDB Community Edition --- Ubuntu installation:
    https://www.mongodb.com/docs/v8.0/tutorial/install-mongodb-on-ubuntu/

-   MongoDB Compass --- installation:
    https://www.mongodb.com/docs/compass/install/

-   Visual Studio Code --- Linux installation:
    https://code.visualstudio.com/docs/setup/linux

-   MongoDB Community Edition:
    https://www.mongodb.com/products/self-managed/community-edition

-   MongoDB GitHub: https://github.com/mongodb/mongo

-   MongoDB Compass GitHub: https://github.com/mongodb-js/compass

-   MongoDB Shell GitHub: https://github.com/mongodb-js/mongosh
