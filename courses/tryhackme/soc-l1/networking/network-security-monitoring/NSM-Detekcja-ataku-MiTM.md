# Przegląd

**MITM (Man-in-the-Middle)** to cyberatak, w którym atakujący potajemnie przechwytuje, a potencjalnie także modyfikuje komunikację między dwiema stronami, na przykład między użytkownikiem a usługą, bez ich wiedzy. Atakujący może podsłuchiwać komunikację, aby kraść wrażliwe dane, takie jak **poświadczenia** czy **dane kart płatniczych**, albo wstrzykiwać złośliwą zawartość. Tego typu ataki mogą dotyczyć każdej organizacji i każdej osoby, szczególnie tam, gdzie **szyfrowanie** lub **uwierzytelnianie** są słabe.
### Jak działają ataki MITM

Ataki MITM zazwyczaj obejmują dwa główne etapy:

**Interception (przechwycenie)**  
Atakujący wstawia się w strumień komunikacji, często wykorzystując słabości protokołów sieciowych albo techniki takie jak **ARP spoofing**, **DNS spoofing** lub **IP spoofing**.

**Manipulation / Decryption (manipulacja / odszyfrowanie)**  
Atakujący próbuje uzyskać dostęp do komunikacji albo ją zmodyfikować, odszyfrowując zakodowane dane lub wstrzykując złośliwą zawartość, np. zmienione odpowiedzi stron WWW albo fałszywe formularze logowania.
### Najczęstsze typy ataków MITM

- **Packet sniffing**  
Przechwytywanie niezaszyfrowanych pakietów danych przesyłanych przez sieć, często w otwartych sieciach Wi-Fi.

- **Session hijacking**  
Kradzież i wykorzystanie tokenów sesyjnych w celu podszycia się pod użytkownika.

- **SSL stripping**  
Obniżenie poziomu połączenia z **HTTPS** do niezabezpieczonego **HTTP**, aby przechwycić albo zmodyfikować przesyłane dane.

- **DNS spoofing**  
Przekierowanie legalnego ruchu do fałszywych domen przez manipulowanie odpowiedziami DNS.

- **IP spoofing**  
Tworzenie złośliwych pakietów IP, które wyglądają tak, jakby pochodziły od zaufanych systemów.

- **Rogue Wi-Fi access point**  
Tworzenie fałszywych sieci Wi-Fi w celu przechwytywania ruchu użytkowników.
### Przykłady z rzeczywistego świata

W 2017 roku **Equifax** doświadczył poważnego naruszenia danych w wyniku ataku MITM, co doprowadziło do ujawnienia wrażliwych danych ponad **100 milionów użytkowników**.

Wśród głośnych ataków znajdowały się również przypadki:

- wstrzykiwania kodu przez dostawców usług internetowych (**ISP**)
- przechwytywania ruchu wyszukiwania przez aktorów państwowych z użyciem **SSL spoofing**

---
## MITM a Cyber Kill Chain

Aby skutecznie analizować zdarzenia bezpieczeństwa i na nie reagować, analityk musi umieścić alerty w szerszym modelu działań przeciwnika. Pojedyncze wskaźniki nabierają znaczenia dopiero wtedy, gdy zostaną powiązane z **TTPs (Tactics, Techniques, and Procedures)** atakującego. Jednym z powszechnie stosowanych modeli jest **Cyber Kill Chain**, czyli framework opisujący typowe etapy zaawansowanego włamania.

Framework ten składa się z siedmiu odrębnych faz:

- **Reconnaissance**  
Przeciwnik zbiera informacje o celu, aby zidentyfikować podatności.

- **Weaponization**  
Przeciwnik łączy exploit ze złośliwym payloadem, tworząc pakiet gotowy do dostarczenia.

- **Delivery**  
Przeciwnik dostarcza przygotowany pakiet do środowiska ofiary.

- **Exploitation**  
Kod przeciwnika zostaje uruchomiony i wykorzystuje podatność programową, sprzętową albo ludzką, aby uzyskać początkowy dostęp.

- **Installation**  
Przeciwnik instaluje malware albo ustanawia trwały backdoor na przejętym zasobie.

- **Command & Control (C2)**  
Przeciwnik ustanawia ukryty kanał komunikacji do sterowania przejętym systemem.

- **Actions on Objectives**  
Przeciwnik realizuje swoje końcowe cele, np. eksfiltrację danych, zniszczenie systemów albo ruch boczny.
### Umiejscowienie MITM w Cyber Kill Chain

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/46-image.png)

**Man-in-the-Middle** to elastyczna technika, którą przeciwnicy wykorzystują głównie w fazach **Exploitation** oraz **Installation**.

**Jako technika eksploatacji**  
Atak MITM wykorzystuje zaufanie i ograniczenia projektowe podstawowych protokołów sieciowych, takich jak **ARP** i **DNS**. Poprzez manipulowanie tymi protokołami atakujący może przechwycić kanał komunikacyjny. Samo przejęcie sesji jest formą eksploatacji, ponieważ narusza integralność sieci i daje przeciwnikowi pierwszy przyczółek do podsłuchu albo aktywnej manipulacji.

**Jako wektor instalacji**  
Gdy atakujący skutecznie zajmie pozycję MITM, przejmuje kontrolę nad strumieniem danych i może używać go jako mechanizmu dostarczania złośliwego payloadu. Przykładowo może wstrzyknąć exploit przeglądarkowy, dropper malware albo **RAT (Remote Access Trojan)** do legalnych, niezaszyfrowanych pobrań. To odpowiada fazie **Installation**, w której przeciwnik ustanawia trwałość lub wdraża dodatkowe narzędzia na systemie ofiary.

Wykrycie ataku MITM jest bardzo istotnym ustaleniem. Oznacza, że przeciwnik aktywnie działa w środkowych fazach włamania, a to daje zespołowi **SOC** ważną szansę na przerwanie łańcucha ataku, zanim osiągnięte zostaną końcowe cele.

# ARP Spoofing i MITM

Przed analizą ataków **ARP spoofing** warto najpierw zrozumieć, czym jest protokół **ARP**, do czego służy oraz w jaki sposób atakujący nadużywają go do przeprowadzenia ataku **Man-in-the-Middle (MITM)**.

### Czym jest protokół ARP - powtórka

**ARP (Address Resolution Protocol)** mapuje adresy **IP** na adresy **MAC** w sieci lokalnej. Gdy urządzenie chce wysłać dane do innego adresu IP, najpierw pyta: **„Kto ma ten adres IP?”**. Właściwe urządzenie odpowiada swoim adresem MAC.
### ARP Spoofing

W ataku **ARP spoofing** napastnik wysyła fałszywe odpowiedzi ARP, aby skłonić urządzenia do powiązania **adresu MAC atakującego** z legalnym adresem IP, najczęściej z **bramą domyślną**. Dzięki temu może **przechwytywać**, **modyfikować** albo **przekierowywać** ruch.
### Dlaczego ARP spoofing działa

ARP **nie posiada mechanizmu uwierzytelniania**. Każde urządzenie może wysłać niezamówiony komunikat typu **is-at**. Atakujący wykorzystuje tę słabość, wysyłając fałszywe odpowiedzi ARP do ofiary i do bramy. Przykładowo:

`192.16.10.100 is at 02:fe:BB:cd:55:55`

czyli atakujący twierdzi, że jest bramą. W efekcie:

- pamięć podręczna ARP ofiary zostaje zatruta
- cały ruch przeznaczony do bramy przechodzi najpierw przez atakującego (**MITM**)
### Wskaźniki ataku

Podczas analizy logów lub ruchu sieciowego pod kątem możliwego ataku **MITM z użyciem ARP spoofing** należy zwracać uwagę na:

- **duplikaty mapowań MAC do IP** – wiele adresów MAC twierdzi, że obsługuje ten sam adres IP
- **niezamówione odpowiedzi ARP** – duża liczba odpowiedzi ARP bez pasujących zapytań, czyli **gratuitous ARP**
- **nietypowo duży wolumen ruchu ARP** – wiele pakietów ARP w krótkim czasie
- **nietypowe trasowanie ruchu** – ruch przekierowany przez adres MAC atakującego
- **wzorce przekierowania bramy** – wiele adresów MAC dla tego samego IP bramy
- **pętle ARP probe / reply** – liczne zapytania w stylu: `Who has 192.168.1.x? Tell 192.168.1.y`
### Informacje o sieci (na podstawie plików z TryHackMe)

|Role|IP|MAC|Notes|
|---|---|---|---|
|**Gateway**|`192.168.10.1`|`-`|legalny router|
|**Attacker**|`-`|`-`|`-`|
|**Victim**|`-`|`-`|`-`|
|**Domain**|`corp-login.acme-corp.local`|`-`|`-`|

---
### Analiza ruchu sieciowego

Należy otworzyć plik **`network-traffic.pcap`** znajdujący się w folderze **`mitm_traffic`** na pulpicie i wykonać poniższe kroki.

### Zawężenie do ruchu ARP

Ponieważ interesuje nas protokół **ARP**, należy najpierw odfiltrować go przy użyciu poniższego filtra. Pozwoli to przeanalizować zapytania i odpowiedzi oraz zauważyć nietypowy wolumen lub wzorce.

|Notes|Wireshark Filter|
|---|---|
|**Cały ruch ARP** – pokazuje wszystkie pakiety ARP, zarówno `who-has`, jak i `is-at`.|`arp`|
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/47-image.png)

Po zastosowaniu filtra widać zarówno **zapytania**, jak i **odpowiedzi** ARP. Należy sprawdzić, czy nie występują **nietypowe** lub **powtarzające się** żądania i odpowiedzi.  
**Ważna uwaga:** naciśnij **CTRL + ALT + 1**, aby poprawić sposób wyświetlania czasu.
### Zapytania ARP

| Notes                                                                                    | Wireshark Filter  |
| ---------------------------------------------------------------------------------------- | ----------------- |
| **Tylko zapytania ARP** – pokazują wszystkie żądania ARP przechwycone od różnych hostów. | `arp.opcode == 1` |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/48-image.png)
### Odpowiedzi ARP

Fałszywe zatruwanie ARP zwykle wykorzystuje **niezamówione odpowiedzi `is-at`**. To bardzo silny wskaźnik podejrzanej aktywności.

| Notes                                                                                | Wireshark Filter  |
| ------------------------------------------------------------------------------------ | ----------------- |
| **Tylko odpowiedzi ARP** – pozwalają wykryć liczne odpowiedzi, w tym gratuitous ARP. | `arp.opcode == 2` |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/49-image.png)

Prawidłowe odpowiedzi zwykle odpowiadają na wcześniejsze zapytania **who-has**. Podejrzana aktywność pojawia się wtedy, gdy widać dużo odpowiedzi bez widocznych zapytań albo wielokrotne ogłaszanie tego samego adresu IP przez podejrzany adres MAC.
### Gratuitous ARP

Podejrzany host może wysyłać wiele **niezamówionych odpowiedzi ARP**, zwłaszcza do wielu odbiorców. Powtarzające się gratuitous ARP mogą oznaczać, że atakujący utrzymuje stan zatrucia ARP.

|Notes|Wireshark Filter|
|---|---|
|**Pakiety gratuitous ARP** – pomagają wychwycić niezamówione odpowiedzi ARP.|`arp.isgratuitous`|
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/50-image.png)
### Ruch ARP związany z bramą

W analizowanym przypadku znamy adres IP i MAC powiązany z bramą. Dlatego można zawęzić analizę do ruchu ARP związanego właśnie z tym hostem.

| Notes                                                                                            | Wireshark Filter                                                            |
| ------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------- |
| **Ruch ARP powiązany z legalną bramą** – pokazuje ruch z IP bramy i jej prawidłowego adresu MAC. | `arp && arp.src.proto_ipv4 == 192.168.10.1 && eth.src == 02:aa:bb:cc:00:01` |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/51-image.png)

W wynikach widać tylko odpowiedzi ARP. Następnie należy zawęzić analizę do samego adresu IP bramy, aby sprawdzić, jakie adresy MAC są z nim kojarzone.
### Zawężenie do IP bramy

|Notes|Wireshark Filter|
|---|---|
|**Odpowiedzi ARP dla IP bramy** – pokazują wszystkie odpowiedzi ARP twierdzące, że pochodzą od adresu IP bramy.|`arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1`|
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/52-image.png)

Wynik wygląda podejrzanie. Widać odpowiedzi ARP przypisujące IP bramy do **podejrzanego adresu MAC**. Częstotliwość tych odpowiedzi wskazuje, że jest to rzeczywiście **ARP spoofing**.

### Potwierdzenie spoofingu ARP

|Notes|Wireshark Filter|
|---|---|
|**Potwierdzenie odpowiedzi „192.168.10.1 is at”** – filtruje odpowiedzi ARP wskazujące, jaki MAC jest reklamowany dla IP bramy.|`arp.opcode ==2 && _ws.col.info contains "192.168.10.1 is at"`|
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/53-image.png)

Ten filtr składa się z dwóch części:

- pierwsza część wybiera **odpowiedzi ARP**
- druga część filtruje zawartość kolumny **Info**, aby pokazać wpisy reklamujące IP bramy

Po dokładnym sprawdzeniu widać, że atakujący wykorzystuje ARP spoofing, aby przypisać **IP bramy do własnego adresu MAC**. Ten sam efekt daje także filtr:

`arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1`

### Analiza podejrzanego adresu MAC

Po wykryciu ARP spoofingu można zawęzić analizę do adresu MAC atakującego, który powiązał się z IP bramy.

|Notes|Wireshark Filter|
|---|---|
|**Odpowiedzi ARP od podejrzanego MAC podszywającego się pod bramę**|`arp.opcode == 2 && arp.src.proto_ipv4 == 192.168.10.1 && eth.src == 02:fe[REDACTED]`|
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/54-image.png)

Wynik jednoznacznie potwierdza, że atakujący **podszywa się pod bramę** przy użyciu ARP spoofing.

### Sprawdzenie duplikatów mapowań IP-MAC

Na końcu można jeszcze potwierdzić atak, filtrując duplikaty mapowań MAC do jednego adresu IP.

| Notes                                                                                                                             | Wireshark Filter                |
| --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| **Wykrywanie duplikatów mapowań IP-MAC** – pomaga potwierdzić, że więcej niż jeden adres MAC rości sobie prawo do tego samego IP. | `arp.duplicate-address-detected |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/55-image.png)

To potwierdza, że atakujący skutecznie przeprowadził **ARP spoofing** i ustawił się pomiędzy ofiarą a bramą. Kolejnym krokiem jest analiza, w jaki sposób mógł następnie wykonać **DNS spoofing**, aby doprowadzić do przekierowania ruchu.

## Zadania

**Ile pakietów ARP pochodzących z adresu MAC bramy zaobserwowano?**

  `arp && arp.src.proto_ipv4 == 192.168.10.1 && eth.src == 02:aa:bb:cc:00:01` - pokazuje ruch z IP bramy i jej prawidłowego adresu MAC.

**Odp. 10**

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/56-image.png)

**Jaki adres MAC został użyty przez atakującego do podszycia się pod bramę?**

Odp. 02:fe:fe:fe:55:55. Używamy filtra - arp.opcode arp.opcode = =2 && _ws.col.info contains "192.168.10.1 is at"

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/57-image.png)


**Ile odpowiedzi Gratuitous ARP zaobserwowano dla `192.168.10.1`?**

**Odp. 2 - tylko te odpowiedzi z "Grauitous ARP for..."**

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/58-image.png)

**Ile unikalnych adresów MAC zgłaszało ten sam adres IP (`192.168.10.1`)?**

Odp. 2 - jak wyżej

**Ile łącznie pakietów ARP spoofing zaobserwowano od atakującego?**

Odp. 14 - sprawdzamy to szukając duplikatów mapowań IP-MAC.

`arp.duplicate-address-detected || arp.duplicate-address-frame`

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/60-image.png)
# Odkrywając DNS Spoofing

Najpierw warto zrozumieć, czym jest **DNS**. Można o nim myśleć jak o **liście kontaktów w telefonie**. Nie pamiętasz numerów swoich znajomych — po prostu klikasz ich imię. Podobnie DNS tłumaczy **przyjazne dla człowieka nazwy stron internetowych** (np. `www.google.com`) na **adresy IP**, które rozumie komputer.
## Czym jest DNS Spoofing

**DNS spoofing** (nazywany też **DNS cache poisoning**) polega na tym, że atakujący **psuje ten mechanizm** i podaje komputerowi **zły „numer telefonu”** dla strony, którą ofiara próbuje odwiedzić.
To bardzo skuteczna technika do przeprowadzenia ataku **Man-in-the-Middle (MITM)**.
### Jak to działa

1. Ofiara próbuje wejść na stronę banku, np. `my-real-bank.com`.
2. Atakujący, który znajduje się już w sieci lokalnej (np. dzięki **ARP spoofingowi**), przechwytuje zapytanie DNS ofiary.
3. Następuje **spoofing** — atakujący szybko wysyła fałszywą odpowiedź DNS, która mówi:  
   `my-real-bank.com` znajduje się pod moim adresem IP: `ATTACKER_IP`.
4. Komputer ofiary ufa tej odpowiedzi i zapisuje ją w **cache DNS**.
5. Gdy ofiara próbuje połączyć się z bankiem, w rzeczywistości łączy się z serwerem atakującego, który może hostować **idealną kopię prawdziwej strony bankowej**.
6. Atakujący znajduje się teraz „pośrodku” i może przechwytywać wszystko, co wpisuje ofiara, w tym **login** i **hasło**.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/61-image.png)
### Wskaźniki ataku

Podczas analizy logów albo ruchu sieciowego pod kątem możliwego ataku **MITM z użyciem DNS spoofing** należy zwracać uwagę na:

- **wiele odpowiedzi DNS dla tego samego zapytania**  
  Legalny resolver i sfałszowany host odpowiadają na to samo zapytanie. To **najbardziej wiarygodny wskaźnik**.
- **odpowiedź DNS z nieoczekiwanego źródła**  
  Odpowiedź DNS przychodzi z adresu IP, który nie odpowiada żadnemu skonfigurowanemu resolverowi, np. nie jest to `8.8.8.8` ani wewnętrzny serwer DNS.
- **podejrzanie niski TTL (Time-To-Live)**  
  Atakujący mogą używać bardzo niskich wartości TTL (**1–30 s**), aby zatrute wpisy były krótkotrwałe i łatwe do ponownego nadpisania.
- **niezamówione odpowiedzi DNS**  
  Odpowiedź DNS pojawia się bez odpowiadającego jej zapytania DNS od ofiary.
## Analiza ruchu sieciowego

#### Zawężenie do ruchu DNS

Ponieważ interesuje nas protokół **DNS**, należy najpierw odfiltrować cały ruch DNS.

| Notes                                                                                                               | Wireshark Filter |
| ------------------------------------------------------------------------------------------------------------------- | ---------------- |
| **Cały ruch DNS** – pokazuje wszystkie zapytania i odpowiedzi DNS, co pozwala zauważyć nietypowe wzorce i anomalie. | `dns`            |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/62-image.png)
W wynikach będą widoczne zarówno **zapytania DNS**, jak i odpowiadające im **odpowiedzi DNS**.

#### Filtrowanie legalnego ruchu

Legalne serwery DNS, np. **Google DNS `8.8.8.8`**, odpowiadają z dobrze znanego zewnętrznego adresu IP. Filtrując odpowiedzi z tego adresu, można zobaczyć, jak wygląda **normalny ruch DNS** do porównania.

| Notes                                                                                               | Wireshark Filter                               |
| --------------------------------------------------------------------------------------------------- | ---------------------------------------------- |
| **Odpowiedzi z legalnego serwera DNS** – pokazują prawidłowe odpowiedzi DNS pochodzące z `8.8.8.8`. | `dns.flags.response == 1 && ip.src == 8.8.8.8` |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/63-image.png)
Wynik pokazuje poprawne odpowiedzi DNS z prawidłowego serwera.

#### Analiza wszystkich odpowiedzi DNS

Następnie warto przeanalizować wszystkie odpowiedzi DNS.

|Notes|Wireshark Filter|
|---|---|
|**Wszystkie odpowiedzi DNS** – pozwalają wyszukać odpowiedzi pochodzące z nietypowych adresów IP.|`dns.flags.response==1`|
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/64-image.png)

W wynikach należy szukać odpowiedzi pochodzących z adresów innych niż typowy serwer DNS. Po dokładnym sprawdzeniu można zauważyć **jedną odpowiedź DNS pochodzącą z IP innego niż `8.8.8.8`**. To bardzo interesujący ślad i potencjalny dowód **DNS spoofingu**.

#### Odpowiedzi od serwera DNS

Dla porównania można jeszcze raz zawęzić widok tylko do odpowiedzi od prawidłowego serwera DNS.

| Notes                                                                            | Wireshark Filter                               |
| -------------------------------------------------------------------------------- | ---------------------------------------------- |
| **Odpowiedzi z serwera DNS** – pokazują tylko odpowiedzi pochodzące z `8.8.8.8`. | `dns.flags.response == 1 && ip.src == 8.8.8.8` |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/65-image.png)
#### Ruch DNS dla interesującej nas domeny

Teraz należy przeanalizować ruch DNS związany z interesującą domeną:

`corp-login.acme-corp.local`

|Notes|Wireshark Filter|
|---|---|
|**Cały ruch DNS dla wskazanej domeny** – pokazuje wszystkie zapytania i odpowiedzi związane z `corp-login.acme-corp.local`.|`dns && dns.qry.name == "corp-login.acme-corp.local"`|
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/66-image.png)
#### Odpowiedzi dla domeny pochodzące od prawidłowego DNS

Następnie warto sprawdzić odpowiedzi DNS dla tej domeny, ale tylko te pochodzące od prawidłowego serwera `8.8.8.8`.

| Notes                                                                                                                              | Wireshark Filter                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Prawidłowe odpowiedzi DNS dla domeny** – pokazują odpowiedzi dla `corp-login.acme-corp.local` pochodzące od legalnego resolvera. | `dns.flags.response == 1 && ip.src == 8.8.8.8 && dns.qry.name == "corp-login.acme-corp.local"` |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/67-image.png)

Wynik wygląda normalnie, zgodnie z oczekiwaniami.

#### Odpowiedzi dla domeny pochodzące z innych źródeł niż DNS server

Najważniejszy krok to sprawdzenie, czy odpowiedzi dla tej samej domeny pochodzą także z innych adresów niż prawidłowy serwer DNS.

| Notes                                                                                                                            | Wireshark Filter                                                                               |
| -------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Podejrzane odpowiedzi DNS dla domeny** – pokazują odpowiedzi dla `corp-login.acme-corp.local`, które nie pochodzą z `8.8.8.8`. | `dns.flags.response == 1 && ip.src != 8.8.8.8 && dns.qry.name == "corp-login.acme-corp.local"` |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/68-image.png)
To właśnie tak wygląda **DNS spoofing**. Wynik pokazuje, że **jeden z systemów wewnątrz sieci działa jak fałszywy serwer DNS** i wysyła spreparowane odpowiedzi DNS.

Reasumując - analiza z dwóch poprzednich zadań pokazuje:

- doszło do **udanego, wieloetapowego ataku MITM**
- atakujący najpierw zatruł mapowanie **ARP** dla bramy `192.168.10.1`
- następnie wysłał **sfałszowane odpowiedzi DNS** dla `corp-login.acme-corp.local`
- w efekcie ofiara została przekierowana na **adres IP atakującego**

Kolejnym krokiem jest zrozumienie, **dlaczego stosuje się SSL stripping** oraz znalezienie dowodów na to, że właśnie ta technika doprowadziła do kradzieży danych ofiary.

### Zadania

**Ile odpowiedzi DNS zostało odkrytch w domenie corp-login.acme-corp.local?**

- Musimy odfiltrować wyniki według nazwy zapytania i ustawić flagę odpowiedzi na 1. 
  `dns.flags.response == 1 && dns.qry.name == "corp-login.acme-corp.local"`

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/69-image.png)

**Odp. 211**

**Ile odpowiedzi DNS zostało odkrytch z innych adresów IP niż 8.8.8.8?**

**dns.flags.response == 1 && ip.src != 8.8.8.8 && dns.qry.name == "corp-login.acme-corp.local**

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/70-image.png)

**Odp. 2**

**Jaki adres IP zwróciła sfałszowana odpowiedź DNS atakującego dla tej domeny?**

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/71-image.png)
**Odp. 192.168.10.55b**

# Wyłapywanie SSL Stripping w logach

**SSL stripping** to technika **Man-in-the-Middle**, w której atakujący przechwytuje i modyfikuje ruch tak, aby usunąć albo uniemożliwić użycie szyfrowania **TLS** pomiędzy klientem a serwerem. W efekcie klient komunikuje się przez **HTTP** zamiast **HTTPS**. Atakujący utrzymuje bezpieczną sesję **HTTPS** z prawdziwym serwerem, a jednocześnie przekazuje ofierze zwykły **HTTP**, co pozwala mu podsłuchiwać ruch i przechwytywać poświadczenia.

---
## Jak to działa

1. Ofiara inicjuje połączenie **HTTPS** ze stroną internetową.
2. Atakujący przechwytuje to żądanie, np. przy użyciu **ARP spoofingu** albo fałszywego punktu dostępowego.
3. Atakujący łączy się z prawdziwą stroną przez **HTTPS**, ale odpowiedź przekazuje ofierze już przez **HTTP**.
4. Ofiara nieświadomie korzysta z **HTTP**, przez co wrażliwe dane są przesyłane **jawnym tekstem**.

---
## Wskaźniki SSL stripping

Podczas analizy należy zwracać uwagę na następujące oznaki:

**Początkowe żądanie vs. dalsza komunikacja**  
Użytkownik może początkowo próbować połączyć się przez **HTTPS** na porcie **443**, ale kolejne pakiety nagle przechodzą na **nieszyfrowany HTTP** na porcie **80** dla tej samej domeny.

**Redirecty / przepisywanie linków**  
Należy monitorować przekierowania (**HTTP status code 301, 302**), które uporczywie kierują żądanie HTTPS do zasobu HTTP.

**Błędy certyfikatów**  
Atakujący zwykle stara się to ukryć, ale czasami początkowy **TLS/SSL Handshake** może się nie powieść albo może pojawić się **self-signed certificate**, jeśli używa bardziej bezpośredniego proxy.

---
## Analiza ruchu sieciowego
#### Zawężenie do ruchu SSL/TLS

Ponieważ interesuje nas **HTTPS**, zaczynamy od wyizolowania ruchu SSL/TLS:

`tls || ssl`

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/72-image.png)

Ten filtr pokazuje cały ruch związany z **SSL/TLS**.
#### Analiza ruchu SSL naszego serwera

Następnie należy zastosować filtr pokazujący ustanowione handshaki TLS do naszego serwera. To potwierdza, że strona normalnie używa **TLS** do komunikacji.

`tls.handshake.type == 1 && tls.handshake.extensions_server_name == "corp-login.acme-corp.local"`

Jedną z najważniejszych obserwacji jest tutaj potwierdzenie, że analizowana domena rzeczywiście korzysta z **TLS**.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/73-image.png)

#### Pokazanie przekierowania DNS poprzedzającego stripping

Hipoteza jest taka, że **SSL stripping** został wykonany dopiero po skutecznym **DNS spoofingu**, który skierował ofiarę na adres IP atakującego. W poprzednim zadaniu został już zidentyfikowany adres IP atakującego odpowiedzialnego za DNS spoofing. Teraz należy wyizolować odpowiedzi DNS pochodzące od atakującego, aby pokazać, że ofiara została skierowana właśnie na jego adres.

`dns.flags.response == 1 && ip.src == 192.168.10.55 && dns.qry.name == "corp-login.acme-corp.local"`

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/74-image.png)

Wynik pokazuje dwa przypadki, w których adres IP atakującego wysłał sfałszowane odpowiedzi DNS dla interesującej nas domeny.
#### Potwierdzenie, że TLS znika

Jednym z głównych wskaźników **SSL stripping** jest to, że po spoofingu domena przestaje wykonywać handshaki TLS do prawdziwego serwera. To potwierdza brak ruchu TLS od ofiary do legalnego serwera. Należy więc sprawdzić ruch HTTP pomiędzy ofiarą a atakującym:

`http && ip.src == 192.168.10.10 && ip.dst == 192.168.10.55`

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/75-image.png)

Widać wyraźnie, że ofiara połączyła się z serwerem po wykonaniu SSL stripping i **zalogowała się**.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/76-image.png)

W ruchu można również odnaleźć **poświadczenia użytkownika przesyłane jawnym tekstem**, co potwierdza, że atakujący zdołał przechwycić dane logowania ofiary.

W tym scenariuszu można by szukać także innych oznak SSL stripping, ale tutaj zaobserwowano przede wszystkim jeden kluczowy wskaźnik:  
**ruch HTTPS do portalu został sprowadzony do HTTP**.
#### Podsumowanie analizy

Poniżej znajduje się podsumowanie incydentu wraz z osią czasu ataku:

**ARP Spoofing (cache poisoning)**  
Atakujący rozpoczął zatruwanie ARP, wysyłając niezamówione odpowiedzi **ARP is-at**, podszywając się pod adres IP bramy.

**DNS Spoofing (forged DNS responses)**  
Ofiara wysłała zapytanie DNS o `corp-login.acme-corp.local`.  
Atakujący odesłał sfałszowaną odpowiedź DNS, wskazując tę domenę na adres **192.168.10.55**.

**SSL Stripping (TLS downgrade / credential capture)**  
Ofiara rozpoczęła połączenie do rozwiązanego adresu IP i trafiła na **HTTP do atakującego**.  
Zaobserwowano przesłanie poświadczeń metodą **POST** w **jawnym tekście**.

## Zadania

**Jak dużo zapytań POST zostało zaobserwowane na naszej domenie corp-login.acme-corp.local?**

**http && ip.src == 192.168.10.10 && ip.dst == 192.168.10.55**

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/77-image.png)

**Odp. 1**

**Jakie jest hasło ofiary które zostało znalezione jako plaintext po udanym attaku SSL Stripping?**

Wchodzimy w zapytanie POST, następnie Hypertext Transfer Protocol -> HTML Form URL Encoded:

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/78-image.png)

**Odp. Secret123!**