# Adaptation of Genomic Foundation Models for Plastic Degradation-Associated Bacterial Sequence Representation

[![ICMLA 2026](https://img.shields.io/badge/ICMLA-2026-blue)](https://www.icmla-conference.org/)
[![DNABERT-2](https://img.shields.io/badge/Backbone-DNABERT--2-4C72B0)](https://github.com/MAGICS-LAB/DNABERT_2)
[![DNABERT-S](https://img.shields.io/badge/Backbone-DNABERT--S-55A868)](https://github.com/MAGICS-LAB/DNABERT_S)
[![Models](https://img.shields.io/badge/Hugging%20Face-Models-yellow)](https://huggingface.co/astanesc)

**Adaptation of Genomic Foundation Models for Plastic Degradation-Associated Bacterial Sequence Representation**  
*2026 International Conference on Machine Learning and Applications (IEEE ICMLA 2026)*

## Overview

Training genomic foundation models from scratch requires large sequence corpora and substantial computational resources. This project investigates a more computationally accessible alternative: **continued pretraining of existing genomic foundation models on a specialized bacterial sequence domain**.

We adapt two related genomic foundation models:

- **DNABERT-2**, a general multi-species genomic foundation model.
- **DNABERT-S**, a species-aware model initialized from DNABERT-2 and further trained using curriculum contrastive learning.

The adaptation domain is constructed from bacterial genomic sequences associated with plastic biodegradation using [PlasticDB](https://plasticdb.org/).

**Research question:** Can small-scale continued pretraining specialize genomic representations for plastic-degradation-associated bacteria while preserving knowledge acquired during foundation-model pretraining?

## Approach

Four PlasticDB-derived adaptation corpora are evaluated: **complete genomes | chromosomes | scaffolds | contigs**
Both DNABERT-2 and DNABERT-S are adapted using curriculum contrastive learning and evaluated in two complementary ways:

1. **Embedding-space evaluation** using three recently sequenced bacterial isolates, assembled genomes, and PacBio raw reads.
2. **Downstream task evaluation** using human and prokaryotic promoter-classification benchmarks.

See [Methods](docs/methods.md) and [Evaluation](docs/evaluation.md) for details.

## Key Findings

- Small-scale continued pretraining reshapes genomic embedding structure.
- Adaptation depends on both the starting backbone and the assembly-level corpus.
- Complete-genome adaptation performs best for DNABERT-2.
- DNABERT-S begins with stronger species-aware representations but is more corpus-sensitive.
- Adaptation effects remain visible on PacBio raw sequencing reads.
- Local embedding changes can be biologically interpretable without implying plastic-degradation function.
- Previously learned information remains usable for promoter classification, although downstream gains are heterogeneous and not systematic.

Detailed results are available in [Results](docs/results.md).

## Documentation

- [Methods](docs/methods.md) - adaptation corpora, contrastive training, and hyperparameters
- [Evaluation](docs/evaluation.md) - embedding-space and promoter-classification protocols
- [Results](docs/results.md) - assembled genomes, raw reads, local embedding behavior, and promoter results
- [Limitations](docs/limitations.md) - interpretation, confounding factors, and experimental controls
- [References](docs/references.md) - published papers and external resources

## Models
Adapted model checkpoints are available through Hugging Face: [https://huggingface.co/astanesc/](https://huggingface.co/astanesc/)

## Repository Scope
This repository contains the scientific code associated with the study, including:<br>
- PlasticDB-derived sequence preparation
- genomic foundation-model adaptation
- embedding extraction
- assembled-genome clustering evaluation
- raw-read clustering evaluation
- promoter fine-tuning and evaluation
- statistical analysis<br>
Institutional infrastructure, credentials, cloud provisioning, and Azure-specific deployment scripts are not included.

## Software Attribution
This work builds on the public implementations of [DNABERT-2](https://github.com/MAGICS-LAB/DNABERT_2) and [DNABERT-S](https://github.com/MAGICS-LAB/DNABERT_S)<br>
Plastic degradation-associated microorganisms were identified using [PlasticDB](https://plasticdb.org/).<br>
Please cite the corresponding published papers listed in [References](docs/references.md).

### Citation
If you use this repository, adapted models, or results from this work, please cite:<br>
**Adaptation of Genomic Foundation Models for Plastic Degradation-Associated Bacterial Sequence Representation.** <br>
*2026 International Conference on Machine Learning and Applications (IEEE ICMLA 2026).*<br>
IEEE Xplore:  https://ieeexplore.ieee.org/document/11760871/
