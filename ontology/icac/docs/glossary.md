# Glossary

## Acronyms

- **CAID**: Child Abuse Image Database
- **CADF**: Cloud Auditing Data Federation
- **CASE**: Cyber-investigation Analysis Standard Expression
- **CSAM**: Child Sexual Abuse Material
- **ESP**: Electronic Service Provider
- **ICAC**: Internet Crimes Against Children
- **ICCAM**: International Child Sexual Exploitation Image Database
- **INHOPE**: International Association of Internet Hotlines
- **JSON-LD**: JavaScript Object Notation for Linked Data
- **LEA**: Law Enforcement Agency
- **NCMEC**: National Center for Missing & Exploited Children
- **NSRL**: National Software Reference Library
- **PII**: Personally Identifiable Information
- **RDF**: Resource Description Framework
- **SHACL**: Shapes Constraint Language
- **SPARQL**: SPARQL Protocol and RDF Query Language
- **TLP**: Traffic Light Protocol
- **TURTLE**: Terse RDF Triple Language
- **UCO**: Unified Cyber Ontology

## Key Terms

### Classes
- **HotlineReport**: A report of potential child exploitation material
- **EvidenceItem**: Digital evidence associated with a report
- **HotlineAction**: An action taken in processing a report
- **ICACInvestigation**: An investigation into child exploitation
- **AutomatedReporterAgent**: Software system that automatically generates reports
- **HashFeedbackAction**: Action recording feedback on hash matches
- **URLReference**: Reference to a URL containing potential CSAM

### Properties
- **reportedBy**: Links a report to its reporter
- **hasEvidence**: Links a report to its evidence
- **triggersAction**: Links a report to actions taken
- **performedBy**: Links an action to its performer

### Status Values
- **status-new**: Report is newly received
- **status-in-progress**: Report is being processed
- **status-in-review**: Report is under review
- **status-forwarded**: Report has been forwarded to LEA
- **status-closed**: Report processing is complete
- **status-reopened**: Report has been reopened for additional review

### Classification Values
- **classification-confirmed**: Material confirmed as CSAM
- **classification-false-positive**: Material not CSAM
- **classification-uncertain**: Requires further review
- **classification-legal**: Material is legal but concerning
- **classification-other**: Other classification

See the [HotlineCaseStatus](https://ontology.unifiedcyberontology.org/hotlines/2025/core#HotlineCaseStatus) SKOS concept scheme for the complete list of status values.

## License

This project is licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0). 