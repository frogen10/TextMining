# Text Mining Project

## Opis projektu

Ten projekt służy do analizy tekstów literackich w języku polskim. Wykorzystuje bibliotekę `nltk` do przetwarzania tekstu oraz bibliotekę `morfeusz2` do lematyzacji. Projekt zawiera korpus dokumentów literackich oraz listę polskich stop-słów, które są wykorzystywane do wstępnego przetwarzania tekstu.

## Struktura projektu

- **literatura/**: Folder zawierający pliki tekstowe z literaturą.
- **stopwords_pl.txt**: Lista polskich stop-słów używana do filtrowania nieistotnych słów.
- **text_mining.ipynb**: Główny notebook zawierający kod do analizy tekstu.
- **requirements.txt**: Lista zależności wymaganych do uruchomienia projektu.

## Wymagania

Aby uruchomić projekt, należy zainstalować wymagane biblioteki. Można to zrobić za pomocą polecenia:

```bash
pip install -r [requirements.txt](http://_vscodecontentref_/3)

pip freeze > requirements.txt