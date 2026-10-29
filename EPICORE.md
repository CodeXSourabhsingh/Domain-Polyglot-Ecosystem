
🧬 EPI-CORE: Pathogen & Microbiome Tracker

A Production-Grade Clinical API merging viral genomic surveillance with host microbiome diversity.

Built by Sourabh Singh | Python | FastAPI | Docker | SQLAlchemy | MySQL | Biopython

---

Overview

EPI-CORE is a bio-defense pipeline that correlates two critical layers of epidemiology: the pathogen's ability to escape immunity, and the host's immune system strength.

It helps researchers answer two questions:

1. The Disguise: How dangerous is the viral mutation (e.g., Omicron)?
2. The Security Guard: How strong is the patient's gut microbiome (Shannon Diversity)?

By merging these two data points, the engine calculates a Combined Risk Assessment.

Why this project exists (The Analogy)

When a virus mutates, it is a burglar putting on a new disguise to sneak past the locks. Your gut microbiome is the security guard.

Public health data is siloed. We analyze the virus in one lab and the patient's microbiome in another. But a burglar is only dangerous if the guard is asleep. EPI-CORE exists to connect the pathogen to the host.

What the Pipeline Does

The system follows a strict 3-step architecture:

1. The Disguise (Viral Mutation Analysis)

· Fetches real viral genomes (e.g., SARS-CoV-2 Omicron) from the NCBI database.
· Scans the sequence for mutations that increase Transmissibility or Immune Escape (e.g., E484K, N501Y).

2. The Security Guard (Microbiome Dashboard)

· Ingests operational taxonomic unit (OTU) data for gut microbiome samples.
· Calculates the Shannon Diversity Index to measure community richness and evenness.
· Low diversity = "sleeping guards" (compromised immunity).

3. The Combined Risk Assessment (The Merge)

· If a high-escape virus meets a patient with low microbiome diversity, the engine flags a CRITICAL RISK.
· Results are securely logged to a MySQL vault via SQLAlchemy.

---

🏗️ Production Architecture

This is not a local script. It is a production-grade backend system.

· The Bouncer (FastAPI): A REST API layer that validates JSON inputs via Pydantic and handles all requests.
· The Black Box (Docker): The entire engine and its heavy dependencies (Pandas, NumPy, Biopython) are containerized for cloud deployment.
· The Password (JWT Auth): OAuth2 Bearer token security. Only authenticated researchers can trigger the engine.
· The Vault (SQLAlchemy + MySQL): Every calculation is securely persisted to a relational database, maintaining a full clinical audit trail without storing PII.

---

🛠️ Tech Stack

· Backend: Python, FastAPI, Uvicorn
· Database: MySQL, SQLAlchemy ORM
· Bioinformatics: Biopython, NCBI E-utilities
· Data Science: Pandas, NumPy
· Infrastructure: Docker, JWT (JSON Web Tokens)
· Testing: Pytest

---

🧪 Validation & Testing (Test-Driven Development)

In clinical software, a math error is a liability. EPI-CORE is validated with a custom Pytest suite targeting the worst-case biological scenarios.

The suite covers:

· Shannon Math: Ensuring the diversity index calculates correctly even with zero or single-species samples.
· Unknown Lineages: Ensuring the engine fails gracefully if a new variant doesn't match known signatures.
· Combined Risk Logic: Validating the exact boundaries where a virus goes from "Elevated" to "Critical."

Result: 8/8 Passing.

(Insert Pytest terminal screenshot here)


---

⚠️ Honest Limitations

· Research Use Only: This tool is a decision-support prototype. It does not provide clinical diagnoses.
· Data Dependency: The engine relies on the NCBI API. If NCBI goes down, the engine will return a safe error.
· Human-in-the-loop: The system flags risk; the researcher makes the final call.

---

👨‍💻 About the Architect

I am Sourabh Singh. I am 20 years old, 3 months into coding, and self-taught. I don't just build prototypes; I build production-grade systems. I am looking for clinic partners, CROs, or biotech founders who need a technical co-founder to build their MVP from 0 to 1. I build the architecture; we share the upside.

"The mode is a data decision, not a capability decision. We build the bridge; the physician decides."
