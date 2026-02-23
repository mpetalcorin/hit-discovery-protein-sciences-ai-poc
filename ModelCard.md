# Model Card, Proof-of-Concept Models

This repository contains multiple lightweight models trained on synthetic datasets to demonstrate discovery workflows. The models are intentionally simple, interpretable, and reproducible.

## 1. Models Included

### A. SAR Active Classifier (unstructured + structured)
**Goal:** Predict whether a compound is active, then rank candidates for confirmation.

**Inputs:**
- Unstructured string: SMILES-like token sequence
- Structured numeric features: MW, cLogP, tPSA
- Categorical metadata: vendor, library

**Model family:**
- Logistic Regression with:
  - char n-gram TF-IDF features for SMILES-like text
  - scaled numeric features
  - one-hot categorical features

**Output:**
- Probability of being active
- Ranked list for follow-up assays

### B. Peptide-Protein Binding Regressors
**Goal:** Predict peptide binding strength for reagent prioritisation.

**Physics-inspired baseline:**
- Ridge regression on interpretable features:
  - length, hydrophobicity proxy sum, charge proxy sum, aromatic count, motif indicator

**Sequence ML model:**
- Ridge regression on:
  - char n-gram TF-IDF features on peptide sequence
  - plus numeric features above

**Output:**
- Predicted binding strength (pKd), ranked peptides for synthesis and validation

## 2. Intended Use

**Intended use:**
- Demonstrate capability in:
  - modelling unstructured and multidimensional data
  - decision-focused ranking
  - integration with HTS and protein sciences workflows
  - reproducible analysis and reporting

**Not intended for:**
- Real drug discovery decision-making
- Clinical decision-making
- Deployment without retraining on real, validated datasets

## 3. Training Data

All training data is synthetic and generated inside the notebook:
- HTS-like plate readouts with control wells and plate effects
- SAR-like activity labels generated from latent motif/property rules plus noise
- Peptide binding simulated from a latent energy rule plus noise
- Proteomics LFQ-like intensities with intensity-dependent missingness

No human subjects, patient data, or proprietary datasets are used.

## 4. Evaluation

### SAR active classifier
- Evaluated using:
  - AUROC
  - AUPRC (more informative under class imbalance)
  - Precision-Recall curve

### Peptide binding regressors
- Evaluated using:
  - RMSE
  - R²
  - predicted vs true scatter plot

All evaluations are performed on held-out test splits with fixed random seed for reproducibility.

## 5. Ethical Considerations

- The models are not trained on human data.
- Outputs should not be used to guide medical or safety decisions.
- The repo is designed to demonstrate technical workflow design, not to claim biological truth.

## 6. Limitations

- Chemical strings are SMILES-like placeholders, not chemically validated structures.
- Feature-label relationships in SAR and peptide tasks are synthetic by construction.
- Metrics reflect learnability of simulated relationships and are not a claim of real-world predictive performance.

## 7. Reproducibility

- Fixed seed used for dataset generation and train/test splits.
- Deterministic pipeline, outputs written to `az_poc_notebook/`.
- Workflow stubs provided (`workflow/Snakefile`, `workflow/main.nf`) to illustrate scaling patterns.

## 8. References (literature-indexed anchors)

- Zhang JH, Chung TDY, Oldenburg KR. A simple statistical parameter for use in evaluation and validation of high throughput screening assays. *J Biomol Screen* (1999). https://doi.org/10.1177/108705719900400206
- Cox J, et al. Accurate proteome-wide label-free quantification by delayed normalization and maximal peptide ratio extraction (MaxLFQ). *Mol Cell Proteomics* (2014). https://doi.org/10.1074/mcp.M113.031591
