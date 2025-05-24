# Glossary

## Acronyms

- **CAID**: Child Abuse Image Database
- **CADF**: Cloud Auditing Data Federation
- **CASE**: Cyber-investigation Analysis Standard Expression
- **CSAM**: Child Sexual Abuse Material
- **ESP**: Electronic Service Provider
- **ICAC**: Internet Crimes Against Children
- **ICMEC**: International Centre for Missing & Exploited Children
- **ICCAM**: International Child Sexual Exploitation Image Database
- **INHOPE**: International Association of Internet Hotlines
- **JSON-LD**: JavaScript Object Notation for Linked Data
- **LEA**: Law Enforcement Agency
- **MLAT**: Mutual Legal Assistance Treaty
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

### Core Classes
- **HotlineReport**: A report of potential child exploitation material
- **EvidenceItem**: Digital evidence associated with a report
- **HotlineAction**: An action taken in processing a report
- **ICACInvestigation**: An investigation into child exploitation
- **AutomatedReporterAgent**: Software system that automatically generates reports
- **HashFeedbackAction**: Action recording feedback on hash matches
- **URLReference**: Reference to a URL containing potential CSAM

### Criminal Activity Classes
- **ProductionOffense**: Child sexual abuse material production activity
- **CustodialRelationship**: Trust relationship involving authority over children
- **GroomingSolicitation**: Grooming or solicitation of children for sexual purposes
- **Sextortion**: Sexual extortion incidents involving children
- **LiveStreamingCSA**: Live streaming of child sexual abuse
- **DigitallyGeneratedCSAMIncident**: AI-generated or manipulated CSAM

### Investigation Classes
- **UnderCoverOperation**: Covert investigation activities
- **TacticalOperation**: High-risk law enforcement operations
- **MultiJurisdictionalOperation**: Cross-jurisdictional investigations
- **ForensicAcquisitionAction**: Digital evidence collection and imaging
- **ContentDetectionAction**: Automated CSAM detection and classification
- **LegalProcessAction**: Initiation of legal processes (warrants, subpoenas)
- **VictimRescueAction**: Operations to rescue and protect victims

### Victim Services Classes
- **VictimImpactAssessment**: Comprehensive trauma and harm evaluation
- **TaskForceOperation**: Multi-agency coordinated operations
- **TherapeuticIntervention**: Treatment and support services for victims
- **ComplexTrauma**: Severe psychological harm from abuse
- **VictimRecoveryProgram**: Long-term support and rehabilitation services

### Registry & Compliance Classes
- **RegisteredOffender**: Individual in sex offender registry system
- **ComplianceMonitoringOperation**: Registry compliance verification activities
- **RegistrationRecord**: Official registry documentation
- **ComplianceViolation**: Failure to meet registry requirements
- **NotificationRequirement**: Community notification obligations

### International Classes
- **CrossBorderInvestigation**: International coordination activities
- **TrainingProgram**: Professional development and capacity building
- **PreventionProgram**: Education and awareness initiatives
- **LegalHarmonization**: International legal framework alignment
- **MutualLegalAssistance**: International legal cooperation mechanisms

### Technical Classes
- **ForensicImage**: Bit-for-bit copy of digital storage device
- **PhotoDNAHash**: Microsoft PhotoDNA hash value for image matching
- **DetectionResult**: Outcome of automated content analysis
- **SocialMediaPlatform**: Online platform used for communication or content sharing
- **ContentModerationCapability**: Platform's ability to detect and remove illegal content

### Properties
- **reportedBy**: Links a report to its reporter
- **hasEvidence**: Links a report to its evidence
- **triggersAction**: Links a report to actions taken
- **performedBy**: Links an action to its performer
- **depictsChild**: Links digital artifact to depicted child (TLP-RED by default)
- **producesArtifact**: Links an event to digital artifacts created
- **involvesVictim**: Links an event to victim roles
- **involvesOffender**: Links an event to offender roles
- **hasStep**: Links investigation to lifecycle steps
- **nextStep**: Chronological sequence in workflows
- **previousStep**: Reverse chronological sequence
- **severityLevel**: Severity rating (0-3 scale)

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

### Registry Tier Classifications
- **Tier I**: Low-risk offenders (10-15 year registration)
- **Tier II**: Moderate-risk offenders (25 year registration)
- **Tier III**: High-risk offenders (lifetime registration)

### Traffic Light Protocol (TLP) Classifications
- **TLP-RED**: Critical sensitivity, no sharing (default for depictsChild)
- **TLP-AMBER**: Limited sharing within organization
- **TLP-GREEN**: Community sharing allowed
- **TLP-WHITE**: Public information, unrestricted sharing

### Operation Types
- **Named Operations**: Coordinated multi-agency operations (e.g., "Operation Cyber Highway Safety Check")
- **Seasonal Operations**: Operations timed to seasonal patterns (e.g., spring break)
- **Compliance Operations**: Large-scale registry verification activities
- **Rescue Operations**: Emergency response to save children from ongoing abuse
- **Prevention Campaigns**: Educational and awareness programs

### Investigative Techniques
- **Undercover Infiltration**: Covert penetration of criminal networks
- **Digital Forensics**: Technical analysis of digital evidence
- **Hash Matching**: Automated comparison of known CSAM signatures
- **Behavioral Analysis**: Pattern recognition in grooming and exploitation
- **Cross-Platform Analysis**: Investigation across multiple digital services

### International Frameworks
- **ICMEC Global Partnership**: Cooperation with 120+ countries
- **CSAM Model Law**: Template legislation for international harmonization
- **Cross-Border Information Sharing**: Secure international data exchange
- **Capacity Building**: Training and technical assistance programs
- **Policy Harmonization**: Alignment of legal frameworks across jurisdictions

### Performance Metrics
- **Arrest Rate**: Arrests per search warrant executed
- **Rescue Rate**: Children rescued per operation
- **Compliance Rate**: Registry offenders in compliance with requirements
- **Training Reach**: Number of professionals trained globally
- **Prevention Effectiveness**: Impact measurement of education programs

### Technology Integration
- **UCO Compatibility**: Native integration with Unified Cyber Ontology
- **CASE Export**: Seamless export to CASE investigation format
- **JSON-LD Context**: Developer-friendly API integration
- **SHACL Validation**: Automated data quality verification
- **SPARQL Analytics**: Query-based operational intelligence

See the individual ontology modules and their SKOS concept schemes for complete term definitions and relationships.

## License

This project is licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0). 