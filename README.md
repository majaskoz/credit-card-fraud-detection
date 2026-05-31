# Detekcja Oszustw Kardowych (Credit Card Fraud Detection)

Projekt realizuje proces klasyfikacji transakcji oszukańczych na silnie niezbalansowanym zbiorze danych (0.17% transakcji to fraudy), wykorzystując redukcję wymiarowości (PCA) oraz techniki resamplingu.

## Results and Model Comparison

The main challenge of the project was to balance precision and recall.

* **Model 1: Logistic Regression (Cost-Sensitive)**
  * Recall: `0.89` | Precision: `0.06` | F1-Score: `0.12`
  * *Verdict:* Commercially unviable – generates as many as 1982 false positives.
  
* **Model 2: Random Forest (SMOTE + RUS)**
  * Recall: `0.80` | Precision: `0.64` | F1-Score: `0.71`
  * *Verdict:* Best recall (misses only 29 frauds), at the cost of 67 false positives.
  
* **Model 3: Tuned Random Forest (RandomizedSearchCV)**
  * Recall: `0.73` | Precision: `0.96` | F1-Score: `0.83`
  * *Verdict:* The most balanced and secure operational model (only 5 false positives).

---

## Metodologia i Stack 

1.  **Preprocessing & Redukcja Wymiarowości:** Standaryzacja (`StandardScaler`) oraz Analiza Komponentów Głównych (`PCA`). Wybór 26 komponentów pozwolił na wyjaśnienie 90% wariancji danych.
2.  **Balansowanie Klas:** Zastosowanie pipline składającego się z oversamplingu `SMOTE` (do poziomu 10%) oraz undersamplingu `RandomUnderSampler` (do poziomu 50%).
3.  **Optymalizacja:** Przeszukiwanie siatki hiperparametrów metodą `RandomizedSearchCV` z walidacją krzyżową `StratifiedKFold` nakierowaną na metrykę `average_precision`.

**Stack:** Python, Scikit-Learn, Imbalanced-Learn, Pandas, NumPy.

---

## Szybki start

```bash
git clone [https://github.com/majaskoz/credit-card-fraud-detection.git](https://github.com/majaskoz/credit-card-fraud-detection.git)
pip install scikit-learn imbalanced-learn pandas numpy
