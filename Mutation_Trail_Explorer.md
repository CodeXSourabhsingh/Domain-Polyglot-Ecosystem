
🧬 Mutation Trail Explorer: Precision Medicine Pipeline

Built by Sourabh Singh | Python, Streamlit, MySQL, Biopython, Py3Dmol, ChEMBL API

THE PROBLEM

In precision medicine, a genetic mutation is just the starting point. A researcher must trace the entire trail:

1. Where does CRISPR cut the DNA?
2. How does that mutation physically break the protein structure?
3. What targeted drug can fix the broken protein?

Currently, these steps are fragmented across different databases (NCBI, PDB, ChEMBL). Researchers waste hours manually copying and pasting between them, breaking the "Trail" and losing the clinical context.

THE SOLUTION

Mutation Trail Explorer is a unified, 4-step pipeline that connects the entire genomic journey into a single, auditable dashboard.

The Architecture (The 4 Steps):

1. The Tailor (CRISPR Target Analysis)

· The engine fetches the raw DNA sequence from the NCBI database based on the target gene (e.g., HBB).
· It simulates PAM scanning and gRNA matching, calculating on-target and off-target cuts.
· It maps the GC content to ensure the cut is biologically viable.

2. The Check (Human-in-the-Loop)

· "Do you verify this is the correct biological sequence?"
· The pipeline hard-stops. It does not automate clinical decisions. The researcher must verify the sequence before proceeding to structural analysis.

3. The Broken Zipper (Protein Impact Analysis)

· The engine maps the DNA mutation to its 3D protein structure using PDB and Py3Dmol.
· It calculates the Kyte-Doolittle hydrophobicity profile to see how the mutation alters the protein's surface.
· It uses BLOSUM62 matrix scoring to classify the mutation as Destabilizing or Neutral.

4. The Cure (Drug Interaction Discovery)

· The engine queries the ChEMBL API for targeted therapies.
· It normalizes all drug binding affinities (IC50, Ki, Kd) into nanomolar (nM) values.
· It classifies the binding strength (Very Strong, Strong, Moderate, Inactive) to help researchers identify viable treatments.

---

🛠️ THE TECH STACK

· Language: Python
· Bioinformatics APIs: NCBI E-utilities, RCSB PDB, ChEMBL
· Libraries: Biopython, Py3Dmol, Pandas, NumPy
· Database: MySQL (Relational Schema for audit trails)
· UI: Streamlit, Matplotlib

---

🧪 VALIDATION (Test-Driven Development)

I don't just build; I validate. The engine is tested against the worst-case biological scenarios.

The Pytest Suite covers:

· CRISPR Math: Reverse complements, lowercase sequence normalization, empty sequence handling.
· Protein Physics: Extreme hydrophobicity boundaries (+4.5 to -4.5) and invalid amino acid handling.
· BLOSUM62 Logic: Testing conservative (I->V) vs. destabilizing (E->V) mutations.
· API Unit Conversions: Converting uM, mM, pM, and M into exact nM values to prevent drug classification errors.

Result: 18/18 Boundary Tests Passing.

<img width="1920" height="1080" alt="Screenshot 2026-10-26 230301" src="https://github.com/user-attachments/assets/92bb06b6-96c3-4582-9880-3654fd1911a3" />


---

🚀 HOW TO RUN LOCALLY

1. Clone the repository:
   ```bash
   git clone https://github.com/CodeXSourabhsingh/Mutation-Trail-Explorer.git
   cd Mutation-Trail-Explorer
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Set up your config.py (or Streamlit secrets) with your MySQL credentials.
4. Run the app:
   ```bash
   streamlit run app.py
   ```

---

⚠️ HONEST LIMITATIONS

· For Research Use Only: This tool is a decision-support prototype. It does not provide clinical diagnoses or medical prescriptions.
· PDB Dependency: The 3D protein rendering requires a valid PDB ID. If the specific mutated protein has not been crystallized and uploaded to the RCSB database, the engine will return an error.
· API Latency: The engine relies on live public APIs (NCBI, ChEMBL). High traffic on their servers may slow down the pipeline.

---

"The mode is a data decision, not a capability decision. We build the bridge; the physician decides."
