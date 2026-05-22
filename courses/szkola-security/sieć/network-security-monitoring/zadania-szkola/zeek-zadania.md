
1. **Za pomocą narzędzia Zeek wypakuj z pliku logi w formacie TSV.** 

Wpisujemy komendę **zeek -r (nazwapliku)**. Mozemy potem to przenieść do osobnego folderu "tsv" dla porządku - "mv *.log tsv"

![alt](courses/szkola-security/sieć/network-security-monitoring/zadania-szkola/Attachments/1-image.png)
![alt](courses/szkola-security/sieć/network-security-monitoring/zadania-szkola/Attachments/2-image.png)

2. Jaki UID posiada log w pliku werid.log i czego dotyczy oraz kiedy dokładnie zdarzenie to miało miejsce? 

**a) UID - CMXWyy31OHwyQKUnNk
b) HTTP_version_mismatch   - klient i serwer mają mismatch w wersji HTTP
c) GMT: Sunday, January 16, 2022 9:10:01.279 AM**

![[courses/szkola-security/sieć/network-security-monitoring/zadania-szkola/Attachments/6-image.png]]
![[courses/szkola-security/sieć/network-security-monitoring/zadania-szkola/Attachments/4-image.png]]
![alt](courses/szkola-security/sieć/network-security-monitoring/zadania-szkola/Attachments/5-image.png)

3. Sformatuj komendę, która z pliku conn.log pozwoli na wyświetlanie danych 5-tuple. 
[https://jumpcloud.com/it-index/understanding-the-5-tuple-in-network-communication](https://jumpcloud.com/it-index/understanding-the-5-tuple-in-network-communication) 

**cat conn.log | zeek-cut id.orig_h id.orig_p id.resp_h id.resp_p proto | head**

**id.orig_h (addr)**  - Adres IP inicjującego połączenie (originator/source) - Source IP Address

**id.orig_p (port)**  - Port źródłowy (na hoście inicjującym). - Source Port number

**id.resp_h (addr)**  - Adres IP odpowiadającego endpointu (responder/destination). - Destination IP Address

**id.resp_p (port)**  - Port docelowy (na hoście odpowiadającym). - Destination Port Number

**proto (enum**)  - Protokół transportowy: tcp, udp, icmp itd. - Protocol

![[courses/szkola-security/sieć/network-security-monitoring/zadania-szkola/Attachments/7-image.png]]

4. **Na podstawie wyniku zadania 3. Jaki procent komunikacji to pakiety TCP?** 

**cat conn.log | zeek-cut id.orig_h id.orig_p id.resp_h id.resp_p proto | grep "tcp" | wc -l**

Odp. 2315

![[courses/szkola-security/sieć/network-security-monitoring/zadania-szkola/Attachments/8-image.png]]

5. **Do komendy z zadania 3 dodaj pole service. Przeanalizuj zidentyfikowane przez Zeeka usługi. Czy narzędzie zidentyfikowało usługi wszystkich przesyłanych pakietów?** 

Musimy przefiltrować wszystkie "puste" pola z kolumny service. cat conn.log | zeek-cut id.orig_h id.orig_p id.resp_h id.resp_p proto service | grep "-"

![[courses/szkola-security/sieć/network-security-monitoring/zadania-szkola/Attachments/10-image.png]]

Albo odejmując separatorem verbose te, gdzie nie ma wyrażenia "http".** cat conn.log | zeek-cut id.orig_h id.orig_p id.resp_h id.resp_p proto service | grep "-"

![[courses/szkola-security/sieć/network-security-monitoring/zadania-szkola/Attachments/9-image.png]]

Odpowiedź: narzędzie nie zidentyfikowało usług wszystkich przesyłanych pakietów.

5. Jakie źródłowe adresy IP biorą udział w komunikacji i jaka jest ilość ruchu powiązana z tymi adresami IP? 

6. Na podstawie pliku http.log z identyfikuj wszystkie podejrzane parametry user-agent oraz ilości ruchu z nimi powiązane. 

7. Przeanalizuj 7 pakietów powiązanych z podejrzanym ruchem jednego z user-agentów z zadania 7. Jakie złośliwe zachowanie możesz tu zidentyfikować?