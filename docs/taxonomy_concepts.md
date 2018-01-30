Taxonomy Concepts

![diagram](taxonomy_concept_diagram.png "Taxonomy Concepts")

Based on work done by the [Catalogue of Life Plus (CoL+)]( https://github.com/Sp2000/colplus) project.

## How to store
This section is "work-in-progress"
 * Homotypic synonyms
   * The originally published name is stored in the `name` table
   * All homotypic synonyms point to the originally published name using `origin_name_id`
   * The status of each homotypic synonyms is set accordingly (e.g. Orthographic variant)
   
 * Heterotypic synonyms
   * The taxon points to the "accepted" name
   * All heterotypic synonyms are recorded in the `synonym` table
   * If the synonym refers to a new combination then `origin` is set "basionym" ?
   * If the synonym refers to a new split then `origin` is set "pro parte" ?
  
