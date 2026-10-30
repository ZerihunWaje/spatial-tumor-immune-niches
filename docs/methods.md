# Methods

## Preprocessing
- Counts loaded from `cell_feature_matrix.h5` (gene probes only; control probes removed) and joined with cell centroids from `cells.csv.gz`.
- QC: cells with fewer than 10 transcripts and genes detected in fewer than 5 cells were removed (165,423 of 167,780 cells kept; all 313 genes kept).
- Normalization: total-count normalization followed by log1p. All panel genes were used (no highly variable gene selection), because the panel is small and targeted.

## Clustering and annotation
- PCA (30 components) → kNN graph (15 neighbors) → UMAP → Leiden clustering (resolution 0.5, igraph), which gave 10 clusters.
- Cell types were assigned with marker gene scores (`scanpy.tl.score_genes`): each cluster got the type with the highest mean score. The result was checked against the top Wilcoxon marker genes per cluster.

## Spatial analysis (squidpy)
- **Spatial graph:** 10 nearest neighbors on cell centroids.
- **Neighborhood enrichment:** permutation test (500 permutations) of cell-type pairs among spatial neighbors; reported as z-scores.
- **Co-occurrence:** probability ratio p(type | tumor) / p(type) across distance, on a central 2 × 2 mm window (18,762 cells).
- **Spatially variable genes:** Moran's I on the spatial graph, analytic p-values with Benjamini–Hochberg correction.
- **Niches:** for each cell, the cell-type composition of itself plus its 10 neighbors; k-means (k = 8) on these vectors.
- **Ligand–receptor:** `squidpy.gr.ligrec` with the OmniPath database, 200 permutations, on a 30,000-cell subsample.

## Contrast
- Tumor cells were split by the immune fraction of their neighborhood: top quartile (immune-rich, n = 22,424) vs. bottom quartile (immune-poor, n = 44,687). The bottom group is larger because many tumor cells have zero immune neighbors.
- Differential expression: Wilcoxon rank-sum test, Benjamini–Hochberg correction; significance at adjusted p < 0.05 and |log2FC| > 0.5.
- Genes typical of neighboring cell types (macrophage, fibroblast, T cell) were flagged as likely segmentation spillover.

## Software
Python 3.13 · scanpy 1.12 · squidpy 1.8 · anndata · scikit-learn · matplotlib · seaborn (run on Google Colab).
