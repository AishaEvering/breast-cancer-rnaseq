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

**Status:**

- Selected a project-specific download manifest rather than using GDC, because GSE103001 is distributed through NCBI GEO. The manifest will record source URLs, filenames, file sizes, SHA-256 checksums, and download dates to support data provenance and reproducibility.

---

**Dataset:** GSE103001

**Archive:** `GSE103001_RAW.tar`

**Archive SHA-256:** `420440701f4bbc558e38f472bf141fe6022709eb0d874da650cdfda8dfe460d0`

**Inspection commands:**

```bash
tar -tf data/raw/GSE103001_RAW.tar | wc -l
tar -tf data/raw/GSE103001_RAW.tar | sort
```

**Observations:**

- Archive contains 44 entries, all appearing to be gzipped HTSeq gene-count files.
- 22 filenames begin with BCTN.
- 22 filenames begin with BCTP.
- Sample identifiers appear to form 22 matched tumor-normal pairs.
- Filenames indicate STAR alignment, reverse-stranded HTSeq counting, and Ensembl GRCh37 release 75 annotation.

**Validation status:**

- Archive readability: Passed.
- Expected file count: Passed.
- Patient pairing: Pending GEO metadata verification.
- Tissue condition labels: Pending GEO metadata verification.
- Count file integrity: Pending.

**Next step:** Retrieve GEO sample metadata and validate patient pairing before constructing the DESeq2 count matrix.

## 2026-11-13 — GSE103001 Metadata Validation

Objective: Inspect GEO sample metadata and identify eligible matched tumor-normal pairs for a pilot analysis.

Results:

- Parsed 31 sample metadata fields from the GEO series matrix.
- Confirmed 44 samples representing 22 patients.
- Verified that all 22 patients have both normal and tumor samples.
- Confirmed that all 22 tumor samples are annotated ER+/HER2−.
- Identified ER subtype distribution: A (12 tumors), B (10 tumors).
- Identified and corrected a condition-classification issue caused by assuming tumor tissue descriptions contained the word "tumor".

Conclusion: The metadata supports a paired tumor-normal analysis using patient identity as a blocking factor.

Remaining work:

- Review documented sample exclusions and QC concerns.
- Select 4 matched pilot pairs using predefined criteria.
- Export and validate sample_metadata.csv.
- Generate the download manifest.

Status: Metadata inspection complete; pilot selection pending.
