## Reproducibility: Random Seed

**Status:** Planned — implement when analysis begins.

**Proposed seed:** `42`

```r
set.seed(42)
```

**Rationale:** Ensure reproducibility for analysis steps involving random operations, such as simulations or stochastic algorithms.

**Notes:**

- Standard DESeq2 differential expression calculations are deterministic.
- Record the seed in the relevant analysis scripts.
- Document any additional seeds or stochastic parameters if required.
- Verify reproducibility using the documented software environment.

**Implementation date:** TBD

## 2026-11-12 — Dataset Selection: GSE103001

**Objective:** Identify differentially expressed genes between ER-positive breast tumors and matched adjacent normal breast tissue.

**Selected dataset:** GSE103001

**Rationale:**

The dataset contains 22 reported matched tumor-normal pairs from patients with ER-positive breast cancer.

The paired experimental design allows us to account for patient-specific variation when comparing gene expression between tumor and normal tissue.

The dataset also provides gene-level raw count files generated using HTSeq, allowing us to begin differential expression analysis without repeating read alignment and quantification.

**Proposed analysis:**

- Validate sample metadata and patient pairing.
- Inspect raw gene-count files.
- Investigate the original study's sample exclusions.
- Perform exploratory data analysis and quality control.
- Use DESeq2 with a paired experimental design.
- Identify significantly differentially expressed genes.
- Investigate biological functions associated with those genes.

**Proposed DESeq2 design:**

`~ patient + condition`

**Important considerations:**

- Adjacent normal tissue is not necessarily equivalent to tissue from cancer-free individuals.
- The original study reports excluding one patient because of aberrant strand specificity. I must verify the affected samples before determining our final sample count.
- Gene annotations must be compatible with the original GRCh37/Ensembl 75 reference.

**Status:** Dataset selected. Metadata documentation initiated. Sample validation pending.
