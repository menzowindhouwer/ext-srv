# SKG-IF Service Extension
---
title: Service 
parent: Interoperability framework
ancestor: SKG-IF
layout: default
nav_order: 2
---
# SKG-IF Service Extension

A Service is a type of software application or component that provides specific 
functionality or operations over a network, often via the internet, and is typically accessed 
through an interface such as an API or a web application.
(note Service is renaming of Software Service for which still used in many discussion documents)



## Properties

The properties set was suggested and informed from a number of examples both thematic and general:
- The different CMDI schema for tools & services used in the [VLO catalogue], esp the  [UDPipe example] 
- [SSHOMP catalogue] (tools and services) different examples
- [ELG catalogue] (tools and services) different examples
- [CLARIN LR Switchboard schema]
- The [Schema.org SoftwareApplication] type has many useful properties 
- The [EOSC Service Profile 4.1 rc (latest) and 5.0]


### `local_identifier`
*String* (mandatory): Unique code identifying a [Software Service] in the SKG (if any, otherwise "stateless identifier").

{: .highlight }
**Suggestion:** Use a URL as a string to make this entity dereferenceable on the Web. For additional information, see the [section 'Local identifiers of entities' of the Interoperability Framework](/interoperability-framework/#local-identifiers-of-entities).

```json
    "local_identifier": "11234/1-4816"
```

### `identifiers`
*List* (recommended): Objects representing external identifiers for the entity. 

Each identifier is structured as follows:
- `scheme` *String* (mandatory): The scheme for the external identifier.
- `value` *String* (mandatory): The external identifier.

**Note:** the current version of SKG-IF includes the following types of identifiers (to be specified as strings in the field “scheme”): `doi`, `handle`, `pmid`, `url`, `omid`, ...

```json
    "identifiers": [
        {
            "scheme": "handle",
            "value": "11234/1-4816"
        },
        {
            "scheme": "doi",
            "value": "10.18653/v1/K18-2020"
        }
    ]
```

### `entity_type`
*String* (mandatory): Field stating what kind of entity is being serialised. 

Needed for parsing purposes; fixed to `service`.

```json
    "entity_type": "service"
```

### `name`
*Object* (optional): The names of a [Software service] (multiple for multilingualism). 

The object is a dictionary, the keys represent language codes following [ISO 639-1]; the special key `none` is reserved whenever the information about the language is not available or cannot be shared.

```json
    "name": {
        "en": "UDPipe",
        "zh-cn": "UDPipe 工具"        
    },
    "alt_label": {
        "en": ["UDPipe 2", "UDPipe 2.0"]
    }
```

### `description`
*Object* (optional): The description of a [Service] (multiple for multilingualism).

The object is a dictionary, the keys represent language codes following [ISO 639-1]; the special key `none` is reserved whenever the informtion about the language is not available or cannot be shared.

```json
    "descriptions": {
        "en": ["UDPipe 2 is a Python prototype, capable of performing tagging, lemmatization and syntactic analysis of CoNLL-U input. It took part in several competitions, reaching excellent results in all of them", "Summary"],
        "none": ["ontaligestring"]
    }
```


### `audience_byrole`
*Object* (optional): the audience(s) that the service is intended to be used by
This can  both express desire and/or design of the service operators. Values are mandatory taken from 
the https://vocabs.sshopencloud.eu/vocabularies/sshoc-audience/audienceScheme 
```json
    "@context": {
        sshocaudience: "https://vocabs.sshopencloud.eu/vocabularies/sshoc-audience/"
    },
    "intended_audience": ["sshocaudience:public", "sshocaudience:student" ]
```

### `audience_byjurisdiction`
*Object* (optional): the jurisdiction that is given by the service operator's legal status limits
the audience. value take from either Global, Institution, National, or Regional aka multiple countries, from https://zenodo.org/records/15516020)
```json
    "jurisdiction": ["ds_jurisdiction_research_infrastructure", "ds_jurisdiction-regional" ]
```

### `disciplines`
*List* (optional):  The disciplines for which a [Software Service] is dedicated. 
The disciplines must be specified using the Library of Congress Classification codes, 
available at https://id.loc.gov/authorities/classification (e.g. PA3000-PA3049 for classical literature). 
In case a [Service] is discipline agnostic, the string "all" should be specified.
```json
    "@context": {
        loc: "https://id.loc.gov/authorities/classification/"
    }
    "discipline": [
        "loc:QC790.95-QC791.8"
    ]
```

### `isaccessible_for free`
*String* (optional): A property to signal that the Service is accessible for free.

``` json


    "is_accessible_for_free": true
```

### `entity_type`
*String* (mandatory) indicating what type of entity is being serialised.

Needed for parsing purposes; fixed to `service`.

```json
   "entity_type": "service"
```

### `invocation_type`
*List* (mandatory): the way the service is used or called. multiple values are possible, access rights and licenses are assued to be the same.
values are specified by vocabulary https://vocabs.sshopencloud.eu/vocabularies/invocation-type/invocationTypeScheme

```json
    "@context": {
        sshocinvt: "https://vocabs.sshopencloud.eu/vocabularies/invocation-type/"
    },
    "invocation_type": [ "sshocinvt:restfullWebservice", "sshocinvt:webApplication" ]
```

### `life_cycle_status`
*List* (optional): indicates the development cycle and/or maturity status of the service. values are by vocabulary
https://vocabs.sshopencloud.eu/vocabularies/eosc-life-cycle-status/ Originally specified in the EOSC Service Profile. Could extend with TRL classifications.
```json
     "@context": {
        elcs: "https://vocabs.sshopencloud.eu/vocabularies/eosc-life-cycle-status/"
     }
    "life_cycle_status": ["elcs:life_cycle_status_production", "elcs:TRL6" ]    
```    

### `website`
*String* (mandatory): landingpage for the service. preferably one maintained by the service operator 

```json
    "website": "https://ufal.mff.cuni.cz/udpipe/2"
```

### `availablity_geographic`
*List* (optional): list of countries and regions where the service is made available eg. for license reasons. 

```json
     "@context": {
        eoscgeoavail: "https://vocabs.sshopencloud.eu/vocabularies/eosc-life-cycle-status/"
     },
    "availability_geographic": ["eoscgeoavail:eu","eoscgeoavail:uk"]
```    

### `supported_language`

*List* (optional) if applicable the language(s) the service is able to process, values provided as ISO369-2 language codes

``` json
    "@context": {
       lexvo: "http://lexvo.org/id/"
     },
     "supported_language": ["lexvo:iso639-3/de","lexvo:iso639-3/nl"]
```

### `relevant_organisations`
*List* (optional):  [Organisation] identifiers associated with and relevant for a [Service].
identifiers can be of local or global identifier system type eg. ror, uri 

```json
    "relevant_organisations": [
        "https://lindat.mff.cuni.cz", 
        "https://ror.org/03wp25384"

    ]
```
foaf:Organization items defined separately elsewhere 

```json
    {
      "@id": "https://lindat.mff.cuni.cz",
      "@type": "foaf:Organization",
      "name": "LINDAT/CLARIAH-CZ Research Infrastructure",
      "description": "Hosts the production service instance and provides long-term repository, compute resources and user support.",
      "url": "https://lindat.mff.cuni.cz"
    }

``` 

### `keywords`
*List* (optional): list of keywords relevant for service discovery, values may be simple strings or concept URIs

```json
    "keywords": ["https://www.wikidata.org/wiki/Q30642","parsing",]
``` 

### `deployment_of`
*List* (optional) Research Product of type software, software class or sourcecode rep  link that the service is based on

```json
    "deployment_of": [
        { "@id": "https://github.com/ufal/udpipe", "@type": "schema:SoftwareSourceCode"},
        { "@id": "http://example.org/research_product/RP_101", "@type": "skg:research_product"}
    ]
    
```

### `contributions`
*List* [Agents] that contributed to a [Service] (optional): 

```json
    "contributions": [ 
           {
                    "by": "University of Sheffield",
                    "role": "operator"
                },
                {
                    "by": "UK Research and Innovation agency",
                    "role": "funder"
                }  
]    
```


----
[Research product]: {% link interoperability-framework/docs/research-product.md %}
[Agent]: {% link interoperability-framework/docs/agent.md %}
[ISO 639-1]: https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes

