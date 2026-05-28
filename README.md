# Detekcja Oszustw Kardowych (Credit Card Fraud Detection)

Projekt realizuje proces klasyfikacji transakcji oszukańczych na silnie niezbalansowanym zbiorze danych (0.17% transakcji to fraudy), wykorzystując redukcję wymiarowości (PCA) oraz techniki resamplingu.

## Wyniki i Porównanie Modeli
Głównym wyzwaniem projektu było zbalansowanie precyzji z czułością.

* **Model 1: Regresja Logistyczna (Cost-Sensitive)**
    * Recall: `0.89` | Precision: `0.06` | F1-Score: `0.12`
    * *Werdykt:* Nieużyteczny biznesowo – generuje aż 1982 fałszywe alarmy.
* **Model 2: Las Losowy (SMOTE + RUS)**
    * Recall: `0.80` | Precision: `0.64` | F1-Score: `0.71`
    * *Werdykt:* Najlepsza czułość (omija tylko 29 oszustw), kosztem 67 fałszywych alarmów.
* **Model 3: Strojony Las Losowy (RandomizedSearchCV)**
    * Recall: `0.73` | Precision: `0.96` | F1-Score: `0.83`
    * *Werdykt:* Najbardziej zrównoważony i bezpieczny model operacyjny (tylko 5 fałszywych alarmów).

---

## Metodologia i Stack 

1.  **Preprocessing & Redukcja Wymiarowości:** Standaryzacja (`StandardScaler`) oraz Analiza Komponentów Głównych (`PCA`). Wybór 26 komponentów pozwolił na wyjaśnienie 90% wariancji danych.
2.  **Balansowanie Klas:** Zastosowanie pipline składającego się z oversamplingu `SMOTE` (do poziomu 10%) oraz undersamplingu `RandomUnderSampler` (do poziomu 50%).
3.  **Optymalizacja:** Przeszukiwanie siatki hiperparametrów metodą `RandomizedSearchCV` z walidacją krzyżową `StratifiedKFold` nakierowaną na metrykę `average_precision`.

**Stack:** Python, Scikit-Learn, Imbalanced-Learn, Pandas, NumPy.

---

## Szybki start

```bash
git clone [https://github.com/TWÓJ_NICK/NAZWA_REPOZYTORIUM.git](https://github.com/TWÓJ_NICK/NAZWA_REPOZYTORIUM.git)
pip install scikit-learn imbalanced-learn pandas numpy
