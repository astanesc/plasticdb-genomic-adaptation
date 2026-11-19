# Results

## Evaluation Genomes

Embedding-space evaluation uses three newly sequenced bacterial isolates:

- *Sphingobium yanoikuyae* CC4533 ([Mitra and Stanescu, 2026](https://doi.org/10.1128/mra.01181-25))
- *Acidovorax temperans* LMJ ([Mitra and Stanescu, 2024](https://doi.org/10.1128/mra.01293-23))
- *Microbacterium* sp. Clip185 ([Mitra and Stanescu, 2025](https://doi.org/10.1128/mra.01348-24))

Complete genome assemblies and PacBio raw reads are available for all three isolates.

## Assembled-Genome Clustering

Embeddings were generated from non-overlapping 2.5 kbp windows and clustered using k-means with `k = 3`.
Performance was evaluated using Adjusted Rand Index (ARI), Normalized Mutual Information (NMI), and cluster purity.

Key observations:
- All four PlasticDB adaptations improve assembled-genome clustering relative to DNABERT-2.
- Complete-genome adaptation produces the strongest DNABERT-2 result.
- DNABERT-S begins with substantially stronger species-aware clustering than DNABERT-2.
- DNABERT-S + complete genomes produces the strongest assembled-genome result overall.
- DNABERT-S is more sensitive to the assembly-level adaptation corpus.
- Scaffold adaptation substantially reduces DNABERT-S clustering performance.

## PacBio Raw-Read Clustering

The same model configurations were evaluated directly on PacBio raw sequencing reads using balanced subsets ranging from 1,000 to 9,500 reads per organism.
At 9,500 reads per organism:

| Model | ARI |
|---|---:|
| DNABERT-2 | 0.3849 |
| **DNABERT-2 + genomes** | **0.7423** |
| DNABERT-S | 0.7718 |
| DNABERT-S + genomes | 0.7941 |
| **DNABERT-S + chromosomes** | **0.8114** |
| DNABERT-S + contigs | 0.8022 |

Key observations:
- Complete-genome adaptation is the strongest DNABERT-2 configuration at every evaluated read-set size.
- DNABERT-S + chromosomes produces the highest ARI at 9 of the 10 evaluated subset sizes.
- DNABERT-S + contigs produces the highest ARI at the 2,000-read subset.
- Adaptation effects remain visible when evaluation shifts from assembled genomes to raw sequencing reads.
- Scaffold adaptation again produces a substantial degradation for DNABERT-S.

## Promoter Classification

Downstream transfer was evaluated using human promoter tasks from GUE-v2/prom and organism-specific prokaryotic promoter tasks from iPro-MP.
Each baseline and adapted model was fine-tuned using 10 matched random seeds. Statistical testing used paired, two-sided t-tests on seed-level F1 differences, with Benjamini-Hochberg correction applied within benchmark and backbone families. Across the human GUE-v2/prom and prokaryotic iPro-MP benchmarks:
- 123 of 216 baseline-versus-adapted comparisons, or **57%**, produced a higher adapted-model mean F1.
- Six positive differences were nominally significant before multiple-testing correction.
- None remained significant after Benjamini-Hochberg correction.

These results indicate that previously learned genomic information remains usable after PlasticDB adaptation, but promoter-classification gains are heterogeneous and not systematic.
