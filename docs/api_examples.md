# Notes on other taxonomy APIs

## Links to external taxonomy APIs
* [GBIF](https://www.gbif.org/developer/species) : multiple hierarchies
* [Catalogue of Life](http://www.catalogueoflife.org/content/web-services)
* Global Names [resolver](http://resolver.globalnames.org/api) and [index](https://github.com/dimus/gni/wiki/api)
* [Open Tree of Life](https://github.com/OpenTreeOfLife/germinator/wiki/Open-Tree-of-Life-Web-APIs) : [Karen](https://github.com/kcranston) helped design
* the [taxize](https://www.r-project.org/nosvn/pandoc/taxize.html) R package wraps these and other taxonomy APIs; see their list for many more links

## GBIF

Separates methods into: 1) returning information about name usages; 2) searching names; and 3) parsing names. Name usage methods take a taxon ID, which you can obtain using the search methods if you have a taxon string. Key methods:

**Information about name usages**

* `/species` : list usage across checklists
* `/species/{int}` : get single name usage
* `/species/{int}/{detail}` : get detail (parents, children, vernacular names, media, etc) about a name usage

**Searching names**

* `/species` : list exact match on canonical name, i.e. without authorship
* `/species/match` : fuzzy matching (only parameters are ranks)
* `/species/search` : full text search based on variety of parameters
* `/species/suggest` : autocomplete based on prefix matching

## Open Tree of Life

Separates methods into 1) taxonomic name resolution ; and 2) information about taxa and taxon relationships. The `taxonomy` methods take a taxon ID, which you can get from a name using the `tnrs` methods. Key methods:

* `/taxonomy/taxon_info` : get information about a specific taxon based on ID; optionally returns information about children and / or lineage
* `/taxonomy/subtree` : return the subtree descended from a particular taxon ID; limits number of levels returned
* `/taxonomy/mrca` : return the most recent common ancestor of two or more taxa
* `/tnrs/match_names` :
* `/tnrs/autocomplete_name` :

## Catalogue of Life

(_API to be replaced by Catalogue of Life Plus at some point in the future_). Entire API in one method, `webservice` controlled with parameters:

* `/webservice?name=` : search; exact unless wildcard in value
* `/webservice?id=` : get record with specific ID

Allows user to specify format (terse / full) to control amount of info returned, and each format has different limits on number of results.
