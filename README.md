# DMF-DM-seq

High-throughput data analysis of miRNA. After obtaining miRNA sequencing data, cutadapt (version 3.4) was used to remove adapters and trim low-quality bases from high-throughput single-cell miRNA data, with parameters set to: -q 20 -j 20 -e 0.2 -n 2 -O 10 -m 15. The quality-controlled sequences were then aligned to reference genomes and miRNA groups using mapper.pl in miRDeep2 (version 1.1.2). 

High-throughput data analysis of mRNA. After obtaining the cDNA sequencing data, trim_galore (version 0.6.10) is used to filter the data and remove adapter sequences, with the parameters set as: -q 25 --phred33 --length 25 -e 0.1 --stringency 4 --paired. The quality-controlled data is then aligned using STAR (version 2.7.3a) for paired-end mapping. For the data that requires downsampling, random sampling will be carried out to achieve the desired sequencing depth. The R package ggplot2 (version 3.4.4) is used to create bar charts, correlation scatter plots, and other graphics.

Co-analysis of miRNA and mRNA. Differential gene expression analysis was performed using the R package DESeq2 (version 1.38.3), with normalization based on the mean of raw data, and genes selected based on log2FoldChange >= 1 or <=-1 and res1$padj < 0.05. Differential genes were visualized using pheatmap (version 1.0.12) and EnhancedVolcano (version 1.16.0). GO and KEGG pathway enrichment analysis was performed using clusterProfiler (version 4.6.1) and ggplot2 (version 3.4.1), with parameters set to pvalueCutoff = 0.05, pAdjustMethod = "BH", and qvalueCutoff = 0.05. Cell clustering analysis for three cell types was performed using Seurat (version 4.3.0) and ggplot2 (version 3.4.1). miRNA target mRNAs were collected from three databases (miRWalk, TargetScan, and miRDB) and their intersection was used as a new database for co-analysis of miRNA and mRNA. MiRNAs expressed in each cell and with expression levels greater than 10 were selected from the expression matrix. Target mRNAs of these miRNAs were then identified from the new co-analysis database, and gene set enrichment analysis was performed using gsea (version 4.3.2). Differential expression analysis was performed using DESeq2 (version 1.38.3) based on the expression matrix, with H2228 and H1975 used for differential gene analysis of A549 followed by merging of differential expression results. KEGG pathway analysis was performed using dplyr (version 1.1.0), clusterProfiler (version 4.6.1), and ggplot2 (version 3.4.1), selecting important pathways that involve targeted genes. MiRNAs that could express these genes were then identified from the co-analysis database and ranked based on context score provided by TargetScan. miRNA-mRNA interaction pairs with log2FoldChange >= 2 or <=-2 and res1$padj < 0.01 were selected for subsequent analysis. MiRNAs with at least one overlapping gene were considered to be related, and the relationship between miRNAs involved in the pathway was characterized by the Jaccard similarity coefficient of overlapping genes. Cytoscape (version 3.9.1) was used to visualize the relationship heatmap.
