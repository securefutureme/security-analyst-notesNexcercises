
## 1access.log

1. Jak duży jest plik logów? 

2. Jaki zakres czasu jest zawarty w logach? 

3. W jakim forcie jest plik logów oraz, którego pliku jest kopią? 

4. Ile i jakie adresy IP wysyłały żądania do aplikacji webowej w analizowanym zakresie czasu? 

5. Jakie zasoby URI były najczęściej odwiedzane w analizowanym zakresie czasu? (podaj ilość wysłanych top5 żądań) 

6. Przeanalizuj zalogowane parametry useragent. Zidentyfikuj użyte przez atakującego narzędzia. 

7. Jaką technikę ataku na aplikację webową wykorzystano? 

8. Przeanalizuj ruch manualny do aplikacji webowej. Zidentyfikuj kroki atakującego. Ilokrotnie i kiedy nastąpiło zalogowanie się do aplikacji?



2access.log

1. Jak duży jest plik logów? 

Używamy popularnych komend do sprawdzania wielkości plików/folderów: **du i ls**

![alt](/courses/szkola-security/siem/analiza-logow-cli-zadania-szkola/Attachments/1-image.png)

**Odp. 2840b (2.8Mb)**

2. Jaki zakres czasu jest zawarty w logach? 

Używamy dwóch komend - head i tail do sprawdzenia początku i końca logów.

![alt|697](/courses/szkola-security/siem/analiza-logow-cli-zadania-szkola/Attachments/2-image.png)

**Odp. 24/May/2022:04:13:49 +0200 UTC - 24/May/2022:05:27:40 +0200 UTC****

3. W jakim for(ma)cie jest plik logów oraz, którego pliku jest kopią? 

![alt](/courses/szkola-security/siem/analiza-logow-cli-zadania-szkola/Attachments/3-image.png)

**Format: *apache combined* - na końcu ma Referrer i User-Agent w cudzysłowaćh**
https://httpd.apache.org/docs/2.4/logs.html

![alt](/courses/szkola-security/siem/analiza-logow-cli-zadania-szkola/Attachments/4-image.png)

**Plik jest kopią: *other_vhost_access.log* - zwykle ten plik zaczyna się od nazwy hosta (wirtualnego) - dopeiero potem IP.**

3. Ile i jakie adresy IP wysyłały żądania do aplikacji webowej w analizowanym zakresie czasu? 

4. Przeanalizuj zalogowane parametry useragent. Zidentyfikuj użyte przez atakującego narzędzia. 

5. Przeanalizuj ruch do różnych uri oraz odstęp czasu pomiędzy wysyłanymi żądaniami. Czy atakujący wykonywał atak manualnie? 

6. Jaką technikę ataku na aplikację webową wykorzystano? 

7. Kiedy atakujący wykonał atak? 

8. Jakie informacje uzyskałby atakujący w przypadku powodzenia ataku?

3access.log

1. Jak duży jest plik logów? 2. Jaki zakres czasu jest zawarty w logach? 3. W jakim forcie jest plik logów oraz, którego pliku jest kopią? 4. Ile i jakie adresy IP wysyłały żądania do aplikacji webowej w analizowanym zakresie czasu? 5. Przeanalizuj zalogowane parametry useragent. Zidentyfikuj użyte przez atakującego narzędzia. 6. Z jakiego kraju najprawdopodobniej pochodzi atakujący? (albo chce, żebyśmy tak myśleli) 7. Przeanalizuj ruch dotyczący niecodziennego parametru useragent? Czy widzisz w nim coś niepokojącego? 8. Jakie 3 techniki ataku potrafisz zidentyfikować na podstawie ruchu z poprzedniego zadania? 9. Jakie komendy zostały wykonane przez atakującego na serwerze? 10. Opisz słownie kroki atakującego na podstawie wykonanych komend.