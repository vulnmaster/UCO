# ICAC Ontology Family

This repository contains the Internet Crimes Against Children (ICAC) Ontology Family, a suite of interconnected ontologies designed to represent and share data about child exploitation investigations and hotline operations. These ontologies extend the Unified Cyber Ontology (UCO) and CASE (Cyber-investigation Analysis Standard Expression) to provide a standardized, interoperable framework for this critical domain.

## Overview

The ICAC Ontology Family aims to address the challenge of siloed data in child protection by providing a common semantic model. This allows for more effective data sharing, integration, and analysis across different organizations and systems involved in combating child exploitation.

Key goals include:

*   **Standardization:** Provide a common vocabulary and structure for ICAC-related data.
*   **Interoperability:** Enable seamless data exchange between different tools and systems used by Law Enforcement Agencies (LEAs), hotlines, and Electronic Service Providers (ESPs).
*   **Modularity:** Offer a core ontology with specific extensions for different needs (e.g., hotline operations, US-specific NCMEC reporting).
*   **Data Quality:** Enforce data consistency and validity through SHACL shapes.
*   **Extensibility:** Allow for future expansion to cover new aspects of ICAC investigations and new regional requirements.

## Modules

The ICAC Ontology Family is organized into several key modules:

*   **`icac-core.ttl`:** The foundational ontology defining core concepts, relationships, and investigation lifecycle actions relevant to all ICAC cases. Imports UCO and CASE.
*   **`hotlines-core.ttl`:** An ontology specifically for modeling hotline operations, including report intake, evidence management, classification, status tracking, and actions like forwarding to LE or issuing takedown requests. Imports UCO.
*   **`icac-us-ncmec.ttl`:** A US-specific extension for representing data according to the National Center for Missing & Exploited Children (NCMEC) Cybertip report format. Imports `icac-core.ttl`.
*   **`*-shapes.ttl`:** SHACL (Shapes Constraint Language) files (`icac-core-shapes.ttl`, `hotlines-core-shapes.ttl`) that provide validation rules for the data described by the ontologies.
*   **`contexts/`:** JSON-LD context files to aid developers in working with the ontologies in JSON-based environments.
*   **`examples/`:** Sample instance data in Turtle format, demonstrating how to use the ontologies to represent real-world scenarios (e.g., `hotline-lifecycle.ttl`, `investigation-lifecycle.ttl`).
*   **`queries/`:** A collection of SPARQL queries for various analytical and operational tasks.
*   **`docs/`:** Comprehensive documentation, including:
    *   `architecture.md`: System architecture and module relationships.
    *   `design.md`: Detailed design principles and technical specifications.
    *   `PRD.md`: Product Requirements Document.
    *   `user_doc.md`: Guide for end-users and developers.
    *   `glossary.md`: Definitions of key terms and acronyms.

## Getting Started

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/ucoProject/ontology-icac.git # Or your repository URL
    cd ontology-icac
    ```
2.  **Review the Documentation:** Start with this README and then explore the detailed documents in the `docs/` directory, particularly the `user_doc.md` for usage instructions.
3.  **Explore the Ontologies:** Use an ontology editor like Protégé to open the `.ttl` files and examine the class and property hierarchies.
4.  **Examine Examples:** The `examples/` directory provides concrete instances of how the ontologies are used.
5.  **Run Validation:** Set up the Docker environment (see `docker-compose.yaml` and `user_doc.md`) to validate the ontologies and example data using pySHACL and ROBOT.

## Contributing

Contributions are welcome! Please see the [CONTRIBUTING.md](CONTRIBUTING.md) file for guidelines on how to contribute to this project, including style guides, commit conventions, and testing procedures.

## License

This project is licensed under the Apache License 2.0. See the [LICENSE.md](LICENSE.md) file for the full license text.

## Issues and Support

Please raise any issues or questions via the GitHub issue tracker for this repository. 