# Data

Dataset: Cardiotocography, UCI Machine Learning Repository
https://archive.ics.uci.edu/dataset/193/cardiotocography (licence CC BY 4.0)

The notebook loads the raw data directly with the ucimlrepo package (id = 193).

ctg_clean.csv is our clean dataset: 2,113 exams, 18 features and the target NSP (1 = normal, 2 = suspect, 3 = pathological).
We removed the CLASS column (leakage), 13 duplicated rows, and the features Mean, Mode and DS (see the notebook).
