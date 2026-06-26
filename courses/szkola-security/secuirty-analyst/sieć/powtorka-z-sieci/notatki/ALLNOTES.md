# WSTĘP - SIEĆ / WIRESHARK

### TCP/IP vs OSI (Open System Interconnection model)

##### **W modelu OSI zapamiętaj:**  

**Polski: APSTSŁF** 

(Aplikacji (layer 7), Prezentacji, Sesji, Transportu, Sieci, Łącza dan., Fizyczna (layer 1)->)  

np. **Anka Patrzy że Staś To Szybko Ładnie Fotografuje**  
  
**Angielski: APSTNDP**

(Applicat., Present., Session, Transport, Network, Data Link, Physical) 

**Anka Patrzy że Staś Teraz Niesie Duży Plecak**  
  
**W Modelu TCP/IP zapamiętaj:**  

**Polski: ATSIDS** 

(Aplikacji, Transportu, Internetu, Dostępu do sieci)  

np. **Anka Trzepie Sidłem I Dociera Sankami**  
  
**Angielski: ATNNI** 

(Application, Transport, Network, Network Interface)  

np. **Anka Trzepie Nienagannie Niebieskie Irysy**

  
**TCP / UDP są w 4 warstwie (3 warstwa TCP) - transportowej**  

**IPv4 / IPv6 są w 3 warstwie (2 warstwa TCP)- sieciowej/internetowej**  

### **Warstwa 1 - Fizyczna (Dostępu Do Sieci)  

**Warstwa fizyczna** odpowiada za przesyłanie sygnałów w sieci. Jej zadaniem jest zamiana bitów informacji na sygnały, które mogą zostać przesłane przez dane medium transmisyjne, takie jak **kable, światłowody czy sieci bezprzewodowe**.

Aby przesłać dane przez nośnik, warstwa fizyczna wykorzystuje kilka podstawowych elementów:

- **medium transmisyjne** oraz odpowiednie **złącze**,
- sposób **reprezentacji bitów** w danym medium,
- metody **kodowania danych** i informacji sterujących,
- **układy nadawcze i odbiorcze** w urządzeniach sieciowych.

Po przejściu przez medium transmisyjne sygnały są **odczytywane i zamieniane z powrotem na bity**, a następnie przekazywane do **warstwy łącza danych** jako kompletna ramka.

https://kaser.zsl.gda.pl/PSK%202/6.%20Model%20OSI%20-%20warstwa%20fizyczna.pdf
  
### **Warstwa 2 - Łącza danych (Dostępu Do Sieci)**  

Głównym celem jest detekcja błędów, które się pojawiły w warstwie pierwszej oraz kontrola/ustalanie reguł przepływu danych przez warstwę fizyczną.” 
  
##### **MAC (Media Access Control):**

[https://pl.wikipedia.org/wiki/Adres_MAC](https://pl.wikipedia.org/wiki/Adres_MAC)
[https://bluecatnetworks.com/blog/mac-address-vs-ip-address-whats-the-difference/](https://bluecatnetworks.com/blog/mac-address-vs-ip-address-whats-the-difference/)
[https://whatismyipaddress.com/mac-address](https://whatismyipaddress.com/mac-address)”  
  
**Do zapamiętania:**  

- Unikalny w skali świata, przypisany fabrycznie do karty sieciowej  
- 8c:30:0f:f8:27:69  
- pierwsze 6 oktetów pozwala identyfikować producenta karty sieciowej  
- Można je zmieniać (spoofować) z poziomu systemu operacyjnego  

### **Warstwa 3 - Internetowa**  

Umożliwia komunikację między urządzeniami, które nie są bezpośrednio połączone fizycznie.

IP:

[https://www.cloudflare.com/learning/network-layer/internet-protocol/](https://www.cloudflare.com/learning/network-layer/internet-protocol/)
[https://en.wikipedia.org/wiki/Internet_Protocol](https://en.wikipedia.org/wiki/Internet_Protocol)
[https://www.avast.com/c-ip-address-public-vs-private](https://www.avast.com/c-ip-address-public-vs-private)
[https://www.ibm.com/docs/en/networkmanager/4.2.0?topic=translation-private-address-ranges  
(https://www.ibm.com/docs/en/networkmanager/4.2.0?topic=translation-private-address-ranges)

**Do zapamiętania:**

- Adresy IP można spoofować (podrabiać)
- Podzielona na prywatne vs publiczne. Prywatne mogą się powtarzać ale nie są routowalne. Publiczne są unikalne i routowalne  
- jest logicznym adresem interfejsu sieciowego urządzenia pracującego w sieci  

#### Maski podsieci:

[https://avinetworks.com/glossary/subnet-mask/](https://avinetworks.com/glossary/subnet-mask/)
[https://en.wikipedia.org/wiki/Subnetwork](https://en.wikipedia.org/wiki/Subnetwork)
[https://www.cloudaccess.net/cloud-control-panel-ccp/157-dns-management/322-subnet-masks-reference-table.html](https://www.cloudaccess.net/cloud-control-panel-ccp/157-dns-management/322-subnet-masks-reference-table.html)
[https://dnsmadeeasy.com/support/subnet](https://dnsmadeeasy.com/support/subnet)
[https://docs.microsoft.com/en-us/troubleshoot/windows-client/networking/tcpip-addressing-and-subnetting](https://docs.microsoft.com/en-us/troubleshoot/windows-client/networking/tcpip-addressing-and-subnetting)


**Do zapamiętania:** 

- Maska mówi, która część adresu IP to sieć, a która to konkretny host; pomaga zdecydować „czy to adres lokalny, czy przez bramę”.
- Najwygodniej zapisujemy ją w CIDR: adres/ liczba_bitów_sieci (np. 192.168.1.10/24 = maska 255.255.255.0).  
- Liczba po ukośniku to liczba jedynek w masce (np. /24 ma 24 bity sieci).
- W IPv6 używamy wyłącznie prefiksu CIDR (np. /64); zasada „część sieci + część hosta” pozostaje ta sama.
- „Ostatni adres w podsieci” to broadcast – trafia do wszystkich urządzeń w tej podsieci. (Przykład dla IPv4.)
- Maska dotyczy adresów IP; adresy MAC nie używają masek (to identyfikatory warstwy sprzętowej). [](https://www.cloudflare.com/learning/network-layer/what-is-a-subnet/?utm_source=chatgpt.com) 

##### **Address Broadcast:**

[https://www.omnisecu.com/tcpip/broadcast-mac-address.php](https://www.omnisecu.com/tcpip/broadcast-mac-address.php)
[https://www.ionos.com/digitalguide/server/know-how/broadcast-address/](https://www.ionos.com/digitalguide/server/know-how/broadcast-address/)
[https://en.wikipedia.org/wiki/Broadcast_address](https://en.wikipedia.org/wiki/Broadcast_address)
[https://www.pcmag.com/encyclopedia/term/broadcast-address](https://www.pcmag.com/encyclopedia/term/broadcast-address)

**Do zapamiętania:**  

- Ostatni adres IP w każdej podsieci to broadcast
- Adres broadcast służy do wysyłania komunikacji do wszystkich hostów w sieci zamiast do jednego
- Adres broadcast warstwy 2 (MAC) jest zawsze FF:FF:FF:FF:FF:FF
- Broadcast “to krzyk” w sieci, który usłyszy każde urządzenie
- Unicast to “szept” skierowany do osoby

**ARP (Address Resolution Protocol):**

[https://en.wikipedia.org/wiki/Address_Resolution_Protocol](https://en.wikipedia.org/wiki/Address_Resolution_Protocol)
[https://www.techtarget.com/searchnetworking/definition/Address-Resolution-Protocol-ARP](https://www.techtarget.com/searchnetworking/definition/Address-Resolution-Protocol-ARP)
[https://www.geeksforgeeks.org/how-address-resolution-protocol-arp-works/](https://www.geeksforgeeks.org/how-address-resolution-protocol-arp-works/)
[https://www.omnisecu.com/tcpip/address-resolution-protocol-arp.php](https://www.omnisecu.com/tcpip/address-resolution-protocol-arp.php)


**Do zapamiętania:**

- ARP służy do ustalenia jaki MAC ma dany adres IPv4 – potrzebne, by wysłać pakiet w lokalnej sieci - czyli do translacji adresów IP na MAC i viceversa.
- Pytanie „kto ma ten IP?” idzie broadcastem (MAC FF:FF:FF:FF:FF:FF); odpowiedź wraca unicastem do pytającego.
- Działa na skraju warstwy 2 i 3
- Gratuitous ARP = ogłoszenie swojego IP↔MAC bez pytania; służy m.in. do wykrywania konfliktów IP i szybkiego przełączenia po awarii.
- ARP działa tylko w obrębie tej samej podsieci/VLAN (nie przechodzi przez routery).
- Słaby punkt: ARP spoofing/poisoning (fałszywe odpowiedzi); obrona to m.in. Dynamic ARP Inspection + DHCP Snooping na przełącznikach.

##### **Switch vs router:**

[https://blog.router-switch.com/2021/10/difference-between-router-and-switch/](https://blog.router-switch.com/2021/10/difference-between-router-and-switch/)
[https://www.guru99.com/router-vs-switch-difference.html](https://www.guru99.com/router-vs-switch-difference.html)
[https://www.javatpoint.com/switch-vs-router](https://www.javatpoint.com/switch-vs-router)

**Do zapamiętania:**

- Switch - warstwy 2 ; router - warstwa 3
- Switch łączy urządzenia w jednej podsieci na podstawie adresów MAC
- Router łączy podsieci i routuje pakiety między nimi na podstawie adresu IP, stanowi granicę domeny broadcastowej (broadcast’y nie wychodzą poza podsieći
### **Warstwa 4 - Transportowa** 

Zarządza przesyłaniem danych między aplikacjami. Odpowiada za dzielenie danych na segmenty, numerowanie, retransmisję i kontrolę błędów.  
  
**TCP vs UDP:**

[https://www.guru99.com/tcp-vs-udp-understanding-the-difference.html](https://www.guru99.com/tcp-vs-udp-understanding-the-difference.html)
[https://www.freecodecamp.org/news/tcp-vs-udp/](https://www.freecodecamp.org/news/tcp-vs-udp/)
[https://www.diffen.com/difference/TCP_vs_UDP](https://www.diffen.com/difference/TCP_vs_UDP)

- TCP - powolny, UDP - szybki (mają pakiet dropy)
- TCP - upewnia się że dane zostały przesłane oraz w odpowiedniej kolejności
- UDP - po prostu wysyła dane, nieuporządkowane
##### **3-way handshake:**

[https://www.guru99.com/tcp-3-way-handshake.html](https://www.guru99.com/tcp-3-way-handshake.html)
[https://www.sciencedirect.com/topics/computer-science/three-way-handshake](https://www.sciencedirect.com/topics/computer-science/three-way-handshake)
[https://afteracademy.com/blog/what-is-a-tcp-3-way-handshake-process](https://afteracademy.com/blog/what-is-a-tcp-3-way-handshake-process)
[https://pl.wikipedia.org/wiki/Protok%C3%B3%C5%82_sterowania_transmisj%C4%85](https://pl.wikipedia.org/wiki/Protok%C3%B3%C5%82_sterowania_transmisj%C4%85)
[https://users.cs.northwestern.edu/~agupta/cs340/project2/TCPIP_State_Transition_Diagram.pdf  
(https://users.cs.northwestern.edu/~agupta/cs340/project2/TCPIP_State_Transition_Diagram.pdf)

**Do zapamiętania:**

- Trzy kroki: SYN → SYN/ACK → ACK — po nich zaczynają płynąć dane.
- Cel: uzgodnić parametry połączenia (m.in. numery sekwencji) i potwierdzić gotowość obu stron.
- Handshake dotyczy TCP; UDP nie ma tego etapu.**


![alt](/courses/szkola-security/secuirty-analyst/sieć/powtorka-z-sieci/notatki/Attachments/image.png)
![alt](/courses/szkola-security/secuirty-analyst/sieć/powtorka-z-sieci/notatki/Attachments/image-1.png)

### **Warstwa 5 - Sesji (Aplikacji)**

**Warstwa sesji** odpowiada za **nawiązywanie, utrzymywanie i kończenie sesji komunikacyjnej** między aplikacjami. Kontroluje przebieg dialogu pomiędzy urządzeniami, dba o synchronizację wymiany danych i może wyznaczać **punkty kontrolne**, dzięki którym po przerwaniu połączenia transmisję można wznowić od ostatniego zapisanego miejsca, a nie od początku. W praktyce modelu TCP/IP funkcje tej warstwy często nie występują jako osobna warstwa, lecz są realizowane razem z mechanizmami wyższych poziomów.

Aby zapewnić poprawną komunikację, warstwa sesji:

- **zestawia, utrzymuje i zamyka sesję**,
- **synchronizuje** wymianę danych między aplikacjami,
- umożliwia stosowanie **checkpointów** (punktów kontrolnych),
- wspiera **wznawianie połączenia** po błędzie lub zerwaniu transmisji.

**Do zapamiętania:**

- odpowiada za **dialog między aplikacjami**,
- pilnuje początku, trwania i zakończenia sesji,
- umożliwia wznowienie transmisji od ostatniego punktu kontrolnego,
- jest szczególnie ważna tam, gdzie trzeba utrzymać ciągłość komunikacji.

https://kaser.zsl.gda.pl/PSK%202/2.%20Model%20OSI%20-%20warstwa%20aplikacji%20prezentacji%20i%20sesji.pdf

##### NetBios

https://pl.wikipedia.org/wiki/NetBIOS
https://users.pja.edu.pl/~s3452/prezentacja/html/netbios_netbeui.html
### **Warstwa 6 - Prezentacji (Aplikacji)**

**Warstwa prezentacji** odpowiada za sposób przedstawienia danych tak, aby aplikacja po stronie odbiorcy mogła je poprawnie odczytać. Jej zadaniem jest **tłumaczenie formatów danych**, **kodowanie i dekodowanie**, **kompresja** oraz **szyfrowanie i deszyfrowanie** informacji. Dzięki temu dwa różne systemy mogą wymieniać dane mimo różnic w sposobie ich zapisu i reprezentacji.

Do podstawowych zadań warstwy prezentacji należą:

- **konwersja formatów danych**,
- **kodowanie i dekodowanie** zestawów znaków,
- **kompresja i dekompresja** danych,
- **szyfrowanie i deszyfrowanie** informacji.

Przykłady standardów i mechanizmów związanych z tą warstwą:

- **SSL/TLS**,
- **JPEG**,
- **MPEG**.

**Do zapamiętania:**

- dba o **format danych**,
- „tłumaczy” dane między różnymi systemami,
- odpowiada za **szyfrowanie** i **kompresję**,
- sprawia, że dane są zrozumiałe dla aplikacji odbiorcy.

https://jchost.pl/blog/tls/

### **Warstwa 7 - Aplikacji**

**Warstwa aplikacji** jest najwyższą warstwą modelu OSI i znajduje się **najbliżej użytkownika**. Zapewnia programom użytkowym dostęp do usług sieciowych, czyli umożliwia korzystanie z takich usług jak **strony WWW, poczta elektroniczna, przesyłanie plików czy rozwiązywanie nazw domen**. To właśnie tutaj działają protokoły, z których korzystają przeglądarki internetowe, klienci poczty i inne aplikacje sieciowe.

Warstwa aplikacji realizuje między innymi:

- udostępnianie **usług sieciowych** aplikacjom użytkownika,
- inicjowanie komunikacji użytkownika z siecią,
- obsługę **żądań i odpowiedzi** między aplikacjami,
- wymianę danych w usługach WWW, poczty i transferu plików.

Przykładowe protokoły tej warstwy:

- **HTTP / HTTPS** – obsługa stron internetowych,
- **SMTP** – wysyłanie poczty elektronicznej,
- **DNS** – tłumaczenie nazw domen na adresy IP,
- **FTP** – przesyłanie plików.

**Do zapamiętania:**

- to warstwa **najbliższa użytkownikowi**,
- nie jest samą aplikacją, tylko warstwą dostarczającą jej usługi sieciowe,
- korzystają z niej np. **przeglądarki, klienci poczty i programy FTP**,
- typowe protokoły: **HTTP, SMTP, DNS, FTP**.

https://www.cloudflare.com/learning/ddos/what-is-layer-7/

https://www.geeksforgeeks.org/computer-networks/protocols-application-layer/

https://pl.wikipedia.org/wiki/Domain_Name_System
### RODZAJE ATAKÓW SIECIOWYCH

##### DDoS - Distributed Denial of Service 

Atak „zatykający” usługę tak, by legalni użytkownicy nie mogli z niej skorzystać. Rozproszone = Distributed = ruch leci z wielu maszyn/użytkowników naraz (najczęściej botnet z przejętych urządzeń/serwerów).  
  
1. Wolumenowe (warstwa sieci): celem jest „zalać rurę” samą ilością danych.  
	**Przykłady:**  
	UDP flood (puste pakiety), ICMP flood (ping), amplifikacja/odbicie: DNS/NTP/SSDP/CLDAP – mała prośba → duża odpowiedź do ofiary (często ze sfałszowanym źródłem).  
  
2. Ataki na protokół (warstwa transportu): „męczenie” stosu TCP/IP, żeby zjadał zasoby. Przykłady: SYN flood (opis poniżej), ACK/RST flood, fragmentacja IP.
3. Aplikacyjne (warstwa www/API): uderzają w logikę serwisu – mało ruchu, duży koszt po stronie aplikacji. Przykłady: HTTP GET/POST flood, „Slowloris” (bardzo wolne nagłówki), ataki na drogie endpointy (np. wyszukiwanie/raporty).  
  
**SYN Flood** - napastnik zasypuje serwer pakietami SYN (początek połączenia TCP) i nie kończy uzgadniania (brak ostatniego ACK). Serwer trzyma „półotwarte” wpisy w tabeli połączeń i w końcu nie ma miejsca dla normalnych klientów.  
W celu: wyczerpania pamięci/CPU na obsługę niedokończonych sesji, czasem też łącze (jeśli wolumen duży).  

**[SYN FLOOD Explained](https://www.cloudflare.com/learning/ddos/syn-flood-ddos-attack/)**

Jak to wygląda „w logach i drutach”

- Wolumenowe: nagły skok przepływu (Gb/s), jeden/ kilka protokołów, mało stanów TCP.
- Protokół: masa „gołych” flag TCP (SYN/ACK/…); dużo retransmisji, serwer odrzuca nowe sesje
- Aplikacyjne: normalnie wyglądające żądania HTTP, ale nienaturalna skala/kadencja do wybranych URL-i; CPU aplikacji rośnie, łącze jeszcze daje radę.

[DDoS attack explained](https://www.cloudflare.com/learning/ddos/what-is-a-ddos-attack/)
###### Ataki Reflected / Amplification

**Amplification** = wzmocnienie: napastnik wybiera takie usługi/zapytania, gdzie mała prośba wywołuje dużą odpowiedź. Dzięki temu z niewielkiego własnego ruchu robi się ogromny ruch na ofiarę (wzmocnienie razy X). Najczęściej wykorzystuje się „otwarte” serwery DNS, NTP, SSDP itd.
  
**Reflected (odbity)**: napastnik wysyła prośbę do cudzej usługi (np. DNS/NTP/SSDP) ze sfałszowanym adresem źródłowym ofiary. Serwer odsyła odpowiedź do ofiary, więc prawdziwe źródło ataku się „chowa” za urządzeniami pośrednimi.  
To podstawa wielu ataków DDoS, bo UDP nie wymaga na starcie potwierdzenia nadawcy.

W praktyce ataki są reflected + amplification jednocześnie: odbicie ukrywa źródło, a wzmocnienie „pompuje” wolumen.
###### Ataki DNS amplification

1. Napastnik wysyła krótkie zapytanie DNS do wielu otwartych resolverów (serwerów, które odpowiadają każdemu), podszywając się pod IP ofiary.
2. Te serwery odsyłają duże odpowiedzi do adresu ofiary, „zalewając” jej łącze/systemy. Cloudflare  

[DNS amplification explanation](https://www.cloudflare.com/learning/ddos/dns-amplification-ddos-attack/)

**Dlaczego DNS dobrze „wzmacnia”?**

Zapytania bywają małe (dziesiątki–setki bajtów), a odpowiedzi potrafią mieć kilka kilobajtów — szczególnie przy rekordach TXT i przy DNSSEC, gdzie podpisy kryptograficzne zwiększają rozmiar. EDNS rozszerza dopuszczalny rozmiar UDP do typowo kilku KB, co dodatkowo ułatwia wzmocnienie. 

Współczynnik wzmocnienia (przykład):  
jeżeli zapytanie ma ~64 B, a odpowiedź ~6400 B, to mamy ~100× więcej ruchu w stronę ofiary. To ilustracja ogólnej zasady „małe pytanie → wielka odpowiedź”. (Dokładne liczby zależą od konkretnego pytania i konfiguracji serwera.)  
  
**I tak przykład:**  

1. 1000 hackerów wysyła 100 podrobionych zapytań DNS w ciągu 1 sec. do różnych serwerów DNS.  
2. Hakerzy wysyłają 1000x1000x64= 64 mil. B/s = 64 MB/s (ale tylko 64KB/s per 1 osoba)
3. Ofiara otrzymuje 1000x1000x6400 = 6.4 GB/s ruchu  
  
Ofiara w logach i plikach pcap widzi tylko adresy losowych serwerów DNS!  

Cechy charakterystyczne w telemetrii:  
mnóstwo odpowiedzi DNS z wielu serwerów świata do jednego IP ofiary; ofiara nie wysłała odpowiadających zapytań (bo źródło było sfałszowane). 

###### Inne ataki DDoS: 

UDP flood - zalew setkami tysięcy pakietów UDP na losowe porty.

Efekt: host/sieć traci czas na „odbieranie” i generowanie ICMP „port unreachable”.  

Jak to poznać: ogromny, rozproszony ruch UDP bez sensownych sesji.  
  
ICMP Flood  -  masowe echa („pingi”) lub inne typy ICMP.

Efekt: zapycha łącze i CPU urządzeń po drodze.

Jak to poznać: ciągłe, duże wolumeny ICMP z wielu źródeł.  
  
Ping of Death - specjalnie sfragmentowane pingi > maks. rozmiaru pakietu, kiedyś wysypywały systemy.

Efekt: dawniej crash hosta; dziś rzadkie dzięki łatkom.

Jak to poznać: nietypowe fragmenty/oversize ICMP.  
  
Slowloris - bardzo wolne wysyłanie nagłówków HTTP, utrzymywanie tysięcy „niedokończonych” połączeń.

Efekt: serwer www trzyma otwarte wątki/gniazda i nie obsługuje legitnych użytkowników, mimo niewielkiego wolumenu ruchu.

Jak to poznać: dużo półotwartych żądań HTTP, niskie Mbps, a wysoki „concurrency” na serwerze; logi pokazują długie czasy i niedokończone nagłówki.

###### Praktyka DDoS - wykrywanie

[DDoS analysis step by step](https://medium.com/@ronak.d.sharma111/analyzing-a-ddos-attack-using-wireshark-8535274cd00e)

1. Głównym założeniem w wykrywaniu DDoS jest wykrycie nietypowych zachowań jak:  
	- **przy atakach na protokół (np. SYN flood, fragmentacja IP, ACK/RST flood)**
		Jak rozpoznać:  dużo pakietów z konkretną flagą TCP (np. SYN) i mało odpowiedzi; masa „półpołączeń”; błędy w „Expert Info” (Wireshark) lub w NetFlow: ogrom flows z minimalną liczbą bajtów.
		Co notować: docelowy IP/port, liczby SYN/s (lub innej flagi), asymetria ruchu (A→B >> B→A).  
	- **Ataki wolumenowe (przepustowość/„zalanie rury”)**
		Jak rozpoznać: wykres I/O idzie „w sufit” (Mb/s/Gb/s), protokół często UDP lub ICMP; w NetFlow rośnie „bytes per second” do jednego celu.
		Co notować: piki przepustowości, top protokoły i porty, top AS/źródła.  
	- **Aplikacyjne (HTTP/HTTPS, „Slowloris”, ciężkie endpointy)** 
		Jak rozpoznać: dużo żądań HTTP do jednego URL-a/hosta, długie czasy odpowiedzi, wiele równoległych połączeń; małe Mb/s, a CPU na serwerze „w czerwonym”.  
		Co notować: docelowa domena/URL, liczba żądań/s, wzorce User-Agent/IP, czy to GET/POST.
	- **Reflected / Amplified (DNS i inne odbicia)**  
		Jak rozpoznać: u ofiary w pcap widzisz masę odpowiedzi DNS (lub NTP/SSDP/CLDAP) bez odpowiadających zapytań; źródła to tysiące serwerów na świecie. 
		Co notować: lista serwerów „odbijających” (IP, port 53/123/1900…), rozmiary odpowiedzi, szacowany współczynnik „wzmocnienia”.
	- **Ping of Death (historyczny, ale wiedzieć warto)** 
		Jak rozpoznać: nietypowa fragmentacja i „za duże” pakiety ICMP. Dziś rzadko, bo systemy są załatane. 
		Co notować: czasy/źródła, typy ICMP, dowód na oversize/fragmenty
	- **ICMP Flood (ping flood)**  
		Jak rozpoznać: w pcap/NetFlow dominują pakiety/protokoły ICMP do jednego celu; przepustowość rośnie.  
		Co notować: ilość ICMP/s, top źródła/ASN, czy są odpowiedzi Echo Reply (często brak, bo ofiara nie wyrabia).
	- UDP flood 
		- Jak rozpoznać: mnóstwo małych pakietów UDP, wiele źródeł, mało odpowiedzi z serwera; w pcap widać też później ICMP Port Unreachable (serwer odpowiada, że port zamknięty). 
		- Co notować: dokąd leci (IP/porty), ile pakietów/s, czy pojawia się dużo ICMP „unreachable”.

2. Uproszczony „plan oględzin” pcap/NetFlow
	- Sprawdź kiedy i ile: I/O Graphs (pik? ściana?), Protocol Hierarchy (przy TCP sprawdzamy odchylenia (End Packets) /Top flows
	- Ustal ofiara + port: Conversations/Endpoints (duża asymetria do jednego IP).
	- Zidentyfikuj rodzaj:  
	    – dużo SYN → warstwa TCP (SYN flood),  
	    – masa UDP/ICMP → wolumenowe,  
	    – HTTP/HTTPS do jednego URL → aplikacyjne,  
	    – same odpowiedzi DNS/NTP → reflected/amplified.  
    
    - Zrób listę źródeł (top 10/50), zapisz wolumen/s, porty i protokoły — to materiał do blokad/zgłoszeń.
    - Wyeksportuj mały pcap z reprezentatywnymi pakietami (dowód do zgłoszenia).

**Przydatne filtry:**  

**ip.addr == (IP ATAKUJĄCEGO) && ip.addr == (IP OFIARY)**

![alt](/courses/szkola-security/secuirty-analyst/sieć/powtorka-z-sieci/notatki/Attachments/image-2.png)
######  TSHARK TIPS:

Zaletą tsharka jest szybkie przetwarzanie plików pcap.  
Tak jak w Wiresharku, możemy wyświetlać Statystyki jak Endpointy (IP,TCP etc), Conversations, Packet Lengths etc.

**Przykłady:**

![alt](/courses/szkola-security/sieć/powtorka-z-sieci/notatki/Attachments/image-3.png|697)
![alt](/courses/szkola-security/sieć/powtorka-z-sieci/notatki/Attachments/image-4.png|697)

**NFDUMP:**

![alt](/courses/szkola-security/sieć/powtorka-z-sieci/notatki/Attachments/image-5.png|697)
![alt](/courses/szkola-security/secuirty-analyst/sieć/powtorka-z-sieci/notatki/Attachments/image-6.png)

By zrobić graf jak w Wiresharku, należy weksportować nfdumpa do pliku .csv poleceniem  

**nfdump -r nfcapd.202204061026 -o csv > netflow.csv**
##### Atak MITM (Man-in-the-Middle)

[MitM Explained](https://www.imperva.com/learn/application-security/man-in-the-middle-attack-mitm/)

###### FAKE DNS

1. Alicja wpisuje janiepawle.pl. Jej urządzenie pyta DNS „jaki jest adres IP tej domeny?”. W otwartej sieci (McD Wi-Fi) ruch nie jest chroniony, więc „zły” może wtrącić swoją odpowiedź.
2. Atakujący ma kontrolę nad DNS (np. podał w sieci swój serwer DNS przez fałszywy DHCP albo „przegonił” odpowiedź prawdziwego DNS szybciej niż on). Wysyła więc fałszywą odpowiedź: „janiepawle.pl = 13.37.13.37” (jego serwer), zamiast prawdziwego 123.123.123.123.
3. Telefon/laptop wierzy temu DNS i łączy się pod 13.37.13.37. Od tej chwili prośby Alicji (HTTP/HTTPS) lecą do serwera hakera.
4. On może:  
- na HTTP (bez szyfrowania) w pełni podsłuchiwać i podmieniać treść (loginy, formularze, pliki);
- na HTTPS natrafia na przeszkodę: przeglądarka sprawdza certyfikat.  
- Jeśli haker nie ma ważnego certyfikatu dla janiepawle.pl, przeglądarka krzyczy (ostrzeżenie o certyfikacie) — to moment, w którym użytkownik powinien się wycofać.  
- Haker może próbować obejść: SSL-strip (zmusza do wersji http://, jeśli strona nie wymusza HTTPS/HSTS), fałszywą domeną-bliźniakiem (np. janiepawIe.pl z literą „I” zamiast „l” — wtedy certyfikat będzie „prawidłowy”, ale dla innej domeny), albo rzadziej — mieć dostęp do zaufanego certyfikatu (np. na zainfekowanym urządzeniu doinstalowano mu „zaufany” urząd certyfikacji).

Gdy ruch trafia do hakera, ten może robić pełne MiTM: czytać, modyfikować, a nawet przekazywać dalej na prawdziwy serwer (żeby użytkownik nic nie zauważył), działając jak „przekaźnik” pośrodku.

**Jak to wygląda (w zrzucie ruchu):**

- W DNS widać, że janiepawle.pl nagle rozwiązuje się na nietypowe IP (13.37.13.37), często z bardzo niskim TTL.
- Odpowiedź DNS może przyjść z innego serwera niż zazwyczaj (inny adres/MAC).
- Jeśli dojdzie do HTTPS, przeglądarka zgłasza błąd certyfikatu lub SNI/Cert pokazują domenę inną niż oczekiwana; przy SSL-strip widzisz, że po kliknięciu w HTTPS następuje przekierowanie do HTTP.

Szyfrowane protokoły mocno utrudniają MiTM  
- HTTPS chroni treść i tożsamość serwera, o ile nie ignorujesz błędów certyfikatu i jest HSTS (bez tego możliwy SSL-strip).  
- DNSSec chroni między serwerami DNS; użytkownika w publicznym Wi-Fi lepiej chroni DoH/DoT lub VPN.  
- VPN zamyka cały ruch w tunelu (uwaga na split-tunneling i fałszywe konfiguracje).  
- SSH/IPsec są mocne pod warunkiem poprawnej weryfikacji kluczy i nowoczesnych szyfrów.

Gdy niższa warstwa jest podatna, samo szyfrowanie czasem nie wystarczy  
Zła konfiguracja, ataki na niższą warstwę (L2/L3), Downgrade, Zaufany fałszywy root CA, Zainfekowany klient kradnie dane przed/po szyfrowaniu.

###### Atak ARP Spoofing

ARP spoofing „działa”, bo ARP jest z natury naiwny: każdy w tej samej podsieci może krzyknąć „ten adres IP to mój MAC” – bez podpisu, bez weryfikacji, bez pamiętania „kto pierwszy był prawdziwy”. Systemy zwykle przyjmują ostatnią odpowiedź, jaka przyszła (albo dowolną, która dotrze), i nadpisują swoją tablicę ARP. ARP projektowano dla zaufanych, małych LAN-ów, nie z myślą o wrogach.

Przyklad:

1. HOST A chce gadać z 192.168.0.2. Wysyła broadcast ARP: „kto ma 192.168.0.2? podaj MAC”. Ten pakiet słyszy każdy w VLAN-ie. 
2. Prawowity HOST B (192.168.0.2) odsyła unicastem: „192.168.0.2 ma MAC_B”. A zapisuje to w ARP cache i zaczyna wysyłać ramki do MAC_B.  
3. HOST D (atakujący) wtrąca się na dwa sposoby:
4. Wyścig: od razu odsyła fałszywą odpowiedź (albo nawet kilka, co chwilę), że „192.168.0.2 ma MAC_D”. Jeśli jego odpowiedź dotrze szybciej albo później, ale system A akceptuje „ostatnią odpowiedź”, wpis w ARP u A zmienia się na MAC_D.
5. Bez pytania: wysyła gratuitous ARP (ogłoszenie „sam do siebie”) mówiąc „192.168.0.2 ↔ MAC_D”. Wielu hostów przyjmie to na wiarę i nadpisze tablicę, mimo że A o nic nie pytał.
6. Od tej chwili A wysyła ruch do D, bo „wierzy”, że MAC_D to 192.168.0.2. D może:
7. grać MiTM: przekazywać dalej do B (przepisać adres docelowy na MAC_B), podsłuchując i ewentualnie zmieniając treść;
8. robić DoS: po prostu nie przekazywać dalej, więc A „traci” kontakt z B.
9. Żeby utrzymać kontrolę, D co jakiś czas powtarza fałszywe ARP-y (ARP cache wygasa). Równolegle zwykle truje też w drugą stronę: mówi B, że „192.168.0.1 (A) ma MAC_D”, by cały ruch A↔B przechodził przez D.

ARP jest starym protokołem - oraz “ufającym”. W czystym L2 nie ma mechanizmu zaufania, więc jedno złośliwe urządzenie może wprowadzać innych w błąd.  
Dlatego w nowoczesnych sieciach trzeba dołożyć kontrolę na switchach (DAI/DHCP Snooping/802.1X) i segmentację — inaczej ARP spoofing pozostaje banalny.

  
[Czym jest QUIC?](https://owl.wf/strona_www/quic-protokol-nowej-generacji/)

Protokół QUIC to nowy szyfrowany protokół sieciowy warstwy transportowej. QUIC został zaprojektowany, aby ruch HTTP był bezpieczniejszy, wydajniejszy i szybszy.

###### Praktyka MiTM

**TIP:**  
**Są narzędzia typu NDR (Network Detection and Response) w firmach, które generują pcap’y do tyłu :)**


1. Filtrujemy HTTP (filter -> http)
2. **Szukamy nietypowych rzeczy (na podstawie mitm4.pcapng**

![alt](/courses/szkola-security/secuirty-analyst/sieć/powtorka-z-sieci/notatki/Attachments/image-7.png)

5. Host: szkolasecurity.pl, a Destination IP = 10.0.0.137 
	(jest to adres z “naszej” sieci). To pachnie fałszywym DNS/„rogue proxy” – publiczna domena nie powinna rozwiązywać się na lokalne 10.x.x.x.
	
	Można sprawdzić w pcapie - w DNS -> odpowiedź A dla tej domeny (TTL niski?).
6. Żądanie GET /calc.exe do 8.8.8.8:8080 i odpowiedź 200 OK (x-msdos-program). Google DNS (!!!) nie serwuje EXE, a port 8080 to zwykle port przechwytującego proxy.
	→ To artefakt numer 1: File → Export Objects → HTTP→ calc.exe do analizy.
7. Wiele GET do szkolasecurity.pl, ale do 10.0.0.137. Legalny serwis powinien iść do publicznego IP (nie 10.x).
	→ do zanotowania: IP 10.0.0.137 jako podejrzany węzeł MiTM.
8. Wnioski z Source/Destination:  
    10.0.0.137 / 00:0c:29:b9:01:a9 pełni rolę rogue proxy/web-serwera i/lub DNS-podmieniacza.  
    Ofiara wysyła HTTP do lokalnego IP (nie do prawdziwego publicznego adresu), a pośrednik serwuje treść i pliki (w tym calc.exe). Brama 00:50:56:… nie „widzi” tych rozmów – dzieją się lokalnie w LAN.
9. użycie filtrów arp i dns pozwalają nam zobaczyć:  
    - W kółko lecą ogłoszenia „10.0.0.1 is at 00:0c:29:b9:01:a9” wysyłane przez 00:0c:29:b9:01:a9 do ofiary 00:0c:29:5c:2f:a2. To klasyczne trucie ARP: napastnik podszywa się pod bramę 10.0.0.1.
    - Pojawiają się też „Who has 10.0.0.100? Tell 10.0.0.137” oraz „10.0.0.137 is at 00:0c:29:b9:01:a9” — napastnik (10.0.0.137) ogłasza swój MAC i „zaciąga” ruch do siebie.
    - Efekt: host ofiary zapisze w ARP, że brama 10.0.0.1 ma MAC napastnika 00:0c:29:b9:01:a9 → cały ruch idzie przez atakującego (MiTM) albo w ogóle „ginie” (DoS).
    - Ofiara pyta 8.8.8.8, a w odpowiedziach na A szkolasecurity.pl dostaje 10.0.0.137 (adres prywatny z LAN). To DNS spoofing/„rogue resolver”: publiczna domena nie powinna rozwiązywać się na lokalny 10.x.x.x.

**Analiza wniosków:**

1. Ktoś zrobił atak ARP spoofing, przekierował cały ruch na siebie, po czym “zaspoofował” adres 8.8.8.8 na swojej maszynie lokalnej, i zaczął serwować odpowiedzi DNS tak jakby z adresu 8.8.8.8
2. Po wyeksportowaniu plików (Export Objects - > HTTP) i po otworzeniu pliku HTMLowego, widać, że użytkownik musiał kliknąć na podrobioną stronę internetową:

![alt](/courses/szkola-security/secuirty-analyst/sieć/powtorka-z-sieci/notatki/Attachments/image-8.png)

3. Udowodniliśmy że pracownik kliknął i ściągnął ten plik binarny
4. Atakującemu atak się udał (ARP spoofing / MiTM)

##### Skanowanie - np. portów (czy to jest atak?)

Jest to … “odpukanie” adresów i portów, żeby sprawdzić, które usługi są dostępne i jak są skonfigurowane. Samo w sobie nie wygląda jak atak, tylko bardziej jak rozpoznanie.

Atakujący robią to by znaleźć błędy i podatności (otwarte porty, słabe wersje usług, domyślne strony). To zwykle wstęp do ataku. Widzimy tego dużo bo w internecie roi się od automatycznych skanerów (boty, badacze, Shodan) tak zwany “szum”.

[Network Scanning Explained v1](https://www.dnsstuff.com/network-scanning)

[Network Scanning Explained v2](https://www.hackingloops.com/port-scanning-in-cybersecurity/)

**Napopularniejsze toole:**

- Nmap
- Rustscan
- Naabu
- Angry IP scanner
###### Rodzaje skanów

**Pasywne:**  

obserwujesz to, co już „wycieka” do świata, bez dotykania celu.  
  
Przykład:  WHOIS/DNS/Certyfikaty (CT logs), Shodan/Censys, zbiory OSINT, analiza NetFlow/telemetrii po naszej stronie, podsłuch w własnym punkcie (mirror/SPAN).  
Zwykle niewykrywalne u ofiary; można jedynie zauważyć wzrost zapytań OSINT o naszą domenę/ASN (pośrednio). Są powolne i niedokładne. Male ryzyko prawne.  
  
**Aktywne:**  

wymagają kontaktu z infrastrukturą celu = zostawiają ślady, dają dużo lepsze pokrycie i więcej szczegółów niż skany pasywne  
  
Przykłady: skan portów (SYN/CONNECT/UDP), baner grabbing (HTTP/SSH/SMTP), skany wersji (nmap -sV), słowniki na loginy, testy podatności (DAST, Nessus/Qualys), fuzzing (wysyłanie różnych danych wejściowych) endpointów.

**Skany sieciowe (warstwa L3/L4 - sieciowa i transportowa):**

- portów - wykonywane w celu wykrycia jakie usługi działają na hoście (np. 22/SSH, 80/HTTP, 3389/RDP).  
	SYN scan („półotwarty”): wysyłasz SYN na porty; SYN-ACK = otwarty, RST = zamknięty, brak odpowiedzi = filtrowany. Szybki i mało „widoczny” dla aplikacji.  
- Istnieje wiele odmian skanów portów np. TCP Connect (pełne 3-way), ACK/FIN/Xmas (omijanie filtrów), UDP scan (wolniejszy, szuka usług na UDP).  
- Nmap - podstawowe narzędzie do skanu portów  
-  adresów IP - służą odkryciu jakie urządzenia znajdują się w sieci
- Wykorzystują pakiety ICMP (ping) bądź protokoły niższego poziomu (warstwa 2) do zmapowania sieci lokalnej  
  
Skany podatnościowe:

- są robione po to, by znaleźć dziury w systemach i apkach, zanim zrobi to ktoś “o niecnych zamiarach”
- sprawdzają wersje/usługi/konfiguracje i porównują z bazą znanych luk (CVE), czasem testują proste wektory ataku. Wynik to lista problemów z oceną ryzyka (CVSS) i poradą „co naprawić”.
- mogą szukać też typowych błędów w konfiguracji (słabe hasła, publiczne dostępne panele, itd.)
- Jest wiele różnych metodologii
1. skan bez logowania - służą skanowaniu urządzeń z takiej pozycji jaką widzi je atakujący
2. skany z logowaniem - wykorzystują konta dostępowe aby głębiej przeskanować system

**Nessus / Qualys –** skanery infrastruktury i konfiguracji (agentowe i z sieci), bogate raporty.

**OpenVAS (Greenbone)** – open-source odpowiednik; dobre na start/laby.

**Nikto** – prosty skaner serwerów WWW (nagłówki, znane błędy), do szybkiego „health checku” warstwy web.

###### Praktyczna analiza skanu

TIP - flaga RST - Reset, nieudane połączenie. Zapamiętać przy analizowaniu skanu, ponieważ to pokazuje ilość wykonywanych “skanów”. Wystarczy zaaplikować:

**tcp.flags == 0x0014 by wylistować wszystkie “nieudane” połączenia TCP.**

  
Najlepiej taki skan przeanalizować w taki sposób:  
1. Statistics - > Conversation -> TCP  
2. Port B -> sortujemy. Tutaj możemy zaobserować, czy skan “leciał” po wszystkich portach:

![alt](/courses/szkola-security/secuirty-analyst/sieć/powtorka-z-sieci/notatki/Attachments/image-9.png)

4. Następnie patrzymy Packets A->B i Packets B->A. Tutaj, jeżeli widzimy pakiety o wielkości 1 bajta, po obu stronach, możemy wywnioskować, że to były pakiety SYN -> RST . Jeżeli w Packets A->B będzie 2 bajty, a w Packets B->A, daje to na 3-way handshake, i w ten sposób “ktoś” dowiedział się o istnieniu otwartego portu.
5. Możemy to też sprawdzić aplikując kolumnę Destination Port do “Column Preferences”.
6. Filtrem (ip.src == 10.0.0.20) && !(tcp.flags == 0x0014) możemy sprawdzić jakie porty są dla atakującego otwarte.
  
**Porty filtrowane:**  

![alt](/courses/szkola-security/secuirty-analyst/sieć/powtorka-z-sieci/notatki/Attachments/image-10.png)

1. Statistics - > Conversation -> TCP  
2. Tutaj widzimy w pakietach B->A zero bajtów. To nam pokazuje, że porty były filtrowane i nie odesłały żadnej odpowiedzi.

UWAGA: to samo skanowanie może wyglądać zupełnie inaczej zależnie od miejsca, gdzie „podsłuchujesz”:
- przed firewallem: widzisz wiele prób + dużo „ciszy” (FILTERED),
- za firewallem: widzisz tylko to, co przepuszczono; zablokowanych portów nie widać wcale.

***ZAWSZE ZWRACAJ UWAGĘ SKĄD (Z JAKIEGO MIEJSCA W SIECI) JEST PCAP!***
