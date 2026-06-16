# breast-cancer-mrna-analysis
Differential expression analysis of BRCA subtypes using GSE96058 (n=3,409) with limma in Python via rpy2.

This project performs differential expression analysis on the GSE96058 breast cancer RNA-seq dataset (3,409 samples, log2 FPKM) from GEO. PAM50 subtype labels (Luminal A, Luminal B, Basal, HER2-enriched, Normal-like) are extracted from sample metadata and used to run all pairwise comparisons using limma via rpy2. Outputs include ranked DEG tables (all, upregulated, downregulated) for each comparison, along with PCA, volcano, and heatmap visualisations. Analysis was run on Google Colab due to dataset size.
30,865 genes × 3,409 samples 
