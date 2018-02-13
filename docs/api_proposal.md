# Taxonomy API proposal

Design document for DINA taxonomy API methods. Expanded from [Taxonomy API discussion](https://docs.google.com/spreadsheets/d/1uaJh1qt6mvY0ZCEB6uBKdnUnyGdpQnZcnFqTMHTS5pA/edit#gid=0) google doc.

See [DINA glossary](https://github.com/DINA-Web/dina-use-cases/blob/master/glossary.md) for terms.

See [API example doc](https://github.com/DINA-Web/taxonomy/blob/master/docs/api_examples.md) for notes on non-DINA taxonomy APIs

## Assumptions

* taxonomy = hierarchy = classification
* there will be some canonical root URL for the API, format to be determined
* the API will be versioned, and we may deprecate older versions in the future
* taxonomic names are not guaranteed to be unique
  * therefore, cannot safely perform CRUD options based on name strings without disambiguation
* one goal is to harmonize with existing taxonomy APIs (improved interoperability with other services and future modules)

## Methods

* /taxon : return info about a taxon
* /search : return potentially matching taxa
* /mrca : return the most recent common ancestor of two or more taxa
* /about : return information about the taxonomy
* /rank : return the rank of a taxon
* /subtree : return the subtree descended from a taxon

## Questions for discussion

* Will a single DINA system store more than one taxonomy?
  * if more than one, how does a API user disambiguate?
  * disambiguation required for all methods vs some methods?
* What is the minimum metadata required to create a new taxon?
* IDs vs names
  * REST APIs generally operate on a resource (a unique thing) and names are not unique (see Assumptions)
  * one workflow: user provides a name, we give back a list of potentially matching names. Each returned name has some metadata (enough for a user to decide which one they want) and an identifier. Using the identifier, they can access operations on that taxon.
  * which methods only take IDs vs names?
* assigning IDs to taxa
  * what entity does an ID apply to?
  * assign IDs based on some concept of what the ID refers to
  * can force unique versions of names (i.e. by using author, year, parent taxon, etc).
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
