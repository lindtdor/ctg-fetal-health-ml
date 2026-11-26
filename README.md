# CTG fetal health classification

ML project - ESILV A4 MedTech & Santé
Linda ING, Lutèce HECKEL, Laureline JOUSSET

## Project
We want to predict the fetal state (normal, suspect or pathological) from cardiotocography (CTG) exams. It's a supervised classification problem with 3 classes.

## Dataset
Cardiotocography dataset from UCI (id 193): https://archive.ics.uci.edu/dataset/193/cardiotocography
2,126 exams, 21 features, no missing values. Target = NSP (1 normal, 2 suspect, 3 pathological).
We don't use the CLASS column because it gives the answer (leakage).

## Project structure

    ctg-fetal-health-ml/
    ├── README.md
    ├── requirements.txt
    ├── data/
    │   ├── README.md
    │   └── ctg_clean.csv
    ├── notebooks/
    │   └── CTG_week2_data_analysis_baseline.ipynb
    └── ai-governance/
        ├── PROMPT_LOG.md
        └── AI_AUDIT.md

To run: open the notebook in Colab and run all cells (packages in requirements.txt).

## Progress
- Week 1: topic and specification (done)
- Week 2: cleaning, data analysis, baseline (done)
- Week 3: other models, ensemble, one algorithm not seen in class (to do)
- Week 4: test set, report, oral (to do)

## Week 2
Cleaning: we removed CLASS and 13 duplicated rows, so we have 2,113 exams. Classes are imbalanced: 77.9% normal, 13.8% suspect, 8.3% pathological.

Data analysis: histograms, boxplots by class and correlation heatmap (see notebook). Mean, Mode and Median are very correlated (0.89 to 0.95).

Features: we keep 18 features. We removed Mean and Mode (same info as Median) and DS (non zero for only 7 exams). The clean data is in data/ctg_clean.csv.

Evaluation: stratified split 80/20 (the test set is not used yet) and 5-fold cross validation on the train set. Because of the imbalance we look at macro-F1 and recall of the pathological class, not only accuracy.

Baseline results (cross validation on the train set):

| Model | Accuracy | Macro-F1 | Balanced acc. | Recall pathological |
|---|---|---|---|---|
| Dummy (most frequent) | 0.779 | 0.292 | 0.333 | 0.000 |
| LogReg, 21 features | 0.888 | 0.779 | 0.769 | 0.714 |
| LogReg balanced, 21 features | 0.864 | 0.781 | 0.850 | 0.850 |
| LogReg, 18 features | 0.893 | 0.792 | 0.780 | 0.750 |
| LogReg balanced, 18 features | 0.860 | 0.776 | 0.846 | 0.843 |

The dummy model has 0.78 accuracy but finds 0 pathological cases, so accuracy alone is not enough. With class_weight="balanced" the logistic regression finds more pathological cases (recall 0.84 instead of 0.75).

## Next steps
Try kNN, SVM, random forest, an ensemble and one algorithm not seen in class.

## Team
Linda: notebook and GitHub. Lutèce and Laureline: review.
Our AI use is described in the ai-governance folder.

## References
- Campos, D. & Bernardes, J. (2000). Cardiotocography. UCI Machine Learning Repository. https://doi.org/10.24432/C51S4N
- Ayres-de Campos et al. (2000). SisPorto 2.0: a program for automated analysis of cardiotocograms. J Matern Fetal Med, 9(5), 311-318.
