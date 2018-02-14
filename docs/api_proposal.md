# Taxonomy API proposal

Design document for DINA taxonomy API methods. Expanded from [Taxonomy API discussion](https://docs.google.com/spreadsheets/d/1uaJh1qt6mvY0ZCEB6uBKdnUnyGdpQnZcnFqTMHTS5pA/edit#gid=0) google doc.

In this doc:
* [Assumptions](#assumptions)
* [Methods](#methods)
* [Questions](#questions)

See [DINA glossary](https://github.com/DINA-Web/dina-use-cases/blob/master/glossary.md) for terms.

See [API example doc](https://github.com/DINA-Web/taxonomy/blob/master/docs/api_examples.md) for notes on non-DINA taxonomy APIs

## Assumptions

* taxonomy = hierarchy = classification = checklist
* there will be some canonical root URL for the API, format to be determined
* the API will be versioned, and we may deprecate older versions in the future
* exact format / fields of result TBD; examples below are just for discussion about general form of result for each method
* taxonomic names are not guaranteed to be unique
  * therefore, cannot safely perform CRUD options based on name strings without disambiguation
* one goal is to harmonize with existing taxonomy APIs (improved interoperability with other services and future modules)

## Methods

At a high level, we need methods to
1. Search for taxa based on name strings (taxonomic name resolution)
1. Search taxa based on some parameter
1. Get a specific  taxon
1. Return information about the taxonomic hierarchy / relationships between taxa.

Here is a proposed list of key methods:

### /tnrs
Method for taxonomic name reconciliation; returns potentially matching taxa (exact or fuzzy matching; uses information about synonyms)

`/tnrs?name="Genus speices"`

returns:
```
{
  "numberMatches" : 3,
  "bestMatch" : {
    "id" : 3,
    "canonicalName" : "Genus species",
    "matchScore" : 0.8
    },
  "alternateMatches" : [
    { _info about next match here_ },
    { _info about next match here_ }
  ]
}
```

### /autocomplete
Return a list of potentially matching taxa based on given prefix; for UI search boxes

`/autocomplete?prefix="Gen"`

Return format same as [tnrs](#tnrs).

### /search
Search taxa based on a variety of parameters (rank, author, year, etc)  

`/search?author="Linnaeus"&rank="order"`

Return format same as [tnrs](#tnrs).

### /taxon
Return a specific taxon resource; takes ID as parameter

  `/taxon/{id}`

returns:
```
{
  "id" : id,
  "canonicalName" : "Genus species",
  "scientificName" : "Genus species (author, year)",
  "synonyms" : ["synonym1", "synonymn2"],
  "rank" : "genus"
}
```

### /about
Return information about a taxonomic hierarchy.

```
{
  "taxonomyId" : id,
  "lastEdited" : "2018-12-14",
  "numberTaxa" : 96323,
  "rootTaxonId" : 2,
  "rootTaxonName" : "Life"
}
```

### /mrca

Return the most recent common ancestor of two or more taxa

  `/mrca?taxa=["Genus sp1", "Genus sp2"]`

returns:
```
{
  "mrca" : {
    "id" : id,
    "canonicalName" : "Genus species",
    "scientificName" : "Genus species (author, year)",
    "synonyms" : ["synonym1", "synonymn2"],
    "rank" : "genus"
  }
}
```

### /subtree
Return the subtree descended from a taxon

`/subtree?taxon=id`

Returns json with subtree, limited and / or paginated if large number of levels / children.

## Questions

* Will a single DINA system store more than one taxonomy?
  * if more than one, how does a API user disambiguate?
  * disambiguation required for all methods?
* What is the minimum metadata required to create a new taxon?
* IDs vs names
  * REST APIs generally operate on a resource (a unique thing) and names are not unique (see Assumptions)
  * one workflow: user provides a name, we give back a list of potentially matching names. Each returned name has some metadata (enough for a user to decide which one they want) and an identifier. Using the identifier, they can access operations on that taxon.
  * which methods only take IDs vs names?
* assigning IDs to taxa
  * what entity does an ID apply to?
  * assign IDs based on some concept of what the ID refers to
  * do IDs change? get deleted / deprecated? if so, how do we manage this?
* how much taxonomy editing functionality will we provide through the API?
  * delete a taxon (re-assigning children to parent?)
  * move a taxon (and children)
  * merge taxa
  * rename taxon
  * split taxon
* limits / pagination
  * on methods like subtree, limit levels
  * lists for lineage / children can be very long
