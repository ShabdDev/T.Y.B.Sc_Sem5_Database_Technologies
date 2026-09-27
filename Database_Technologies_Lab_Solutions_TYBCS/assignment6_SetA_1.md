# Assignment 6 — Set A
## Student–Course Relationship Analysis using Cypher

## Problem
Create `Student` and `Course` nodes and connect them using `ENROLLED_IN`.

## 1. Create Student nodes

```cypher
CREATE
  (:Student {StudentID:"S101",Name:"Amit",City:"Pune"}),
  (:Student {StudentID:"S102",Name:"Priya",City:"Mumbai"}),
  (:Student {StudentID:"S103",Name:"Rahul",City:"Pune"}),
  (:Student {StudentID:"S104",Name:"Sneha",City:"Nashik"}),
  (:Student {StudentID:"S105",Name:"Neha",City:"Pune"});
```

## 2. Create Course nodes

```cypher
CREATE
  (:Course {CourseID:"C101",CourseName:"Database Technologies"}),
  (:Course {CourseID:"C102",CourseName:"Cloud Computing"}),
  (:Course {CourseID:"C103",CourseName:"Data Structures"});
```

## 3. Create enrollment relationships

```cypher
MATCH
  (s1:Student {StudentID:"S101"}),
  (s2:Student {StudentID:"S102"}),
  (s3:Student {StudentID:"S103"}),
  (s4:Student {StudentID:"S104"}),
  (s5:Student {StudentID:"S105"}),
  (c1:Course {CourseID:"C101"}),
  (c2:Course {CourseID:"C102"}),
  (c3:Course {CourseID:"C103"})
CREATE
  (s1)-[:ENROLLED_IN]->(c1),
  (s1)-[:ENROLLED_IN]->(c2),
  (s2)-[:ENROLLED_IN]->(c1),
  (s3)-[:ENROLLED_IN]->(c1),
  (s3)-[:ENROLLED_IN]->(c3),
  (s4)-[:ENROLLED_IN]->(c2),
  (s5)-[:ENROLLED_IN]->(c1),
  (s5)-[:ENROLLED_IN]->(c3);
```

## Q4. Display all Student nodes

```cypher
MATCH (s:Student)
RETURN s;
```

## Q5. Display all Course nodes

```cypher
MATCH (c:Course)
RETURN c;
```

## Q6. Students enrolled in a particular course

```cypher
MATCH (s:Student)-[:ENROLLED_IN]->(c:Course {CourseName:"Database Technologies"})
RETURN s.Name AS Student;
```

## Q7. Courses taken by a specific student

```cypher
MATCH (s:Student {Name:"Amit"})-[:ENROLLED_IN]->(c:Course)
RETURN c.CourseName AS Course;
```

## Q8. Number of students in each course

```cypher
MATCH (s:Student)-[:ENROLLED_IN]->(c:Course)
RETURN c.CourseName AS Course, count(s) AS StudentCount
ORDER BY StudentCount DESC;
```

## Q9. Students from a particular city

```cypher
MATCH (s:Student {City:"Pune"})
RETURN s;
```

## Q10. Complete graph structure

```cypher
MATCH (s:Student)-[r:ENROLLED_IN]->(c:Course)
RETURN s,r,c;
```

## Result
Student and Course nodes were created, connected through enrollment relationships, and analyzed using pattern matching and aggregation.
