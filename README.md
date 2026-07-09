# RNAseq-Analysis-Aged-TBI

### Project Overview
This repository contains the workflow and scripts used to perform differential expression and pathway analysis on bulk RNA-sequencing data from a murine model. The goal of this project was to investigate how the aging brain's transcriptomic response to traumatic brain injury (TBI) differs from a healthy, young brain's response, specifically by analyzing gene expression and mapping significant shifts to biological pathways. 

*Data sourced from Bolte et al. (2023) eLife 12:e81154 (NCBI GEO: GSE206932).*

### Technical Stack
* **Languages:** R
* **Sequencing Data:** Bulk RNA-sequencing (Count matrices)
* **Tools & Packages:** DESeq2, tidyverse, ggplot2, EnhancedVolcano, pheatmap, org.Mm.eg.db, gage, pathview

### Pipeline Workflow
**Steps:** Data Import & Cleaning -> Normalization & Dispersion Estimation (DESeq2) -> Dimensionality Reduction (PCA) -> Differential Expression Analysis (Volcano Plots) -> Gene Symbol to Entrez ID Mapping -> Pathway Enrichment (GAGE) -> Pathway Visualization (Pathview)

### Results
Starting with raw bulk RNA-seq count data across four experimental groups (Young Sham, Young TBI, Aged Sham, Aged TBI), the data was normalized and analyzed for differential expression. 

* **Variance & Clustering:** Principal Component Analysis (PCA) successfully clustered the samples by age and injury status, matching the variance observed in the published literature.
* **Pathway Analysis:** GAGE pathway analysis revealed that the **Extracellular Matrix (ECM) receptor interaction pathway (KEGG ID: mmu04512)** is significantly down-regulated in aged TBI mice (p = 0.016).
* **Biological Significance:** Pathway visualization (Pathview) showed widespread suppression of key structural proteins, including Collagen isoforms (Col1a, Col2a), Laminin, Tenascin, and Thrombospondin. This coordinated downregulation suggests that aged brains fail to maintain structural integrity and extracellular matrix remodeling following a TBI, likely explaining their delayed recovery compared to young mice.

### Limitations and Future Improvements
This pipeline successfully validates the transcriptomic signatures of aging in TBI recovery, but there are a few areas for optimization:
* **Reproducibility:** The current R script utilizes hardcoded local file paths. A future update will transition these to relative paths and include an automated script to download the raw count matrix directly from NCBI GEO, allowing anyone to clone and run the repository seamlessly.
* **Cell-Type Specificity:** Since this is bulk RNA-seq data, the signals from specific cell types (like meningeal fibroblasts, which are highly responsible for collagen production) are averaged out. A future extension of this project could involve analyzing single-cell RNA-seq (scRNA-seq) data to isolate the exact cellular source of the ECM downregulation.

### Repository Structure

```text

├── data/
│   └── GSE206932_merged.counts.bulk.csv   # Raw bulk RNA-seq count matrix from NCBI GEO
├── figures/
│   ├── PCA.png                            # Principal Component Analysis plot of sample variance
│   ├── AgedSham_vs_AgedTBI.png            # Volcano plot: Aged Sham vs Aged TBI differential expression
│   ├── YoungSham_vs_AgedSham.png          # Volcano plot: Young Sham vs Aged Sham differential expression
│   ├── YoungSham_vs_YoungTBI.png          # Volcano plot: Young Sham vs Young TBI differential expression
│   ├── YoungTBI_vs_AgedTBI.png            # Volcano plot: Young TBI vs Aged TBI differential expression
│   ├── mmu04512.png                       # Reference KEGG pathway map for ECM-receptor interaction
│   └── mmu04512.pathview.png              # Pathview visualization showing down-regulated ECM genes
├── results/
│   ├── deseq-results2.txt                 # Full DESeq2 output table with log2FoldChange and p-values
│   └── mmu04512.xml                       # KEGG pathway XML file used for local Pathview rendering
├── Aged-TBI-RNAseq-Analysis.Rmd           # RMarkdown file containing the DESeq2 and Pathview pipeline
├── Aged-TBI-RNAseq-Analysis.pdf           # Detailed project documentation and full report
└── README.md                              # Project overview and repository guide
