# Report / Podsumowanie projektu

## 1. Cel projektu

Celem projektu było przygotowanie modeli uczenia maszynowego do klasyfikacji ryzyka cukrzycy oraz przeprowadzenie analizy wyjaśnialności modeli z wykorzystaniem metod XAI.

Problem został sformułowany jako klasyfikacja binarna:
- `0` — brak cukrzycy,
- `1` — cukrzyca.

## 2. Zbiór danych

W projekcie wykorzystano zbiór Pima Indians Diabetes Dataset. Zbiór zawiera dane diagnostyczne pacjentek, takie jak poziom glukozy, BMI, ciśnienie krwi, poziom insuliny, wiek oraz liczba ciąż.

Zmienną docelową jest `Outcome`.

## 3. Preprocessing danych

W wybranych kolumnach medycznych wykryto wartości `0`, które są trudne do interpretacji medycznej i mogą oznaczać brak lub błędny pomiar. 

W głównym wariancie projektu usunięto obserwacje zawierające wartości `0` w tych kolumnach. Po oczyszczeniu danych liczba obserwacji zmniejszyła się z 768 do 392. Jest to ograniczenie projektu, ale pozwoliło pracować na bardziej spójnym zbiorze danych.

## 4. Modele

W projekcie wytrenowano i porównano trzy modele klasyfikacyjne:

- Logistic Regression,
- Random Forest,
- SVC.

Logistic Regression pełnił rolę modelu interpretowalnego z natury. Random Forest oraz SVC wykorzystano jako modele bardziej złożone i porównawcze.

## 5. Ocena modeli

Modele oceniono za pomocą metryk:

- accuracy,
- balanced accuracy,
- precision,
- recall,
- F1-score,
- ROC AUC.

Na pojedynczym podziale train/test najwyższą wartość accuracy osiągnął model SVC. Random Forest uzyskał najwyższy recall oraz F1-score dla klasy 1, co oznacza, że najlepiej wykrywał rzeczywiste przypadki cukrzycy. Logistic Regression osiągnął najwyższą wartość ROC AUC na pojedynczym podziale train/test.

Dodatkowo zastosowano walidację krzyżową Stratified K-Fold. Wyniki cross validation pokazały, że modele osiągały zbliżone wartości ROC AUC, a najwyższy średni wynik uzyskał Random Forest.

## 6. Wyjaśnialność modeli XAI

W części XAI zastosowano kilka metod wyjaśnialności:

- współczynniki Logistic Regression,
- Permutation Importance,
- SHAP summary plot,
- SHAP bar plot,
- SHAP waterfall plot,
- LIME,
- PDP / ICE,
- dodatkowo współczynniki i Permutation Importance dla SVC.

Dla Logistic Regression przeanalizowano współczynniki oraz Permutation Importance. Dla Random Forest wykonano szerszą analizę post-hoc, ponieważ jest to model złożony. Wykorzystano SHAP, LIME oraz PDP/ICE. Dla SVC wykonano dodatkową interpretację za pomocą współczynników modelu liniowego oraz Permutation Importance.

## 7. Najważniejsze wyniki XAI

Najważniejszą cechą w większości metod okazała się `Glucose`. Jej wysoka wartość zwiększała przewidywane prawdopodobieństwo klasy 1, czyli cukrzycy.

Istotne znaczenie miały również:

- `BMI`,
- `Age`,
- `DiabetesPedigreeFunction`,
- `Insulin`.

Wyniki różnych metod XAI były w dużej mierze spójne, ponieważ większość z nich wskazywała poziom glukozy jako kluczową cechę wpływającą na decyzje modeli.

## 8. Ograniczenia projektu

Projekt ma charakter edukacyjny i nie powinien być traktowany jako narzędzie diagnostyczne. Ważnym ograniczeniem jest zmniejszenie liczby obserwacji po usunięciu wierszy z wartościami `0`. Po oczyszczeniu danych zbiór zmniejszył się z 768 do 392 obserwacji.

Ponadto interpretacje XAI pokazują sposób działania modeli na konkretnym zbiorze danych i przy przyjętych decyzjach preprocessingowych. Nie są one równoznaczne z pełną interpretacją medyczną.

## 9. Wnioski końcowe

Projekt pokazał, że modele uczenia maszynowego mogą skutecznie klasyfikować ryzyko cukrzycy na podstawie prostych danych diagnostycznych. Najlepsze wyniki były zbliżone dla kilku modeli, jednak Random Forest okazał się szczególnie interesujący ze względu na wysoki recall oraz najlepszy średni ROC AUC w walidacji krzyżowej.

Analiza XAI pozwoliła sprawdzić, które cechy wpływały na predykcje modeli. Najważniejszą zmienną była `Glucose`, co jest zgodne z intuicją dotyczącą problemu cukrzycy. Dzięki metodom takim jak SHAP, LIME, Permutation Importance oraz PDP/ICE możliwe było zarówno globalne, jak i lokalne wyjaśnienie działania modeli.