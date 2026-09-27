# Assignment 6 — Set B
## Social Network Analysis using Cypher

## 1. Create Person nodes

```cypher
CREATE
  (:Person {PersonID:"P101",Name:"John",City:"Pune"}),
  (:Person {PersonID:"P102",Name:"Priya",City:"Mumbai"}),
  (:Person {PersonID:"P103",Name:"Amit",City:"Pune"}),
  (:Person {PersonID:"P104",Name:"Riya",City:"Nashik"}),
  (:Person {PersonID:"P105",Name:"Rahul",City:"Delhi"}),
  (:Person {PersonID:"P106",Name:"Neha",City:"Pune"});
```

## 2. Create FRIEND relationships

```cypher
MATCH
  (p1:Person {Name:"John"}),
  (p2:Person {Name:"Priya"}),
  (p3:Person {Name:"Amit"}),
  (p4:Person {Name:"Riya"}),
  (p5:Person {Name:"Rahul"}),
  (p6:Person {Name:"Neha"})
CREATE
  (p1)-[:FRIEND]->(p2),
  (p1)-[:FRIEND]->(p3),
  (p2)-[:FRIEND]->(p3),
  (p2)-[:FRIEND]->(p4),
  (p3)-[:FRIEND]->(p5),
  (p3)-[:FRIEND]->(p6),
  (p4)-[:FRIEND]->(p5);
```

## Q3. Display all persons

```cypher
MATCH (p:Person)
RETURN p;
```

## Q4. Direct friends of a person

```cypher
MATCH (p:Person {Name:"John"})-[:FRIEND]->(f:Person)
RETURN f.Name AS Friend;
```

## Q5. Mutual friends between two persons

Example: John and Priya:

```cypher
MATCH
  (a:Person {Name:"John"})-[:FRIEND]->(m:Person),
  (b:Person {Name:"Priya"})-[:FRIEND]->(m)
RETURN m.Name AS MutualFriend;
```

## Q6. Friends of friends

```cypher
MATCH (p:Person {Name:"John"})-[:FRIEND*2]->(fof:Person)
RETURN DISTINCT fof.Name AS FriendOfFriend;
```

## Q7. Count friends for each person

```cypher
MATCH (p:Person)-[:FRIEND]->(f:Person)
RETURN p.Name AS Person, count(f) AS FriendCount
ORDER BY FriendCount DESC;
```

## Q8. Persons from a city

```cypher
MATCH (p:Person {City:"Pune"})
RETURN p;
```

## Q9. Shortest connection path

```cypher
MATCH p=shortestPath(
  (a:Person {Name:"John"})-[:FRIEND*]-(b:Person {Name:"Rahul"})
)
RETURN p;
```

## Q10. Complete social network

```cypher
MATCH (p1:Person)-[r:FRIEND]->(p2:Person)
RETURN p1,r,p2;
```

## Result
The social network was created and analyzed using direct relationships, mutual-friend queries, variable-length traversal, counts, and shortest-path analysis.
