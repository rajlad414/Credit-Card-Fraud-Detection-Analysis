## Fraud Detection Analysis

This project analyzes a dataset of Amazon transactions to identify fraudulent activity. The analysis focuses on exploring the data, identifying patterns, and building models to classify transactions as fraudulent or legitimate.

### Data Description

The [dataset](https://drive.google.com/drive/folders/1z-hBt1dBEpwbCw2vHecr3Wi14UN5oEHP?usp=sharing) consists of 31 features (V1 to V28, Time, Amount, Class) for both training (227845 rows) and testing (56962 rows) datasets. The "Class" feature indicates whether a transaction is fraudulent (1) or legitimate (0).

* **Preprocessing:**
    * No missing values were found.
    * The "brand" column was dropped as all transactions were from Amazon.
    * Feature correlation analysis revealed weak negative correlations between "Class" and V12, V14, V17, and a weak positive correlation between "Time" and V3.
    * Analysis of transaction time identified peak fraudulent activity between 11th-12th hour on day 1 and 2nd-3rd hour on day 2.
    * Analysis of transaction amounts showed the highest fraud occurrences for amounts between 1 euro and 500 euros, with peak fraud occurring during peak hours and lower fraud at night for transactions exceeding 2500 euros.
    * Based on boxplots, outliers exceeding 1.5 times the interquartile range (0.47) were removed.
    * The "Time" column was dropped after converting time into 48-hour intervals.
    * The final training dataset has 211504 rows and 31 features, while the testing dataset has 52877 rows and 30 features.
    * The dataset is highly imbalanced, with approximately 2.1 lakhs legitimate transactions and only 337 fraudulent transactions.

### Model Performance

Several machine learning models were trained and evaluated on the preprocessed data. The following table summarizes the performance metrics (accuracy, precision, F1-score, recall) for each model:

| Model        | Accuracy | Precision | F1-Score | Recall |
|--------------|-----------|------------|----------|--------|
| GaussianNB   | 0.93      | 0.970       | 0.92      | 0.88    |
| LogisticRegression | 0.95      | 0.980       | 0.95      | 0.93    |
| SVC          | 1.00      | 0.870       | 0.86      | 0.86    |
| RandomForestClassifier | 1.00      | 0.950       | 0.88      | 0.82    |
| XGBClassifier | 1.00      | 0.970       | 0.90      | 0.85    |
| ANN          | 1.00      | 0.999       | 0.58      | 0.55    |

**Note:** Although ANN achieved the highest accuracy, its low recall indicates a high number of false negatives (failing to identify fraudulent transactions).

### Anomaly Detection

Anomaly detection was explored to identify transactions deviating from the expected behavior of legitimate transactions. While non-fraudulent transactions tend to have higher anomaly scores, some fraudulent transactions can have scores that overlap with legitimate ones, making them more challenging to detect solely based on anomaly scores.

### Conclusion

This analysis identified patterns in fraudulent transactions within the Amazon transaction dataset. We built and evaluated various machine learning models for fraud classification, with Logistic Regression and XGBoost performing well despite the imbalanced dataset. While achieving high accuracy, some models struggled with identifying fraudulent transactions (low recall). Further exploration of techniques to handle imbalanced data and improve recall is recommended. Additionally, anomaly detection offers a complementary approach to fraud identification.
