# Results

## Overall Findings

The experiments show that small-scale continued pretraining can meaningfully reshape genomic representations without requiring de novo foundation-model training.

### Assembled-Genome Clustering
Embeddings were generated from non-overlapping 2.5 kbp windows from three recently sequenced bacterial isolates and clustered using k-means with k = 3.
Performance was evaluated using Adjusted Rand Index (ARI), Normalized Mutual Information (NMI), and cluster purity.

- All four PlasticDB adaptations improve assembled-genome clustering relative to DNABERT-2.
- Complete-genome adaptation produces the strongest DNABERT-2 result.
- DNABERT-S begins with substantially stronger species-aware clustering than DNABERT-2.
- DNABERT-S + complete genomes produces the strongest assembled-genome result overall.
- DNABERT-S is more sensitive to the assembly-level adaptation corpus.
- Scaffold adaptation substantially reduces DNABERT-S clustering performance.

### PacBio Raw-Read Clustering
The same model configurations were evaluated directly on PacBio raw sequencing reads.
Balanced subsets ranging from 1,000 to 9,500 reads per organism were used.

- Complete-genome adaptation is the strongest DNABERT-2 configuration at every evaluated read-set size.
- DNABERT-S + chromosomes produces the highest ARI at 9 of the 10 evaluated subset sizes.
- DNABERT-S + contigs produces the highest ARI at the 2,000-read subset.
- Adaptation effects remain visible when evaluation shifts from assembled genomes to error-prone raw sequencing reads.
- Scaffold adaptation again produces a substantial degradation for DNABERT-S.

### Promoter Classification
Downstream transfer was evaluated using human promoter tasks from GUE-v2/prom and organism-specific prokaryotic promoter tasks from iPro-MP.
Each baseline and adapted model was fine-tuned using 10 matched random seeds. Statistical testing used paired, two-sided t-tests on seed-level F1 differences.
Benjamini-Hochberg correction was applied within benchmark and backbone families. The results indicate that promoter-classification capability is generally retained after PlasticDB adaptation, but there is no evidence for a systematic downstream promoter-classification advantage.Across the human GUE-v2/prom and prokaryotic iPro-MP benchmarks

- 123 of 216 baseline-versus-adapted comparisons, or **57%**, produced a higher adapted-model mean F1.
- Six positive differences were nominally significant before multiple-testing correction.
- None remained significant after Benjamini-Hochberg correction.

These results indicate that previously learned genomic information remains usable after adaptation, but promoter-classification gains are heterogeneous and not systematic.
