# AI audit

Cases where the AI gave us something wrong, how we saw it and what we changed.

## 1. Order of the cleaning steps
- **What the AI did:** the first version of the code removed the duplicated rows before dropping the CLASS column. It found 11 duplicates.
- **How we saw it:** after dropping CLASS we checked again and there were still 2 duplicated rows. These rows had a different CLASS, so they were not seen as duplicates before.
- **What we changed:** we drop CLASS first, then remove duplicates. Now 13 rows are removed and we have 2,113 exams.

## 2. Comments that did not match the results
- **What the AI did:** some text cells said that Mean, Mode and Median are strongly correlated with LB, and that DP is mostly non zero.
- **How we saw it:** we compared with the outputs. The strong correlations (above 0.8) are between Mean, Mode and Median (0.89 to 0.95), LB is not in this list. And most exams have DP = 0.
- **What we changed:** we rewrote the comments from what the plots and tables really show.

## 3. Code that crashed
- **What the AI did:** the boxplots used ax.boxplot(..., labels=...).
- **How we saw it:** the cell gave a TypeError with the matplotlib version in Colab.
- **What we changed:** we used seaborn boxplots (sns.boxplot) instead.

## Things we checked and that were correct
- CLASS is removed: it contains patterns like FS and SUSP that directly give the NSP class, so keeping it would be leakage.
- The StandardScaler is inside the Pipeline, so it is fitted only on the training folds during cross-validation.
- The train/test split is stratified, so the 3 classes keep the same proportions.
- The test set is not used yet. All baseline results come from 5-fold cross-validation on the train set.
- We do not use accuracy alone because the classes are imbalanced.
