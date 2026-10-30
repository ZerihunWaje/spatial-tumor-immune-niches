# Result tables

| File | Content |
|---|---|
| `cell_type_counts.csv` | Number and share of cells per annotated cell type |
| `nhood_enrichment_zscores.csv` | Neighborhood enrichment z-scores between cell types (squidpy, 500 permutations) |
| `niche_composition.csv` | Average neighbor composition per niche (k-means, k = 8) with niche names |
| `top_spatially_variable_genes.csv` | Top 15 genes by Moran's I |

The notebook also writes the full tables when run: `moran_spatially_variable_genes.csv` (all 313 genes), `de_tumor_immune_rich_vs_poor.csv` (all genes, Wilcoxon + BH) and `niche_by_cell_type_counts.csv`.
