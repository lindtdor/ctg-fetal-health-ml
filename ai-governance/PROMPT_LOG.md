# Prompt log

We used an AI assistant (Claude) during the project. Below are the main prompts (translated from French) and what we did with the answers.

## 1. Choice of the dataset (week 1)
- **Prompt:** "We need a supervised ML project linked to MedTech & Health. The data must be labelled with no missing values. Can you propose some datasets?"
- **What the AI suggested:** a few datasets, including Parkinson voice data and Cardiotocography (CTG).
- **What we checked:** we chose CTG and loaded it ourselves from UCI. In the notebook we checked the labels (NSP, 3 classes) and that there are 0 missing values.

## 2. Problem and metric
- **Prompt:** "How do we know if the baby is fine with the CTG data? Is it a classification problem? Which metric should we use?"
- **What the AI suggested:** a 3-class classification on NSP, and not only accuracy because the classes are imbalanced.
- **What we checked:** 78% of the exams are normal. The dummy model gets 0.78 accuracy but finds 0 pathological cases, so we also use macro-F1, balanced accuracy and the recall of the pathological class.

## 3. Notebook code (week 2)
- **Prompt:** "Help us write the code for the data analysis and the baseline, step by step, in a simple way."
- **What the AI suggested:** code for the notebook cells (loading, cleaning, plots, split, baseline models).
- **What we did:** we ran each cell in Colab, checked the outputs, asked questions when something was not clear and fixed the mistakes we found (see AI_AUDIT.md).

## 4. Features we keep
- **Prompt:** "Why only 18 features? Do we need all 21?"
- **What the AI suggested:** remove Mean and Mode (very correlated with Median) and DS (almost always 0).
- **What we checked:** correlations of 0.89 to 0.95 on the heatmap, DS is non-zero for only 7 exams, and the logistic regression gives almost the same results with 18 and 21 features (macro-F1 0.792 vs 0.779).
