### Templates for annotations
In these templates only triples related to the semantic model are included. They exclude annotation triples such as ex:anno1 rdf:type oa:annotation, and triples that relate to the verbatim transcription.

**Table 1.** List of minimal mandatory triples generated with the TYPE annotation of an entity, example for taxon.

|subject                | predicate                        | object    |           
|---|---|---
|`ex:taxon1`            |`rdf:type`                        |`dwc:Taxon`     |

**Table 2.** List of minimal mandatory triples generated with every annotation of an entity from an OBSERVATION RECORD. The 1 is an identifier for the full record. Should decide how and when this number is generated so that duplicate triples can be merged (we don't want a separate graph for each entity in an observation record that is annotated)


|subject                | predicate                        | object    |           
|---|---|---
|`ex:taxon1`            |`rdf:type`                        |`dwc:Taxon`           
|`ex:identification1`   |`rdf:type`                        |`dwc:Identification`  
|`ex:organism1`         |`rdf:type`                        |`foaf:Person`         
|`ex:occurrence1`       |`rdf:type`                        |`dwc:Occurrence`      
|`ex:event1`            |`rdf:type`                        |`dwc:Event`           
|`ex:date1`             |`rdf:type`                        |`nhc:Date`            
|`ex:humanObservation1` |`rdf:type`                        |`dwc:HumanObservation`
|`ex:location1`         |`rdf:type`                        |`dwc:Location`        |
|`ex:identifier1`       |`rdf:type`                        |`foaf:Person`         |
|`ex:recorder1`         |`rdf:type`                        |`foaf:Person`         |
|`ex:author1`           |`rdf:type`                        |`foaf:Person`         |
|`ex:taxon1`            |`nhc:scientificNameAuthorship`    |`ex:author1`          |
|`ex:identification1`   |`dwciri:toTaxon`                  |`ex:taxon1`           |
|`ex:identification1`   |`dsw:isBasedOn`                   |`ex:humanObservation1`|
|`ex:identification1`   |`dwciri:identifiedBy`             |`ex:identifier1`      |
|`ex:organism1`         |`dsw:hasIdentification`           |`ex:identification1`  |
|`ex:organism1`         |`dsw:hasOccurrence`               |`ex:occurrence1`      |
|`ex:organism1`         |`dsw:hasDerivative`               |`ex:humanObservation` |
|`ex:occurrence1`       |`dwciri:recordedBy`               |`ex:recorder1`        |
|`ex:occurrence1`       |`dsw:atEvent`                     |`ex:event1`           |
|`ex:occurrence1`       |`dsw:hasEvidence`                 |`ex:humanObservation1`|
|`ex:occurrence1`       |`dsw:occurrenceOf`                |`ex:organism1`        |
|`ex:event1`            |`dsw:locatedAt`                   |`ex:location1`        |
|`ex:event1`            |`nhc:verbatimDate`                |`ex:date1`            |
|`ex:event1`            |`dsw:eventOf`                     |`ex:occurrence1`      |
|`ex:humanObservation1` |`dsw:isBasisForId`                |`ex:identification1`  |
|`ex:humanObservation1` |`dsw:derivedFrom`                 |`ex:organism1`        |
|`ex:humanObservation1` |`dsw:isEvidenceFor`               |`ex:occurrence1`      |

If possible, any of the ex:type+identifier instances (of type Taxon, or Location) are replaced through the GUI by an existing external IRI

### Additional enrichments

Optional (but recommended) triples ADDITIONALLY generated per annotation type, applies to both TYPE and OBSERVATION RECORD annotations (depending on GUI fields that are filled in for the object. With measurement or fact, there is no extra field in the GUI, as the annotation is of a whole table or paragraph):

**Taxon.**

|subject                | predicate                        | object               |
|---|---|---
|`ex:taxon1`            |`nhc:taxonRank`                   |`ex:species`(or other)|
|`ex:taxon1`            |`nhc:belongsToTaxon`              |`ex:species`(or other)|
|`ex:taxon1`            |`nhc:belongsToTaxon`              |`ex:taxon2`(any other annotated taxon)|


**Location.**

|subject                | predicate                        | object               |
|---|---|---
|`ex:location1`         |`dwciri:inDescribedPlace`         |`http://sws.geonames.org/1648473`|
|`http://sws.geonames.org/1648473` | `rdf:type`            |`gn:Feature`          |

**Measurement (table) 4.**

|subject                | predicate                        | object               |
|---|---|---
|`ex:humanObservation1` |`dsw:hasDerivative`               |`ex:measurementOrFact1`  |

**Measurement (anatomical entity).**

|subject                | predicate                        | object                |
|---|---|---
|`ex:humanObservation1` |`dsw:hasDerivative`               |`ex:measurementOrFact1` |
|`ex:measurementOrFact1` |`nhc:measuresOrDescribes`         |`UBERON:0001062`  (a subclass of) |

**Measurement (property or attribute).**

|subject                | predicate                        | object               |
|---|---|---
|`ex:humanObservation1`  |`dsw:hasDerivative`               |`ex:measurementOrFact1`  |
|`ex:measurementOrFact1` |`nhc:measuresOrDescribes`         |`ncit:c20189`  (a subclass of) |


### Use cases
Field notes are collections of observation records ([`dwc:HumanObservation`](https://dwc.tdwg.org/terms/#humanobservation)) that describe the occurrence ([`dwc:Occurrence`](https://dwc.tdwg.org/terms/#occurrence)) of an organism ([`dwc:Organism`](http://rs.tdwg.org/dwc/terms/Organism)) at a certain location ([`dwc:Location`](https://dwc.tdwg.org/terms/#location)) and date ([`nhc:Date`](http://makingsense.liacs.nl/rdf/nhc-content/2018-04-04.html#Date)). An observation record most often includes  an identification ([`dwc:Identification`](https://dwc.tdwg.org/terms/#identification)) to a taxon ([`dwc:Taxon`](https://dwc.tdwg.org/terms/#taxon)), and accompanying measurements and facts ([`dwc:MeasurementOrFact`](https://dwc.tdwg.org/terms/#measurementorfact), [`UBERON:0001062`](http://purl.obolibrary.org/obo/UBERON_0001062), [`ncit:C20189`](http://purl.obolibrary.org/obo/NCIT_C20189)) that were used for identification. These observation records usually span multiple field notes, but can also be very short utterances such as on page 3: _Sci. Diard Buitenzorg_, most likely referring to the occurrence of another organism with the same identification.

**Table 1.** List of use cases with annotation classes and properties.

|class| property | example | annotation type |
|---|---|---|---|
|`dwc:Taxon`|`rdf:type`|[`1_1`](#Example-1_1)| TYPE |
||`dsw:hasIdentification`|[`1_2`](#Example-1_2)| OBSERVATION RECORD|
||`nhc:additionalIdentification`|[`1_3`](#Example-1_3)| OBSERVATION RECORD|
|`foaf:Person`|`rdf:type`|[`2_1`](#Example-2_1)| TYPE|
||`nhc:scientificNameAuthorship`|[`2_2`](#Example-2_2)| OBSERVATION RECORD|
||`dwciri:identifiedBy`|[`2_3`](#Example-2_3)| OBSERVATION RECORD|
|| `dwciri:recordedBy`|[`2_4`](#Example-2_4)| OBSERVATION RECORD|
|`dwc:Location`|`rdf:type`|[`3_1`](#Example-3_1)| TYPE|
|| `dsw:locatedAt`|[`3_2`](#Example-3_2)| OBSERVATION RECORD|
|`dwc:MeasurementOrFact`|`rdf:type`|[`4_1`](#Example-4_1)| TYPE|
||`dsw:derivedFrom`|[`4_2`](#Example-4_2) | OBSERVATION RECORD|
|`ncit:C20189` (propertyOrAttribute)|`rdf:type`|[`5_1`](#Example-5_1)| TYPE|
||`nhc:measuresOrDescribes`|[`5_2`](#Example-5_2)| OBSERVATION RECORD|
|`UBERON:0001062` (anatomicalEntity)|`rdf:type`|[`6_1`](#Example-6_1)|TYPE|
||`nhc:measuresOrDescribes`|[`6_2`](#Example-6_2) | OBSERVATION RECORD|
|`nhc:Date`|`rdf:type`|[`7_1`](#Example-7_1)|TYPE|
||`nhc:verbatimDate`|[`7_2`](#Example-7_2)| OBSERVATION RECORD|


### Example 1_1

Property: `rdf:type`

Input: [JSON](/data/json/example_1_1.json)

Output: [RDF/Turtle](/data/rdf/example_1_1.ttl)|[JSON-LD](/data/rdf/example_1_1.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the written text _Pteropus minimus_

* Fill in the pop-up form/table:

|Key|Value|Notes|Diff Expected
|---|-----|-----|-----
| Entity type/`text` | `Taxon` |  The handwritten text contains a taxon name. | Should be a drop-down menu with all possible classes
| verbatim text/`verbatim` | _Pteropus minimus_ | The verbatim text as written in the bounding box |
| language/`language` | _la_ | [ISO code](https://www.iso.org/iso-639-language-codes.html) for _latin_ |  add autocomplete/drop down menu
| Select property/`property` | `type`  | This refers to an entity annotation without further interpretation, merely specifying that the bounding box contains a taxon. |
| type/`type` | `taxon` |  auto-fill from entity type |
| Belongs to taxon/`belongstotaxon` | `https://identifiers.org/taxonomy:9397` | refers to _Chiroptera_ (order) in NCBI Taxonomy. Choice should be made whether this can be an IRI from an external database, or whether it should point to an already annotated verbatim entity. (such as _Chiroptera_ on page 2) | **question:** who do we allow to annotate, and who to interpret the data
| Taxon rank/`rank`| `scientificName` | refers to the verbatim text (_Pteropus minimus_); allowed values: `kingdom`,`class`,`order`,`family`,`genus`, `specificEpithet`, `scientificName`) | add values to drop-down menu


### Example 1_2

Property: [`dsw:hasIdentification`](http://purl.org/dsw/hasIdentification)

Input: [JSON](/data/json/example_1_2.json)

Output: [RDF/Turtle](/data/rdf/example_1_2.ttl)|[JSON-LD](/data/rdf/example_1_2.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the written text _Pteropus minimus_

* Fill in the pop-up form/table:

|Key|Value|Notes|Diff Expected
|---|-----|-----|-----
| Entity type/`text` | `Taxon` | The handwritten text contains a taxon name. | Should be a drop-down menu with all possible classes
| verbatim text/`verbatim` | _Pteropus minimus_ | The verbatim text as written in the bounding box |
| language/`language` | _la_ | [ISO code](https://www.iso.org/iso-639-language-codes.html) for _latin_ | add autocomplete/drop down menu
| Select property/`property` | Organism identification to/`hasIdentification` | The annotation of an entity that refers to the identification of an organism (a taxon name as the initialisation of a field observation record, usually a new genus or scientificName). |
| type/`type` | `taxon` | auto-fill from entity type |
| Belongs to taxon/`belongstotaxon` | `https://identifiers.org/taxonomy:9397` | refers to _Chiroptera_ (order) in NCBI Taxonomy. Choice should be made whether this can be an IRI from an external database, or whether it should point to an already annotated verbatim entity. (such as _Chiroptera_ on page 2) | **question:** who do we allow to annotate, and who to interpret the data
| Taxon rank/`rank` | `scientificName` | from list (`kingdom`,`class`,`order`,`family`,`genus`, `specificEpithet`, `scientificName`) | should be drop-down menu
| Identified by/`person` | `https://viaf.org/viaf/45106482/` | Corresponds to meaning of [`dwc:identifiedBy`](https://dwc.tdwg.org/terms/#dwc:identifiedBy) (people, groups, or organizations who assigned the Taxon to the subject). Preferably enter an instance of the class `foaf:Person` (or organization). Here, the writer of the field book is known (_Heinrich Kuhl_), but leave empty if unknown. | should be retrievable from pre-populated triple store
| Organism ID/`organismID` | `1` | Maps to [`dwc:organismID`](https://dwc.tdwg.org/terms/#dwc:organismID). Should be generated automatically, used to link all information belonging to an observation record of a single organism occurrence together. `1` is a placeholder; an unique ID should be generated for the organism record.\* | **important note**: when is this organism and possibly also occurrence ID generated? It allows all information belonging to the occurrence or organism observation to be linked together. Hence, how will we enforce this in the backend?

\* In the absence of a persistent global unique identifier, construct one from a combination of identifiers in the record that will most closely make the ID globally unique. Examples: http://arctos.database.museum/guid/MSB:Mamm:233627, 000866d2-c177-4648-a200-ead4007051b9, urn:catalog:UWBM:Bird:89776.


### Example 1_3

Property: [`nhc:additionalIdentification`](http://makingsense.liacs.nl/rdf/nhc/additionalIdentification)

Input: [JSON](/data/json/example_1_3.json)

Output: [RDF/Turtle](/data/rdf/example_1_3.ttl)|[JSON-LD](/data/rdf/example_1_3.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 8

* Annotate -> Click and Drag -> draw a bounding box around the written text _Pteropus_

* Fill in the pop-up form/table:

|Key|Value|Notes|Diff Expected
|---|-----|-----|-----
| Entity type/`text` | `Taxon` | The handwritten text contains a taxon name. |
| verbatim text/`verbatim` | _Pteropus_ | The verbatim text as written in the bounding box |
| language/`language` | _la_ | [ISO code](https://www.iso.org/iso-639-language-codes.html) for _latin_ | add autocomplete/drop down menu
| Select property/`property` | Additional identification to/`additionalIdentification` | The annotation of an entity that refers to an _additional_ (secondary) identification of an organism (a scientific name as the initialisation of a field observation record). Usually, this is a second identification performed at a later stage (with availability of more knowledge for identification). Within this field note, the organism is first identified in the field as a new taxon _Gymnonotus_. |
| type/`type` | `taxon` | auto-fill from entity type |
| Belongs to taxon/`belongstotaxon` | `https://identifiers.org/taxonomy:9397` | refers to _Chiroptera_ (order) in NCBI Taxonomy. Choice should be made whether this can be an IRI from an external database, or whether it should point to an already annotated verbatim entity. (such as _Chiroptera_ on page 2) (question: who do we allow to annotate, and who to interpret the data) |
| Taxon rank | `genus` | from list (`kingdom`,`class`,`order`,`family`,`genus`, `specificEpithet`, `scientificName`)|
| Organism ID/`organismsID`| `2` | Matches to [`dwc:organismID`](https://dwc.tdwg.org/terms/#dwc:organismID). Should be generated automatically. `2` is a placeholder; an unique ID should be generated for the organism record.\*| This additional identification should refer to the same organism ID as the first identification (`dsw:hasIdentification`). **important note**: when is this organism and possibly also occurrence ID generated? It allows all information belonging to the occurrence or organism observation to be linked together. Hence, how will we enforce this in the backend?
| Occurrence ID/`identificationID` _AK_: `occurenceID`?| `1` | Maps to [`dwc:identificationID`](https://dwc.tdwg.org/terms/#dwc:identificationID) _AK_: `dwc:occurenceID`?. Should be generated automatically. `1` is a placeholder; some unique ID should be generated for the organism record.\* | Should potentially be removed, or should be the same as the occurrence ID generated for the first identification, as it is based on information from the same organism occurrence. Right now, the pop-up table for example_1_2 does not prompt for occurrenceID.


### Example 2_1

Property: `rdf:type`

Input: [JSON](/data/json/example_2_1.json)

Output: [RDF/Turtle](/data/rdf/example_2_1.ttl)|[JSON-LD](/data/rdf/example_2_1.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the written text _Geoff_

* Fill in the pop-up form/table:

|Key|Value|Notes|Diff Expected
|---|-----|-----|-----
| Entity type/`text` | `Person` |  The handwritten text contains a person name. | Should be a drop-down menu with all possible classes
| verbatim text/`verbatim` | _Geoff_ | The verbatim text as written in the bounding box |
| language | | | _AK_: remove
| Select property/`property` | `Type`  | This refers to an entity annotation without further interpretation, merely specifying that the bounding box contains a person. |
| type | `person` |  auto-fill from entity type |
| Instance/`instance` | `http://viaf.org/viaf/39377694` | Link the bounding box to the IRI if known. Here the person Étienne Geoffroy-Saint-Hilaire. | Preferably these can be retrieved with semantic autocomplete


### Example 2_2

Property: [`nhc:scientificNameAuthorship`](http://makingsense.liacs.nl/rdf/nhc/scientificNameAuthorship)

Input: [JSON](/data/json/example_2_2.json)

Output: [RDF/Turtle](/data/rdf/example_2_2.ttl)|[JSON-LD](/data/rdf/example_2_2.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the written text _Geoff_

* Fill in the pop-up form/table:

|Key|Value|Notes|Diff Expected
|---|-----|-----|-----
| Entity type/`text` | `Person` | The handwritten text contains a person name. | Should be a drop-down menu with all possible classes
| verbatim text/`verbatim` | _Geoff_ | The verbatim text as written in the bounding box |
| language | | | _AK_: remove
| Select property/`property` | Author of scientific name/`scientificNameAuthorship` | The annotation of an entity that refers to a person that was the (published) author of a scientific name. Maps to [`dwc:scientificNameAuthorship`](https://dwc.tdwg.org/terms/#dwc:scientificNameAuthorship) The author is a crucial part of the taxon. Preferably, here, it refers to the persistent IRI of a person, such as `http://viaf.org/viaf/39377694` |
| type | `taxon` | auto-fill from entity type |
| Belongs to taxon/`belongstotaxon` | `nc:taxon1` | This field should contain the IRI that was generated when annotating the annotated scientific name, the subject of [`dwc:scientificNameAuthorship`](https://dwc.tdwg.org/terms/#dwc:scientificNameAuthorship) (here the annotated text: _Pteropus minimus_ on page 3) | **important note** The way it is setup now requires prior annotation of the taxon to which this name belongs. We should consider whether this makes sense.
| viaf IRI/`person` | `http://viaf.org/viaf/39377694` | the persistent identifier for the author of the scientific name. |  `nc:taxon1` [`dwc:scientificNameAuthorship`](https://dwc.tdwg.org/terms/#dwc:scientificNameAuthorship) `http://viaf.org/viaf/39377694`. Prompt should be changed to, e.g., person IRI instead of viaf IRI, as it could also be an orcid or other persistent identifier.


### Example 2_3

Property: [`dwciri:identifiedBy`](https://dwc.tdwg.org/list/#dwciri_identifiedBy)

Input: [JSON](/data/json/example_2_3.json)

Output: [RDF/Turtle](/data/rdf/example_2_3.ttl)|[JSON-LD](/data/rdf/example_2_3.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the written text _Diard_

* Fill in the pop-up form/table:

|Key|Value|Notes | Diff Expected
|---|-----|-----|-----
| Entity type/`text` | `Person` | The handwritten text contains a person name. | Should be a drop-down menu with all possible classes
| verbatim text/`verbatim` | _Diard_ | The verbatim text as written in the bounding box |
| language | | | _AK_: remove
| Select property/`property` | Organism identified by/`identifiedBy` | Maps to `dwciri:identifiedBy`
| type | `taxon` | auto-fill from entity type |
| Organism ID/`organismID` | `1` | Maps to [`dwc:organismID`](https://dwc.tdwg.org/terms/#dwc:organismID). Should be generated automatically, used to link all information belonging to an observation record of a single organism occurrence together. `1` is a placeholder; an unique ID should be generated for the organism record.\* | **important note**: when is this organism and possibly also occurrence ID generated? It allows all information belonging to the occurrence or organism observation to be linked together. Hence, how will we enforce this in the backend?
| viaf IRI/`person` | `http://viaf.org/viaf/39377694` | the persistent identifier for the person. | Prompt should be changed to, e.g., person IRI instead of viaf IRI, as it could also be an orcid or other persistent identifier.


### Example 2_4

Property: [`dwciri:recordedBy`](https://dwc.tdwg.org/list/#dwciri_recordedBy)

Input: [JSON](/data/json/example_2_4.json)

Output: [RDF/Turtle](/data/rdf/example_2_4.ttl)|[JSON-LD](/data/rdf/example_2_4.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the written text _Diard_

* Fill in the pop-up form/table:

|Key|Value|Notes|Diff Expected
|---|-----|-----|-----
| Entity type/`text` | `Person` | The handwritten text contains a person name. |  Should be a drop-down menu with all possible classes
| verbatim text/`verbatim` | _Diard_ | The verbatim text as written in the bounding box |
| language | | | _AK_: remove
| Select property/`property` | Occurrence recorded by/`recordedBy` | The annotation of an entity that refers to a person that recorded the occurrence of the organism. Maps to `dwciri:recordedBy`|
| type | `taxon` | auto-fill from entity type |
| viaf IRI/`person` | `http://viaf.org/viaf/39377694` | the persistent identifier for the person. |  Prompt should be changed to, e.g., person IRI instead of viaf IRI, as it could also be an orcid or other persistent identifier.


### Example 3_1

Property: `rdf:type`

Input: [JSON](/data/json/example_3_1.json)

Output: [RDF/Turtle](/data/rdf/example_3_1.ttl)|[JSON-LD](/data/rdf/example_3_1.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the written text _Buitenzorg_

* Fill in the pop-up form/table:

|Key|Value |Notes | Diff Expected
|---|-----|-----|-----
| Entity type | `Location` |  The handwritten text contains a location name. | Should be a drop-down menu with all possible classes
| verbatim text | _Buitenzorg_ | The verbatim text as written in the bounding box |
| language |  nl | [ISO code](https://www.iso.org/iso-639-language-codes.html) for _latin_ |  
| Select property | `Type`  | This refers to an entity annotation without further interpretation, merely specifying that the bounding box contains a location. |
| type | `location` |  auto-fill from entity type |
| instance | `http://sws.geonames.org/1648473/` | Link the bounding box to the IRI if known. Here the location _Buitenzorg_, currently called _Bogor_. | Preferably these instances can be retrieved with semantic autocomplete


### Example 3_2

Property: `dsw:locatedAt`

Input: [JSON](/data/json/example_3_2.json)

Output: [RDF/Turtle](/data/rdf/example_3_2.ttl)|[JSON-LD](/data/rdf/example_3_2.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the written text _Bagalonga_

* Fill in the pop-up form/table:

|Key|Value |Notes | Diff Expected
|---|-----|-----|-----
| Entity type | `Location` | The handwritten text contains a location name. | Should be a drop-down menu with all possible classes|  
| verbatim text | _Bagalonga_ | The verbatim text as written in the bounding box |
| language | | [ISO code](https://www.iso.org/iso-639-language-codes.html)  |add autocomplete/drop down menu
| Select property | `Occurrence located at` | The annotation of an entity that refers to the location where the observation of the organism occurrence took place. Maps to `dsw:locatedAt`. The prompt `Additional occurrence located at` should be merged with this one. |
| type | `taxon` | auto-fill from entity type |
| gn:geonamesfeature IRI |  | if known, the persistent identifier for the location from the geonames ontology, e.g., `http://sws.geonames.org/1648473/` (stands for _Buitenzorg_, also _Bogor_) |
| organism ID | `1` | Maps to [`dwc:organismID`](https://dwc.tdwg.org/terms/#dwc:occurrenceID). Should be generated automatically. `1` is a placeholder; an unique ID should be generated for the organism record.* | **important note**: when is this organism and possibly also occurrence ID generated? It allows all information belonging to the occurrence or organism observation to be linked together. Hence, how will we enforce this in the backend?


### Example 4_1

Property: `rdf:type`

Input: [JSON](/data/json/example_4_1.json)

Output: [RDF/Turtle](/data/rdf/example_4_1.ttl)|[JSON-LD](/data/rdf/example_4_1.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the table

* Fill in the pop-up form/table:

|Key|Value |Notes | Diff Expected
|---|-----|-----|-----
| Entity type | `MeasurementOrFact` |  The handwritten text contains a measurement or fact. | Should be a drop-down menu with all possible classes
| verbatim text |  | leave empty |
| language |   | [ISO code](https://www.iso.org/iso-639-language-codes.html) for _latin_ | should be removed here
| Select property | `Type`  | This refers to an entity annotation without further interpretation, merely specifying that the bounding box contains a measurement or fact. |
| type | `measurementorfact` |  auto-fill from entity type |
| instance |  | Should be left empty | This field should be removed here.


### Example 4_2

Property: `dsw:derivedFrom`

Input: [JSON](/data/json/example_4_2.json)

Output: [RDF/Turtle](/data/rdf/example_4_2.ttl)|[JSON-LD](/data/rdf/example_4_2.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the measurement or fact (such as a table or a statement about the animal)

* Fill in the pop-up form/table:

|Key|Value |Notes | Diff Expected
|---|-----|-----|----
| Entity type | `MeasurementOrFact` | The handwritten text contains a table or other measurement or fact. | Should be a drop-down menu with all possible classes|  
| verbatim text | leave empty |  |  |
| language | leave empty | [ISO code](https://www.iso.org/iso-639-language-codes.html) | add autocomplete/drop down menu |
| Select property | `Identification based on (table)` |  should be table _or_ paragraph| |
| type | `measurementorfact` | auto-fill from entity type |
| organism ID | `1` | Maps to [`dwc:organismID`](https://dwc.tdwg.org/terms/#dwc:occurrenceID). Should be generated automatically. `1` is a placeholder; an unique ID should be generated for the organism record.* | **important note**: when is this organism and possibly also occurrence ID generated? It allows all information belonging to the occurrence or organism observation to be linked together. Hence, how will we enforce this in the backend?  |


### Example 5_1

Property: `rdf:type`

Input: [JSON](/data/json/example_5_1.json)

Output: [RDF/Turtle](/data/rdf/example_5_1.ttl)|[JSON-LD](/data/rdf/example_5_1.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the handwritten word _Color_

* Fill in the pop-up form/table:

|Key|Value |Notes | Diff Expected
|---|-----|-----|-----
| Entity type | `PropertyOrAttribute` |  The handwritten text contains a property or attribute name. | Should be a drop-down menu with all possible classes
| verbatim text | _Color_ | The verbatim text as written in the bounding box |
| language |  nl | [ISO code](https://www.iso.org/iso-639-language-codes.html) for _latin_ |  
| Select property | `Type`  | This refers to an entity annotation without further interpretation, merely specifying that the bounding box contains a property or attribute name. |
| type | `propertyOrAttribute` |  auto-fill from entity type |
| instance | `http://identifiers.org/ncit/C37927` | Link the bounding box to the IRI if known. Here the property _Color_. | Preferably these instances can be retrieved with semantic autocomplete

* Check generated triples in the [RDF store](http://localhost:8080/rdf4j-workbench/repositories/mem-rdf/query).


### Example 5_2

Property: `nhc:measuresOrDescribes` and `propertyOrAttribute`

Input: [JSON](/data/json/example_5_2.json)

Output: [RDF/Turtle](/data/rdf/example_5_2.ttl)|[JSON-LD](/data/rdf/example_5_2.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the handwritten word _Color_

* Fill in the pop-up form/table:

|Key|Value |Notes  | Diff Expected
|---|-----|-----|-----
| Entity type | `propertyOrAttribute` | The handwritten text contains an indication of a property or attribute of the described organism. | Should be a drop-down menu with all possible classes|  
| verbatim text | _Color_ |  |  |
| language | la | [ISO code](https://www.iso.org/iso-639-language-codes.html)  |add autocomplete/drop down menu
| Select property | `Table/paragraph measures or describes` | Indicating that a table or a paragraph describes the certain property or attribute, here the _Color_ of the animal | |
| type | `propertyOrAttribute` | auto-fill from entity type |
| `ncit:propertyorattribute subclass IRI` | `http://identifiers.org/ncit/C37927` | A subclass of `http://identifiers.org/ncit/C20189` or `propertyOrAttribute` from the NCIT ontology.
| organism ID | `1` | Maps to [`dwc:organismID`](https://dwc.tdwg.org/terms/#dwc:occurrenceID). Should be generated automatically. `1` is a placeholder; an unique ID should be generated for the organism record.* | **important note**: when is this organism and possibly also occurrence ID generated? It allows all information belonging to the occurrence or organism observation to be linked together. Hence, how will we enforce this in the backend?  |


### Example 6_1

Property: `rdf:type`

Input: [JSON](/data/json/example_6_1.json)

Output: [RDF/Turtle](/data/rdf/example_6_1.ttl)|[JSON-LD](/data/rdf/example_6_1.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the handwritten word _Dentibus_

* Fill in the pop-up form/table:

|Key|Value |Notes | Diff Expected
|---|-----|-----|-----
| Entity type | `AnatomicalEntity` |  The handwritten text contains the name of an anatomical entity. | Should be a drop-down menu with all possible classes
| verbatim text | _Dentibus_ | The verbatim text as written in the bounding box |
| language |  nl | [ISO code](https://www.iso.org/iso-639-language-codes.html) for _latin_ |  
| Select property | `Type`  | This refers to an entity annotation without further interpretation, merely specifying that the bounding box contains the name of an anatomical entity. |
| type | `anatomicalentity` |  auto-fill from entity type |
| instance | `http://purl.obolibrary.org/obo/UBERON_0003672` | Link the bounding box to the IRI if known. Here the anatomical entity _Dentibus_. | Preferably these instances can be retrieved with semantic autocomplete

* Check generated triples in the [RDF store](http://localhost:8080/rdf4j-workbench/repositories/mem-rdf/query).


### Example 6_2

Property: `nhc:measuresOrDescribes` and `anatomicalEntity`

Input: [JSON](/data/json/example_6_2.json)

Output: [RDF/Turtle](/data/rdf/example_6_2.ttl)|[JSON-LD](/data/rdf/example_6_2.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 3

* Annotate -> Click and Drag -> draw a bounding box around the handwritten word _Dentibus_

* Fill in the pop-up form/table:

|Key|Value |Notes | Diff Expected
|---|-----|-----|-----
| Entity type | `anatomicalEntity` | The handwritten text contains the name of an anatomical entity of the described organism. | Should be a drop-down menu with all possible classes|  
| verbatim text | _Dentibus_ |  | |
| language | la | [ISO code](https://www.iso.org/iso-639-language-codes.html)   | add autocomplete/drop down menu
| Select property | `Table/paragraph measures or describes` | Indicating that a table or a paragraph describes the certain anatomical entity, here the _Dentibus_ (teeth) of the animal | |
| type | `anatomicalEntity` | auto-fill from entity type |
| `uberon:anatomicalentity subclass IRI` | `http://purl.obolibrary.org/obo/UBERON_0003672` | A subclass of `http://purl.obolibrary.org/obo/UBERON_0001062` or `anatomical entity` from the uberon ontology.
| organism ID | `1` | Maps to [`dwc:organismID`](https://dwc.tdwg.org/terms/#dwc:occurrenceID). Should be generated automatically. `1` is a placeholder; an unique ID should be generated for the organism record.* | **important note**: when is this organism and possibly also occurrence ID generated? It allows all information belonging to the occurrence or organism observation to be linked together. Hence, how will we enforce this in the backend? |


### Example 7_1

Property: `rdf:type`

Input: [JSON](/data/json/example_7_1.json)

Output: [RDF/Turtle](/data/rdf/example_7_1.ttl)|[JSON-LD](/data/rdf/example_7_1.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 4

* Annotate -> Click and Drag -> draw a bounding box around the handwritten words _10 April 1821_

* Fill in the pop-up form/table:

|Key|Value |Notes | Diff Expected
|---|-----|-----|-----
| Entity type | `date` |  The handwritten text contains a date. | Should be a drop-down menu with all possible classes
| verbatim text | _10 April 1821_ | The verbatim text as written in the bounding box |
| language |  nl | [ISO code](https://www.iso.org/iso-639-language-codes.html) for _latin_ |  
| Select property | `Type`  | This refers to an entity annotation without further interpretation, merely specifying that the bounding box contains a date. |
| type | `date` |  auto-fill from entity type |
| instance | | this field should be removed | instead of the instance field, we would like to see the same fields as when the property `Organism described on` is selected, minus the organism ID field. See example [`example 7_2`](#Example-7_2) and corresponding ttl file [`example_7_2.ttl`](/data/rdf/example_7_2.ttl) file.

* Check generated triples in the [RDF store](http://localhost:8080/rdf4j-workbench/repositories/mem-rdf/query).


### Example 7_2

Property: `nhc:verbatimDate` and `rdf:type`\*

Input: [JSON](/data/json/example_7_1.json)

Output: [RDF/Turtle](/data/rdf/example_7_1.ttl)|[JSON-LD](/data/rdf/example_7_1.jsonld)

Steps:

* Go to http://localhost:8080/semanticAnnotator/

* Register -> Save

* Collections -> manuscript MMNAT01_AF -> page 4

* Annotate -> Click and Drag -> draw a bounding box around the handwritten date _10 april 1821_

* Fill in the pop-up form/table:

|Key|Value |Notes | Diff Expected
|---|-----|-----|-----
| Entity type | `date` | The handwritten text contains a date, either a day, month year, or a combination thereof. | Should be a drop-down menu with all possible classes|  
| verbatim text | _10 april 1821_ |  Text as is, no formatting| |
| language | nl | [ISO code](https://www.iso.org/iso-639-language-codes.html)   | add autocomplete/drop down menu
| Select property | `Organism described on` | Indicates that the observation of the animal was on a certain date |  |
| type | `date` | auto-fill from entity type |
| Year (yyyy) | 1821 || should not be auto-filled with a 0
| Month (mm) | 04 | |should not be auto-filled with a 0
| Day (dd) | 10 | |should not be auto-filled with a 0
| organism ID | `1` | Maps to [`dwc:organismID`](https://dwc.tdwg.org/terms/#dwc:occurrenceID). Should be generated automatically. `1` is a placeholder; an unique ID should be generated for the organism record.* | **important note**: when is this organism and possibly also occurrence ID generated? It allows all information belonging to the occurrence or organism observation to be linked together. Hence, how will we enforce this in the backend?  |


\* For the `rdf:type` variant of `nhc:Date`, the fields should be the same, only omitting the field `organism ID`.

**General notes:**

* (back-end) Most annotations (except for variety 1, a class annotation) link to an annotation record, and atm, some annotations therefore depend on the prior annotation of other named entities. However, these annotation events should be able to occur un any order and the code should reflect this.  

* (relates to front-end) The entity type field should produce a drop-down menu with the possible classes  (`taxon`, `person`, `location`, `date`, `anatomical entity`, `measurementOrFact`) rather than a free-text field. Similarly, the entry to this field should limit the number of possibilities for the `select property` field. (E.g., `person` -> `Type`, `Author of scientific name`, `Organism identified by`, `Occurrence recorded by`/`Additional Occurrence recorded by`)
