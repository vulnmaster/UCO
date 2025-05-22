# ICAC Ontology Family Architecture

## Import Chain

```mermaid
graph TD
    subgraph UCO
        UCO[UCO Core]
    end

    subgraph ICAC
        ICAC[icac-core.ttl]
        ICAC_SHAPES[icac-core-shapes.ttl]
        HOTLINES[hotlines-core.ttl]
        HOTLINES_SHAPES[hotlines-core-shapes.ttl]
        NCMEC[icac-us-ncmec.ttl]
    end

    subgraph Examples
        HOTLINE_EX[hotline-lifecycle.ttl]
        INVEST_EX[investigation-lifecycle.ttl]
    end

    UCO --> ICAC
    ICAC --> HOTLINES
    ICAC --> NCMEC
    HOTLINES -.-> HOTLINES_SHAPES
    ICAC -.-> ICAC_SHAPES
    HOTLINES --> HOTLINE_EX
    ICAC --> INVEST_EX

    linkStyle 4,5 stroke-dasharray: 5 5
```

> **Note**: Shapes files (dotted lines) are used for validation but not imported by production graphs.

## Data Flow

```mermaid
graph LR
    subgraph Input
        JSON[JSON-LD Report]
        API[API Submission]
        FORM[Web Form]
    end

    subgraph Processing
        VALID[SHACL Validation]
        TRANS[Transform to RDF]
        STORE[Fuseki Store]
    end

    subgraph Output
        CASE[CASE Export]
        SPARQL[SPARQL Queries]
        VIZ[Visualization]
    end

    JSON --> TRANS
    API --> TRANS
    FORM --> TRANS
    TRANS --> VALID
    VALID --> STORE
    STORE --> CASE
    STORE --> SPARQL
    STORE --> VIZ
```

## Class Hierarchy

```mermaid
classDiagram
    class UCOObservable {
        +String id
        +DateTime createdTime
    }
    
    class HotlineReport {
        +ReporterRole reportedBy
        +HotlineOrganization receivedBy
        +EvidenceItem[] hasEvidence
        +HotlineAction[] triggersAction
    }
    
    class ICACInvestigation {
        +HotlineReport[] hasReport
        +InvestigationAction[] hasAction
        +String status
    }
    
    class AutomatedReporterAgent {
        +String softwareVersion
        +String vendorName
    }
    
    UCOObservable <|-- HotlineReport
    UCOObservable <|-- ICACInvestigation
    HotlineReport --> ICACInvestigation
    UCOObservable <|-- AutomatedReporterAgent
```

## Property Relationships

```mermaid
graph TD
    subgraph Report
        R[HotlineReport]
        E[EvidenceItem]
        A[HotlineAction]
    end

    subgraph Investigation
        I[ICACInvestigation]
        IA[InvestigationAction]
    end

    R -->|hasEvidence| E
    R -->|triggersAction| A
    I -->|hasReport| R
    I -->|hasAction| IA
    A -->|nextStep| A
    IA -->|nextStep| IA
```

## Diagram Export

These diagrams are automatically exported to SVG format in the CI pipeline. You can find the rendered versions in `/docs/img/`:

- `architecture-import-chain.svg`
- `architecture-data-flow.svg`
- `architecture-class-hierarchy.svg`
- `architecture-property-relationships.svg`

See [Glossary](glossary.md) for acronyms and key terms. 