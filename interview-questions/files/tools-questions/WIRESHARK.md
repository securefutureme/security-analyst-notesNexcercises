
- Masz plik PCAP i masz wykonać wstępną analizę ruchu. Co zrobisz, żeby:  
    a) znaleźć 3-way handshake TCP,  
    - szukamy flag SYN->SYN/ACK->FIN - w takiej sekwencji (możemy użyć filtra tcp.flag)  
    - Jeśli jest tylko SYN bez odpowiedzi albo retransmisje, to może wskazywać na problem sieciowy, filtrowanie lub skanowanie.  
      
    b) określić protokół warstwy aplikacyjnej,  
    - Najpierw otwieram pcap w Wireshark i używam Statistics ->Protocol Hierarchy.  
    - potem weryfikuję przez kolumnę Protocol - filtrowanie po ruchu np. http, dns, tls  
    - analizuję porty i zawartości pakietów (Follow TCP/UDP Stream) jeśli protokół nie został rozpoznany automatycznie  
      
    c) ustalić, czy w ruchu przesłano dane logowania  
    - możemy użyć “Follow TCP stream” na pierwszym pakiecie, żeby zobaczyć całą sesję i sprawdzić czy przypadkiem hasła nie zostały przesłany jawnym tekstem.  
      
    d) sprawdzić, czy da się odzyskać przesłany plik?
    

- najpierw sprawdzamy filtr tcp.dstport == 20  - protokół FTP na 20 jest od transferu danych. Szukamy pakietów które mogą wskazywać o transferze plików (wielkość pakietów ma znaczenie)
    
- jeżeli w pakiecie znajdziemy coś świadczącego o rozszerzeniu pliku .txt .pdf itd. wycinamy dane i zapisujemy do pliki (oczywiście jak nie jest zaszyfrowany).
    
- alternatywnie File - > Export Objects 