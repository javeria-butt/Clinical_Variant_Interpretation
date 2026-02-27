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

## Clinical Findings Summary

| Condition | Gene | Variant (HGVSp) | Pathogenicity Predictor | ACMG Classification |
| :--- | :--- | :--- | :--- | :--- |
| **Cystic Fibrosis** | *CFTR* | p.Phe508del | AlphaMissense: Likely Pathogenic | Pathogenic |
| **Familial Hypercholesterolemia** | *LDLR* | p.Asp227Glu | REVEL: 0.82 | Likely Pathogenic |
| **Phenylketonuria** | *PAH* | p.Arg408Trp | AlphaMissense: Pathogenic | Pathogenic |

## Usage Instructions

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

## Repository Contents
| File/Folder | Description |
| :--- | :--- |
| `Data/` | Filtered VCF files and the final Excel Clinical Annotation Report. |
| `Screenshots_acb/` | Visual evidence from AlphaMissense and REVEL for prioritized variants. |
| `README.md` | Project documentation, workflow summary, and findings. |

## Tools and Databases
| Tool | Version | Purpose |
| :--- | :--- | :--- |
| **BCFTools** | latest | VCF filtering and processing |
| **ClinVar** | 2026 | Clinical significance reference |
| **AlphaMissense** | v1.0 | Deep-learning pathogenicity prediction |
| **REVEL** | latest | Ensemble missense variant scoring |

## Data Summary
| Parameter | Value |
| :--- | :--- |
| **Reference Genome** | GRCh38 (hg38) |
| **Genes Analyzed** | CFTR, LDLR, PAH |
| **Classification Standard** | ACMG/AMP Guidelines |
