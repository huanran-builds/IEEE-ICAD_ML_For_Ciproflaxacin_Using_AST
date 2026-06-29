# Ciprofloxacin Resistance Predictor (metadata-only)

Code for the IEEE ICAD 2026 paper "Machine Learning-based Prediction of
Ciprofloxacin Resistance in Escherichia coli Using Antimicrobial Susceptibility
Testing Metadata."

First author: Huanran Yu (Jordan High School). GitHub: huanran-builds

## What this does
Predicts ciprofloxacin resistance in E. coli from routinely collected
antimicrobial susceptibility testing (AST) metadata alone — no whole-genome
sequencing required. The goal is a resistance-prediction tool deployable in
clinical settings that have AST data but no sequencing capacity.

## Results (held-out test set)
Class-weighted random forest on 7,629 BV-BRC-derived isolates (25% resistant):
- Accuracy: ~90% (0.896)
- F1, resistant class: 0.748
- Precision, resistant class: 0.971
- ROC-AUC: 0.835

Benchmarked against majority-class and shallow decision-tree baselines, plus a
class-weighted logistic regression. Includes ablations quantifying the
contribution of MIC fields and laboratory metadata.

## Method
- Features: MIC measurements + lab descriptors (typing method, platform, vendor,
  testing standard), median imputation for numeric and one-hot for categorical.
- Models: class-weighted random forest (primary) and logistic regression.
- Evaluation: stratified 5-fold CV + 80/20 held-out split.

## Note
High metadata-only performance partly reflects laboratory and breakpoint
structure in AST data; the paper treats this model as a strong non-genomic
baseline, not a replacement for genomic methods. See the paper's discussion.
