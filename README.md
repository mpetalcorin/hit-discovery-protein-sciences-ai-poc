# hit-discovery-protein-sciences-ai-poc
integrating HTS QC (Z′), multimodal ML hit ranking, peptide–protein binding prediction, LFQ proteomics differential analysis, and workflow-ready SQL, graph, and pipeline scaffolding.

This repository is an **end-to-end proof-of-concept** demonstrating in **hit discovery analytics, protein sciences modelling, and discovery data engineering**.

It includes simulated but **literature-anchored** datasets and a complete workflow that mirrors common early discovery tasks:
- HTS plate QC, normalisation, robust hit calling, and plate artefact visualisation.
- Integration across **flat files (CSV)**, **SQL (SQLite)**, and a simple **graph** abstraction (compound–assay–target).
- AI/ML modelling on **unstructured** representations (SMILES-like strings, peptide sequences) plus structured features.
- LFQ proteomics-style missingness and differential analysis with prioritisation for follow-up.
- Reproducible outputs, project structure, and workflow stubs (Snakemake, Nextflow).

> Note: The chemical strings in this repo are **SMILES-like placeholders** for unstructured modelling demonstrations, not chemically validated structures. The objective is to showcase modelling patterns, QC logic, and decision workflows.

## Repository Structure

- `Hit Discovery Protein Sciences.ipynb`  
  Main notebook, generates all datasets, figures, and summary outputs.

- `az_poc_notebook/`
  - `data/raw/`  
    Raw-style exports (HTS plate-level, LFQ raw)
  - `data/processed/`  
    QC tables, SAR simulation tables, DE results, SQLite database
  - `figs/`  
    Figures saved during execution
  - `reports/`  
    Short executive summary
  - `workflow/`  
    Pipeline stubs for Snakemake and Nextflow
  - `src/azpoc/`  
    Minimal Python package skeleton (stub CLI)


## What This Demonstrates 

### Essential requirements
- **Multidimensional / unstructured datasets (molecular / discovery context)**  
  HTS assay matrices, unstructured strings, peptide sequences, LFQ proteomics-style matrices.
- **Python + SQL + multi-source integration**  
  CSV + SQLite + graph abstraction.
- **Computational workflows and reproducibility**  
  Deterministic outputs, fixed seeds, workflow stubs, structured folder layout.
- **Reporting, conclusions, and recommended actions**  
  Ranked lists, enrichment estimates, and follow-up suggestions suitable for cross-functional teams.

### Desirables
- **AI/ML + physics-inspired modelling**  
  Peptide binding, physics-inspired baseline vs sequence ML.
- **High-throughput assay analytics**  
  HTS QC via Z′, normalisation, robust hit calling, heatmap artefact checks.
- **Software mindset**  
  Repo layout, packaging stub, CLI stub, workflow stubs.

## Quickstart
1. Open `Hit Discovery Protein Sciences.ipynb`
2. Run all cells
3. Review generated outputs under `az_poc_notebook/`

### minimal environment 
```bash
python -m venv .venv
source .venv/bin/activate
pip install -U pip
pip install numpy pandas scikit-learn matplotlib scipy networkx 
```
## Core Outputs 
### HTS
	•	figs/01_hts_zprime_hist.png
Plate QC distribution (Z′ factor)
	•	figs/02_hts_pct_inhibition_hist.png
Primary screen signal distribution (% inhibition)
	•	figs/03_hts_plate_heatmap.png
Plate artefact visualisation (heatmap)

### SAR Modelling (unstructured + structured)
	•	figs/04_sar_pr_curve.png
Precision–recall curve for active classification
	•	Tables in data/processed/simulated_sar_compounds.csv
Ranked candidates with structured properties

### Peptides (protein sciences)
	•	figs/05_peptide_pred_vs_true.png
Predicted vs true binding strength for sequence model
	•	data/processed/simulated_peptide_binding.csv
Synthetic peptide binding dataset

### Proteomics (LFQ-style)
	•	figs/06_proteomics_volcano.png
Differential analysis volcano plot
	•	data/processed/simulated_lfq_de_results.csv
DE table with FDR

### Data integration
	•	data/processed/az_poc.sqlite
SQLite database with example query patterns

### Scientific Benchmark Anchors (journal-indexed)
	•	HTS assay QC and Z′ factor:
	•	Zhang JH, Chung TDY, Oldenburg KR. J Biomol Screen (1999). PMID: 10838414.
	•	Label-free proteomics quantification (MaxLFQ approach and LFQ context):
	•	Cox J, et al. Mol Cell Proteomics (2014). PMCID: PMC4159666.

These are used as conceptual anchors for QC metrics and intensity scale behaviour, not as a source of real experimental data.

## Limitations
	•	Synthetic datasets are simulated datasets, not patient data, not proprietary.
	•	SMILES-like strings are not validated chemistry, they exist to demonstrate unstructured modelling patterns.
	•	Proteomics imputation is intentionally simple to keep the pipeline readable; production workflows may use more robust methods depending on design.

## License
MIT

## Contact
Mark I.R. Petalcorin
GitHub: https://github.com/mpetalcorin
