# Assignment 5 — Set C
## Social Network Graph in Neo4j

## Graph model

Labels:
- `Person`
- `Affiliation`
- `Group`
- `Story`
- `Timeline`
- `Message`

Relationships:
- `Person -[:FRIEND_OF]-> Person`
- `Person -[:AFFILIATED_TO]-> Affiliation`
- `Person -[:BELONGS_TO]-> Group`
- `Person -[:CREATES]-> Story`
- `Story -[:REFERS_TO]-> Person`
- `Person -[:CREATES]-> Timeline`
- `Timeline -[:CONTAINS]-> Message`
- `Timeline -[:REFERENCES]-> Story`

## Create sample graph

```cypher
CREATE
  (j:Person {name:"John",city:"Pune"}),
  (p:Person {name:"Priya",city:"Mumbai"}),
  (a:Person {name:"Amit",city:"Pune"}),
  (r:Person {name:"Riya",city:"Nashik"}),
  (tech:Affiliation {name:"Tech Club"}),
  (cs:Group {name:"CS Students"}),
  (s:Story {title:"My Neo4j Lab"}),
  (t:Timeline {name:"John Timeline"}),
  (m:Message {text:"Welcome to my timeline"})

CREATE
  (j)-[:FRIEND_OF {since:2020}]->(p),
  (j)-[:FRIEND_OF {since:2021}]->(a),
  (p)-[:FRIEND_OF {since:2022}]->(r),
  (j)-[:AFFILIATED_TO]->(tech),
  (j)-[:BELONGS_TO]->(cs),
  (j)-[:CREATES]->(s),
  (s)-[:REFERS_TO]->(p),
  (j)-[:CREATES]->(t),
  (t)-[:CONTAINS]->(m),
  (t)-[:REFERENCES]->(s)
```

## Q1. List all persons

```cypher
MATCH (p:Person)
RETURN p;
```

## Q2. List friends of a person

```cypher
MATCH (p:Person {name:"John"})-[:FRIEND_OF]->(f:Person)
RETURN f.name AS Friend;
```

## Q3. List affiliations of a person

```cypher
MATCH (p:Person {name:"John"})-[:AFFILIATED_TO]->(a:Affiliation)
RETURN a.name AS Affiliation;
```

## Q4. Friends of John with year since John knows them

```cypher
MATCH (j:Person {name:"John"})-[r:FRIEND_OF]->(f:Person)
RETURN f.name AS Friend, r.since AS SinceYear;
```

## Q5. Affiliations of John

```cypher
MATCH (j:Person {name:"John"})-[:AFFILIATED_TO]->(a:Affiliation)
RETURN a.name;
```

## Q6. Display complete social network graph

```cypher
MATCH (n)-[r]->(m)
RETURN n,r,m;
```

## Q7. Display all Friend relationships

```cypher
MATCH (p1:Person)-[r:FRIEND_OF]->(p2:Person)
RETURN p1.name AS Person1, r.since AS Since, p2.name AS Person2;
```

## Result
The social-network graph was modeled and the requested person, friend, affiliation, timeline, and relationship queries were implemented.
