
🧬 PGx Engine: Precision Dosing API

https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white https://img.shields.io/badge/mysql-%2300f.svg?style=for-the-badge&logo=mysql&logoColor=white https://img.shields.io/badge/Pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white

A Production-Grade Pharmacogenomics API adjusting drug doses based on genetic mutations.

Built by Sourabh Singh | Python | FastAPI | Docker | SQLAlchemy | MySQL

---

Overview

Standard drug dosing is blind to genetics. A patient with a genetic mutation in the CYP2C9 enzyme (a "Poor Metabolizer") processes drugs like Warfarin at a drastically slower rate. Prescribing a standard dose leads to drug accumulation, toxicity, and potentially fatal internal bleeding.

The PGx Engine is a REST API that scans for genetic mutations, calculates how the mutation alters the drug's half-life, and dynamically adjusts the Loading and Maintenance dose to safe levels.

The Analogy: The Traffic Jam & The Delivery Truck

· The Traffic Jam (Genetics): The API scans for the CYP2C9 mutation. If the patient is a "Poor Metabolizer," the enzyme highway is jammed.
· The Delivery Truck (PK Math): Because the highway is jammed, the drug (the delivery truck) stays in the body longer. The engine mathematically extends the drug's half-life (e.g., from 40 hours to 140 hours) and dynamically drops the maintenance dose (e.g., from 4.07mg to 0.81mg) to prevent toxicity.

---

🏗️ Production Architecture (The API Factory)

This is not a local script. It is a containerized, secure microservice.

· The Bouncer (FastAPI): Ingests JSON patient data (genetics, weight, target concentration) and validates it using Pydantic.
· The Black Box (Docker): Containerized for seamless deployment across local and cloud environments.
· The Password (JWT Auth): OAuth2 Bearer token security. Only authenticated clinicians can trigger the dosing engine.
· The Vault (SQLAlchemy + MySQL): Every genetic dose adjustment is securely logged into a relational database for clinical audit trails.

---

📊 The Audit Trail (Data Persistence)

Clinical software must be auditable. The PGx Engine does not just calculate in the browser; it writes every decision to a MySQL database via SQLAlchemy.

The audit log captures:

· patient_id
· gene & mutation (e.g., CYP2C9, 3/3)
· phenotype (Poor Metabolizer)
· base_half_life vs adjusted_half_life
· standard_dose vs personalized_dose
· timestamp

This ensures a physician can track the exact mathematical logic used to adjust a patient's dose, creating a defensive legal and clinical shield.

---

🧪 Validation (Test-Driven Development)

In clinical pharmacology, a math error is a liability. The engine is validated using a Pytest suite that tests the boundaries of genetic multipliers and pharmacokinetic crashes.

· Test Coverage: Normal Metabolizer (*1/*1), Intermediate (*1/*2), Poor Metabolizer (*3/*3), and extreme weight boundaries.
· Crash Prevention: Tests explicitly ensure the API does not crash if a patient has a half-life of 0 (ZeroDivisionError prevention).
· Result: 45 passing Pytest cases.

```bash
collected 45 items
test_pgx.py::test_cyp2c9_multipliers[*1/*1-1.0-Normal Metabolizer] PASSED
test_pgx.py::test_cyp2c9_multipliers[*2/*2-3.5-Poor Metabolizer] PASSED
test_pgx.py::test_cyp2c9_multipliers[*3/*3-3.5-Poor Metabolizer] PASSED
test_pgx.py::test_pk_math_extreme_weights PASSED
test_pgx.py::test_zero_div_zero_half_life PASSED
==================== 45 passed in 1.84s ====================
```

---

🚀 How to Run Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/CodeXSourabhsingh/pgx-production-api.git
   cd pgx-production-api
   ```
2. Create Virtual Environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install Dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Set up Environment Variables:
   Create a .env file in the root directory:
   ```env
   MYSQL_HOST=localhost
   MYSQL_USER=root
   MYSQL_PASSWORD=your_password
   MYSQL_DATABASE=pgx_vault
   JWT_SECRET_KEY=your_super_secret_key
   ```
5. Run the Engine:
   ```bash
   uvicorn app.main:app --reload
   ```
   Access the Swagger UI at http://localhost:8000/docs to authenticate and test the API.

---

📂 Project Structure

```text
pgx-production-api/
│
├── app/
│   ├── main.py          # FastAPI application instance
│   ├── database.py      # SQLAlchemy setup and MySQL connection
│   ├── models.py        # Database tables (Audit Vault)
│   ├── schemas.py       # Pydantic data validation models
│   ├── auth.py          # JWT Authentication logic
│   └── logic/
│       ├── cyp2c9.py    # CYP2C9 genetic multipliers
│       └── pk_math.py   # Pharmacokinetic dose calculations
│
├── tests/
│   ├── test_pgx.py      # Pytest boundary and crash-prevention tests
│   └── __init__.py
│
├── Dockerfile           # Container configuration
├── requirements.txt     # Python dependencies
└── README.md            # This file
```

---

🧠 About the Architect

Sourabh Singh
I am a Full-Stack Systems Architect and Domain Polyglot. I learn a medical specialty, model its decision logic, and ship a production-grade platform. I don't just build backends; I build the deterministic safety gates that protect patients and reduce clinical liability. I bridge the gap between complex medicine and clean code.

---

🛡️ Final Statement

The PGx Engine is not just a calculator. It is a deterministic safety layer. It enforces safety over convenience, explainability over opacity, and mathematical precision over blind standard dosing.

Designed for teams that care about one thing above all else:
Getting the clinical decision right before the patient is put at risk.
