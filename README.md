# Adaptation of Genomic Foundation Models for Plastic Degradation-Associated Bacterial Sequence Representation

[![ICMLA 2026](https://img.shields.io/badge/ICMLA-2026-blue)](https://www.icmla-conference.org/)
[![DNABERT-2](https://img.shields.io/badge/Backbone-DNABERT--2-4C72B0)](https://github.com/MAGICS-LAB/DNABERT_2)
[![DNABERT-S](https://img.shields.io/badge/Backbone-DNABERT--S-55A868)](https://github.com/MAGICS-LAB/DNABERT_S)
[![Models](https://img.shields.io/badge/Hugging%20Face-Models-yellow)](https://huggingface.co/astanesc)

[**Adaptation of Genomic Foundation Models for Plastic Degradation-Associated Bacterial Sequence Representation**](https://ieeexplore.ieee.org/document/11760871/)  
*2026 International Conference on Machine Learning and Applications (IEEE ICMLA 2026)*

## Overview

Training genomic foundation models from scratch requires large sequence corpora and substantial computational resources. This project investigates a more computationally accessible alternative: **continued pretraining of existing genomic foundation models on a specialized bacterial sequence domain**.

We adapt two related genomic foundation models:

- **[DNABERT-2](https://github.com/MAGICS-LAB/DNABERT_2)**, a general multi-species genomic foundation model.
- **[DNABERT-S](https://github.com/MAGICS-LAB/DNABERT_S)**, a species-aware model initialized from [DNABERT-2](https://github.com/MAGICS-LAB/DNABERT_2) and further trained using curriculum contrastive learning.

The adaptation domain is constructed from bacterial genomic sequences associated with plastic biodegradation using [PlasticDB](https://plasticdb.org/).

**Research question:** Can small-scale continued pretraining specialize genomic representations for plastic-degradation-associated bacteria while preserving knowledge acquired during foundation-model pretraining?

## Approach

Four PlasticDB-derived adaptation corpora are evaluated: **complete genomes | chromosomes | scaffolds | contigs**<br>
Both [DNABERT-2](https://github.com/MAGICS-LAB/DNABERT_2) and [DNABERT-S](https://github.com/MAGICS-LAB/DNABERT_S) are adapted using curriculum contrastive learning and evaluated in two complementary ways: (1) **Embedding-space evaluation** using three recently sequenced bacterial isolates, assembled genomes, and PacBio raw reads, and (2) **Downstream task evaluation** using human and prokaryotic promoter-classification benchmarks. See [Methods](docs/methods.md) and [Results](docs/results.md) for details.

## Key Findings

- Small-scale continued pretraining reshapes genomic embedding structure.
- Adaptation depends on both the starting backbone and the assembly-level corpus.
- Complete-genome adaptation performs best for DNABERT-2.
- DNABERT-S begins with stronger species-aware representations but is more corpus-sensitive.
- Adaptation effects remain visible on PacBio raw sequencing reads.
- Local embedding changes can be biologically interpretable without implying plastic-degradation function.
- Previously learned information remains usable for promoter classification, although downstream gains are heterogeneous and not systematic.
- Detailed results are available in [Results](docs/results.md).

## Documentation
- [Methods](docs/methods.md) - adaptation corpora, contrastive training, and hyperparameters
- [Results](docs/results.md) - assembled genomes, raw reads, local embedding behavior, and promoter results

## Models
Adapted model checkpoints are available through Hugging Face: [https://huggingface.co/astanesc/](https://huggingface.co/astanesc/)

## Software Attribution and Citations
This work builds on the public implementation of [DNABERT-2](https://github.com/MAGICS-LAB/DNABERT_2) and [DNABERT-S](https://github.com/MAGICS-LAB/DNABERT_S).<br>
Plastic degradation-associated microorganisms were identified using [PlasticDB](https://plasticdb.org/).<br><br>
If you use this repository, adapted models, the three bacterial genomes, or results from this work, please cite:<br>
- [Adaptation of Genomic Foundation Models for Plastic Degradation-Associated Bacterial Sequence Representation](https://ieeexplore.ieee.org/document/11760871/)
- [*Sphingobium yanoikuyae* CC4533](https://doi.org/10.1128/mra.01181-25)
- [*Acidovorax temperans* LMJ](https://doi.org/10.1128/mra.01293-23)
- [*Microbacterium* sp. Clip185](https://doi.org/10.1128/mra.01348-24)
