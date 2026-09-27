# Assignment 5 — Set A
## Song Database Modeling in Neo4j and Cypher

## Graph model

Labels:
- `Artist`
- `Song`
- `RecordingCompany`
- `RecordingStudio`
- `SongAuthor`

Relationships:
- `Artist -> PERFORMS -> Song`
- `Song -> WRITTEN_BY -> SongAuthor`
- `Song -> RECORDED_IN -> RecordingStudio`
- `RecordingStudio -> MANAGED_BY -> RecordingCompany`
- `RecordingCompany -> FINANCES -> Song`

## 1. Create sample graph

```cypher
CREATE
  (a1:Artist {name:"Arjun"}),
  (a2:Artist {name:"Priya"}),
  (s1:Song {title:"Believer",year:2017}),
  (s2:Song {title:"Imagine",year:1971}),
  (s3:Song {title:"Perfect",year:2017}),
  (w1:SongAuthor {name:"Author One"}),
  (w2:SongAuthor {name:"Author Two"}),
  (st1:RecordingStudio {name:"Studio A"}),
  (st2:RecordingStudio {name:"Studio B"}),
  (c1:RecordingCompany {name:"MusicCorp"}),
  (c2:RecordingCompany {name:"SoundWorks"})

CREATE
  (a1)-[:PERFORMS]->(s1),
  (a1)-[:PERFORMS]->(s3),
  (a2)-[:PERFORMS]->(s2),
  (s1)-[:WRITTEN_BY]->(w1),
  (s2)-[:WRITTEN_BY]->(w2),
  (s3)-[:WRITTEN_BY]->(w1),
  (s1)-[:RECORDED_IN]->(st1),
  (s2)-[:RECORDED_IN]->(st2),
  (s3)-[:RECORDED_IN]->(st1),
  (st1)-[:MANAGED_BY]->(c1),
  (st2)-[:MANAGED_BY]->(c2),
  (c1)-[:FINANCES]->(s1),
  (c2)-[:FINANCES]->(s2)
```

## Q1. Display all Artists

```cypher
MATCH (a:Artist)
RETURN a;
```

## Q2. Display all Songs

```cypher
MATCH (s:Song)
RETURN s;
```

## Q3. Display Artist and Songs they perform

```cypher
MATCH (a:Artist)-[:PERFORMS]->(s:Song)
RETURN a.name AS Artist, s.title AS Song;
```

## Q4. Songs written by a specified author

Example for `Author One`:

```cypher
MATCH (s:Song)-[:WRITTEN_BY]->(a:SongAuthor {name:"Author One"})
RETURN s.title AS Song;
```

## Q5. Record companies that financed a specified song

Example for `Believer`:

```cypher
MATCH (c:RecordingCompany)-[:FINANCES]->(s:Song {title:"Believer"})
RETURN c.name AS Company;
```

## Q6. Artists performing a specified song

```cypher
MATCH (a:Artist)-[:PERFORMS]->(s:Song {title:"Believer"})
RETURN a.name AS Artist;
```

## Q7. Songs recorded by a specified studio

```cypher
MATCH (s:Song)-[:RECORDED_IN]->(st:RecordingStudio {name:"Studio A"})
RETURN s.title AS Song;
```

## Q8. Display Song, Studio, and Company

```cypher
MATCH (s:Song)-[:RECORDED_IN]->(st:RecordingStudio)-[:MANAGED_BY]->(c:RecordingCompany)
RETURN s.title AS Song, st.name AS Studio, c.name AS Company;
```

## Q9. Complete Song Information

```cypher
MATCH (a:Artist)-[:PERFORMS]->(s:Song)-[:RECORDED_IN]->(st:RecordingStudio)-[:MANAGED_BY]->(c:RecordingCompany)
OPTIONAL MATCH (s)-[:WRITTEN_BY]->(w:SongAuthor)
RETURN
  s.title AS Song,
  s.year AS Year,
  collect(DISTINCT a.name) AS Artists,
  collect(DISTINCT w.name) AS Authors,
  st.name AS Studio,
  c.name AS Company;
```

## Result
The Song graph was modeled using nodes, relationships, labels, and properties, and the required Cypher retrieval queries were implemented.
