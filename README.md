# Blue-breasted Quail RNA-seq Public Release

Versioned public-release packages for the RNA-seq study of blue-breasted quail
reared at high and low altitudes.

## Download

Download the complete reproducibility package from the
[Releases](../../releases) page.

## Package structure

```text
public_release/
├── code/
│   ├── analysis/                     # TPM, PCA, DESeq2, enrichment, and interaction analyses
│   └── orgdb/                        # Scripts for constructing the custom OrgDb package
├── data/
│   ├── sample_metadata.csv           # Public metadata for 240 samples
│   └── <tissue>/                     # Gene-level count, TPM, and KEGG information
├── orgdb/
│   ├── inputs/                       # Annotation inputs and reference GTF
│   └── package/                      # Installable custom OrgDb source package
├── results/
│   ├── <tissue>/
│   │   ├── differential_expression/  # DESeq2 and DEG result tables
│   │   ├── enrichment/               # GO, KEGG, and gene-list outputs
│   │   └── pca/                      # PCA outputs
│   └── interaction_effect_analysis/  # Liver and whole-blood interaction analysis
└── README.md

Run scripts from code/analysis/. Tissue-specific scripts require the
TISSUE_CODE environment variable:
```bash
Set-Location code/analysis
$env:TISSUE_CODE = "Li"
Rscript 02_PCA_DESeq2.R
```
Valid tissue codes are Li, Wb, He, Lu, Ki, Pe, and Bc.
The interaction-effect analysis uses liver and whole-blood data:
```
Set-Location code/analysis
Rscript 06_factorial_DESeq2.R
```
Before GO enrichment analysis, install the included custom OrgDb package:
```
Rscript code/orgdb/install_orgdb.R
```
For a tissue or comparison without a GO or KEGG enrichment-result file, no
reportable enriched terms were obtained for that analysis.


## Data availability

Raw sequencing reads are deposited in the NCBI Sequence Read Archive under
BioProject accession `PRJNAxxxxxx`.


## License

Analysis code is licensed under the [MIT License](LICENSE-CODE).

Unless otherwise noted, processed data, sample metadata, and analysis results
are licensed under [CC BY 4.0](LICENSE-DATA).

Third-party resources, including reference annotations and materials derived
from external databases, retain their respective original licenses.
