# 🧬 PGx Engine: Precision Dosing API

[![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com/)
[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)

A prototype pharmacogenomics API that estimates how genetic variation can influence dose adjustments for drugs such as warfarin.

Built by Sourabh Singh | Python | FastAPI | Docker | SQLAlchemy | MySQL

---

## Overview

Standard drug dosing often assumes a uniform rate of metabolism. In reality, a patient's genotype can meaningfully change how a drug is processed. For example, a patient with a CYP2C9 variant associated with reduced enzyme activity may metabolize certain drugs more slowly. This can lengthen a drug's effective half-life and influence the appropriate loading and maintenance dose.

The PGx Engine is a lightweight REST API that models this relationship. It accepts patient-level inputs such as genotype, weight, and target concentration, then applies a simplified pharmacokinetic adjustment model to estimate an adjusted dose.

This project is best understood as a domain modeling and engineering exercise: it demonstrates how to turn pharmacogenomic logic into an API, persist dose decisions, and structure testing around edge cases.

> Important: This project is intended for learning, prototyping, and software design exploration. It is not a clinical decision-support system, and its outputs should not be treated as medical advice or a final prescribing recommendation.

---

## Why the problem matters

The central challenge is simple: the same standard dose may not behave the same way across patients.

A patient with a reduced-function CYP2C9 phenotype may process a drug more slowly than a normal metabolizer. In such cases, the standard dose may produce a higher-than-expected exposure. The project models this by:

- examining genotype or phenotype information
- estimating a metabolic multiplier
- adjusting the effective half-life
- recalculating a personalized dose based on simplified PK logic

This is a useful learning example because it makes the decision logic auditable and explainable.

---

## The analogy: traffic jam and delivery truck

- The traffic jam: genetics and metabolism. A reduced-function genotype can slow drug processing.
- The delivery truck: the drug dose. If the route is slowed, the truck takes longer to move through the system.
- The adjustment: the API estimates a longer effective half-life and changes the dose to better reflect the slower metabolic pathway.

This is a conceptual analogy for how the PK calculation is designed, not a statement of validated clinical behavior.

---

## Architecture

This project is structured as a containerized, secure API service that can be run locally or deployed in a more production-like environment.

- FastAPI: handles request validation, routes, and API responses
- Docker: provides a consistent runtime environment
- JWT authentication: restricts access to authenticated clinicians or users
- SQLAlchemy + MySQL: stores dosing decisions for auditing and traceability

In practice, the architecture separates:

- API ingestion and validation
- business logic for pharmacokinetic adjustment
- persistence of dose decisions
- test validation for edge conditions

---

## Audit trail and data persistence

Clinical and operational software should be auditable. This project stores dose decisions in a MySQL database using SQLAlchemy so each calculation can be reviewed later.

The audit log captures fields such as:

- patient_id
- gene and genotype/phenotype
- base half-life and adjusted half-life
- standard dose and personalized dose
- timestamp

This enables traceability of the logic used at the time of recommendation. In a real clinical system, these logs should also be subject to strict access control, retention policies, and privacy safeguards.

> Recommended improvement for production: store only the minimum needed data, encrypt sensitive fields, and include access logging and role-based authorization.

---

## Test-driven validation

The logic is validated with a Pytest suite designed to cover key boundary conditions and failure scenarios.

Examples of coverage include:

- normal metabolizer genotype cases
- intermediate metabolizer cases
- poor metabolizer cases
- extreme weight values
- zero or near-zero half-life handling to prevent runtime crashes

Example test output:

```bash
collected 45 items
...
==================== 45 passed in 1.84s ====================
```

These tests provide useful confidence that the code handles common edge cases in the modeled logic. However, they validate software behavior, not clinical safety or regulatory compliance.

---

## Local setup

### 1) Clone the repository

```bash
git clone https://github.com/CodeXSourabhsingh/pgx-production-api.git
cd pgx-production-api
```

### 2) Create a virtual environment

```bash
python -m venv venv
source venv/bin/activate
# On Windows: venv\Scripts\activate
```

### 3) Install dependencies

```bash
pip install -r requirements.txt
```

### 4) Configure environment variables

Create a `.env` file in the project root:

```env
MYSQL_HOST=localhost
MYSQL_USER=root
MYSQL_PASSWORD=your_password
MYSQL_DATABASE=pgx_vault
JWT_SECRET_KEY=your_super_secret_key
```

### 5) Run the API

```bash
uvicorn app.main:app --reload
```

Then open the Swagger UI at:

```text
http://localhost:8000/docs
```

---

## Project structure

```text
pgx-production-api/
├── app/
│   ├── main.py          # FastAPI application instance
│   ├── database.py      # SQLAlchemy setup and MySQL connection
│   ├── models.py        # Database models for stored audit records
│   ├── schemas.py       # Pydantic validation models
│   ├── auth.py          # JWT authentication logic
│   └── logic/
│       ├── cyp2c9.py    # CYP2C9 phenotype/genotype logic
│       └── pk_math.py   # Pharmacokinetic dose calculations
├── tests/
│   ├── test_pgx.py      # Pytest boundary and safety tests
│   └── __init__.py
├── Dockerfile           # Container configuration
├── requirements.txt     # Python dependencies
├── README.md            # Project documentation
└── .env                 # Local environment configuration
```

---

## Example use case

A clinician or developer submits patient parameters such as:

- genotype: `CYP2C9 *3/*3`
- weight: `70 kg`
- target concentration: an example value used in PK estimation

The API returns an adjusted dose estimate based on the modeled assumptions.

A useful improvement for this project would be to include one real request/response example in the README so prospective users can understand the API contract immediately.

---

## About the architect

Sourabh Singh

I am a Full-Stack Systems Architect and Domain Polyglot. I explore specialized disciplines, model their decision logic, and translate that knowledge into production-oriented software systems. My goal is to design systems that are explainable, testable, and useful beyond a single local script.

---

## Final statement

The PGx Engine demonstrates how genetic variation can be translated into a formal software model for dose estimation. It is a useful example of API design, PK modeling, persistence, and edge-case testing in a healthcare-related domain.

It is best viewed as an engineering prototype and learning platform rather than as a clinically validated treatment tool. In healthcare software, trust comes from transparency, validation, controlled deployment, and domain expertise—not from marketing language alone.

Designed for teams that want to explore how software can model biological variability while remaining explainable, auditable, and testable.

---

## Recommended next improvements

1. Add a sample API request and response payload.
2. Add explicit disclaimers about clinical scope and safety.
3. Clarify which gene-drug relationships are modeled and what assumptions they rely on.
4. Add API authentication examples for Swagger and curl usage.
5. Include DB migration steps and a schema diagram.
6. Add CI badges and a reproducible test command in the README.
7. Separate educational content from production-readiness claims.

These changes would make the project feel more credible, easier to understand, and better aligned with real-world engineering standards.

---

## Suggested title variation

If you want a more polished title, consider:

- PGx Engine: Pharmacogenomics Dose Modeling API
- Precision Dosing API for Pharmacogenomic Decision Support
- CYP2C9 Dose Adjustment Engine

These alternatives are more precise and less promotional than the current title.

---

## Optional closing note

If you'd like, I can also rewrite this into:

- a cleaner GitHub README version
- a more executive / portfolio style version
- a more technical architecture document version
- a concise project landing page for LinkedIn or a portfolio site

I can turn this into a final polished README in one pass.

```json
{
  "status": "ready_for_polish",
  "recommended_focus": [
    "clinical_disclaimer",
    "technical_precision",
    "repo_setup_clarity",
    "audit_and_security_language"
  ]
}
```

---

This rewrite intentionally reduces overclaiming and focuses on what the project actually demonstrates: a software system for modeling pharmacogenomic dosing logic, validating edge cases, and persisting decision records in a structured API architecture.




























































































































































































































































































































































"}