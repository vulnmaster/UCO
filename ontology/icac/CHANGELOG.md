# Changelog

All notable changes to the ICAC ontology family will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.4.0] - 2024-03-20

### Added
- AutomatedReporterAgent class for software-based reporting
- isAnonymous flag on ReporterRole
- firstSeen and foundAtURL properties on EvidenceItem
- severityLevel constraints (0-5) in SHACL
- SKOS concept schemes for status and classification
- incidentCode property in NCMEC extension
- JSON-LD context for hotlines
- Docker/CI toolchain with Fuseki and pySHACL
- ROBOT validation integration
- Comprehensive documentation suite

### Changed
- Updated IntakeChannel to use uco-core:Observable
- Enhanced SHACL validation rules
- Improved example data
- Updated documentation structure

### Fixed
- Removed duplicate CONTRIBUTING.md files
- Fixed version history in CHANGELOG
- Corrected import statements

## [0.3.0] - 2024-02-15

### Added
- Initial public release of ICAC ontology family
- Core investigation classes
- Hotline reporting structure
- Basic SHACL validation
- Example data sets

### Changed
- Aligned with UCO 1.1.0
- Updated documentation

## [0.1.0] - 2023-12-01

### Added
- Internal development version
- Basic ontology structure
- Initial class definitions
- Property definitions 