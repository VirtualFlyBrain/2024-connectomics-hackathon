## Cypher queries

### Databases, Sites, APIs and accessions


```cypher
MATCH p=(ds:DataSet)<-[]-(i:Individual { short_form: "VFB_jrchjte4"})-[r]-(s:Site) 
return r.accession, s.label, ds.label, ds.short_form
```

(use return p to see full paths)

Sites are external sites that we link to.  The edge has the ID of the entity in the external site as the value of accession[0]
Datasets are collections of data linking to single publications. Sometimes these are refs for full connectomes, often not.

<img width="436" alt="image" src="https://github.com/user-attachments/assets/21838814-b1f3-4b48-a655-1d7ddd272148">
