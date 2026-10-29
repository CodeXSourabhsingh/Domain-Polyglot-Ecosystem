# EPI-CORE: Pathogen & Microbiome Risk Intelligence

A clinical decision-support system that correlates viral genomic surveillance with host microbiome diversity to estimate epidemiological risk.

Built by Sourabh Singh | Python | FastAPI | Docker | SQLAlchemy | MySQL | Biopython

---

## Executive Summary

EPI-CORE is designed to connect two critical signals in infectious disease surveillance:

1. The pathogen's ability to evade immune protection
2. The host's immune resilience, represented by microbiome diversity

The platform analyzes viral mutations, evaluates their risk profile, and compares that against gut microbiome diversity metrics such as the Shannon Diversity Index. The result is a combined risk assessment that helps researchers and public-health teams identify cases where a high-risk viral variant coincides with weakened host defense capacity.

This project is intended for research and decision support, not clinical diagnosis. It is designed as a secure, extensible backend system that can ingest biological data, compute risk signals, and persist full audit records for reproducible analysis.

---

## Why this project exists

Public health data is often fragmented: viral sequencing data is generated in one environment, while host microbiome data is measured elsewhere. This makes it difficult to understand the relationship between pathogen escape potential and host immune readiness.

EPI-CORE addresses that gap by merging these datasets into a single analytical pipeline.

The analogy is straightforward:

- A viral mutation is a disguise used by a pathogen to evade immune detection.
- The gut microbiome acts as a defense layer that reflects host resilience.
- If a highly immune-escaping virus encounters a host with low microbiome diversity, the risk profile becomes significantly more concerning.

The goal is not to replace clinical judgment, but to give researchers a structured way to interpret high-risk scenarios.

---

## Problem Statement

In infectious disease intelligence, two questions are often treated separately:

- How dangerous is the pathogen?
- How resilient is the host?

Most systems are optimized for one perspective at a time. Viral surveillance tools focus on mutation analysis, while microbiome tools focus on diversity metrics. There is a limited number of systems that combine these dimensions into a single risk model.

This disconnect creates blind spots in translational epidemiology. A pathogen may appear dangerous in isolation, but its effective threat depends on the host environment, especially when diversity in the gut microbiome is low.

EPI-CORE attempts to bridge that gap using data-driven logic and a reproducible backend architecture.

---

## Core Functionality

The platform follows a three-layer analytical flow:

### 1. Viral Mutation Analysis

- Fetches viral genomic sequences from trusted sources such as NCBI
- Identifies high-risk mutations associated with transmissibility or immune escape
- Evaluates variant signatures such as E484K, N501Y, and other lineage markers
- Flags mutations with a strong risk profile based on known biological patterns

### 2. Microbiome Diversity Analysis

- Ingests operational taxonomic unit (OTU) or abundance data from host samples
- Computes Shannon Diversity Index to measure community richness and evenness
- Interprets low diversity as reduced immune-supporting ecological balance
- Identifies cases with weaker host resilience

### 3. Combined Risk Assessment

- Combines pathogen escape potential with host microbiome diversity
- Applies a risk rule engine to classify outcomes as Low, Elevated, High, or Critical
- Persists results in a secure audit trail for traceability and review

---

## System Architecture

EPI-CORE is built as a backend service, designed for scalable deployment and secure handling of analytical workflows.

### Components

- API Layer: FastAPI service for request validation, routing, and response handling
- Processing Engine: Python-based analysis layer for sequence evaluation and microbiome calculations
- Database Layer: SQLAlchemy + MySQL for persistence and audit logging
- Containerization: Docker-based deployment for reproducible environments
- Auth Layer: JWT-based access control to restrict system use
- Testing Layer: Pytest-driven validation for edge cases and risk logic

### High-Level Flow

1. Request arrives via authenticated API
2. Viral sequence and microbiome data are validated
3. Mutation analysis is executed
4. Diversity metrics are computed
5. Risk logic combines both signals
6. Result is stored in MySQL with metadata and timestamps
7. Response is returned to the caller

---

## Technical Stack

- Backend: Python, FastAPI, Uvicorn
- Database: MySQL, SQLAlchemy ORM
- Bioinformatics: Biopython, NCBI E-utilities
- Data Science: Pandas, NumPy
- Infrastructure: Docker, JWT
- Testing: Pytest

---

## Data Flow and Risk Model

The engine uses a layered decision framework:

- Viral risk signal: derived from mutation profile and lineage risk
- Host resilience signal: derived from microbiome diversity index
- Combined risk: ecosystem-level assessment based on interaction between the two

### Simplified Example

If a sample contains:

- a highly immune-escaping viral profile
- low gut microbiome diversity

Then the engine flags a higher combined-risk state, such as Critical.

In practical terms:

- High viral escape + stable microbiome = elevated, but not necessarily critical
- High viral escape + low diversity = concerning and often critical

This logic supports interpretation, not diagnosis.

---

## Risk Logic Example

A simple representation of the scoring logic could be structured like this:

- Low diversity sample: Shannon Index below threshold
- High variant risk: mutation signature indicates immune escape
- Combined classification:
  - Low: minimal concern
  - Elevated: moderate concern
  - High: notable risk
  - Critical: high escape potential + low host resilience

These thresholds are configurable and should be validated against real-world datasets before deployment in a clinical or research environment.

---

## API Design

The system exposes a RESTful API for secure interaction.

### Example Request

```json
{
  "virus": {
    "lineage": "Omicron",
    "sequence": "ATG..."
  },
  "microbiome": {
    "otu_data": [
      { "species": "Bacteroides", "abundance": 150 },
      { "species": "Firmicutes", "abundance": 120 }
    ]
  }
}
```

### Example Response

```json
{
  "lineage": "Omicron",
  "viral_risk": "High",
  "microbiome_diversity": 1.84,
  "risk_level": "Critical",
  "summary": "High immune-escape viral profile combined with low microbiome diversity."
}
```

The API layer validates input, performs authentication, and ensures results are stored in the system with audit metadata.

---

## Database and Audit Model

EPI-CORE stores calculation metadata to preserve traceability and accountability.

### Core persistence concepts

- request metadata
- lineage or viral sequence inputs
- mutation analysis outputs
- Shannon diversity values
- combined risk classification
- timestamps
- researcher or system identifier

This is designed to support reproducibility without unnecessarily storing personal identifying information.

---

## Validation and Testing

Clinical and bioinformatic systems require trust. EPI-CORE is validated using a focused Pytest suite covering critical edge cases and risk boundaries.

### Test Coverage

- Shannon diversity calculation under zero and singleton species scenarios
- Unknown lineage handling and graceful failure paths
- Combined risk classification thresholds
- Boundary conditions where risk escalates from Elevated to Critical
- 
<img width="1860" height="747" alt="Screenshot 2026-10-24 155547" src="https://github.com/user-attachments/assets/18f69f9b-5bc7-4b50-ac8c-bc7b203f4ab6" />

### Current Validation Status

The project includes automated validation for key model behaviors and is structured to support continuous verification as new datasets and logic branches are added.

---

## Honest Limitations

EPI-CORE is intentionally scoped as a research and decision-support tool, not a clinical diagnostic engine.

### Current limitations

- Research use only: the system does not provide medical diagnosis
- Data dependency: calculation quality depends on external biological data sources
- Human oversight required: the final decision remains with the researcher or clinician
- Prototype maturity: while designed as a production-oriented backend, real-world deployment should include additional validation and regulatory review

The project is best understood as a decision-support framework for translational analysis and exploratory clinical informatics.

---

## Production Readiness Goals

The current system is structured around production-minded principles:

- API-driven architecture
- Dockerized deployment model
- JWT-based authentication
- SQLAlchemy persistence layer
- testable logic and reproducible outcomes
- secure audit trail

Future production work should include:

- advanced access control and role management
- stronger data validation schemas
- deployment pipeline automation
- formal observability and monitoring
- deeper biological validation against curated datasets

---

## Roadmap

### Phase 1: Core MVP

- viral mutation scanning
- microbiome diversity metric calculation
- risk rule engine
- database persistence
- API layer and auth

### Phase 2: Research Readiness

- expanded lineage database
- improved mutation annotation
- richer microbiome input standards
- stronger validation suite

### Phase 3: Pilot Deployment

- cloud deployment
- monitoring and error tracking
- role-based access control
- benchmark comparisons against real datasets

### Phase 4: Clinical Translation

- integration with regulated environments
- stronger data governance
- clinician-facing outputs
- formal validation and collaboration with domain experts

---

## About the Architect

"I am Sourabh Singh. I am 20 years old, 3 months into coding, and self-taught. I don't just build prototypes; I build production-grade systems. I am the Domain Polyglot—I bridge the gap between complex medicine and clean code. I am not looking for a standard 9-to-5 role. I am actively exploring collaborations with researchers, clinicians, biotech teams, and founders who need a technical co-founder to build their MVP from 0 to 1. I build the architecture; we share the upside."

## Closing Statement

The mode is a data decision, not a capability decision. We build the bridge between complex biological signals and actionable interpretation. The physician, researcher, or public-health professional remains the final decision-maker.

EPI-CORE is a framework for making that bridge more transparent, structured, and useful.

---

## Contact

For collaborations, technical discussions, or research partnerships, reach out via the project repository or associated contact channels.

---

## License and Usage

This project is intended for research and educational exploration. It should be used responsibly and within the boundaries of ethical scientific and clinical practice.

---

## Final Note

EPI-CORE is best described as a decision-support platform that helps connect pathogen escape potential with host resilience. Its value lies in combining biological signals into a single analytical model that can support deeper understanding of risk in infectious disease scenarios.

This project is a strong foundation for future research, validation, and domain collaboration.

