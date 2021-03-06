# Misused Obsolete Label

**Problem:** A non-deprecated class has the "obsolete" prefix. This may mean that a deprecated class is missing the `owl:deprecated` annotation, or that this prefix was added accidentally.

**Solution:** Remove the "obsolete" prefix or add the `owl:deprecated` annotation.

```sparql
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX oboInOwl: <http://www.geneontology.org/formats/oboInOwl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?entity ?property ?value WHERE {
  VALUES ?property { rdfs:label }
  ?entity ?property ?value .
  FILTER NOT EXISTS { ?entity owl:deprecated true }
  FILTER (?entity != oboInOwl:ObsoleteClass)
  FILTER regex(?value, "^obsolete", "i")
  FILTER (!isBlank(?entity))
}
ORDER BY ?entity
```
