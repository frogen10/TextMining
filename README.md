# Analiza tekstu – opis kroków i uzasadnienie

---

## 1. Import bibliotek

Importujemy niezbędne biblioteki do przetwarzania tekstu, analizy danych, wizualizacji oraz uczenia maszynowego.  
**Dlaczego?**  
Każda z nich odpowiada za inny etap pipeline'u:  
- `nltk`, `morfeusz2` – przetwarzanie języka naturalnego (tokenizacja, lematyzacja)
- `sklearn` – wektoryzacja, modelowanie tematów, klasteryzacja
- `matplotlib`, `wordcloud` – wizualizacja wyników
- `pandas`, `numpy` – operacje na danych

---

## 2. Utworzenie korpusu dokumentów

```python
corpus_dir="./literatura"
corpus = PlaintextCorpusReader(corpus_dir, ".*\.txt")
files = corpus.fileids()
```
---

## 3. Wstępne przygotowanie dokumentów

- Wczytanie tekstów do słownika
- Usunięcie interpunkcji
- Zamiana na małe litery
- Lematizacja (morfeusz2)
- Usunięcie stopwords

**Dlaczego taka kolejność?**  
- Najpierw czyszczenie i normalizacja tekstu (małe litery, interpunkcja), by uniknąć rozdzielania tych samych słów na różne formy.
- Lematizacja pozwala sprowadzić słowa do podstawowej formy, co poprawia jakość analizy tematycznej i n-gramów.
- Usunięcie stopwords redukuje szum i skupia analizę na słowach niosących znaczenie.

---

## 4. Utworzenie macierzy cech

- `CountVectorizer` – macierz częstości słów
- `TfidfVectorizer` – macierz tf-idf

**Dlaczego oba?**  
- CountVectorizer pokazuje surową częstość słów.
- TfidfVectorizer uwzględnia unikalność słów w dokumentach, co jest lepsze do modelowania tematów i klasteryzacji.

---

## 5. Wizualizacja chmur słów

Tworzymy chmurę słów dla każdego dokumentu.

**Dlaczego?**  
Chmura słów pozwala szybko zobaczyć, które słowa dominują w danym tekście.

---

## 6. Modelowanie tematów (Topic Modeling)

- LDA (Latent Dirichlet Allocation)
- NMF (Non-negative Matrix Factorization)

**Dlaczego te modele?**  
Oba są popularne do ekstrakcji tematów z tekstu. LDA lepiej radzi sobie z dużymi zbiorami, NMF jest prostszy i często daje bardziej interpretowalne wyniki.

---

## 7. Wizualizacja tematów i udziału tematów w dokumentach

Tworzymy wykresy słów kluczowych dla tematów oraz udziału tematów w dokumentach.

**Dlaczego?**  
Pozwala to zrozumieć, jakie tematy zostały wykryte i jak rozkładają się w zbiorze dokumentów.

---

## 8. Analiza skupień (klasteryzacja)

- AgglomerativeClustering na macierzy tf-idf (Ward) i na macierzy odległości euklidesowej (Complete linkage)
- Wizualizacja dendrogramów

**Dlaczego?**  
Klasteryzacja pozwala zobaczyć, które dokumenty są do siebie najbardziej podobne. Dwa podejścia (Ward i Complete linkage) pokazują różne perspektywy podobieństwa.

---

## 9. Analiza n-gramów

- Tworzenie n-gramów (np. trigramów) dla każdego dokumentu i całego korpusu
- Wizualizacja najczęstszych n-gramów

**Dlaczego?**  
N-gramy pokazują najczęściej współwystępujące frazy, co pozwala lepiej zrozumieć charakterystyczne zwroty i styl tekstów.

---

## Dlaczego NMF jest często lepszy od LDA?

NMF (Non-negative Matrix Factorization) jest często preferowany w analizie tematów tekstowych, szczególnie w języku polskim i przy krótkich dokumentach, z kilku powodów:

- **Lepsza interpretowalność** – NMF wymusza nieujemność wag, dzięki czemu tematy są bardziej jednoznaczne, a słowa przypisane do tematów są łatwiejsze do interpretacji.
- **Praca na macierzy tf-idf** – NMF bardzo dobrze współpracuje z macierzą tf-idf, co pozwala lepiej wyłuskać unikalne słowa dla tematów. LDA najlepiej działa na surowych licznościach słów.
- **Stabilność dla krótkich tekstów** – NMF lepiej radzi sobie z krótkimi dokumentami, gdzie LDA może mieć problem z rozkładem tematów.
- **Szybkość i prostota** – NMF jest często szybszy i prostszy w implementacji oraz strojenia parametrów.

## Podsumowanie

Każdy etap pipeline'u został dobrany tak, by:
- Zminimalizować szum i błędy językowe (czyszczenie, lematyzacja, stopwords)
- Wydobyć jak najwięcej informacji z tekstu (wektoryzacja, modelowanie tematów, n-gramy)
- Ułatwić interpretację wyników (wizualizacje, dendrogramy, chmury słów)

Dzięki temu analiza jest kompletna, powtarzalna i łatwa do rozbudowy o kolejne funkcje.
NMF daje bardziej jednoznaczne, łatwiejsze do interpretacji tematy i lepiej sprawdza się w praktycznych zastosowaniach, zwłaszcza przy analizie polskich tekstów i krótkich dokumentów.