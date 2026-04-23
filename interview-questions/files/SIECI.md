#### What is Firewall? 
Czym jest firewall (zapora sieciowa)?  

Firewall jest urządzeniem bądź programem które zawiera zbiór reguł, blokujących lub pozwalających na określony ruch sieciowy.
  
#### What is OSI Model? Explain each layer. 
Czym jest model OSI? Omów każdą warstwę.  

Model OSI jest modelem opisowym - w jaki sposób dane przechodzą przez sieć. Każda posiada swoje informacje, czyli nagłówki. Zmiana zerów i jedynek w solidne dane nazywamy enkapsulacją. I odwrotnie, rozbijanie danych na zera i jedynki to dekapsulacja. Dzieli się na 7 warstw:  
  
- (7) Aplikacji - w tej warstwie jest wszystko to co my widzimy na ekranie, czyli co widzi aplikacja - przeglądarka itp. - mamy tutaj protokoły jak HTTP, SMTP etc.Są tu dane aplikacyjne (data), które występują we wszystkich 3 warstwach od góry.  
  
- (6) Prezentacji  - tutaj zachodzi wszystkie procesy standaryzacji, żeby było zrozumiane dla wszystkich aplikacji i systemów. Czyli procesy szyfrowania danych, kodowanie, kompresja itp.  
  
- (5) Sesji - przy każdym połączeniu musi być i sesja, w tej warstwie jest utrzymywane połączenie logiczne  
  
- (4) Transportowa - odpowiada za to, jak dane są przesyłane między dwoma urządzeniami, czyli czy chcemy je mieć dokładne i wolne, lub niedokładne i szybkie, mówimy tu o protokołach TCP i UDP, czyli np. TCP będzie wybrane przy pobieraniu danych (i przy TCP mamy wybór odpowiednich portów, HTTP, SMTP), a UDP np. w streamowaniu wideo, gdzie jak pojedyncze piksele nie dotrą, to nic wielkiego się nie stanie. W TCP mamy część danych nazywanych segmentami a w UDP datagramy.  
  
- (3) Sieciowa - w tej warstwie decyduje się, jaką drogą pakiety dotrą do celu oraz jakie dane są przesyłane pomiędzy sieciami. Komunikacja odbywa się na poziomie adresów IP. Czyli cały routing odbywa się tutaj. Ta warstwa decyduje o wysyłaniu pakietów z adresu źródłowego do adresu docelowego w miarę najkrótszym czasie. Równiez tutaj się odbywa adresacja IP.  
  
- (2) Łącza danych - tutaj zachodzi komunikacja w tej samej sieci LAN, switche, adresy MAC itp. Jest dodana ramka (frame) z fizycznymi adresami MAC, żeby dane widziały gdzie iść. 

- (1) Fizyczna - w tej warstwie zachodzi bezpośrednia komunikacja pomiędzy urządzeniami, poprzez kable itp, czyli wymiana bitów pomiędzy urządzeniami.

#### What is Three-Way Handshake?
Czym jest trzyetapowy handshake (TCP three-way handshake)?

Three-Way handshake to metoda która opisuje wymianę komunikacji pomiędzy hostami, które używają TCP. Three-way, bo ma trzy “segmenty” - klient wysyła segment z flagą SYN (oraz ze swoim numerem ISN), że chce się połączyć, dostaje zwrotkę od hosta B SYN+ACK acknowledge - “przyjęliśmy Twoją prośbe i odsyłamy swój ISN”, a klient odsyła ACK, z potwierdzeniem ISN serwera.Przez to też TCP jest wolniejszy ale bardziej niezawodny, co szybki i stratny UDP. Mniej znane flagi - RST - resetuje połączenie, PSH - push, wymusza przesyłanie pakietu.  
  

#### What is TCP/IP Model? Explain the difference between OSI and TCP/IP model. 
Czym jest model TCP/IP? Wyjaśnij różnice między modelem OSI a TCP/IP.

**Model TCP/IP jest modelem praktycznym, który w przeciwieństwie do OSI (modelu referencyjnego), ma realne przełożenie jak dane są przesyłane w Internecie.** 

Przede wszystkim jest zorientowany na zestaw protokołów i stanowi podstawę Internetu. Model OSI pozwala na zrozumienie funkcji - **ma charakter dydaktyczny.** 

Przedstawiany jest w czterech warstwach,  
- (4)Aplikacyjna - udostępnia użytkownikom możliwość korzystania z usług sieciowych (HTTPS, IMAP, POP3, DNS, SSH)  
- (3) Transportowa - której głównym zadaniem jest sprawna obsługa komunikacji pomiędzy urządzeniami,  
- (2) Sieciowa - której głównym zadaniem jest znalezienie najkrótszej i najszybszej drogi do urządzenia docelowego przez sieć rozległą,  
- (1 ) Dostępu do sieci - kodowanie danych na jezyk maszynowy, przekazywanie do medium transmisyjnego, adresacja (MAC).  

Jakbyśmy mieli porównać modele, **OSI rozdziela warstwę aplikacyjną modelu TCP/IP na trzy (aplikacyjną, sesji i prezentacji)**. Tak samo jak rozdziela dostępu do sieci na dwa - na fizyczną i łącza danych.  
#### What is ARP? 
Czym jest ARP (Address Resolution Protocol)?  

ARP to protokół (łącza danych - data link layer) który powiązuje adresy MAC i IP w jedną całość. Mamy tak zwane ARP cache, jakby “notes wewnętrzny” w którym urządzenie zapisuje które IP odpowiada danemu adresowi MAC. Zwykle działa na zasadzie ARP request (zapytanie) i ARP Reply (odpowiedź).  
W skrócie: urządzenie, żeby wysłać dane do danego IP musi znać adres MAC. Sprawdza swoją tablicę ARP, jeżeli nic tam nie znajduje, wysyła ARP request w broadcascie (do wszystkich urządzeń w sieci lokalnej). Każde urzadzenie otrzymuje zapytanie, ale tylko te właściwe odpowiada ARP Reply. Ta informacja trafia do ARP cache.  
  

#### What is APIPA address and what it can suggest?

#### What is DHCP?  
Czym jest DHCP ?  
Dynamic Host Configuration Protocol, jest to protokół warstwy aplikacji, odpowiedzialny za dynamiczne przydzielanie adresów IP do hosta. Wyobraźmy sobie, że musimy za każdym razem przydzielać adresy IP naszym kartom sieciowym. DHCP przydziela też maski podsieci, bramę domyślną, serwer DNS itp.  

Reguła DORA - czyli jak działa DHCP - Discover, Offer, Request, Ack, czyli klient najpierw pyta o serwer DHCP w sieci, potem serwer proponuje adresację, potem klient prosi o przydzielenie tej adresacji, i na koniec dostaje zatwierdzenie od serwera. DHCP przydziela adres na określony czas i host go odnawia  

W SOC możemy się spotkać z Rogue DHCP (fałszywy serwer może przekierować ruch przez złośliwą bramę).  


#### Co to jest segmentacja sieci i jaki ma wpływ na bezpieczeństwo?
Segmentacja sieci jest nic innego dzieleniem infrastruktury na strefy o różnym poziomie zaufania (strefa DMZ, VLANy itd),  w celu większej kontroli nad nią (poprzez ACL, mikrosegmentację, firewall).  
Ma duży wpływ na bezpieczeństwo, np. ogranicza ruch boczny (nawet jak atak na hosta sie uda, nie będzie tak łatwo się dostać do kolejnego), zmniejsza “pole rażenia” przy ataku, czyli z danej podsieci już nie będzie tak łatwo się dostać dalej, no i też możemy łatwiej kontrolować co się dzieje stawiając punkty kontrolne, jest tak łatwiej logować i przez to analizować co się dzieje podczas ataków.  
  

#### Przykład ataku lub problemu, który sklasyfikujesz jako atak na warstwę L3 powiedz po czym to poznasz w logach/pcap.

#### Przykład ataku lub problemu, który sklasyfikujesz jako atak na warstwę L4 powiedz po czym to poznasz w logach/pcap.

#### Przykład ataku lub problemu, który sklasyfikujesz jako atak na warstwę L6 powiedz po czym to poznasz w logach/pcap.

####  Przykład ataku lub problemu, który sklasyfikujesz jako atak na warstwę L7 i powiedz po czym to poznasz w logach/pcap.
  
#### Przykład ataku lub problemu, który sklasyfikujesz jako atak na warstwę L2 powiedz po czym to poznasz w logach/pcap.

#### How would you describe HTTPS protocol? - 
Jakbyś opisał protokół HTTPS?  
Jest to bezpieczniejszy przykład HTTP, który pozwala przeglądarce połączyć się ze stroną. Różnica z HTTP jest taka że ma dodatkową warstwę szyfrowania - dzięki czemu dane jak hasła czy numery kart nie są widoczne dla osób po drodze. HTTPS najpierw tworzy szyfrowane połączenie, a dopiero potem wysyła dane.  
Przykład: logujemy się do banku. Przy HTTP może podejrzeć dane na tej samej sieci, przy HTTPS są te dane szyfrowane.  

#### Where does the address 127.0.0.1 lead to? - 
Gdzie prowadzi adres 127.0.0.1?  
Jest to adres używany do komunikacji komputera z samym sobą (lokalny). Można go użyć do np. połączenia z programem uruchomionym na tym samym komputerze na konkretnym porcie. 

  
#### Explain why exposing port 3389 to the internet is a fireable offense.
Wyjaśnij, dlaczego udostępnianie portu 3389 w internecie jest podstawą do zwolnienia.
#### What is NAT and why is it used?
Czym jest NAT i dlaczego się go stosuje?

#### What is the difference between public IP and private IP address?
Jaka jest różnica między adresem publicznym a prywatnym IP?

#### What is a subnet mask and what is its purpose?
Czym jest maska podsieci i do czego służy?

#### What is VLAN and how does it improve security?
Czym jest VLAN i w jaki sposób poprawia bezpieczeństwo?

#### What is DNS tunneling and why is it dangerous?
Czym jest DNS tunneling i dlaczego jest niebezpieczny?

#### What is a proxy server and how can it be used in corporate environments?
Czym jest serwer proxy i jak może być wykorzystywany w środowisku firmowym?

#### What is packet fragmentation and how can it be abused by attackers?
Czym jest fragmentacja pakietów i jak może być wykorzystywana przez atakujących?

#### What indicators in logs or PCAP could suggest a port scan?
Jakie wskaźniki w logach lub PCAP mogą sugerować skanowanie portów?

#### What indicators in logs or PCAP could suggest a SYN flood attack?
Jakie wskaźniki w logach lub PCAP mogą sugerować atak SYN flood?

#### What is ICMP and how can it be used legitimately and maliciously?
Czym jest ICMP i jak może być wykorzystywany legalnie oraz złośliwie?

#### What is the difference between a stateful firewall and a stateless firewall?
Jaka jest różnica między firewallem stanowym (stateful) a bezstanowym (stateless)?

#### How would you identify suspicious outbound traffic in logs or PCAP?
Jak rozpoznałbyś podejrzany ruch wychodzący w logach lub PCAP?

#### You see a host making repeated DNS queries for long, random-looking subdomains under the same domain. What could this indicate and what would you check first?
Widzisz hosta wysyłającego powtarzalne zapytania DNS o długie, losowo wyglądające subdomeny w obrębie tej samej domeny. Co to może oznaczać i co sprawdzisz najpierw?

#### A workstation initiates connections to hundreds of different external IPs on port 443, but the traffic volume is very small. What could this suggest?
Stacja robocza inicjuje połączenia do setek różnych zewnętrznych adresów IP na porcie 443, ale wolumen ruchu jest bardzo mały. Co może to sugerować?

#### In a PCAP, you notice many TCP SYN packets sent to multiple ports on one host, with very few completed handshakes. How would you classify this activity?
W PCAP zauważasz wiele pakietów TCP SYN wysyłanych do wielu portów na jednym hoście, przy bardzo małej liczbie ukończonych handshake’y. Jak sklasyfikujesz taką aktywność?

#### A server suddenly starts responding with a large number of ICMP Destination Unreachable messages. What could be happening?
Serwer nagle zaczyna odpowiadać dużą liczbą komunikatów ICMP Destination Unreachable. Co może się dziać?

#### How would you distinguish in logs between a brute-force attack against a VPN portal and a normal user repeatedly failing to log in?
Jak odróżnisz w logach atak brute-force na portal VPN od zwykłego użytkownika, który wielokrotnie błędnie wpisuje hasło?

#### You see ARP replies in the network even though no ARP requests for those addresses were observed. What attack or issue could this indicate?
W sieci widzisz odpowiedzi ARP, mimo że wcześniej nie było zapytań ARP dla tych adresów. Jaki atak lub problem może to wskazywać?

#### A device receives an APIPA address (169.254.x.x). From an incident response perspective, what are the most likely causes and what should be verified?
Urządzenie otrzymuje adres APIPA (169.254.x.x). Z perspektywy incident response jakie są najbardziej prawdopodobne przyczyny i co należy zweryfikować?

#### What signs in network logs or PCAP might indicate lateral movement over SMB or RDP?
Jakie oznaki w logach sieciowych lub PCAP mogą wskazywać na ruch lateralny z użyciem SMB lub RDP?

#### You notice one internal host generating authentication traffic to many different servers in a short time. What could this mean in a SOC context?
Zauważasz, że jeden host wewnętrzny generuje ruch uwierzytelniający do wielu różnych serwerów w krótkim czasie. Co to może oznaczać w kontekście SOC?

#### How would you recognize beaconing traffic in proxy, firewall, or NetFlow logs?
Jak rozpoznałbyś beaconing w logach proxy, firewalla albo NetFlow?

#### A web server receives many HTTP requests with unusual User-Agents, odd URL encoding, and requests to non-existing paths. What might this indicate?
Serwer WWW otrzymuje wiele żądań HTTP z nietypowymi User-Agentami, dziwnym kodowaniem URL i zapytaniami do nieistniejących ścieżek. Co to może oznaczać?

#### What would make you suspect TLS inspection bypass or suspicious encrypted traffic, even if you cannot decrypt the payload?
Co sprawiłoby, że podejrzewałbyś obejście inspekcji TLS albo podejrzany ruch szyfrowany, nawet jeśli nie możesz odszyfrować payloadu?

#### In firewall logs, one internal IP is denied on many destination ports across many external hosts within a few minutes. Is this more likely scanning or misconfiguration? How would you decide?
W logach firewalla jeden wewnętrzny adres IP dostaje blokady na wiele portów docelowych wobec wielu zewnętrznych hostów w ciągu kilku minut. Czy bardziej wygląda to na skanowanie czy błędną konfigurację? Jak to rozstrzygniesz?

#### What network artifacts could suggest data exfiltration over DNS, HTTPS, or cloud storage services?
Jakie artefakty sieciowe mogą sugerować wyciek danych przez DNS, HTTPS albo usługi chmurowe?

#### During analysis of a PCAP, you see retransmissions, out-of-order packets, and session resets. How do you decide whether this is an attack, network instability, or an application problem?
Podczas analizy PCAP widzisz retransmisje, pakiety out-of-order i resety sesji. Jak decydujesz, czy to atak, niestabilność sieci czy problem aplikacyjny?