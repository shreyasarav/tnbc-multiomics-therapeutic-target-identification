# Integrated Multi-Omics Analysis for Therapeutic Target Identification in Triple-Negative Breast Cancer (TNBC)

*Dataset: GSE27447 | Platform: GPL6244 | Organism: Homo sapiens*

## 1. Project Overview

This project aims to identify biologically relevant molecular features and potential therapeutic targets associated with Triple-Negative Breast Cancer (TNBC) using an integrated computational analysis workflow. The analysis begins with public gene-expression data and progresses through quality assessment, differential expression analysis, gene annotation, functional enrichment, pathway analysis, and visualization.

The present implementation uses the GSE27447 dataset obtained from the NCBI Gene Expression Omnibus (GEO). The dataset contains gene-expression profiles from TNBC and non-TNBC breast tumor samples and is suitable for comparing molecular expression patterns between the two groups.

## 2. Project Objectives

- Analyze gene-expression differences between TNBC and non-TNBC breast tumors.
- Identify top-ranked genes associated with the TNBC expression profile.
- Perform functional enrichment using Gene Ontology (GO).
- Identify enriched biological pathways using KEGG and Reactome.
- Visualize expression patterns using PCA, correlation heatmaps, volcano plots, and gene heatmaps.
- Use the resulting molecular findings as a foundation for downstream therapeutic-target identification.

## 3. Data Source

The primary dataset was obtained from the National Center for Biotechnology Information (NCBI) Gene Expression Omnibus (GEO), a public repository of functional genomics data.

| Data attribute | Project information |
|---|---|
| GEO accession | GSE27447 |
| Study title | FZD7 Plays a Critical Role in Triple Negative Breast Cancer Proliferation |
| Organism | Homo sapiens |
| Experiment type | Expression profiling by array |
| Platform | GPL6244 -- Affymetrix Human Gene 1.0 ST Array |
| Features | 33,297 expression features |
| Samples | 19 total samples |
| TNBC group | 5 tumor samples |
| Non-TNBC group | 14 tumor samples |
| GEO processing | Background correction, quantile normalization and interPLIER summarization |

GEO records for the dataset report that the processed values were background corrected, quantile normalized, and summarized using the interPLIER algorithm with Affymetrix Expression Console. The GEO platform record reports 33,297 processed expression features.

## 4. Software and Packages

The computational analysis was performed in R/RStudio using the following packages:

- **GEOquery** -- Retrieve and work with GEO datasets
- **Biobase** -- ExpressionSet and biological data structures
- **limma** -- Differential expression analysis for microarray data
- **ggplot2** -- Statistical graphics and visualization
- **pheatmap** -- Expression and correlation heatmaps
- **ggrepel** -- Non-overlapping labels in plots
- **dplyr / tidyr / stringr** -- Data manipulation and cleaning
- **clusterProfiler** -- GO and KEGG enrichment analysis
- **org.Hs.eg.db** -- Human gene annotation and identifier mapping
- **GOSemSim** -- Gene Ontology semantic analysis support
- **ReactomePA** -- Reactome pathway enrichment
- **GGally / factoextra** -- Exploratory and multivariate visualization support

## 5. Methodology

1. **Dataset retrieval** -- GSE27447 was retrieved directly from NCBI GEO using the GEOquery package.
2. **Sample group definition** -- Samples were classified using the GEO phenotype field describing disease state: 5 TNBC vs. 14 non-TNBC tumor samples.
3. **Expression data preparation** -- The processed GEO expression matrix was log2-transformed (`log2(expression + 1)`) for downstream linear-model analysis.
4. **Quality control** -- An expression boxplot, PCA, and a Pearson sample-to-sample correlation heatmap were generated across all 19 samples.
5. **Differential expression analysis** -- limma was used with a design matrix (non-TNBC as reference, TNBC as comparison), followed by empirical Bayes moderation. Statistics include log2 fold change, p-value, and Benjamini-Hochberg adjusted p-value.
6. **Candidate gene selection and annotation** -- Top-ranked features were mapped to gene annotations using the GPL6244 feature annotation.
7. **Gene Ontology enrichment** -- Genes were converted to Entrez IDs via org.Hs.eg.db and tested for GO Biological Process, Molecular Function, and Cellular Component enrichment using clusterProfiler.
8. **KEGG pathway analysis** -- KEGG enrichment was performed for the human organism.
9. **Reactome pathway analysis** -- Reactome enrichment was performed using ReactomePA.
10. **Visualization** -- Expression boxplot, PCA plot, correlation heatmap, volcano plot, top-gene heatmap, GO enrichment dot plot, Reactome enrichment plot.

## 6. Analysis Workflow

1. NCBI GEO -> GSE27447 retrieval
2. ExpressionSet and phenotype extraction
3. TNBC vs non-TNBC sample classification
4. Expression data preparation
5. Quality control: boxplot + PCA + correlation heatmap
6. limma differential expression analysis
7. Top-ranked gene identification and annotation
8. Gene identifier conversion
9. GO-BP / GO-MF / GO-CC enrichment
10. KEGG pathway enrichment
11. Reactome pathway enrichment
12. Visualization and result export
13. Downstream therapeutic-target interpretation

## 7. Current Project Findings

- The analysis included 33,297 expression features across 19 samples.
- The comparison consisted of 5 TNBC tumor samples and 14 non-TNBC tumor samples.
- The top-ranked expression features were annotated and used for downstream functional analysis.
- GO Biological Process analysis identified the **glial cell-derived neurotrophic factor receptor signaling pathway** as an enriched biological process (genes: GFRA2, GFRA3).
- GO Molecular Function and Cellular Component analyses did not identify significant terms under the selected criteria.
- KEGG enrichment did not identify significant pathways under the selected criteria.
- Reactome analysis identified **RET signaling** as an enriched pathway, with GFRA2 and GFRA3 contributing to the pathway result.
- PCA, sample-correlation analysis, volcano visualization, and heatmap visualization were generated as part of the analysis workflow.

## 8. Repository Structure

```
.
â”œâ”€â”€ scripts/
â”‚   â””â”€â”€ TNBC_differential_expression_analysis.R   # Full annotated analysis pipeline
â”œâ”€â”€ results/
â”‚   â”œâ”€â”€ tables/
â”‚   â”‚   â”œâ”€â”€ differential_expression_full.csv      # Full limma DE statistics (33,297 features)
â”‚   â”‚   â”œâ”€â”€ top20_annotated_genes.csv              # Top 20 ranked, annotated genes
â”‚   â”‚   â”œâ”€â”€ go_biological_process.csv              # GO-BP enrichment results
â”‚   â”‚   â”œâ”€â”€ go_molecular_function.csv              # GO-MF enrichment results
â”‚   â”‚   â”œâ”€â”€ go_cellular_component.csv              # GO-CC enrichment results
â”‚   â”‚   â”œâ”€â”€ reactome_pathways.csv                  # Reactome enrichment results
â”‚   â”‚   â””â”€â”€ analysis_summary.csv                   # One-line summary per analysis
â”‚   â””â”€â”€ figures/
â”‚       â”œâ”€â”€ 01_expression_boxplot.png
â”‚       â”œâ”€â”€ 02_pca_plot.png
â”‚       â”œâ”€â”€ 03_sample_correlation_heatmap.png
â”‚       â”œâ”€â”€ 04_volcano_plot.png
â”‚       â”œâ”€â”€ 05_top19_gene_heatmap.png              # Top 19 of 20 genes (1 had no mapped symbol)
â”‚       â”œâ”€â”€ 06_go_bp_enrichment_dotplot.png
â”‚       â””â”€â”€ 07_reactome_pathway_enrichment.png
â””â”€â”€ reference/
    â””â”€â”€ PIIS2666166721001854.pdf                   # Pipeline reference publication
```

`GSE27447_RAW.tar` (raw CEL/CHP files) and the saved R workspace (`.RData`) are not tracked in this repository (see `.gitignore`) -- both are large binary files that are fully regenerated by running `scripts/TNBC_differential_expression_analysis.R`, which downloads the processed dataset directly from GEO via `GEOquery::getGEO("GSE27447")`.

## 9. Databases and Resources

- **NCBI Gene Expression Omnibus (GEO)** -- https://www.ncbi.nlm.nih.gov/geo/ -- Primary source of GSE27447 expression and phenotype data.
- **GSE27447 GEO record** -- https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE27447
- **GPL6244** -- https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GPL6244 -- Affymetrix Human Gene 1.0 ST Array platform annotation.
- **Gene Ontology** -- https://geneontology.org/
- **KEGG** -- https://www.genome.jp/kegg/
- **Reactome** -- https://reactome.org/

## 10. Reproducibility

The analysis can be reproduced by running `scripts/TNBC_differential_expression_analysis.R` in RStudio from a clean environment (it installs all required CRAN/Bioconductor packages, then downloads GSE27447 directly from GEO). See the note at the top of the script: one early section (group labeling, log2 transform, boxplot, PCA) was reconstructed to complete the record after R's console-history buffer truncated the original steps, and is flagged for review before re-running end-to-end. Every step from the correlation heatmap onward was recovered unmodified from the original session history.

## 11. Project Scope

This README documents the transcriptomic expression-analysis component and its functional/pathway interpretation. The broader project framework includes mutation analysis, survival analysis, protein-protein interaction analysis, hub-gene identification, drug-target prediction, and optional AI/ML biomarker prediction as downstream modules of the integrated therapeutic-target identification workflow.

## 12. References

- NCBI GEO. GSE27447, *FZD7 Plays a Critical Role in Triple Negative Breast Cancer Proliferation*.
- NCBI GEO. GPL6244, Affymetrix Human Gene 1.0 ST Array platform.
- Gene Ontology Consortium. Gene Ontology: biological process, molecular function, and cellular component annotation.
- Reactome. Curated pathway knowledgebase used for pathway enrichment analysis.

