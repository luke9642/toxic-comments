# Toxic comments classification

## Opis
Dane są wzięte z platformy __kaggle__.
Wykorzystałem bibliotekę tensorflow 2.x z keras'em przy użyciu hardware'u TPU z Google Colab do uczenia modelu.
Użyłem Grid Search'a z biblioteki sklearn do wyboru najlepszego modelu i parametrów.
Do preprocessingu użyłem biblioteki pandas jako podstawa do przetwarzania danych wejściowych oraz gensim do NLP.
Do reprezentacji słów użyłem pretrenowanych wag __GloVe__. Dane ściągam za pomocą pakietu spacy.

## Metody preprocessingu danych:
-   usunięcie znaków, które nie są literami
-   przerobienie tekstu na małe litery
-   usunięcie cyfr
-   usunięcie powtarzających się odstępów
-   dodanie paddingu
-   dodanie indeksu dla słów, których brakuje w GloVe
-   tokenizacja

## Hiperparametry:
-   optimizer Adam
-   metryki accuracy i roc auc
-   validation split 25%
-   300 feature'ów

### Najlepsze parametry (Grid Search):
-   batch_size = 32
-   learning_rate = 0.001

## Model:
-   Embedding layer z pretrenowanymi wagami z GloVe
-   dropout
-   Bidirectional LSTM
-   warstwa konwolucyjna
-   konkatenacja average pooling'u z max pooling'iem
-   warstwa fully connected z funkcją aktywacji sigmoid


Używam metryki  **ROC AUC**, która wydaje się lepiej określać poziom nauczonego modelu, dla tego dataset'u. Zdecydowana większość danych z dataset'u nie jest skategoryzowana jako "toxic comment" więc jeśli model zwracałby same zera podczas predykcji to jego accuracy byłoby nadal dość wysokie.

