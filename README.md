# breast-cancer-mrna-analysis
Differential expression analysis of BRCA subtypes using GSE96058 (n=3,409) with limma in Python via rpy2.

This project performs differential expression analysis on the GSE96058 breast cancer RNA-seq dataset (3,409 samples, log2 FPKM) from GEO. PAM50 subtype labels (Luminal A, Luminal B, Basal, HER2-enriched, Normal-like) are extracted from sample metadata and used to run all pairwise comparisons using limma via rpy2. Outputs include ranked DEG tables (all, upregulated, downregulated) for each comparison, along with PCA, volcano, and heatmap visualisations. Analysis was run on Google Colab due to dataset size.
30,865 genes × 3,409 samples 

Out of these, top 5000 genes with highest variance were taken.
Note: there is a possibility that real DEGs in limma were excluded due to data infeasibilties. PCA on all 30k genes is dominated by noise.

A BH correction of FDR<0.05 was used as the threshold. Bonferroni correction was not used due to increase in false negatives
Comparisons

All 10 pairwise PAM50 subtype comparisons were run:


Basal vs Her2
Basal vs LumA
Basal vs LumB
Basal vs Normal
Her2 vs LumA
Her2 vs LumB
Her2 vs Normal
LumA vs LumB
LumA vs Normal
LumB vs Normal


In each comparison, grp1 = reference (encoded as 0), grp2 = comparison (encoded as 1). Positive logFC means higher expression in grp2; negative logFC means higher expression in grp1.

PCA Analysis:
Each dot represents one patient sample, coloured by PAM50 subtype. PCA compresses 5,000 gene dimensions into two axes that capture the maximum variance in the data.


PC1 (x axis) — explains 9.15% of total variance
PC2 (y axis) — explains 7.34% of total variance
Total variance captured — 16.49%


The low cumulative variance (16.49%) reflects substantial inter-patient heterogeneity in this large population-based cohort (n=3,409), which is expected and normal. The scree plot confirms a clear elbow at PC3 (3.83%), supporting the use of a 2D projection — adding PC3 would not meaningfully improve separation.

What good separation looks like:


Basal subtype should form a clearly distinct cluster — it is the most transcriptionally divergent BRCA subtype
LumA and LumB will overlap somewhat as both are luminal
HER2-enriched typically sits between Basal and Luminal clusters
Normal-like often sits near LumA

Heatmaps:
Shows the expression of the top 50 most significant DEGs (by FDR) across all samples in a pairwise comparison.

Rows — genes (top 50 DEGs)
Columns — samples (all samples from both subtypes in this comparison)
Colour — log2 FPKM expression value

LIMITATIONS

No raw counts — GSE96058 provides log2 FPKM only. DESeq2 and edgeR could not be applied.
Inter-patient heterogeneity — PCA captures only 16.49% variance in PC1+PC2, reflecting the large biological diversity within subtypes in a real-world cohort.

