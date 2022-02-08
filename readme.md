# Poems For France

[PoemsForFrancePrototype](0PoemsForFrancePrototype.xlsx) is the initial dataset in Excel format, with additional tabs for Gephi nodes and edges.

These tabs have been copied to the following csv files in order to more easily generate the Gephi graph:

#### Nodes
- letters
- person
- poems
- publications

#### Edges
- letter_mention_person
- letter_mention_poem
- letter_mention_publication
- person_author_poem

## Results

[The graph](all-plain-p4f.cypher) can be downloaded and dragged into a Neo4j Browser window to import the database

- **Persons** are orange
- **Poems** are red
- **Publications** are blue
- **Letters** are beige

### All Nodes and Edges
![all.png](all.png)

### Direct Connections to and From Cunard
```neo4j
MATCH p=(:Person {firstName:' Nancy'})-[]-() RETURN p
```

![](Nancy1.png)

### Cunard and nodes 2 steps away
Excludes letters sent or received directly by her. Cunard is the orange node in the top left, and Poems for France is the blue node in the middle, surrounded by red poems.

```neo4j
MATCH (p:Person {firstName:' Nancy'})-[]-()-[]-(n) RETURN p,n
```

![](Nancy2.png)


### Notes on querying
- **Person** nodes have property types `firstName` and `lastName`, but **Poem** has property types `authorFirstName` and `authorLastName` ( oversight when importing the data but doesn't cause any issues)
- `firstName` properties have a space at the beginning (ie `firstName: ' Nancy'` not `firstName: 'Nancy'`)

