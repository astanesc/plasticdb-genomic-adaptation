# Methods

## Genomic Foundation Models

We adapt two related genomic foundation models: [DNABERT-2](references.md#dnabert-2) and [DNABERT-S](references.md#dnabert-s).

### DNABERT-2

DNABERT-2 is a 117M-parameter multi-species genomic foundation model pretrained using **Masked Language Modeling (MLM)**. It uses Byte Pair Encoding (BPE) tokenization to represent variable-length nucleotide subsequences.

### DNABERT-S

DNABERT-S is initialized from DNABERT-2 and further trained using **Curriculum Contrastive Learning (C<sup>2</sup>LR)** to produce species-aware genomic representations.

During PlasticDB adaptation:

- **DNABERT-2:** MLM -> C<sup>2</sup>LR
- **DNABERT-S:** C<sup>2</sup>LR -> C<sup>2</sup>LR (training objective remains unchanged)

## PlasticDB Adaptation Corpus

Plastic degradation-associated microorganisms were identified using [PlasticDB](https://plasticdb.org/).
Four genomic assemblies were collected to construct the adaptation corpora:

| Assembly subset | Total organisms | Shared | Unique | Training pairs |
|---|---:|---:|---:|---:|
| Complete genomes | 316 | 302 | 14 | 152,182 |
| Chromosomes | 168 | 160 | 8 | 106,826 |
| Scaffolds | 553 | 462 | 91 | 337,395 |
| Contigs | 539 | 456 | 83 | 330,209 |

The four subsets are intentionally not taxonomically independent. Instead, they represent different forms of genomic context:

- **Complete genomes** preserve the most complete sequence organization.
- **Chromosomes** retain long-range genomic context.
- **Scaffolds** represent partially assembled genomes.
- **Contigs** represent more fragmented draft assemblies.

This design tests whether continued pretraining depends on the assembly-level structure of the adaptation corpus.

## Contrastive Pair Construction

Continued pretraining follows the C<sup>2</sup>LR framework used by DNABERT-S.

Training examples are constructed as follows:

- Positive pairs consist of non-overlapping DNA regions from the same organism.
- Sequences from different organisms act as contrastive negatives.
- Source regions are 10 kbp.
- Source regions are divided into 2 kbp training windows.
- Maximum model input length is 512 BPE tokens.

The same adaptation procedure is applied independently to DNABERT-2 and DNABERT-S for each of the four PlasticDB assembly-level corpora.

## Curriculum Contrastive Learning

Training proceeds over three epochs using a curriculum that changes the contrastive-learning strategy over time.

### Epoch 1: Weighted SimCLR

Epoch 1 uses weighted SimCLR-style contrastive learning.

The objective encourages:

- representations from the same organism to move closer together in embedding space;
- representations from different organisms to move farther apart.

### Epochs 2-3: Manifold i-Mix

Epochs 2 and 3 use manifold i-Mix.

Rather than mixing raw nucleotide sequences, manifold i-Mix interpolates internal hidden representations during contrastive training. This creates intermediate training examples intended to make the contrastive task more difficult.

## Continued-Pretraining Configuration

| Parameter | Value |
|---|---:|
| Epochs | 3 |
| GPU | NVIDIA Tesla T4, 16 GB |
| Per-device batch size | 12 |
| Gradient accumulation | 4 |
| Effective batch size | 48 |
| Learning rate | 3e-6 |
| Contrastive temperature | 0.05 |
| i-Mix alpha | 1.0 |

The experiments were intentionally designed around modest GPU resources rather than large-scale de novo foundation-model pretraining.

## Adapted Model Families

Each backbone is adapted independently using each PlasticDB corpus, producing eight adapted model configurations:

### DNABERT-2

- DNABERT-2 + complete genomes
- DNABERT-2 + chromosomes
- DNABERT-2 + scaffolds
- DNABERT-2 + contigs

### DNABERT-S

- DNABERT-S + complete genomes
- DNABERT-S + chromosomes
- DNABERT-S + scaffolds
- DNABERT-S + contigs

Each adapted model is compared with its corresponding unadapted backbone during evaluation.

## Next

See:

- [Evaluation](evaluation.md) for embedding-space and promoter-classification protocols.
- [Results](results.md) for assembled-genome, raw-read, and promoter results.
- [Limitations](limitations.md) for interpretation and experimental constraints.
- [References](references.md) for the published DNABERT-2, DNABERT-S, PlasticDB, SimCLR, and i-Mix papers.
