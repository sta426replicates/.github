# How many replicates do you actually need for RNA-seq?

A benchmark of differential expression tools (DESeq2, edgeR, limma-voom, Wilcoxon)
at small sample sizes, implemented as [omnibenchmark](https://omnibenchmark.org) modules.
Random subsets of 2–20 replicates of the 48-replicate yeast WT vs snf2 experiment
(Schurch et al. 2016) are scored against the full-replicate comparison.

**Plan:** https://github.com/sta425-replicates/sta425_Project

## Modules

| Stage     | Repository | Entrypoints | Outputs |
|-----------|------------|-------------|---------|
| Data      | https://github.com/sta425-replicates/sta425_data | `default` | `counts.tsv.gz`, `coldata.tsv` |
| Truth     | https://github.com/sta425-replicates/sta425_truth | `default` | `truth.tsv` |
| Subsample | https://github.com/sta425-replicates/sta425_subsample | `default` | `counts.tsv.gz`, `coldata.tsv`, `subsample.json` |
| DE        | https://github.com/sta425-replicates/sta425_de | `deseq2`, `edger`, `limma_voom`, `wilcoxon` | `de_results.tsv`, `de_info.json` |
| Metrics   | https://github.com/sta425-replicates/sta425_metrics | `default` | `scores.tsv` |
| Summary   | https://github.com/sta425-replicates/sta425_summary | `default` | `summary.tsv`, `stability.tsv`, `report.html` |

## Contributing

### Change or add a method

- Add an entrypoint to the stage's repository and list it in that repo's `omnibenchmark.yaml`.
- Follow the file formats in the stage's README; the DE output schema
  (`gene, logFC, pvalue, padj`) is shared by every method.
- Add the module to `benchmark.yaml` in the plan repository.

### Test changes in the benchmark

1. Create a branch (`feat/<name>`), using the same branch name across all linked PRs.
2. Run `ob validate plan benchmark.yaml` and `ob run benchmark.yaml --unpinned`.
3. Open a PR to the plan repository; once merged, pin the module's `commit:` to its new hash.
