# Aromatase Bioactivity Analysis

## Objective
Explore chEMBL bioactivity data for human aromatase, filter to IC50 measurements, and classsify compounds as Active/Intermediate/inactive based on potency threshold.

## Data Source
chEMBL database, target: Aromatase(Homo sapiens)
Downloaded: 24th July 2026

## Bioactivity classification
- Active: IC50 < 100 nM
- Intermediate: 100 nM <= IC50 <= 1000 nM
- Inactive: IC50 > 1000 nM

## Key cleaning steps
1. Filtered to Standard Type == IC50 only (excluded Ki, Ratio, etc)
2. Selected relevant columns (Smiles, Molecular weight, R05 violations, standard value)
3. Dropped rows with missing standard value
4. Removed rows flagged by chEMBL's Data Validity comment("Outside typical range") -this fixed severely skewed summary statistics.

## Results
Of 4,215 IC50-labeled aromatase compounds (after removing ChEMBL-flagged invalid entries):
- Inactive: 1,958 compounds (mean IC50 ≈ 14,040 nM)
- Intermediate: 1,127 compounds (mean IC50 ≈ 437 nM)
- Active: 1,030 compounds (mean IC50 ≈ 30 nM)

## Data quality note
Initial summary statistics were heavily distorted by a small number of ChEMBL entries flagged "Outside typical range" — one row had a reported IC50 of ~3.4 × 10^13 nM. Removing validity-flagged rows corrected the Inactive class mean from 2.9 × 10^10 nM to a biologically plausible 14,040 nM, while the median barely shifted - a useful reminder to check meaan vs median divergence before trusting summary statistics.
