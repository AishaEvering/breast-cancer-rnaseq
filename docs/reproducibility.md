# Reproducibility

## Project

Differential Gene Expression Analysis of ER-Positive Breast Cancer

**Dataset:** GSE103001  
**Source:** https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE103001

## Computational Environment

- Operating system: macOS
- Architecture: Apple Silicon (osx-arm64)
- Environment manager: Anaconda
- Conda environment: `breast-cancer-rnaseq`
- R version: 4.4.3
- DESeq2 version: 1.46.0

Environment specifications are maintained in the project repository.

## Analysis Reproducibility

The following information will be documented as the pipeline develops:

- Data sources and download dates
- Reference genome and gene annotation versions
- Sample inclusion and exclusion criteria
- Data preprocessing and filtering parameters
- DESeq2 experimental design and statistical thresholds
- Random seed usage
- Software versions and dependencies
- Analysis commands and execution order

## Reproducibility Notes

Standard DESeq2 differential expression calculations are deterministic and do not generally require a random seed.

Any stochastic procedures introduced during the analysis will have their random seed and relevant parameters explicitly documented.
