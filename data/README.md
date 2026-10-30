# Data

The raw data is **not stored in this repository** (several GB). The notebook downloads what it needs automatically.

**Dataset:** Xenium FFPE Human Breast Cancer, In Situ Replicate 1
**Provider:** 10x Genomics (Janesick et al., *Nature Communications*, 2023)
**License:** CC BY 4.0

Files used (extracted from the output bundle):
- `cell_feature_matrix.h5`: gene counts per cell (313 genes)
- `cells.csv.gz`: cell centroids in µm, cell and nucleus area, transcript counts

Bundle URL:
https://cf.10xgenomics.com/samples/xenium/1.0.1/Xenium_FFPE_Human_Breast_Cancer_Rep1/Xenium_FFPE_Human_Breast_Cancer_Rep1_outs.zip

When you run the notebook, the files are saved to `data/xenium_breast_rep1/`. That folder is excluded from git.
