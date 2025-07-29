# Detailed Description of Genomic Databases

## Overview

This document provides detailed introduction to various database resources related to DNA information translation and genomic behavior interpretation, as well as their roles in multi-level molecular mechanism maps.

---

## 🧬 I. Central Process of DNA Information Translation: From Sequence to Function Transfer Pathway

### Core Chain (Information Flow):

```
DNA (sequence + epigenetic marks)
   ↓ (transcription initiation and regulation)
Precursor mRNA (regulation, splicing)
   ↓ (maturation and export)
Mature mRNA (stability, localization)
   ↓ (translation and regulation)
Proteins (active complexes, regulatory circuits)
   ↓
Cellular behavior & phenotype
```

Each step involves specific molecular mechanisms and corresponding experimental recording methods.

---

## 🧪 II. Correspondence Between Key Molecules and Experimental Methods

| Biological Level | Core Molecular Behavior | Representative Data Types | What the Data Represents |
|------------------|------------------------|---------------------------|--------------------------|
| **DNA Sequence** | Gene location, promoters, enhancers, etc. | Gene annotation (RefSeq, Ensembl) | Information template |
| **Epigenetic Modifications** | DNA methylation, histone modifications | **Bisulfite-seq**, **ChIP-seq(H3K27ac, H3K4me3)** | Control gene readability |
| **Transcription Factor Binding** | TF-DNA specific binding | **ChIP-seq (TFs)** | Activate or repress transcription |
| **RNA Polymerase Behavior** | Initiation, pausing, elongation, termination | **ChIP-seq(Pol II)**, **NET-seq**, **PRO-seq**, **GRO-seq** | Real-time recording of transcriptional state |
| **RNA Generation** | Transcription product formation | **RNA-seq**, **CAGE** | Actual expression levels and splicing status |
| **RNA Stability and Translation Efficiency** | 3'UTR regulation, nuclear export, translation rate | **Ribo-seq**, **mRNA half-life** | Determine expression output efficiency |
| **Protein Expression** | Synthesis and degradation, post-translational modifications | **Mass spectrometry**, **PaxDb** | Protein abundance |
| **Protein Complex Behavior** | Multi-protein regulatory assembly | **CORUM**, **Reactome Pathways** | Coordinated behavior of molecular machines |
| **Regulatory Feedback** | Self-regulation, interaction networks | **Hi-C**, **TF motif analysis**, **Perturb-seq** | Network-level feedback control |

---

## 🧬 III. Multi-level Behavioral Network Centered on RNA Polymerase II

RNA Polymerase II (Pol II) is the most critical executor in DNA transcription, whose behavior connects epigenetic regulation and expression output. Below is the correspondence between its behavior and different data:

| Pol II Behavior | Data Type | Description |
|-----------------|-----------|-------------|
| **Recruitment to promoter** | ChIP-seq (Pol II + H3K4me3) | Identify gene initiation state |
| **Transcription initiation** | GRO-seq, PRO-seq | Detect active promoters, short transcripts |
| **Pausing (promoter-proximal pausing)** | NET-seq, PRO-seq | Assess transcriptional regulatory strength |
| **Elongation into gene body** | ChIP-seq (Pol II S2P), GRO-seq | Determine full-length mRNA generation |
| **Termination and release** | PolyA-seq, CAGE | Determine transcription termination sites |

These processes are subject to multiple regulations from:
- Epigenetic marks (such as H3K27ac) activating enhancers
- TF and Pol II interactions
- Chromatin conformation (such as looping) regulation

---

## 🔄 IV. Integrated Understanding Model from "Sequence to Behavior"

An integrated perspective is as follows:

```
▶ DNA Sequence
  ├─ Epigenetic modifications (ChIP-seq, BS-seq)
  ├─ TF binding sites (ChIP-seq)
  └─ Promoters/enhancers (ATAC-seq, DNase-seq)

▶ Transcriptional Behavior
  ├─ Polymerase tracks (NET-seq, GRO-seq)
  ├─ Actual expression (RNA-seq)
  └─ Splicing and alternative splicing (Long-read RNA-seq)

▶ Post-transcriptional Regulation
  ├─ Translation efficiency (Ribo-seq)
  ├─ RNA stability (half-life assay)
  └─ mRNA localization (FISH, subcellular fractionation)

▶ Protein Behavior
  ├─ Expression levels (MS-based proteomics)
  ├─ Complex formation (CORUM)
  └─ Functional pathways (Reactome, KEGG)

▶ Network Control
  ├─ Gene regulatory networks (TF-target motifs)
  └─ Feedback and topology (Hi-C, CRISPR perturbation)
```

This model allows you to start from "a DNA fragment" and track its fate in the cell until it becomes part of a molecular network that affects physiological behavior.

---

## 📘 V. Recommended Research/Tool Resources

| Name | Purpose | Link |
|------|---------|------|
| **ENCODE** | Multi-omics data integration platform | [https://www.encodeproject.org/](https://www.encodeproject.org/) |
| **GEO Datasets** | Find specific experimental datasets | [https://www.ncbi.nlm.nih.gov/geo/](https://www.ncbi.nlm.nih.gov/geo/) |
| **UCSC Genome Browser** | Data visualization and track overlay | [https://genome.ucsc.edu/](https://genome.ucsc.edu/) |
| **RegulomeDB** | Prediction of variant effects on regulatory behavior | [http://www.regulomedb.org/](http://www.regulomedb.org/) |
| **WashU Epigenome Browser** | Single-cell & omics data integration | [https://epigenomegateway.wustl.edu/](https://epigenomegateway.wustl.edu/) |

---

## 🔬 VI. Detailed Description of Specific Databases

### 1. **ENCODE (Encyclopedia of DNA Elements)**
- **Website**: https://www.encodeproject.org/
- **Content**: Contains large-scale ChIP-seq, RNA-seq, and GRO-seq data that can be used to analyze RNA polymerase binding and transcriptional activity across the genome
- **Advantages**: Rich data variety, including different cell lines and experimental conditions, suitable for analyzing transcription initiation, pausing, elongation, and other behaviors
- **Application**: Multi-omics data integration platform

### 2. **GEO (Gene Expression Omnibus)**
- **Website**: https://www.ncbi.nlm.nih.gov/geo/
- **Content**: NCBI's gene expression and functional genomics data repository. Contains extensive ChIP-seq and NET-seq data for RNA polymerase II and III
- **Advantages**: Can search keywords like "RNA Polymerase II ChIP-seq" or "PRO-seq" to find multiple high-quality experimental datasets
- **Application**: Find specific experimental datasets

### 3. **Roadmap Epigenomics Project**
- **Website**: http://www.roadmapepigenomics.org/
- **Content**: Provides epigenetic and transcriptional regulation-related data, including DNA methylation, histone modifications, RNA polymerase localization, etc.
- **Application**: If you want to explain transcriptase behavior from chromatin state, it provides valuable auxiliary data

### 4. **UCSC Genome Browser**
- **Website**: https://genome.ucsc.edu/
- **Application**: Data visualization and track overlay
- **Function**: Integrate multiple track data for visualization analysis

### 5. **RegulomeDB**
- **Website**: http://www.regulomedb.org/
- **Application**: Prediction of variant effects on regulatory behavior
- **Function**: Assess potential impact of genetic variants on transcriptional regulation

### 6. **WashU Epigenome Browser**
- **Website**: https://epigenomegateway.wustl.edu/
- **Application**: Single-cell & omics data integration
- **Function**: Support integrated analysis of single-cell data and multi-omics data

### 7. **PaxDb / CORUM / Reactome**
- **Function**: Although they don't directly provide RNA polymerase II dynamic trajectories, these databases can supplement information on **protein expression**, **complex composition**, **transcriptional regulatory pathways**, etc.
- **PaxDb**: Protein expression database
- **CORUM**: Protein complex database
- **Reactome**: Biological reaction pathway database

---

## 🧪 VII. Data Types Corresponding to Experimental Techniques

### Transcription-related techniques:
- **NET-seq (Native Elongating Transcript sequencing)**: Base-precise RNA polymerase active sites; can be used to detect transcriptional pausing and termination
- **PRO-seq (Precision Run-On sequencing)**: Similar to NET-seq, but can capture precise positions of actively transcribing RNA polymerase
- **GRO-seq (Global Run-On sequencing)**: Study genome-wide transcription initiation, pausing, and elongation
- **ChIP-seq (targeting RNA Polymerase II)**: Shows which regions RNA polymerase binds to DNA

### Epigenetic techniques:
- **Bisulfite-seq**: DNA methylation detection
- **ChIP-seq (H3K27ac, H3K4me3)**: Histone modification detection
- **ATAC-seq**: Chromatin accessibility detection
- **DNase-seq**: Open chromatin region detection

### Expression-related techniques:
- **RNA-seq**: Gene expression quantification
- **CAGE**: Precise localization of transcription start sites
- **PolyA-seq**: Transcription termination site detection
- **Long-read RNA-seq**: Full-length transcript and alternative splicing detection

### Translation and protein techniques:
- **Ribo-seq**: Translation efficiency detection
- **Mass spectrometry**: Proteome detection
- **FISH**: mRNA localization detection

### Interaction techniques:
- **Hi-C**: Chromatin three-dimensional structure detection
- **Perturb-seq**: Gene perturbation effect detection

---

## 📌 VIII. Summary

You can systematically explain the DNA information translation process through the following approaches:

1. **Use multi-omics data to restore molecular trajectories**: Such as RNA polymerase behavior, TF binding, epigenetic modifications
2. **Integrate data hierarchies**: From DNA → RNA → Proteins → Functional pathways → Network regulation
3. **Establish analysis pipelines**: Use public databases + bioinformatics pipelines (such as Snakemake, Nextflow) for cross-level modeling
4. **Use behavioral trajectories to predict regulatory causality**: Combine machine learning to build regulatory prediction models or transcriptional control maps

---

## 🔧 IX. Data Acquisition and Analysis Tools

### Search Keyword Examples:
Search in GEO:
```
RNA polymerase II NET-seq Homo sapiens
RNA polymerase PRO-seq mouse
```

### Data Processing Tools:
- **IGV** (visualization tool)
- **deepTools** (data processing)
- **pyBigWig** (Python reading)

### File Formats:
- `.bigWig` format track files
- `.bam` format alignment files

### Analysis Frameworks:
- Machine learning, sequence modeling, or kinetic modeling
- CNN, Transformer and other deep learning models
- Snakemake, Nextflow and other analysis pipeline tools

This database system provides a comprehensive data foundation for understanding gene expression regulation at the molecular level and building genomic behavior prediction models.