# Duplicate Definition

**Problem:** An entity shares an exact definition or elucidation with another entity. Excludes deprecated entities.

**OBO Foundry Principle:** [6 - Textual Definitions](http://obofoundry.org/principles/fp-006-textual-definitions.html)

**Solution:** Update the definition to reflect the entities, or determine if the entities are the same.

```sparql
PREFIX obo: <http://purl.obolibrary.org/obo/>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?entity ?property ?value WHERE {
  VALUES ?property { obo:IAO_0000115
                     obo:IAO_0000600 }
  ?entity ?property ?value .
  ?entity2 ?property ?value .
  FILTER NOT EXISTS { ?entity owl:deprecated true }
  FILTER NOT EXISTS { ?entity2 owl:deprecated true }
  FILTER (?entity != ?entity2)
  FILTER (!isBlank(?entity))
}
ORDER BY DESC(UCASE(str(?value)))
```
