# Multi-omics patient stratification and biomarker discovery in CLL

A reproducible multi-omics integration pipeline that recovers disease subtypes, nominates biomarkers, and
links molecular state to drug response, demonstrated on a chronic lymphocytic leukemia (CLL) cohort.

The workflow mirrors core translational-bioinformatics tasks: integrate heterogeneous omics layers, find
patient subgroups, discover biomarkers, and connect molecular axes to drug sensitivity and clinical class.

## What it does

- Integrates four layers (gene expression, DNA methylation, mutations/CNVs, ex-vivo drug response) over
  200 patients into shared latent factors with **MOFA** (Multi-Omics Factor Analysis), handling missing
  data natively.
- **Validates** the unsupervised factors against known CLL biology.
- **Stratifies** patients into molecular subgroups.
- **Discovers biomarkers** from factor loadings (genes, drugs).
- Identifies a **drug-response biomarker** by correlating ex-vivo response with the disease axis.
- Trains a cross-validated **expression-signature classifier** for prognostic class.

## Key results

| Result | Value |
| --- | --- |
| Factor 1 vs IGHV status (Pearson r) | -0.86 |
| Another factor vs trisomy 12 (Pearson r) | +0.75 |
| Molecular subgroups (k-means on factors) | clean IGHV separation (0.94 / 0.67 / 0.02 mutated) |
| Predict IGHV from gene expression (5-fold CV ROC-AUC) | 0.90 |

The unsupervised integration rediscovers the two dominant molecular axes of CLL with no labels, and the
factor loadings and drug correlations make those axes interpretable and actionable.

## Data

CLL multi-omics cohort of Dietrich et al. (J. Clin. Invest. 2018), distributed by the MOFA project. The
notebook downloads it automatically on first run.

## Run it

```bash
pip install -r requirements.txt
jupyter notebook multiomics_cll_stratification.ipynb
```

## Adapt to your own cohort

The final notebook section shows how to swap in a TCGA or cBioPortal cohort (expression, methylation,
mutation, copy number) and re-run the same integration, stratification, and prediction steps.

## Stack

MOFA (mofapy2), rdata, scikit-learn, pandas, scipy, matplotlib.
