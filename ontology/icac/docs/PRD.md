# ICAC Ontology Family - Product Requirements Document

## Overview
Current ICAC data sets are siloed (NCMEC XML, ICCAM CSV). Our ontologies unify these disparate formats into a standardized, interoperable framework for representing and sharing data about child exploitation investigations and hotline operations. This document outlines the requirements for the 23-module ontology family and its supporting technologies. This family of ontologies was assembled using Claude 4 Sonnet to conduct an analysis of law enforcement and prosecutor's press releases that describe the results of investigations and legal process for crimes against children and trafficking. This family of ontologies extend the Unified Cyber Ontology and the Cyber-investigation Analysis Standard Expression (CASE) Ontology. This make it possible to model all aspects of an child sexual abuse or child sex trafficking investigation, including the digital forensics examination.

## Target Users
1. Law Enforcement Agencies
2. Hotline Organizations
3. Electronic Service Providers
4. Digital Forensics Teams
5. Research Organizations
6. Software Developers
7. Athletic Organizations and Schools
8. Child Protection Services

## Core Requirements

### 1. Ontology Structure
- Must support modular design with clear separation of concerns across 23 specialized modules
- Must maintain compatibility with UCO (Unified Cyber Ontology)
- Must support versioning and backward compatibility
- Must include comprehensive SHACL validation rules
- Must provide JSON-LD context for developer integration
- Must support athletic coaching exploitation and sports authority abuse patterns

### 2. Data Representation
- Must support representation of:
  - Hotline reports and their lifecycle
  - Evidence items (images, videos, URLs)
  - Investigation workflows
  - Cross-border information sharing
  - Automated reporting systems
  - Classification schemes
  - Status tracking
  - Athletic coaching exploitation patterns
  - Physical training coercion mechanisms
  - Team dynamics and authority abuse
  - Educational institution vulnerabilities
  - Parent network discovery patterns

### 3. Interoperability
- Must support export to CASE (Cyber-investigation Analysis Standard Expression)
- Must provide clear mapping to existing standards
- Must support multiple serialization formats (Turtle, JSON-LD, RDF/XML)
- Must include validation tools for data quality
- Must integrate with educational and athletic institution systems

### 4. Security & Privacy
- Must support anonymous reporting
- Must include data minimization principles
- Must encode confidentiality tier (TLP-*) so middleware can block export of TLP-RED nodes
- All triples containing depictsChild must default to TLP-RED; leakage is a critical-severity bug
- Must maintain audit trails
- Must protect sensitive information
- Must support institutional investigation confidentiality

### 5. Developer Experience
- Must provide clear documentation
- Must include example data
- Must offer testing tools
- Must support common development environments
- Must provide validation tools
- Must include athletic exploitation usage examples

## Technical Requirements

### 1. Ontology Components
- Core ICAC ontology
- Hotline operations ontology
- Investigation workflow ontology
- Athletic exploitation ontology
- Regional extensions (e.g., NCMEC)
- Validation shapes
- Example data sets

### 2. Supporting Technologies
- SHACL validation engine
- JSON-LD context processor
- Testing framework
- Documentation generator
- Example data generator
- Docker compose (Fuseki + pySHACL + ROBOT) MUST validate every PR (see /devops)

### 3. Integration Requirements
- Must support SPARQL queries
- Must provide REST API endpoints
- Must support bulk data operations
- Must include error handling
- Must support logging and monitoring
- Must integrate with educational institution systems

## Quality Requirements

### 1. Validation
- Must validate ontology structure
- Must validate instance data
- Must check for consistency
- Must verify cross-references
- Must ensure proper typing
- Must validate athletic exploitation patterns

### 2. Performance
- SPARQL query Q1 (find all open HotlineReports) on 5 M triples MUST return in ≤ 500 ms on 16 GB heap Fuseki
  - See `/queries/Q1.rq` for the exact query
- Must support large datasets (up to 100 M triples)
- Must handle 10 k new reports per day
- Must provide efficient querying
- Must handle concurrent operations
- Must support batch processing
- Must maintain reasonable response times
- Must efficiently process athletic coaching cases with complex team dynamics

### 3. Reliability
- Must maintain data integrity
- Must support backup and recovery
- Must handle errors gracefully
- Must provide status monitoring
- Must support audit logging

## Future Requirements

### 1. Extensibility
- Must support new evidence types
- Must accommodate new workflows
- Must allow for regional variations
- Must support new classification schemes
- Must enable custom extensions
- Must support emerging athletic exploitation patterns

### 2. Integration
- Must support new data sources
- Must enable new analysis tools
- Must accommodate new reporting systems
- Must support new visualization tools
- Must enable new export formats
- Must integrate with athletic organization systems

## Success Criteria
1. Successful integration with existing systems
2. Positive feedback from user community
3. Successful validation of example data
4. Clear documentation and examples
5. Efficient processing of large datasets
6. Successful cross-border data sharing
7. Effective support for investigations
8. Reliable operation in production
9. At least three external tools (Autopsy, Griffeye, PhotoDNA Service) ingest JSON-LD without modification
   - Note: Adapters allowed so long as no ontology changes required
10. Successful modeling of athletic coaching exploitation cases
11. Effective parent network discovery and institutional coordination

## Timeline
- Developer Preview (0.4): May 2025
  - Core functionality complete
  - Basic validation
  - Internal testing
- Public Beta (0.5): Q4 2025
  - Beta with INHOPE pilot
  - Enhanced validation
  - Public documentation
- First Update (0.6): Q2 2026
  - Additional examples
  - Performance improvements
  - Extended tool support
- Major Version (1.0): Q4 2026
  - Full feature set
  - Production ready
  - Complete documentation
- Athletic Enhancement (1.7): Q1 2025
  - Athletic coaching exploitation framework
  - Physical training coercion modeling
  - Team dynamics analysis
  - Parent network discovery

## Support Requirements
- Documentation updates
- User support
- Bug fixes
- Feature requests
- Training materials
- Example updates
- Validation rule updates
- Athletic exploitation case studies

## License

This project is licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).
