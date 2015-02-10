# RESPONSE
* Shows the JSON representation of the result of a GeneticSharingApi request response



#### Metadata 
* Describes the meta data of the response like total hits and paging information
* `href`: `<STIRNG>`; an URL specifying where the contents can be found of the result
* `start`: `<NUMBER>`; index of first hit returned
* `num`: `<NUMBER>`; current number of hit 
* `total`: `<NUMBER>`; total number of hits returned
* `prevHref`: `<STRING>`; an URL specifying where the contents can be found of the previous result
* `nextHref`: `<STRING>`; an URL specifying where the contents can be found of the next result

#### Results
* Is a list containing elements of result objects described below
* `resultType`: `<STRING>`; specifies the type of the query performed values accepted are: `"coordinate"`|`"allele"`
* `referenceAllele`: `<LIST>`; this List represents the allele labels on the X axis
* `alternativeAllele`: `<LIST>`; this List represents the allele labels section on the Y axis
* `chromosome`: `<STRING>`; identifier specifying the chromosome number according to the reference
* `position`: `<NUMBER>`; nucelotide base position on the chromosome 0 based
* `reference`: `<STRING>`; name of the reference genome that was used to map the chromosome and position
* `results`: `<LIST>`; list containing teh values to fill up a matrix design which is labeled by the alternativeAllele and the alternativeAllele fields for example: 



alleles  | C  |  G  | null 
 ------|----|-----|------
   C   | 27 | 124 |   0  
  G   |  0 | 190 |   0  
  null |  0 |  0  |   0  



```json
    {
       "metadata":
       {
           "href": "not supported",
           "start": 0,
           "num": 0,
           "total": 1,
           "prevHref": "not supported yet",
           "nextHref": "not supported"
       },
       "results":
       [
           {
               "resultType": "coordinate",
               "referenceAllele":
               [
                   "C",
                   "G",
                   null
               ],
               "alternativeAllele":
               [
                   "C",
                   "G",
                   null
               ],
               "chromosome": "10",
               "position": 75871735,
               "reference": "GRCh37",
               "result":
               [
                   [
                       27,
                       124,
                       0
                   ],
                   [
                       0,
                       190,
                       0
                   ],
                   [
                       0,
                       0,
                       0
                   ]
               ]
           }
       ]
    }

```
