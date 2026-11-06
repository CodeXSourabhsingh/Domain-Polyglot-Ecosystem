# 🧬 PGx Engine: Precision Dosing API

**A Production-Grade Pharmacogenomics API adjusting drug doses based on genetic mutations.**

Built by Sourabh Singh | Python | FastAPI | Docker | SQLAlchemy | MySQL

---

## Overview
Standard drug dosing is blind to genetics. A patient with a genetic mutation in the CYP2C9 enzyme (a "Poor Metabolizer") processes drugs like Warfarin at a drastically slower rate. Prescribing a standard dose leads to drug accumulation, toxicity, and potentially fatal internal bleeding.

The PGx Engine is a REST API that scans for genetic mutations, calculates how the mutation alters the drug's half-life, and dynamically adjusts the Loading and Maintenance dose to safe levels.

## The Analogy: The Traffic Jam & The Delivery Truck
*   **The Traffic Jam (Genetics):** The API scans for the CYP2C9 mutation. If the patient is a "Poor Metabolizer," the enzyme highway is jammed.
*   **The Delivery Truck (PK Math):** Because the highway is jammed, the drug (the delivery truck) stays in the body longer. The engine mathematically extends the drug's half-life (e.g., from 40 hours to 140 hours) and dynamically drops the maintenance dose (e.g., from 4.07mg to 0.81mg) to prevent toxicity.

---

## 🏗️ Production Architecture (The API Factory)
This is not a local script. It is a containerized, secure microservice.
*   **The Bouncer (FastAPI):** Ingests JSON patient data (genetics, weight, target concentration) and validates it using Pydantic.
*   **The Black Box (Docker):** Containerized for seamless deployment across local and cloud environments.
*   **The Password (JWT Auth):** OAuth2 Bearer token security. Only authenticated clinicians can trigger the dosing engine.
*   **The Vault (SQLAlchemy + MySQL):** Every genetic dose adjustment is securely logged into a relational database for clinical audit trails.

---

## 🧪 Validation (Test-Driven Development)
In clinical pharmacology, a math error is a liability. The engine is validated using a Pytest suite that tests the boundaries of genetic multipliers and pharmacokinetic crashes.
*   **Test Coverage:** Normal Metabolizer (`*1/*1`), Intermediate (`*1/*2`), Poor Metabolizer (`*3/*3`), and extreme weight boundaries.
*   **Crash Prevention:** Tests explicitly ensure the API does not crash if a patient has a half-life of 0 (ZeroDivisionError prevention).
*   **Result:** 45 passing Pytest cases.

---

## 🚀 How to Run Locally
1. **Clone the repository:**
   ```bash
   git clone https://github.com/CodeXSourabhsingh/pgx-production-api.git
   cd pgx-production-api
2. Set up your environment secrets: Create a .env file (MySQL credentials).
3. Build and run with Docker:
   ```bash
   docker build -t pgx-api .
   docker run --env-file .env -p 8000:8000 pgx-api
   ```
4. Access the API: Go to http://localhost:8000/docs to view the interactive Swagger UI. Click Authorize to log in and test the endpoints.

🚨 Live API Demo

· Interactive Swagger UI: [INSERT LIVE RENDER LINK HERE]

⚠️ Honest Limitations

· Research Use Only: This tool is a decision-support prototype. It does not provide clinical diagnoses.
· Drug Coverage: Currently validated for CYP2C9/VKORC1 (Warfarin). Not yet expanded to all CYP450 enzymes.
· Human-in-the-loop: The tool flags risk; the physician makes the final call.

---

👨‍💻 About the Architect

I am Sourabh Singh. I am 20 years old, 3 months into coding, and self-taught. I don't just build prototypes; I build production-grade systems. I am looking for clinic partners or biotech founders who need a technical co-founder to build their MVP from 0 to 1. I build the architecture; we share the upside.

"The mode is a data decision, not a capability decision. We build the bridge; the physician decides."
   
