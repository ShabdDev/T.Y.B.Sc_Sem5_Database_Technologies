# Assignment 6 — Set C
## Employee–Project Management System using Cypher

## 1. Create Employee nodes

```cypher
CREATE
  (:Employee {EmpID:"E101",EmpName:"Amit",Department:"IT"}),
  (:Employee {EmpID:"E102",EmpName:"Priya",Department:"HR"}),
  (:Employee {EmpID:"E103",EmpName:"Rahul",Department:"IT"}),
  (:Employee {EmpID:"E104",EmpName:"Sneha",Department:"Finance"}),
  (:Employee {EmpID:"E105",EmpName:"Neha",Department:"IT"});
```

## 2. Create Project nodes

```cypher
CREATE
  (:Project {ProjectID:"P101",ProjectName:"Banking App",Technology:"Java"}),
  (:Project {ProjectID:"P102",ProjectName:"Cloud Migration",Technology:"AWS"}),
  (:Project {ProjectID:"P103",ProjectName:"Analytics Platform",Technology:"Python"}),
  (:Project {ProjectID:"P104",ProjectName:"DevOps Automation",Technology:"Docker"});
```

## 3. Create WORKS_ON relationships

```cypher
MATCH
  (e1:Employee {EmpID:"E101"}),
  (e2:Employee {EmpID:"E102"}),
  (e3:Employee {EmpID:"E103"}),
  (e4:Employee {EmpID:"E104"}),
  (e5:Employee {EmpID:"E105"}),
  (p1:Project {ProjectID:"P101"}),
  (p2:Project {ProjectID:"P102"}),
  (p3:Project {ProjectID:"P103"}),
  (p4:Project {ProjectID:"P104"})
CREATE
  (e1)-[:WORKS_ON]->(p1),
  (e1)-[:WORKS_ON]->(p4),
  (e2)-[:WORKS_ON]->(p2),
  (e3)-[:WORKS_ON]->(p1),
  (e3)-[:WORKS_ON]->(p3),
  (e4)-[:WORKS_ON]->(p3),
  (e5)-[:WORKS_ON]->(p2),
  (e5)-[:WORKS_ON]->(p4);
```

## Q4. Display all employees

```cypher
MATCH (e:Employee)
RETURN e;
```

## Q5. Display all projects

```cypher
MATCH (p:Project)
RETURN p;
```

## Q6. Employees working on a specific project

```cypher
MATCH (e:Employee)-[:WORKS_ON]->(p:Project {ProjectName:"Banking App"})
RETURN e.EmpName AS Employee;
```

## Q7. Projects assigned to a specific employee

```cypher
MATCH (e:Employee {EmpName:"Amit"})-[:WORKS_ON]->(p:Project)
RETURN p.ProjectName AS Project;
```

## Q8. Count employees working on each project

```cypher
MATCH (e:Employee)-[:WORKS_ON]->(p:Project)
RETURN p.ProjectName AS Project, count(e) AS EmployeeCount
ORDER BY EmployeeCount DESC;
```

## Q9. Projects using a specific technology

```cypher
MATCH (p:Project {Technology:"AWS"})
RETURN p;
```

## Q10. Complete Employee–Project graph

```cypher
MATCH (e:Employee)-[r:WORKS_ON]->(p:Project)
RETURN e,r,p;
```

## Result
The Employee–Project graph was modeled with `WORKS_ON` relationships and analyzed using Cypher pattern matching and aggregation.
