# PGx Engine: Precision Dosing API

A pharmacogenomics decision-support prototype exploring genotype-informed dose calculations for warfarin-related CYP2C9 and VKORC1 variants.

**Technology:** Python · FastAPI · Docker · SQLAlchemy · MySQL

> **Important:** This project is for research and software demonstration only. It is not a medical device or prescribing tool. Do not use its outputs to make treatment decisions. Warfarin dosing requires individualized clinical assessment and qualified clinician oversight.

---

## Overview

Many factors influence a patient's response to warfarin, including genetic variation. PGx Engine is a REST API prototype that accepts patient and genotype information, applies the project's pharmacokinetic and dose-adjustment logic, and returns a calculated result.

The project explores how genetic information can be incorporated into an auditable software workflow. Its calculations should not be interpreted as clinically validated recommendations: the model's assumptions, supported inputs, and outputs must be reviewed against the implementation and appropriate clinical evidence before any research or clinical use.

## How the concept works

- **Genotype input:** The service evaluates the supported CYP2C9 and VKORC1 information provided to it.
- **Calculation:** Project-specific logic applies genetic and pharmacokinetic adjustments to the dosing calculation.
- **Result and record:** The API returns a result and, according to the project design, records dose-adjustment events in a relational database.

Genotype alone does not determine an appropriate warfarin dose. Clinical factors, validated dosing guidance, and clinician judgment remain essential.

## Architecture

- **FastAPI and Pydantic:** HTTP API and request-data validation.
- **Docker:** Containerized application packaging.
- **JWT / OAuth2 bearer authentication:** Authentication for protected API operations, as implemented by the project.
- **SQLAlchemy and MySQL:** Relational persistence for application records and auditability.

The description above summarizes the intended components; consult the source code and deployment configuration for the exact routes, settings, and security behavior.

## Validation and tests

The project describes a Pytest suite covering:

- Normal (`*1/*1`), intermediate (`*1/*2`), and poor (`*3/*3`) CYP2C9 metabolizer examples.
- Extreme weight boundaries.
- Edge cases involving zero half-life and division-by-zero prevention.

The project reports **45 passing Pytest cases**. This is software test coverage, not evidence of clinical validation, safety, or effectiveness. Test results may change as the code evolves; run the suite locally to verify the current state.

## Run locally

The commands below follow the project's published setup instructions. Check the repository and application configuration for the correct environment-variable names and required MySQL settings.

1. Clone the API repository:

   ```bash
   git clone https://github.com/CodeXSourabhsingh/pgx-production-api.git
   cd pgx-production-api
   ```

2. Create a `.env` file containing the required MySQL credentials and application secrets. Do not commit this file or share real credentials.

3. Build and start the container:

   ```bash
   docker build -t pgx-api .
   docker run --env-file .env -p 8000:8000 pgx-api
   ```

4. Open the interactive API documentation at <http://localhost:8000/docs> if the application is running locally and exposes the docs at that route. Use only non-production test data.

## Demo

A hosted demo URL has not been provided. Add a verified Swagger UI link here when one is available; do not publish real patient or genetic data in a public demo.

## Limitations and responsible use

- **Research and demonstration only:** The service does not diagnose, prescribe, or replace a clinician.
- **Limited scope:** The project describes coverage for warfarin-related CYP2C9 and VKORC1 logic; it does not claim support for other drugs or genes.
- **Clinical validation required:** Software tests do not establish clinical validity. Any future clinical use would require appropriate evidence, expert review, governance, and regulatory assessment.
- **Privacy and security:** Genetic and health information is sensitive. Use synthetic data for demos and tests, and do not deploy with real patient data without a suitable privacy, security, and compliance review.
- **Human oversight:** A qualified clinician must independently assess any clinical decision.

## About

PGx Engine is a software project by Sourabh Singh exploring pharmacogenomics, API development, and decision-support workflows. The goal is to investigate how genotype-aware calculations can be made structured and traceable while keeping clinical decisions under qualified human oversight.

> “The mode is a data decision, not a capability decision. We build the bridge; the physician decides.”
