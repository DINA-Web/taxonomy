# Notes on other taxonomy APIs

## Links to external taxonomy APIs
* [GBIF](https://www.gbif.org/developer/species) : multiple hierarchies
* [Catalogue of Life](http://www.catalogueoflife.org/content/web-services)
* Global Names [resolver](http://resolver.globalnames.org/api) and [index](https://github.com/dimus/gni/wiki/api)
* [Canadensys](http://data.canadensys.net/vascan/api) (vascan) : [Christian](https://github.com/cgendreau) helped design
* [Open Tree of Life](https://github.com/OpenTreeOfLife/germinator/wiki/Open-Tree-of-Life-Web-APIs) : [Karen](https://github.com/kcranston) helped design
* [Encyclopedia of Life](http://www.eol.org/api/) : multiple hierarchies
* the [taxize](https://www.r-project.org/nosvn/pandoc/taxize.html) R package wraps these and other taxonomy APIs; see their list for many more links

## GBIF

Separates methods into: 1) returning information about name usages; 2) searching names; and 3) parsing names. Key methods:

**Information about name usages**

* `\species` : list usage across checklists
* `\species\{int}` : get single name usage
* `\species\{int}\{detail}` : get detail (parents, children, vernacular names, media, etc) about a name usage

**Searching names**

* `\species` : exact match on canonical name, i.e. without authorship
* `\species\match` : fuzzy matching (only parameters are ranks)
* `\species\search` : full text search based on variety of parameters
* `\species\suggest` : autocomplete based on prefix matching
