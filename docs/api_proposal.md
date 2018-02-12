# Taxonomy API proposal

DINA taxonomy API methods. Expanded from [Taxonomy API discussion](https://docs.google.com/spreadsheets/d/1uaJh1qt6mvY0ZCEB6uBKdnUnyGdpQnZcnFqTMHTS5pA/edit#gid=0) google doc.

One goal is to harmonize with existing taxonomy APIs, which benefits downstream users. Makes it more likely that our services can be incorporated into integration projects such as [taxize](https://cran.r-project.org/web/packages/taxize/index.html) R package. 

See [DINA glossary](https://github.com/DINA-Web/dina-use-cases/blob/master/glossary.md) for terms. 

## Assumptions

* there will be some canonical root URL, format to be determined
* taxonomic names are not guaranteed to be unique, therefore cannot safely perform CRUD options based on name strings without disambiguation 
* the API will be versioned, and older versions may be deprecated in the future

## Methods

* /taxon : return info about a taxon
* /search : return potentially matching taxa
* /mrca : return the most recent common ancestor of two or more taxa
* /about : return information about the taxonomy
* /rank : return the rank of a taxon
* /subtree : return the subtree descended from a taxon

## Questions for discussion

* how much taxonomy editing functionality will we provide through the API?
** delete a taxon (re-assigning children to parent?)
** move a taxon (and children)
** merge taxa
** rename taxon
** split taxon

* limits / pagination
** on methods like subtree, limit levels / number of children returned
** lineage / children

* IDs vs names
** REST APIs generally operate on a resource (a unique thing)
** one workflow is that the user provides a name, we give back a list of potentially matching names. Each returned name has some metadata (enough for a user to decide which one they want) and an identifier. Using the identifier, they can access operations on that taxon. 
** can assign IDs based on some concept of what the ID refers to
** can force unique versions of names (i.e. by using author, year, parent taxon, etc). 

* Will a single DINA system store more than one taxonomy?

** if more than one, how does a API user disambiguate?
** how does this affect search?

* How do we handle IDs for taxa?

** what entity does an ID apply to?
** do IDs change? if so, how? 
** which methods only take IDs vs names?

* What is the minimum metadata required to create a new taxon?