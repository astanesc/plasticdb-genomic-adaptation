# Results

## Overall Findings

The experiments show that small-scale continued pretraining can meaningfully reshape genomic representations without requiring de novo foundation-model training.

### Promoter Classification

Across the human GUE-v2/prom and prokaryotic iPro-MP benchmarks:

- 123 of 216 baseline-versus-adapted comparisons, or **57%**, produced a higher adapted-model mean F1.
- Six positive differences were nominally significant before multiple-testing correction.
- None remained significant after Benjamini-Hochberg correction.

These results indicate that previously learned genomic information remains usable after adaptation, but promoter-classification gains are heterogeneous and not systematic.
