
**Przydatne komendy:**

**ls** – pokazuje listę plików w katalogu (sprawdzasz czy jest np. access.log).

**pwd** – pokazuje, w jakim katalogu aktualnie jesteś (żeby wiedzieć, skąd czytasz logi).

**file access.log** – sprawdza, jakiego typu jest plik (tekstowy log, nie np. binarka).

**wc -l access.log** – liczy linie w logu, czyli ile masz wpisów/żądań.

**cp access.log copyofaccess.log** – robi kopię logu do pracy, żeby nie tykać oryginału.

**head -n5 copyofaccess.log** – pokazuje pierwsze 5 linii logu (podgląd formatu).

**tail -n5 copyofaccess.log** – pokazuje ostatnie 5 linii (co działo się na końcu).

**cat copyofaccess.log | grep "Majkrosoft Edze"** – wyszukuje w logu wszystkie żądania z tym konkretnym User-Agentem (podejrzany „browser”).

**cat copyofaccess.log | grep php** – wyszukuje wpisy, w których atakował ktoś pliki .php (np. podatne skrypty).

**cat copyofaccess.log | grep "24/May/2022:09:42:42 +0200"** – szuka wszystkich żądań dokładnie z tego momentu czasu.

**cat copyofaccess.log | grep "24/May/2022:09:42:42 +0200" -A3 -B4** – to samo, ale pokazuje 4 linie przed i 3 po (kontekst zdarzenia).

**whatis cut** – krótki opis, do czego służy komenda cut (wycinanie kolumn z tekstu).

**head -1 copyofaccess.log | cut -d" " -f5** – bierze pierwszą linię i wycina 5. „kolumnę” rozdzielaną spacją (np. konkretny fragment wpisu, test jak wygląda podział).

**head -1 copyofaccess.log | cut -d"[" -f2 | cut -d"]" -f1** – z pierwszej linii wycina zawartość pomiędzy [ i ], czyli sam znacznik czasu z logu.

**head -1 copyofaccess.log | cut -d'"' -f4** – z pierwszej linii wyciąga 4. fragment rozdzielany cudzysłowami, czyli zwykle nagłówek Referer.

**head -n1 copyofaccess.log | cut -d' ' -f13**- – z pierwszej linii wycina pola od 13. do końca, czyli zwykle pełnego User-Agenta.

**cat copyofaccess.log | cut -d'"' -f6 | sort | uniq** – wyciąga wszystkie User-Agenty z logu, sortuje i pokazuje unikalne (lista różnych „przeglądarek”/narzędzi).

**cat copyofaccess.log | cut -d'"' -f6 | sort | uniq -c** – to samo, ale z liczbą wystąpień każdego User-Agenta (które narzędzie/UA pojawia się najczęściej)
  
**cat copyofaccess.log | cut -d'"' -f6 | sort -u** – skrótowo: wyciąga User-Agenty i od razu zwraca posortowaną listę unikalnych.  

## Analiza accesslog

1. **Jak duży jest plik logów?** 
2. Jaki zakres czasu jest zawarty w logach?** 
3. **W jakim forcie jest plik logów oraz, którego pliku jest kopią?** 

4. Ułożenie timeline ataku z datami i godzinami z pliku accesslog2.zip
  a)  **pierwszy kontakt z serwerem atakującego**
  b) **wejście atakującego na serwer**
  c) **IP atakującego**

  