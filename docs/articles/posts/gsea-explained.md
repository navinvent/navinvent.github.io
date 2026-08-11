---
date: 2026-08-11
authors:
  - navin
categories:
  - Bioinformatics
---

# What is GSEA?

Gene Set Enrichment Analysis asks a question that a list of individual genes
can't answer on its own: is a whole *set* of related genes behaving differently
between two conditions, even when no single gene screams for attention?

<!-- more -->

## The problem it solves

Differential expression hands you a ranked list of genes. But biology rarely
acts one gene at a time — pathways move together, often in small coordinated
nudges. Twenty genes each shifting a little can matter more than one gene
shifting a lot, and a gene-by-gene threshold will miss it entirely.

## The idea

GSEA walks down your ranked list of all genes and asks whether the members of a
given gene set cluster toward the top (or bottom) more than chance would
predict. It accumulates a running enrichment score, then tests that score
against permutations.

## Worked example

```python
import gsea

results = gsea.run(
    ranked_list=ranked_genes,   # (1)
    gene_sets=hallmark_sets,
    permutations=1000,
)

results.top(10)
```

1. Genes ranked by your differential-expression statistic, most up-regulated
   first.

The output is a set of pathways with enrichment scores and adjusted p-values —
the coordinated signals your per-gene analysis stepped right over.

## The code

The full implementation, install instructions, and API reference:

[:material-github: GSEA Toolkit on GitHub](https://github.com/navinvent/gsea-toolkit){ .md-button .md-button--primary }
