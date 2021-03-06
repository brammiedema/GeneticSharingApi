# Request

**Submit patient variant request:**
`HTTP POST` to remote server: `<base_remote_url>api/v1/getAggregate`
For example: `http://molgenis.gcc.rug.nl/api/v1/getAggregate`


#### queryMetadata 
 ***Mandatory***
 Describes how the query should response and holds information of the submitter.
* `queryID`: `<STIRNG>`; unique within each institute; internal identifier to link the response to a query, in case of long calculation the submitter can be notified when it is done
* `label`: `<STRING>`; name/identifier assigned by the user which can be used to reference the query in a recognizable manner (in an email for example); it should not contain any *personally identifiable information*
* Transparent string, limited to 255 characters in utf-8
* `queryType`: `<STRING>`; 
* Accepted values:
  * `once`: only search once in the current database
  * `periodic`: repeat the search monthly until canceled, reporting new and updated matches
  * If not supported the behaviour of `once` will be used 
* `queryResultFormat`: `<STRING>`; Specifies the respone format

#### Submitter
 ***Mandatory*** if an email response is expected, *Optional* otherwise
 Consists of contact information of the person that submitted the search:
  * `id`: `<STRING>`; the identifier that is requested for accessing the data for user logging purposes (***mandatory***) 
  * `email`: `<STRING>`; the email address where matches can be sent (***mandatory***); the values must conform to the [RFC 2822 address specification](http://tools.ietf.org/html/rfc2822#section-3.4) mailbox format (no group)
  * `name`: `<STRING>`;  the first and last name (*optional*)
  * `institution`: `<STRING>`; human-readable institution name (*optional*)
* **The contact information is for transmitting match results only, and may not be collected and/or used for any other purposes**

#### Query
 ***Mandatory***
* Accepted values: `"allele"`|`"coordinate"`; allele and coodrinate should satisfy the object specification respectively


#### Allele
 ***Optional***
 Will specify a query that returns all variants within a region based on the reference postion specific for the alleles and query as present in the allele object list
* `id`: identifier for the allele query specified
* `operator`: `"IS"` | `"NOT"`; this is to specify to include this allele query or to exclude it from the results
* `source`: `"GRCBUILD"`|`"HGNC"`; specifies the source of the reference 
* `reference`: if `"GRCBUILD"` is specified in source then the format should look like `<chromosome>.<build_id>`for example: `"10.GRCh37"`, if `"HGNC"` is specified in source then the format can be any `<HGNC GENESYMBOL>` for example : `"BRCA1"`   
* `start`: `<NUMBER>`; the start position of the variant within the reference, including the position it self. (0-based)
* `end`: `<NUMBER>`; the end position of the variant within the reference, excluding the position it self. (0-based)
* `allele_sequence`: `<LIST>`; each element in a list specifies an allele e.g `["C","GTCGTGAA"]`

#### Coordinate
 ***Optional***
 Will specify a query that returns all variants within a region based on the reference postion specified in the coordinate object list
* `id`: identifier for the allele query specified t
* `operator`: `"IS"` | `"NOT"`; this is to specify to include this allele query or to exclude it from the results
* `source`: `"GRCBUILD"`|`"HGNC"`; specifies the source of the reference 
* `reference`: if `"GRCBUILD"` is specified in source then the format should look like `<chromosome>.<build_id>`for example: `"10.GRCh37"`, if `"HGNC"` is specified in source then the format can be any `<HGNC GENESYMBOL>` for example : `"BRCA1"`   
* `start`: `<NUMBER>`; the start position of the variant within the reference, including the position it self. (0-based)
* `end`: `<NUMBER>`; the end position of the variant within the reference, excluding the position it self. (0-based)

#### QueryStatement
 ***Mandatory***
* `queryStatement`: `<STRING>`: specifies the relation between the different elements in the allele/coordinate list

# Example query
```json
{
    "queryMetadata": {
        "queryId": "1546",
        "queryType": "once",
        "label": "BramsFavoriteQuery",
        "queryResultFormat": "JSON",
        "submitter": {
            "id": "umcg_gcc_bram",
            "name": "Bram Miedema",
            "email": "b.miedema@somehwere.nl",
            "institution": "UMCG"
        }
    },
    "query": {
        "coordinate": [
            {
                "parameterID" : "a",
                "operator": "IS",
                "source": "GRCBUILD",
                "reference": "10.GRCh37",
                "start": "75871734",
                "end": "75871736"
            },
           {
                "parameterID" : "b",
                "operator": "IS",
                "source": "GRCBUILD",
                "reference": "10.GRCh37",
                "start": "75871734",
                "end": "75871736"
              
            },{
                "parameterID" : "c",
                "operator": "IS",
                "source": "GRCBUILD",
                "reference": "10.GRCh37",
                "start": "75871734",
                "end": "75871736"              
            }

        ]
      
    },
    "queryStatement": "(a|b)|c"
}
```
