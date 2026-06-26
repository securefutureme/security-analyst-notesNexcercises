## Analiza accesslog

1. **Jak duży jest plik logów?** 

Sprawdzamy to standardową komendą ls -lrth.

![alt](courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/14-image.png)

Odp. 12 Kb

2. Jaki zakres czasu jest zawarty w logach?

Łączymy dwie komendy, tail i head by sprawdzić pierwszy i ostatni zapis w logu.

![alt](courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/15-image.png)

**Odp. 24/May/2022:09:42:42 +0200 UTC do 24/May/2022:09:52:03 +0200 UTC**

3. **W jakim formacie jest plik logów oraz, którego pliku jest kopią?** 

Odp. Tak jak w screenshootach powyżej, można zaobserwować, że są to logi w formacie **combined log format**. Jest kopią **other_vhost_access.log** - bo widać hosta wirtualnego na początku logów. 

(**"%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"".**)

4. Ułożenie timeline ataku z datami i godzinami z pliku accesslog.zip

  a)  **pierwszy kontakt z serwerem atakującego**

Użyjmy najpierw **cat access.log | cut -d" " -f2 | sort | uniq -c** do przefiltrowania sobie wszystkich adresów IP z access.log.

![alt](courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/16-image.png)

Odp. 24/May/2022:09:42:42 +0200 UTC

  b) **wejście atakującego na serwer**
  
Jako że to jest bardzo okrojony log, prawdopodobnie wycinek. Można odpowiedzieć - jak wyżej. 

  c) **IP atakującego**

**Odp. 30.13.3.7**


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


  
