Taxonomy Concepts

![diagram](taxonomy_concept_diagram.png "Taxonomy Concepts")

Based on work done by the [Catalogue of Life Plus (CoL+)]( https://github.com/Sp2000/colplus) project.

## How to store
This section is "work-in-progress"
 * Homotypic synonyms ([definition](https://github.com/DINA-Web/dina-use-cases/blob/master/glossary.md#homotypic-synonym))
   * The originally published name is stored in the `name` table
   * All homotypic synonyms point to the originally published name using `origin_name_id`
   * The status of each homotypic synonyms is set accordingly (e.g. Orthographic variant)
   
 * Heterotypic synonyms ([definition](https://github.com/DINA-Web/dina-use-cases/blob/master/glossary.md#heterotypic-synonym))
   * The taxon points to the "accepted" name
   * All heterotypic synonyms are recorded in the `synonym` table
   * New combination
     * `origin` is set "basionym" ?
   * New split
     * Lets A[id=1] be the originally published name that is now splitted into A[id=2] and B[id=3]
     * A[id=1] remains in the `name` table
     * The new names, A[id=2] and B[id=3], are added to the `name` table and their `origin` is set "pro parte" 
     * The `basionym_name_id` is set on A[id=2]
     * 2 taxa pointing to A[id=2] and B[id=3] are created in the `taxon` table
     * 2 synonyms are created in the `synonym` table where the 2 previously created taxa point to the previous name A[id=1]
  
