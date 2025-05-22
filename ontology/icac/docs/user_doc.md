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

## Cookbook

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

Verify both LEAs:
```sparql
SELECT ?report ?canadian_org ?spanish_org
WHERE {
    ?report a hotline:PublicReport ;
            hotline:receivedBy ?canadian_org ;
            hotline:triggersAction ?action .
    ?action a hotline:ForwardToLEAction ;
            hotline:forwardsTo ?spanish_org .
    ?canadian_org hotline:jurisdiction "CA" .
    ?spanish_org hotline:jurisdiction "ES" .
}
```

## Validation

### 1. Using pySHACL
Shapes live in `ontology/icac/hotlines-core-shapes.ttl`:

```bash
pyshacl -s ontology/icac/hotlines-core-shapes.ttl -d your-data.ttl
```

### 2. Common Validation Rules
- Reports must have at least one evidence item
- Evidence items must have a firstSeen timestamp
- Actions must have a performer and timestamps
- Forward actions must specify a target organization

## Troubleshooting

### 1. Common Issues
- Missing required properties
- Invalid data types
- Broken action sequences
- Validation errors
- Performance problems

### 2. Solutions
- Check SHACL validation
- Verify data types
- Review action sequences
- Check property cardinality
- Monitor system resources
- Check the Build badge on README to confirm latest commit passes ROBOT + pySHACL

## FAQ

### 1. Versioning
- Current Version: 0.4.0 (May 2025)
- See CHANGELOG.md for full history
- Follows semantic versioning

### 2. Support
- GitHub issues
- Mailing list
- Documentation updates

## License

This project is licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).

See [Glossary](glossary.md) for acronyms and key terms.
