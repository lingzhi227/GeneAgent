# High-Level Gene LLMs: Natural Language Interpretation of Genomic Behavior

## Overview

This document organizes currently existing research projects or platforms that use large language models (LLMs) for natural language interpretation of genomic behavior. These systems attempt to "translate" information from multi-omics databases into natural language expressions.

---

## 🧠 I. LLM Application Frameworks for Genomic Annotation and Functional Interpretation

### 1. **BioGPT / GeneGPT / SciBERT and Other Fine-tuned LLM Models**

- **Data Foundation**: PubMed abstracts, Gene Ontology, UniProt annotations, etc.
- **Function**: Provide explanatory answers for specified genes, mutations, or pathways
- **Limitations**: Cannot directly understand ChIP-seq, GRO-seq tracks, or multimodal epigenetic data

### 2. **GeneTuring / Genomic LLMs**

From collaborative research between Google DeepMind, Meta AI, and Broad Institute, attempting to use transformer models for "natural language interpretation" of the human genome.

Examples:
- **Enformer** (Basenji successor): Uses sequence context to predict ChIP-seq / RNA-seq tracks
- **GenSLMs** (NVIDIA): Integrates omics data, viral mutations, and functional interpretation

**Purpose**: Model inputs gene region sequences, outputs corresponding epigenetic regulatory behaviors (such as RNA polymerase binding strength, chromatin accessibility, etc.) or functional annotations.

### 3. **Natural Language Interface Platforms (such as Seek AI / BioCypher)**

- Attempt to establish LLM → SQL/GraphQL generators, allowing users to query GEO/ENCODE data using natural language
- For example, input "In which cells is POLR2A enriched near the TP53 promoter?" → automatically convert to API query

---

## 🧬 II. Current Typical Tasks of LLMs on Multi-omics Data

| Task Type | Example Models or Systems | Supported Data Types | Natural Language Behavior |
|-----------|---------------------------|---------------------|---------------------------|
| **Sequence→Function Prediction** | Enformer, Basset | FASTA + ChIP-seq | "This sequence may be an active promoter" |
| **Gene Annotation Explanation** | BioGPT, GeneTuring | UniProt + GO + Literature | "TP53 encodes a transcription factor that regulates cell cycle" |
| **Data Track Summarization** | Still exploring (mostly rules+LLM) | ChIP-seq, GRO-seq | "In liver cells, this gene's expression is driven by enhancer X" |
| **Natural Language Query of Omics Databases** | BioCypher, LangChain + GEO/ENCODE interfaces | Tables/tracks/metadata | "Show all transcription factors upregulated in human liver" |

---

## 🛠 III. Systematic Methods Worth Trying

### A. **Transcriptional Regulation Prediction Through Genomic Large Models like Enformer**

- **Input**: DNA sequence (such as a promoter region)
- **Output**: Predicted Pol II binding strength, RNA-seq signal, DNase-seq accessibility, etc.
- **Advantages**: Pre-trained models have integrated ENCODE / Roadmap data
- **Open Source Code**:
  - [https://github.com/deepmind/deepmind-research/tree/master/enformer](https://github.com/deepmind/deepmind-research/tree/master/enformer)

### B. **Building Natural Language Q&A Interface + Data Warehouse (Knowledge Graph)**

- **Tools**: `LangChain` + `BioCypher` + `ChromaDB` + GEO/ENCODE metadata
- **Capabilities**: Ask questions in natural language → automatically convert to SQL → extract descriptions from multi-omics tracks → call LLM to translate into explanatory language

### C. **Converting Tracks to Images + Vision LLM (such as Gemini, GPT-4o)**

- Export Pol II/GRO-seq tracks from UCSC or WashU browsers as images (or vectors), input into Vision-Language models for "annotation-style interpretation"

---

## 📘 IV. Example: "Natural Language Interpretation of a Gene's Behavior"

**Target Gene**: *TP53*

**Integrated Model Response**:
"TP53 is a tumor suppressor gene highly expressed in multiple tissues, whose transcription is regulated by multiple enhancer regions. In ENCODE data, RNA polymerase II shows significant binding enrichment at its promoter region, particularly showing enhanced GRO-seq and PRO-seq signals in liver and lung cells, indicating high transcriptional activity in these environments. Meanwhile, H3K27ac and H3K4me3 modifications support its promoter open state."

---

## ✅ V. Summary: Are There LLMs That Can Interpret These Databases in Natural Language?

| Question | Answer |
|----------|--------|
| Are there LLMs that provide natural language explanations of gene function? | ✅ Yes, such as BioGPT, GeneTuring |
| Are there LLMs that can interpret track data (such as ChIP-seq)? | 🟡 Some models indirectly support this, such as Enformer which can predict tracks but not natural language output |
| Are there LLMs that can directly integrate GEO/ENCODE? | 🟡 Under development, some achieve natural language queries through API + LLM |
| Are there complete systems that can automatically "understand gene behavior tracks" and explain them? | ❌ Not yet fully implemented, currently requires manual pipeline construction or semi-automated systems |

---

## 🗣 VI. Support Status of Natural Language Explanation Models

### ✅ Examples of Supported Models:

| Model | Supports Natural Language Explanation? | Example |
|-------|---------------------------------------|---------|
| **GeneTuring** | ✅ | "TP53 is a tumor suppressor gene involved in DNA damage response and cell cycle regulation." |
| **BioGPT** | ✅ | "BRCA1 is associated with breast cancer susceptibility and DNA repair." |
| **GeneFormer** | 🟡 (mostly embeddings) | Can be used for transfer tasks, classification, similar gene matching |
| **scGPT / Enformer** | ❌ (outputs numerical tracks) | Does not directly generate language |

### Training Data Sources:
The training data for these natural language explanation models often comes from:
- PubMed abstracts
- Gene Ontology descriptions
- UniProt / NCBI gene function summaries

---

## 🔍 VII. Constructible GeneLM Interface

You can completely combine these two types to create a "track-to-explanation" pipeline:

```
DNA sequence/ChIP-seq tracks (Enformer, scGPT)
    ↓
Structured behavior (RNA expression, regulatory distribution)
    ↓
LLM prompt: "Given the RNA expression profile of TP53, describe its regulation."
    ↓
Natural language explanation (BioGPT, LLaMA + Finetune)
```

> You can research: Can LLMs automatically "learn" biological regulatory semantics based on "behavioral tracks"?

---

## ✅ VIII. Summary Answer to Key Questions

**"What are the results of GeneLM like? Is it given a gene, output an explanation?"**

- **Some GeneLMs (such as BioGPT, GeneTuring)**: Yes, they **accept gene names or descriptions and output natural language explanations**
- **Other GeneLMs (such as Enformer, scGPT)**: **Accept gene sequences or expression data and output numerical tracks or vector representations**, which can be used for regulatory prediction or expression modeling, but not direct natural language

---

## 🚀 IX. Construction Recommendations

If you want to build a system with this capability (such as "track diagrams → LLM interpretation" or "natural language → multi-omics search"), you can:

1. Integrate existing LLM models (such as Enformer, BioGPT)
2. Use Python to interface with GEO/ENCODE APIs to build data extractors
3. Build LangChain-style query-translation systems

### Possible Research Directions:
- Build a "track-to-language explanation" hybrid model
- Design a "reversible GeneLM": can both predict behavior and explain behavioral causes

---

## 📝 Current Development Status

According to the original answer, it is still in the **frontier exploration stage** overall, with no unified LLM that fully supports these databases. Currently, the closest approaches are combinations of several types of solutions, requiring manual pipeline construction or semi-automated systems to achieve complete natural language interpretation of genomic behavior.