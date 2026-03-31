# CHH vs CDGP — Machine Learning Classifier

Code repository for the machine learning analyses in:

Oligogenic burden and machine learning refine early classification of delayed puberty
Maria-Christina Antoniou and Yassine Zouaghi et al. 2026

---

## Overview

This repository contains the analysis notebook used to classify patients with
congenital hypogonadotropic hypogonadism (CHH) from those with constitutional
delay of growth and puberty (CDGP) using clinical, biochemical, and genetic
features.

The approach uses an **Isolation Forest** (and Random Forest comparator) trained
on CHH cohort with internal cross-validation (100–1000 repeated random
70/30 splits). Five model variants are evaluated per feature set, varying
whether and how genetic information is incorporated (see notebook for details).

---

## Repository contents
```
├── genetic_score_IF_training_validation_NP_only.ipynb   # Main analysis notebook
├── OMIM_CHH_genes.xlsx                                  # Curated CHH gene list with inheritance modes
├── Data_for_Lausanne_30_06_2023_full.xlsx               # Clinical data
├── CHH_genes_valid.txt                                  # Gene symbols used for variant filtering
├── results/                                             # Output directory for model performance tables
└── figures/
    └── SHAP_contrib/                                    # SHAP feature importance plots
```

**Data not included** — variant files
(`known_genes_20230828_variants_V8_MT_hg38_*.xlsx`) contain patient-level
information and cannot be shared publicly. Researchers seeking access for
replication purposes may contact [Nelly.Pitteloud@chuv.ch].

---

## Notebook structure

| Section | Description |
|---------|-------------|
| Helper utilities | Metric computation, SHAP plotting |
| Genetic score computation | Inheritance-aware per-gene pathogenicity scoring (AR/AD/XL) |
| Preprocessing | Feature engineering, variant joining, label encoding |
| Model training | `split_and_train_if`, `split_and_train_rf`, `create_stat_df` |
| Main analysis | `run_conditions()` — five model variants × eight feature sets |
| Univariate baselines | Inhibin-B and cryptorchidism+TV as clinical comparators |
| Statistics | Wilcoxon rank-sum tests between model variants |
| SHAP analysis | Decision plots and per-subject force plots |
| Genetic score export | Variant-level annotation with burden-test gene ranks |

---

## Notes on data availability and reproducibility

- Results will vary slightly between runs due to random train/test splits.
  The 1000-repeat setting substantially reduces this variance.
- The Isolation Forest has no fixed random seed by design — this reflects the
  intended evaluation of average performance across many splits rather than a
  single deterministic result.
- If you wish to exactly reproduce a specific run, add `random_state=42` to
  the `train_test_split` and `IsolationForest` calls.

---

## License

Code is released under the MIT License. The gene lists (`OMIM_CHH_genes.xlsx`,
`CHH_genes_valid.txt`) are provided for research use

---

## Contact

Yassine Zouaghi - yzouaghi@stanford.edu
Stanford
