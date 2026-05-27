# HER alloy catalysts dataset and GPR baseline data

This repository contains the tabular data associated with the manuscript:

**Curated dataset of multinary alloy HER catalysts for composition-only modelling with Magpie descriptors and GP baselines**  
Stéphane Gorsse, Tang Bijun, Yaoyao Tang, Ma Mingyu and Zheng Liu.  
Submitted to *Scientific Data*.

The dataset compiles literature-reported multinary alloy catalysts for the hydrogen evolution reaction (HER), with normalized compositions, harmonized catalyst descriptors, source-level electrochemical metadata, composition-derived Magpie descriptors and Gaussian-process-regression-based candidate acquisition outputs.

The purpose of this repository is to support reproducible reuse of the dataset described in the manuscript. It is not a repository of validated optimal catalysts. The model-guided candidates are intended as an experimental acquisition list for future standardized HER measurements.

## Repository structure

```text
data/
├── her_catalysts_dataset_v1.csv
├── her_source_metadata_v1.csv
├── her_ml_harmonized_v1.csv
└── her_candidate_acquisition_100_v1.csv
```

## Data files

### `data/her_catalysts_dataset_v1.csv`

Catalyst-level dataset containing **180 curated catalyst/performance records** after preprocessing and rare-element filtering.

Each row corresponds to one reported catalyst entry and includes:

- DOI-based source reference;
- normalized alloy formula;
- atomic-percent composition for the 18 retained elements: Ag, Al, Au, Co, Cr, Cu, Fe, Ir, Mg, Mn, Mo, Ni, Pd, Pt, Rh, Ru, W and Zn;
- harmonized catalyst descriptors, including form, dimension, phase, pH and synthesis method where available;
- HER target values: onset potential and Tafel slope;
- the 16 selected Magpie descriptors used for the composition-based GPR baseline.

This is the primary catalyst-level dataset for composition-based statistical analysis and baseline machine learning.

### `data/her_source_metadata_v1.csv`

Source-level electrochemical metadata table containing **61 unique source DOIs**.

This file documents the experimental reporting context associated with the HER values in the catalyst-level dataset. It includes:

- onset-potential definition metadata;
- electrolyte identity and concentration;
- temperature when reported;
- reference electrode and potential scale information;
- RHE conversion status;
- iR-compensation information;
- Tafel extraction method and fitting-range information.

Values were recorded only when they could be directly recovered from the source article. Missing or non-recoverable information is encoded as `unknown` rather than inferred.

### `data/her_ml_harmonized_v1.csv`

Harmonized ML-ready table containing the same **180 catalyst entries** as the catalyst-level dataset, merged with machine-readable encodings of catalyst descriptors and source-level electrochemical metadata.

This file is intended for users who want to filter, stratify or model the catalyst data while accounting for study-level reporting context. It includes:

- DOI and formula;
- HER target values;
- elemental composition columns;
- selected Magpie descriptors;
- harmonized catalyst classes;
- pH and synthesis classes;
- phase flags;
- electrolyte-family flags;
- reference-electrode and RHE-conversion encodings;
- iR-compensation and Tafel-analysis classes;
- metadata-coverage indicators.

### `data/her_candidate_acquisition_100_v1.csv`

Model-guided acquisition list containing **100 proposed alloy compositions** for future standardized HER experiments.

These candidates were selected from a constrained virtual composition library using a composition-based Gaussian Process Regression model. The selection balances:

- predicted Tafel slope;
- GPR predictive uncertainty;
- chemical diversity;
- proximity to the training domain.

Each row includes:

- candidate rank;
- acquisition category;
- formula;
- number of elements;
- total platinum-group-metal content;
- predicted Tafel slope;
- predictive uncertainty;
- lower and upper confidence bounds;
- expected improvement;
- nearest-neighbour distance in Magpie descriptor space;
- domain-of-applicability label;
- nearest training analogue;
- elemental composition columns.

This file should be interpreted as a **model-guided experimental acquisition list**, not as a ranking of experimentally validated optimal catalysts.

## Relationship between files

The four files are intended to be used together but serve different purposes.

- `her_catalysts_dataset_v1.csv` provides the curated catalyst compositions, Magpie descriptors and HER targets.
- `her_source_metadata_v1.csv` preserves the source-level experimental context needed to interpret differences between studies.
- `her_ml_harmonized_v1.csv` merges catalyst-level entries with machine-readable metadata encodings for filtering, stratified analysis and modelling.
- `her_candidate_acquisition_100_v1.csv` provides a traceable list of model-guided compositions for future standardized experiments.

The common DOI field links catalyst records to source-level metadata.

## Intended use

This repository is intended for:

- reproducible benchmarking of composition-based regression models for HER alloy catalysts;
- uncertainty-aware Gaussian Process Regression baselines;
- analysis of domain-of-applicability in a small-data regime;
- filtering and stratification by electrochemical reporting context;
- prospective experimental planning and active-learning workflows.

## Limitations

The dataset is derived from heterogeneous literature sources. HER onset potential and Tafel slope values depend on experimental protocol, electrolyte, potential scale, iR correction, fitting range, morphology, phase constitution, support effects and catalyst preparation route.

Accordingly:

- model predictions should not be interpreted as point-accurate HER activity values;
- candidate compositions should not be treated as validated catalysts;
- the acquisition list should be experimentally tested under standardized conditions;
- metadata fields should be used to filter or stratify analyses whenever possible.

## Citation

If you use this dataset, please cite the associated *Scientific Data* article once available:

> Gorsse, S., Tang, B., Tang, Y., Ma, M. & Liu, Z. Curated dataset of multinary alloy HER catalysts for composition-only modelling with Magpie descriptors and GP baselines. *Scientific Data* (in revision).

A final DOI will be added after publication.

## Contact

For questions about the dataset, please contact the corresponding author listed in the associated manuscript.
