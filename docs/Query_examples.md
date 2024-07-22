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


### Database and accession/xref queries on the API.

```
vc.neo_query_wrapper.get_dbs()

Out[26]: 
['vnc1_catmaid_api',
 'vnc_harvard_catmaid_api',
 'flywire_supervoxel',
 'l1em_catmaid_api',
 'fafb_catmaid_api',
 'jrc_slide_code_api',
 'InsectBrainDB',
 'FlyBrain_NDB',
 'catmaid_fafb',
 ...
```

These are a mix of official source DBs & sites that serve data.  We should try to tage source DBs and harmonise the naming.


## Simple ID lookup

## API queries

vc.id_lookup takes offical names (labels) and symbols.  It doesn't take synonyms.

vc.lookup_id('MBON')
Out[28]: 'FBbt_00047953'






