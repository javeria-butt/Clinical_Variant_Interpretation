# Clinical Variant Interpretation of Rare Genetic Disorders

![Bioinformatics](https://img.shields.io/badge/Field-Bioinformatics-brightgreen) ![ACMG](https://img.shields.io/badge/Guidelines-ACMG-red) ![VCF](https://img.shields.io/badge/File-VCF%20v4.2-orange) ![Status](https://img.shields.io/badge/Status-Completed-blue) ![Ubuntu](https://img.shields.io/badge/OS-Ubuntu-E95420?logo=ubuntu&logoColor=white)

## Project Overview
This repository contains a clinical bioinformatics workflow for identifying and interpreting pathogenic variants associated with three rare genetic conditions: **Cystic Fibrosis (CF)**, **Familial Hypercholesterolemia (FH)**, and **Phenylketonuria (PKU)**. The project involves filtering raw patient VCF data, annotating variants, and performing evidence-based pathogenicity assessment using **ACMG/AMP guidelines**.

## Technology Stack
The architecture leverages standard bioinformatics tools and deep-learning predictors for high-accuracy variant interpretation:
* **BCFTools:** For high-stringency filtering and manipulation of VCF files.
* **Ensembl VEP:** Utilized for functional annotation of genomic variants.
* **AlphaMissense (Google DeepMind):** For predicting the structural impact of missense mutations.
* **REVEL:** An ensemble method for predicting the pathogenicity of rare missense variants.

## Workflow Steps
The pipeline is divided into several modular clinical stages:
1. **Filtering:** Extraction of high-quality calls for specific genes (*CFTR*, *LDLR*, and *PAH*) from the patient's whole-genome/exome VCF using `bcftools`.
2. **Pathogenicity Scoring:** Assessment of variants using **AlphaMissense** and **REVEL** to determine computational evidence (PP3).
3. **Clinical Curation:** Integration of **ClinVar** assertions and population frequency data to categorize variants.
4. **Classification:** Final determination of clinical significance (Pathogenic, Likely Pathogenic, or VUS) according to ACMG criteria.

### Disorders and Variants Studied

| # | Disorder | Gene | Variant (HGVS Protein) | Chromosomal Position (GRCh38) |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **Cystic Fibrosis** | *CFTR* | p.Gly551Asp (G551D) | chr7:117,587,806 |
| 2 | **Familial Hypercholesterolemia** | *LDLR* | p.Asp227Glu (D227E) | chr19:11,105,587 |
| 3 | **Phenylketonuria** | *PAH* | p.Arg408Trp (R408W) | chr12:102,852,747 |

### Pathogenicity Summary

| Disorder | Gene | Variant | AlphaMissense Score | REVEL Score | ClinVar Review Status | ACMG Classification |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Cystic Fibrosis** | *CFTR* | p.Gly551Asp | 0.9897 — Likely Pathogenic | 0.99 — Pathogenic | Expert Panel Reviewed ★★★★ | Pathogenic |
| **Familial Hypercholesterolemia** | *LDLR* | p.Asp227Glu | 0.9881 — Likely Pathogenic | 0.864 — Pathogenic | Multiple Submitters ★★★ | Pathogenic |
| **Phenylketonuria** | *PAH* | p.Arg408Trp | 0.999 — Pathogenic | 0.79 — Pathogenic | Expert Panel Reviewed ★★★★ | Pathogenic |


## Reproducing the Analysis

### 1. Setup
Clone the repository to your local environment:
```bash
git clone [https://github.com/javeria-butt/Clinical_Variant_Interpretation.git](https://github.com/javeria-butt/Clinical_Variant_Interpretation.git)
cd Clinical_Variant_Interpretation
```
### 2. View Results
* Detailed variant classifications are located in: `Data/Clinical_Variant_Annotation_Report.xlsx`
* Filtered genomic data is available in: `Data/patient_final_filtered.vcf`
* Visual evidence and pathogenicity plots are stored in: `Screenshots_acb/`

### 3. Reproduce Analysis
You can view the exact bioinformatics steps taken by inspecting the pipeline script:

```bash
cat pipeline.sh
```

### Repository Structure

```text
Clinical_Variant_Annotation/
│
├── Data/
│   ├── patient_variants.vcf                    # Raw curated VCF (ClinVar-sourced variants)
│   ├── patient_final_filtered.vcf              # BCFTools-filtered and fully annotated VCF
│   └── Clinical_Variant_Annotation_Report.xlsx # Complete clinical annotation report
│
├── Screenshots_ACB/
│   ├── CF_Alpha.png / CF_revel.png             # Cystic Fibrosis track visualizations
│   ├── FH_Alpha.png / FH_revel.png             # Familial Hypercholesterolemia track visualizations
│   └── PKU_Alpha.png / PKU_revel.png            # Phenylketonuria track visualizations
│
├── pipeline.sh   # BCFTools variant filtering and extraction pipeline
└── README.md     # Project documentation
```

## Tools and Databases
| Tool | Version | Purpose |
| :--- | :--- | :--- |
| **BCFTools** | latest | VCF filtering and processing |
| **ClinVar** | 2026 | Clinical significance reference |
| **AlphaMissense** | v1.0 | Deep-learning pathogenicity prediction |
| **REVEL** | latest | Ensemble missense variant scoring |

## Conclusion

All three variants identified in this analysis — **CFTR:p.Gly551Asp**, **LDLR:p.Asp227Glu**, and **PAH:p.Arg408Trp** — were classified as **Pathogenic** under ACMG/AMP guidelines. This classification is supported by convergent evidence from functional studies, population genetics, clinical observations, and computational predictors. Both **AlphaMissense** and **REVEL** scores consistently exceeded pathogenicity thresholds across all three variants, reinforcing the reliability of in-silico tools as a complement to experimental and clinical evidence in variant interpretation workflows.

This repository serves as a structured reference for clinical variant annotation methodology, demonstrating how publicly available databases and computational tools can be integrated into a reproducible, evidence-based classification pipeline.
