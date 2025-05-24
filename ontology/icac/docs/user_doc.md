# ICAC Ontology Family - User Documentation

## Quick Start

### Prerequisites
- Basic understanding of RDF and ontologies
- Familiarity with Turtle syntax
- Understanding of UCO (Unified Cyber Ontology)
- Python 3.9+ for validation tools

### Installation
1. Clone the repository:
```bash
git clone https://github.com/ucoProject/ontology-icac.git
cd ontology-icac
```

2. Install dependencies:
```bash
pip install -r requirements.txt
# requirements.txt contents:
# rdflib>=6.3.2
# pyshacl>=0.20.0
# robotframework>=6.1.1
# robotframework-rdflib>=0.1.0
```

3. Start the validation server:
```bash
docker compose -f docker-compose.yaml up -d
```

## Core Concepts

### 1. Hotline Reports
Hotline reports are the foundation of the ontology. They represent reports of potential child exploitation material.

```turtle
@base <https://example.org/hotline/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix uco-core: <https://ontology.unifiedcyberontology.org/core#> .
@prefix uco-observable: <https://ontology.unifiedcyberontology.org/observable#> .
@prefix hotline: <https://ontology.unifiedcyberontology.org/hotlines/2025/core#> .

hotline:report-001 a hotline:PublicReport ;
    hotline:reportedBy hotline:reporter-001 ;
    hotline:receivedBy hotline:org-001 ;
    hotline:hasEvidence hotline:evidence-001 ;
    hotline:intakeChannel hotline:web-form ;
    hotline:status hotline:status-closed .
```

### 2. Evidence Items
Evidence items represent the material reported to hotlines.

```turtle
hotline:evidence-001 a hotline:ImageEvidence ;
    hotline:firstSeen "2024-03-20T10:00:00Z"^^xsd:dateTime ;
    hotline:foundAtURL hotline:url-001 .
```

### 3. Actions
Actions represent the steps taken in processing reports.

```turtle
hotline:action-001 a hotline:ReportReviewAction ;
    hotline:performedBy hotline:analyst-001 ;
    hotline:startTime "2024-03-20T10:05:00Z"^^xsd:dateTime ;
    hotline:endTime "2024-03-20T10:10:00Z"^^xsd:dateTime .
```

## API Reference

### 1. JSON-LD Context
Context files live in `/contexts/`, versioned alongside ontology:

```json
{
  "@context": "https://ontology.unifiedcyberontology.org/hotlines/2025/core/contexts/hotlines-core.jsonld",
  "@type": "HotlineReport",
  "reportedBy": {
    "@type": "ReporterRole",
    "isAnonymous": true
  }
}
```

For local development:
```json
{
  "@context": "contexts/hotlines-core.jsonld",
  "@type": "HotlineReport",
  "reportedBy": {
    "@type": "ReporterRole",
    "isAnonymous": true
  }
}
```

### 2. SPARQL Queries

#### 2.1 Read Operations
```sparql
# Find All Reports
SELECT ?report
WHERE {
    ?report a hotline:HotlineReport .
}

# Find Reports by Status
SELECT ?report
WHERE {
    ?report a hotline:HotlineReport ;
            hotline:status hotline:status-new .
}
```

#### 2.2 Write Operations
```sparql
# Mark Report as Closed
INSERT {
    ?report hotline:status hotline:status-closed ;
            hotline:closedAt ?now .
}
WHERE {
    ?report a hotline:HotlineReport ;
            hotline:status hotline:status-in-progress .
    BIND(NOW() as ?now)
}
```

## Comprehensive Usage Examples

### 1. Creating Reports

#### 1.1 Basic Report
```turtle
hotline:report-002 a hotline:PublicReport ;
    hotline:reportedBy [
        a hotline:ReporterRole ;
        hotline:isAnonymous true
    ] ;
    hotline:receivedBy hotline:org-001 ;
    hotline:hasEvidence hotline:evidence-002 ;
    hotline:intakeChannel hotline:web-form ;
    hotline:status hotline:status-new .
```

#### 1.2 ESP Report
```turtle
hotline:report-003 a hotline:ESPReport ;
    hotline:reportedBy hotline:automated-reporter-001 ;
    hotline:receivedBy hotline:org-001 ;
    hotline:hasEvidence hotline:evidence-003 ;
    hotline:intakeChannel hotline:api ;
    hotline:status hotline:status-new .
```

### 2. Managing Evidence

#### 2.1 Image Evidence
```turtle
hotline:evidence-002 a hotline:ImageEvidence ;
    hotline:firstSeen "2024-03-20T11:00:00Z"^^xsd:dateTime ;
    hotline:foundAtURL hotline:url-002 ;
    uco-observable:hash [
        a uco-observable:Hash ;
        uco-observable:hashValue "abc123"^^xsd:string ;
        uco-observable:hashMethod "SHA-256"
    ] .
```

#### 2.2 URL Evidence
```turtle
hotline:evidence-003 a hotline:URLReference ;
    hotline:firstSeen "2024-03-20T12:00:00Z"^^xsd:dateTime ;
    hotline:foundAtURL hotline:url-003 .
```

### 3. Cross-Border Scenarios

#### 3.1 Canadian Report to Spanish LEA
```turtle
hotline:report-004 a hotline:PublicReport ;
    hotline:reportedBy hotline:reporter-ca-001 ;
    hotline:receivedBy hotline:org-ca-001 ;
    hotline:hasEvidence hotline:evidence-004 ;
    hotline:triggersAction hotline:action-004 .

hotline:action-004 a hotline:ForwardToLEAction ;
    hotline:performedBy hotline:analyst-ca-001 ;
    hotline:forwardsTo hotline:org-es-001 ;
    hotline:startTime "2024-03-20T13:00:00Z"^^xsd:dateTime ;
    hotline:endTime "2024-03-20T13:05:00Z"^^xsd:dateTime .
```

### 4. ICAC Investigation Lifecycle

#### 4.1 Complete Investigation
```turtle
@prefix icac: <https://ontology.unifiedcyberontology.org/icac#> .

icac:investigation-001 a icac:ICACInvestigation ;
    icac:hasStep icac:receive-tip-001, icac:review-tip-001, icac:legal-process-001 ;
    icac:hasReport hotline:report-004 .

icac:receive-tip-001 a icac:ReceiveCybertipAction ;
    icac:nextStep icac:review-tip-001 ;
    uco-action:startTime "2024-03-20T13:00:00Z"^^xsd:dateTime .

icac:review-tip-001 a icac:ReviewCybertipAction ;
    icac:previousStep icac:receive-tip-001 ;
    icac:nextStep icac:legal-process-001 ;
    uco-action:performer icac:analyst-001 .

icac:legal-process-001 a icac:LegalProcessAction ;
    icac:previousStep icac:review-tip-001 ;
    icac:targetsService icac:social-platform-001 ;
    icac:legalInstrument icac:search-warrant-001 .
```

### 5. Production Case Investigation

#### 5.1 CSAM Production Offense
```turtle
@prefix icac-production: <https://ontology.unifiedcyberontology.org/icac/production#> .

icac-production:offense-001 a icac-production:ProductionOffense ;
    icac-production:productionMethod "direct_recording" ;
    icac-production:sessionCount 15 ;
    icac-production:victimCount 2 ;
    icac-production:producedAt icac-production:location-001 ;
    icac-production:usesEquipment icac-production:device-001 .

icac-production:producer-001 a icac-production:Producer ;
    icac-production:holdsPositionOf icac-production:babysitter-role ;
    icac-production:violatesPosition icac-production:trust-violation-001 .
```

### 6. Victim Impact Assessment

#### 6.1 Comprehensive Impact Assessment
```turtle
@prefix icac-impact: <https://ontology.unifiedcyberontology.org/icac/victim-impact#> .

icac-impact:assessment-001 a icac-impact:ComprehensiveImpactAssessment ;
    icac-impact:severityLevel "severe" ;
    icac-impact:assessesVictim icac-impact:victim-001 ;
    icac-impact:identifiesHarm icac-impact:complex-trauma-001 .

icac-impact:complex-trauma-001 a icac-impact:ComplexTrauma ;
    icac-impact:traumaType "complex" ;
    icac-impact:severity "severe" ;
    icac-impact:manifestsAs icac-impact:behavioral-indicator-001, icac-impact:emotional-indicator-001 .

icac-impact:therapeutic-intervention-001 a icac-impact:TraumaTherapy ;
    icac-impact:treatmentModality "CBT" ;
    icac-impact:addressesHarm icac-impact:complex-trauma-001 ;
    icac-impact:treatmentOutcome "partially_successful" .
```

### 7. Task Force Operations

#### 7.1 Multi-Agency Operation
```turtle
@prefix icac-taskforce: <https://ontology.unifiedcyberontology.org/icac/taskforce#> .

icac-taskforce:operation-001 a icac-taskforce:TaskForceOperation ;
    icac-taskforce:operationName "Operation Cyber Highway Safety Check" ;
    icac-taskforce:leadAgency icac-taskforce:arkansas-dps ;
    icac-taskforce:participatingAgency icac-taskforce:local-sheriff-001, icac-taskforce:fbi-field-office-001 ;
    icac-taskforce:arrestCount 42 ;
    icac-taskforce:searchWarrantCount 178 ;
    icac-taskforce:childrenRescued 5 .
```

### 8. Sex Offender Registry Integration

#### 8.1 Registry Compliance Monitoring
```turtle
@prefix icac-registry: <https://ontology.unifiedcyberontology.org/icac/sex-offender-registry#> .

icac-registry:compliance-operation-001 a icac-registry:ComplianceMonitoringOperation ;
    icac-registry:visitCount 1600 ;
    icac-registry:complianceRate 0.95 ;
    icac-registry:violationCount 80 ;
    icac-registry:newArrestCount 12 .

icac-registry:offender-001 a icac-registry:RegisteredOffender ;
    icac-registry:registrationTier "Tier II" ;
    icac-registry:hasRegistrationRecord icac-registry:record-001 ;
    icac-registry:subjectToRestriction icac-registry:internet-restriction-001 .
```

### 9. International Coordination

#### 9.1 Cross-Border Investigation
```turtle
@prefix icac-international: <https://ontology.unifiedcyberontology.org/icac/international#> .

icac-international:cross-border-001 a icac-international:CrossBorderInvestigation ;
    icac-international:originCountry "US" ;
    icac-international:targetCountry "UK" ;
    icac-international:coordinationMechanism icac-international:mutual-legal-assistance ;
    icac-international:informationShared icac-international:evidence-package-001 .
```

### 10. Forensic Analysis

#### 10.1 Digital Forensics Workflow
```turtle
@prefix icac-forensics: <https://ontology.unifiedcyberontology.org/icac/forensics#> .

icac-forensics:acquisition-001 a icac-forensics:ForensicAcquisitionAction ;
    icac-forensics:acquisitionMethod "physical_imaging" ;
    icac-forensics:writeBlockingUsed true ;
    icac-forensics:evidenceSeized icac-forensics:mobile-device-001 ;
    icac-forensics:producesImage icac-forensics:forensic-image-001 .

icac-forensics:analysis-001 a icac-forensics:ForensicAnalysisAction ;
    icac-forensics:analyzesImage icac-forensics:forensic-image-001 ;
    icac-forensics:usesTool icac-forensics:cellebrite-tool ;
    icac-forensics:recoversFiles icac-forensics:recovered-images-001 .
```

## Advanced Query Examples

### 1. Cross-Ontology Analytics
```sparql
# Find investigations with production offenses and victim impact assessments
PREFIX icac: <https://ontology.unifiedcyberontology.org/icac#>
PREFIX icac-production: <https://ontology.unifiedcyberontology.org/icac/production#>
PREFIX icac-impact: <https://ontology.unifiedcyberontology.org/icac/victim-impact#>

SELECT ?investigation ?offense ?assessment ?severity
WHERE {
    ?investigation a icac:ICACInvestigation ;
                  icac:hasStep ?step .
    ?step a icac-production:ProductionOffense .
    ?offense a icac-production:ProductionOffense .
    ?assessment a icac-impact:VictimImpactAssessment ;
               icac-impact:severityLevel ?severity .
}
```

### 2. Task Force Performance Metrics
```sparql
# Calculate task force operation effectiveness
PREFIX icac-taskforce: <https://ontology.unifiedcyberontology.org/icac/taskforce#>

SELECT ?operation ?arrestRate ?rescueRate
WHERE {
    ?operation a icac-taskforce:TaskForceOperation ;
              icac-taskforce:arrestCount ?arrests ;
              icac-taskforce:searchWarrantCount ?warrants ;
              icac-taskforce:childrenRescued ?rescued .
    BIND(?arrests / ?warrants AS ?arrestRate)
    BIND(?rescued / ?arrests AS ?rescueRate)
}
ORDER BY DESC(?arrestRate)
```

### 3. Registry Compliance Analysis
```sparql
# Find compliance violations by registry tier
PREFIX icac-registry: <https://ontology.unifiedcyberontology.org/icac/sex-offender-registry#>

SELECT ?tier (COUNT(?violation) AS ?violationCount)
WHERE {
    ?offender a icac-registry:RegisteredOffender ;
             icac-registry:registrationTier ?tier ;
             icac-registry:hasViolation ?violation .
}
GROUP BY ?tier
ORDER BY DESC(?violationCount)
```

## Validation and Quality Assurance

### 1. Using pySHACL
Shapes live in various `*-shapes.ttl` files:

```bash
# Validate hotline data
pyshacl -s ontology/icac/hotlines-core-shapes.ttl -d your-hotline-data.ttl

# Validate core ICAC data
pyshacl -s ontology/icac/icac-core-shapes.ttl -d your-investigation-data.ttl

# Validate forensic data
pyshacl -s ontology/icac/icac-forensics-shapes.ttl -d your-forensic-data.ttl
```

### 2. Common Validation Rules
- Reports must have at least one evidence item
- Evidence items must have a firstSeen timestamp
- Actions must have a performer and timestamps
- Forward actions must specify a target organization
- Production offenses must specify victim count
- Impact assessments must link to specific victims
- Registry offenders must have valid tier classifications

### 3. Performance Testing
```bash
# Run performance test for Q1 query (must complete in ≤ 500ms on 5M triples)
time sparql --query queries/find_open_reports.rq --data your-5m-triple-dataset.ttl
```

## Development Workflow

### 1. Local Development Setup
```bash
# Start complete development environment
docker compose up -d

# Validate all ontologies
docker exec icac-robot robot validate *.ttl

# Run SHACL validation
docker exec icac-pyshacl pyshacl -s *-shapes.ttl -d examples/*.ttl
```

### 2. Contributing New Examples
1. Create your example in `examples/` directory
2. Ensure it validates against relevant SHACL shapes
3. Add corresponding SPARQL queries in `queries/` directory
4. Update documentation with usage examples
5. Submit pull request with automated CI validation

### 3. Adding New Ontology Modules
1. Follow naming convention: `icac-[domain].ttl`
2. Create corresponding SHACL shapes: `icac-[domain]-shapes.ttl`
3. Add JSON-LD context if needed: `contexts/icac-[domain].jsonld`
4. Create comprehensive examples demonstrating usage
5. Update architecture diagrams and documentation

## Troubleshooting

### 1. Common Issues
- **Missing required properties**: Check SHACL validation output
- **Invalid data types**: Verify XSD type annotations
- **Broken action sequences**: Ensure nextStep/previousStep chains are valid
- **Cross-reference violations**: Validate relationships between ontology modules
- **Performance problems**: Check query patterns and dataset size

### 2. Solutions
- Use SHACL validation for data quality checking
- Verify property cardinality constraints
- Review action workflow sequences
- Monitor system resources during large dataset operations
- Check the build badge on README to confirm latest commit passes validation

### 3. Getting Help
- Check existing GitHub issues
- Review comprehensive examples in `examples/` directory
- Consult SPARQL queries in `queries/` directory for usage patterns
- Join community discussions and working groups

## Integration Patterns

### 1. UCO/CASE Integration
```turtle
# Seamless integration with UCO core concepts
@prefix uco-core: <https://ontology.unifiedcyberontology.org/core#> .
@prefix case-investigation: <https://ontology.caseontology.org/case/investigation#> .

# ICAC investigation extends CASE investigation
icac:investigation-001 a icac:ICACInvestigation, case-investigation:Investigation ;
    uco-core:hasFacet [
        a uco-core:TimestampFacet ;
        uco-core:timestamp "2024-03-20T10:00:00Z"^^xsd:dateTime
    ] .
```

### 2. Multi-System Data Exchange
```turtle
# Support for multiple data formats and systems
icac:investigation-001 icac:exportFormat "CASE-JSON", "UCO-Turtle", "STIX-JSON" ;
                      icac:compatibleWith "Autopsy", "Griffeye", "PhotoDNA-Service" .
```

## License and Support

### 1. Versioning
- Current Version: 0.9.0 (December 2024)
- See CHANGELOG.md for complete version history
- Follows semantic versioning (MAJOR.MINOR.PATCH)
- Coordinated releases across all 22 ontology modules

### 2. Support Channels
- GitHub issues for bug reports and feature requests
- Community mailing list for general discussion
- Working group meetings for stakeholder feedback
- Documentation updates and improvement suggestions

### 3. License
This project is licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).

## Additional Resources

- [Architecture Documentation](architecture.md) - Comprehensive system design
- [Design Document](design.md) - Technical design principles
- [Product Requirements](PRD.md) - Functional and technical requirements
- [Glossary](glossary.md) - Acronyms and key terminology
- [Contributing Guidelines](../CONTRIBUTING.md) - How to contribute to the project
- [Example Files](../examples/) - Real-world usage demonstrations
- [Analytics Queries](../queries/) - Operational intelligence examples
