# Assignment 5 — Set B
## Movie Database Modeling in Neo4j

## Graph model

Labels:
`Actor`, `Movie`, `Role`, `Financier`, `Producer`, `Director`

Relationships:
- `Actor -[:ACTS_IN]-> Movie`
- `Actor -[:PLAYS]-> Role`
- `Director -[:DIRECTS]-> Movie`
- `Producer -[:PRODUCES]-> Movie`
- `Financier -[:FINANCES]-> Movie`

## Create sample graph

```cypher
CREATE
  (a1:Actor {name:"Amit"}),
  (a2:Actor {name:"Priya"}),
  (a3:Actor {name:"Rahul"}),
  (m1:Movie {title:"Tech Dreams",year:2025}),
  (m2:Movie {title:"City Lights",year:2024}),
  (r1:Role {name:"Engineer"}),
  (r2:Role {name:"Doctor"}),
  (d1:Director {name:"Meera"}),
  (d2:Director {name:"Arun"}),
  (p1:Producer {name:"FilmWorks"}),
  (p2:Producer {name:"Star Studios"}),
  (f1:Financier {name:"FinanceCorp"})

CREATE
  (a1)-[:ACTS_IN]->(m1),
  (a2)-[:ACTS_IN]->(m1),
  (a2)-[:ACTS_IN]->(m2),
  (a3)-[:ACTS_IN]->(m2),
  (a1)-[:PLAYS]->(r1),
  (a2)-[:PLAYS]->(r2),
  (d1)-[:DIRECTS]->(m1),
  (d2)-[:DIRECTS]->(m2),
  (p1)-[:PRODUCES]->(m1),
  (p2)-[:PRODUCES]->(m2),
  (f1)-[:FINANCES]->(m1),
  (f1)-[:FINANCES]->(m2)
```

## Q1. List all movies

```cypher
MATCH (m:Movie)
RETURN m;
```

## Q2. List all actors

```cypher
MATCH (a:Actor)
RETURN a;
```

## Q3. Movies acted in by an actor

```cypher
MATCH (a:Actor {name:"Amit"})-[:ACTS_IN]->(m:Movie)
RETURN m.title AS Movie;
```

## Q4. Movies directed by a director

```cypher
MATCH (d:Director {name:"Meera"})-[:DIRECTS]->(m:Movie)
RETURN m.title AS Movie;
```

## Q5. Producers of a movie

```cypher
MATCH (p:Producer)-[:PRODUCES]->(m:Movie {title:"Tech Dreams"})
RETURN p.name AS Producer;
```

## Q6. Actors, movies and directors

```cypher
MATCH (a:Actor)-[:ACTS_IN]->(m:Movie)<-[:DIRECTS]-(d:Director)
RETURN a.name AS Actor, m.title AS Movie, d.name AS Director;
```

## Q7. Actors in a specified movie

```cypher
MATCH (a:Actor)-[:ACTS_IN]->(m:Movie {title:"Tech Dreams"})
RETURN a.name AS Actor;
```

## Q8. Movies produced by a producer

```cypher
MATCH (p:Producer {name:"FilmWorks"})-[:PRODUCES]->(m:Movie)
RETURN m.title AS Movie;
```

## Q9. Complete movie information

```cypher
MATCH (m:Movie)
OPTIONAL MATCH (a:Actor)-[:ACTS_IN]->(m)
OPTIONAL MATCH (d:Director)-[:DIRECTS]->(m)
OPTIONAL MATCH (p:Producer)-[:PRODUCES]->(m)
OPTIONAL MATCH (f:Financier)-[:FINANCES]->(m)
RETURN
  m.title AS Movie,
  m.year AS Year,
  collect(DISTINCT a.name) AS Actors,
  collect(DISTINCT d.name) AS Directors,
  collect(DISTINCT p.name) AS Producers,
  collect(DISTINCT f.name) AS Financiers;
```

## Result
The Movie graph and all nine requested Cypher queries were implemented.
