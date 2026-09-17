# Clase-genomica-funcional
# Functional Genomics of Coffea arabica in response to Xylella fastidiosa

This repository contains the code used for the functional genomics analysis of the transcriptomic response of two *Coffea arabica* cultivars, Catuai and CR95, to *Xylella fastidiosa* infection.

The main objective was to compare the transcriptional response of both cultivars and identify differentially expressed genes, enriched biological processes, transcription factors, and regulatory motifs potentially associated with the response to *X. fastidiosa*.

## Experimental design

The RNA-seq dataset included 15 samples divided into four experimental groups:

- Catuai saline control: n = 3
- Catuai Xylella: n = 5
- CR95 saline control: n = 4
- CR95 Xylella: n = 3

Differential expression was evaluated independently for each cultivar by comparing Xylella-treated samples against saline controls.

## Analysis workflow

The general analysis workflow was:

FastQC → Trimmomatic → HISAT2 → featureCounts → DESeq2 → CAMERA/GO → KEGG Mapper → Transcription factor analysis → MEME/TOMTOM/FIMO

An additional exploratory WGCNA analysis was performed to evaluate gene co-expression patterns.

## Repository contents

### `DESeq_and_KEGG_Mapper.R`
Contains the main differential expression analysis, including:

- Count and metadata import
- Gene filtering
- DESeq2 normalization and differential expression analysis
- Variance stabilizing transformation
- PCA
- Hierarchical clustering heatmap
- Volcano plots
- DEG classification
- Preparation of KO identifiers for KEGG Mapper visualization

Significant genes were defined using:

`padj < 0.05`

Induced genes:

`padj < 0.05` and `log2FoldChange > 0`

Repressed genes:

`padj < 0.05` and `log2FoldChange < 0`

### `CAMERA_GO.R`
Contains the functional enrichment analysis performed separately for Catuai and CR95 using CAMERA.

The workflow includes:

- TMM normalization
- voom transformation
- GO gene set preparation
- CAMERA competitive gene set testing
- FDR correction
- GO term visualization
- Jaccard similarity analysis
- Enrichment network construction

Significant GO terms were defined as:

`FDR < 0.05`

### `Transcription_factors.R`
Contains the identification and classification of significantly differentially expressed transcription factors.

Functional annotation was used to identify transcription factor families including WRKY, MYB, NAC, bZIP, AP2/ERF and others.

### `MEME_and_FIMO.txt`
Contains the commands used for promoter and motif analysis, including:

- Selection of significantly induced protein coding genes
- Extraction of 1,000 bp upstream promoter regions with BEDTools
- De novo motif discovery with MEME
- Motif comparison with TOMTOM using JASPAR CORE Plants
- Motif scanning with FIMO

The promoter analysis was performed separately for Catuai and CR95.

### `WGCNA.R`
Contains the exploratory weighted gene co-expression network analysis.

The analysis includes:

- Selection of the 5,000 genes with highest expression variance
- Soft threshold selection
- Construction of a signed co-expression network
- Identification of co-expression modules
- Evaluation of the Cultivar × Treatment interaction
- Module membership analysis
- Integration with DESeq2 interaction results
- Preparation and export of network information to Cytoscape

## Reference genome

The *Coffea arabica* Coffea Arabica ET-39 HiFi reference genome and corresponding annotation were obtained from NCBI.

NCBI accession:

`GCF_036785885.1`

## Main software

- R 4.5.2
- DESeq2 1.48.1
- edgeR 4.6.3
- limma 3.64.3
- ggplot2 4.0.3
- pheatmap 1.0.13
- EnhancedVolcano 1.26.0
- GO.db 3.21.0
- AnnotationDbi 1.70.0
- WGCNA
- BEDTools 2.31.1
- MEME Suite 5.5.9
- Cytoscape 3.10.4

## Input files

The main R analyses require:

- `Matrix_hisat2.txt`: featureCounts-derived gene count matrix generated from HISAT2 alignments
- `metadata.txt`: sample information containing cultivar and treatment
- Functional annotation file containing gene IDs, gene descriptions, GO terms, KEGG identifiers and protein domains

Large sequencing files such as FASTQ and BAM files are not included in this repository.

## Authors

Functional Genomics course project.
Tecnológico de Monterrey.
