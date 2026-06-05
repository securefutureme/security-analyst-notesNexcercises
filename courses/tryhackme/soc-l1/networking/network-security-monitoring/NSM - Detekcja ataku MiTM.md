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
