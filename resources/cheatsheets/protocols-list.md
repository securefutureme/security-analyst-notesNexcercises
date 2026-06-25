

Szybka ściąga przedstawiająca najczęściej spotykane protokoły sieciowe, ich zastosowanie, domyślne porty oraz podstawowe informacje istotne podczas administracji, analizy ruchu i pracy SOC.

> Numery portów są wartościami domyślnymi. Usługi mogą zostać skonfigurowane do działania na innych portach.

---
## Spis treści

- [[#Podstawowe pojęcia]]
- [[#Szybka ściąga portów]]
- [[#Najważniejsze zależności]]
- [[#TCP i UDP]]
- [[#Zakresy portów]]
- [[#Najczęściej używane protokoły]]
- [[#Protokoły WWW]]
- [[#Rozwiązywanie nazw i konfiguracja sieci]]
- [[#Zdalne zarządzanie]]
- [[#Transfer i udostępnianie plików]]
- [[#Poczta elektroniczna]]
- [[#Uwierzytelnianie i usługi katalogowe]]
- [[#Monitoring i logowanie]]
- [[#Routing i infrastruktura sieciowa]]
- [[#VPN i tunelowanie]]
- [[#Bazy danych]]
- [[#Numery protokołów IP]]
- [[#Protokoły a model OSI]]
- [[#Filtry Wireshark]]
- [[#Uwagi bezpieczeństwa]]

---
# Podstawowe pojęcia

## Protokół

Protokół sieciowy określa zasady komunikacji pomiędzy urządzeniami.

Definiuje między innymi:

- format przesyłanych danych,
- sposób nawiązywania połączenia,
- sposób adresowania,
- obsługę błędów,
- kolejność przesyłania informacji,
- mechanizmy uwierzytelniania i szyfrowania.

## Port

Port identyfikuje konkretną usługę działającą na urządzeniu.

Przykład:

```text
192.168.1.10:443
```

- `192.168.1.10` — adres IP hosta,
- `443` — port usługi HTTPS.

Jedna aplikacja może nasłuchiwać na kilku portach, a port domyślny może zostać zmieniony przez administratora.

---

# TCP i UDP

## TCP

TCP — **Transmission Control Protocol** — jest protokołem połączeniowym.

Najważniejsze cechy:

- zestawia połączenie przed przesłaniem danych,
- zapewnia właściwą kolejność segmentów,
- potwierdza odbiór danych,
- retransmituje utracone segmenty,
- zapewnia kontrolę przepływu.
  
Przykładowe protokoły korzystające z TCP:

- HTTP,
- HTTPS,
- SSH,
- SMTP,
- IMAP,
- SMB.

### TCP three-way handshake

```text
Klient → SYN → Serwer
Klient ← SYN-ACK ← Serwer
Klient → ACK → Serwer
```
## UDP

UDP — **User Datagram Protocol** — jest protokołem bezpołączeniowym.

Najważniejsze cechy:

- nie zestawia połączenia,
- nie gwarantuje dostarczenia danych,
- nie zapewnia właściwej kolejności pakietów,
- ma mniejszy narzut niż TCP,
- jest przydatny tam, gdzie liczy się szybkość.

Przykładowe protokoły korzystające z UDP:

- DNS,
- DHCP,
- NTP,
- SNMP,
- TFTP,
- część komunikacji VoIP.

---

## Porównanie TCP i UDP

|Cecha|TCP|UDP|
|---|---|---|
|Typ komunikacji|Połączeniowy|Bezpołączeniowy|
|Potwierdzenie odbioru|Tak|Nie|
|Kolejność danych|Gwarantowana|Niegwarantowana|
|Retransmisja|Tak|Nie|
|Narzut|Większy|Mniejszy|
|Typowe zastosowanie|WWW, poczta, pliki|DNS, streaming, VoIP|

---

# Zakresy portów

|Zakres|Nazwa|Zastosowanie|
|--:|---|---|
|`0–1023`|Well-known ports|Standardowe usługi systemowe|
|`1024–49151`|Registered ports|Zarejestrowane aplikacje i usługi|
|`49152–65535`|Dynamic/private ports|Porty tymczasowe klientów|

Port źródłowy klienta jest często losowym portem dynamicznym.

Przykład:

```text
192.168.1.20:53142 → 93.184.216.34:443
```

- `53142` — tymczasowy port klienta,
- `443` — port usługi HTTPS.

# Najczęściej używane protokoły

|Port|Protokół|Transport|Zastosowanie|
|--:|---|---|---|
|`20`|FTP Data|TCP|Przesyłanie danych FTP w trybie aktywnym|
|`21`|FTP Control|TCP|Sterowanie sesją FTP|
|`22`|SSH|TCP|Bezpieczny dostęp zdalny|
|`23`|Telnet|TCP|Nieszyfrowany dostęp zdalny|
|`25`|SMTP|TCP|Przesyłanie poczty pomiędzy serwerami|
|`53`|DNS|TCP/UDP|Rozwiązywanie nazw domenowych|
|`67`|DHCP Server|UDP|Serwer DHCP|
|`68`|DHCP Client|UDP|Klient DHCP|
|`69`|TFTP|UDP|Prosty transfer plików|
|`80`|HTTP|TCP|Nieszyfrowany ruch WWW|
|`88`|Kerberos|TCP/UDP|Uwierzytelnianie domenowe|
|`110`|POP3|TCP|Odbieranie poczty|
|`123`|NTP|UDP|Synchronizacja czasu|
|`135`|MS RPC|TCP/UDP|Microsoft Remote Procedure Call|
|`137–139`|NetBIOS|TCP/UDP|Starsze usługi sieciowe Windows|
|`143`|IMAP|TCP|Dostęp do poczty na serwerze|
|`161`|SNMP|UDP|Monitoring urządzeń|
|`162`|SNMP Trap|UDP|Powiadomienia SNMP|
|`179`|BGP|TCP|Routing pomiędzy systemami autonomicznymi|
|`389`|LDAP|TCP/UDP|Usługi katalogowe|
|`443`|HTTPS|TCP|Szyfrowany ruch WWW|
|`445`|SMB|TCP|Udostępnianie plików i zasobów Windows|
|`465`|SMTPS|TCP|SMTP z szyfrowaniem implicit TLS|
|`500`|IKE|UDP|Negocjowanie połączeń IPsec|
|`514`|Syslog|UDP/TCP|Przesyłanie logów|
|`587`|SMTP Submission|TCP|Wysyłanie poczty przez klientów|
|`636`|LDAPS|TCP|LDAP chroniony TLS|
|`989`|FTPS Data|TCP|Dane FTPS w trybie implicit TLS|
|`990`|FTPS Control|TCP|Sterowanie FTPS w trybie implicit TLS|
|`993`|IMAPS|TCP|IMAP chroniony TLS|
|`995`|POP3S|TCP|POP3 chroniony TLS|
|`1433`|Microsoft SQL Server|TCP|Baza danych MSSQL|
|`1521`|Oracle Database|TCP|Baza danych Oracle|
|`1701`|L2TP|UDP|Tunelowanie VPN|
|`1723`|PPTP|TCP|Starszy protokół VPN|
|`1812`|RADIUS|UDP|Uwierzytelnianie|
|`1813`|RADIUS Accounting|UDP|Rozliczanie sesji|
|`2049`|NFS|TCP/UDP|Udostępnianie plików Unix/Linux|
|`3306`|MySQL/MariaDB|TCP|Baza danych|
|`3389`|RDP|TCP/UDP|Pulpit zdalny Windows|
|`4500`|IPsec NAT-T|UDP|IPsec przez NAT|
|`5060`|SIP|TCP/UDP|Sygnalizacja VoIP|
|`5061`|SIP-TLS|TCP|Szyfrowana sygnalizacja VoIP|
|`5432`|PostgreSQL|TCP|Baza danych|
|`5900`|VNC|TCP|Zdalny pulpit|
|`5985`|WinRM HTTP|TCP|Zdalne zarządzanie Windows|
|`5986`|WinRM HTTPS|TCP|Szyfrowane zarządzanie Windows|
|`6379`|Redis|TCP|Baza danych in-memory|
|`6514`|Syslog over TLS|TCP|Szyfrowane przesyłanie logów|
|`8080`|HTTP Alternate|TCP|Alternatywny port HTTP|
|`8443`|HTTPS Alternate|TCP|Alternatywny port HTTPS|
|`9200`|Elasticsearch|TCP|API Elasticsearch|
|`27017`|MongoDB|TCP|Baza danych MongoDB|
# Protokoły WWW

## HTTP

```text
Port: 80/TCP
```

HTTP służy do przesyłania stron internetowych, danych API oraz innych zasobów.

Dane nie są domyślnie szyfrowane.

Przykład:

```http
GET /index.html HTTP/1.1
Host: example.com
```
## HTTPS

```text
Port: 443/TCP
```

HTTPS to HTTP zabezpieczony przy użyciu TLS.

Zapewnia:

- szyfrowanie transmisji,
- integralność danych,
- uwierzytelnienie serwera za pomocą certyfikatu.

> HTTPS chroni transmisję, ale nie oznacza automatycznie, że sama strona jest bezpieczna lub godna zaufania.

---
## WebSocket

WebSocket umożliwia dwukierunkową, trwałą komunikację pomiędzy klientem i serwerem.

Najczęściej wykorzystuje:

```text
ws://  → zwykle port 80
wss:// → zwykle port 443
```

Przykładowe zastosowanie:

- czaty,
- gry sieciowe,
- powiadomienia w czasie rzeczywistym,
- panele monitorujące.

---
# Rozwiązywanie nazw i konfiguracja sieci

## DNS

```text
Port: 53/UDP i 53/TCP
```

DNS zamienia nazwy domenowe na adresy IP.

Przykład:

```text
example.com → 93.184.216.34
```

UDP jest używany dla większości standardowych zapytań.

TCP może być wykorzystywany między innymi dla:

- dużych odpowiedzi,
- transferów stref,
- odpowiedzi, które nie mieszczą się w pojedynczym datagramie UDP.

Typowe rekordy DNS:

|Rekord|Znaczenie|
|---|---|
|`A`|Adres IPv4|
|`AAAA`|Adres IPv6|
|`CNAME`|Alias domeny|
|`MX`|Serwer pocztowy|
|`NS`|Serwer nazw|
|`TXT`|Informacje tekstowe|
|`PTR`|Odwrotne mapowanie adresu|
|`SOA`|Informacje o strefie|
## DHCP

```text
Serwer: 67/UDP
Klient: 68/UDP
```

DHCP automatycznie przydziela:

- adres IP,
- maskę podsieci,
- bramę domyślną,
- serwery DNS,
- czas dzierżawy.

Proces DORA:

```text
Discover
Offer
Request
Acknowledge
```
## ARP

ARP mapuje adres IPv4 na adres MAC w lokalnej sieci.

Przykład:

```text
192.168.1.1 → AA:BB:CC:DD:EE:FF
```

ARP nie używa portów TCP ani UDP.

Możliwe zagrożenia:

- ARP spoofing,
- ARP poisoning,
- atak Man-in-the-Middle.

---
## ICMP

ICMP służy do diagnostyki i zgłaszania błędów sieciowych. Nie używa portów TCP ani UDP.

Przykładowe narzędzia:

```bash
ping 8.8.8.8
traceroute 8.8.8.8
```
## NTP

```text
Port: 123/UDP
```

NTP synchronizuje czas systemowy.

Prawidłowy czas jest istotny dla:

- logów,
- certyfikatów,
- Kerberosa,
- korelacji zdarzeń w SIEM,
- analizy incydentów.
# Zdalne zarządzanie

## SSH

```text
Port: 22/TCP
```

SSH zapewnia szyfrowany dostęp do powłoki systemu.

Umożliwia również:

- wykonywanie poleceń,
- transfer plików,
- tunelowanie portów,
- uwierzytelnianie kluczami.

Przykład:

```bash
ssh user@192.168.1.10
```
## Telnet

```text
Port: 23/TCP
```

Telnet przesyła dane, w tym hasła, w formie nieszyfrowanej. Nie powinien być używany do administracji przez niezaufane sieci.

Bezpieczniejsza alternatywa:

```text
SSH
```
## RDP

```text
Port: 3389/TCP i UDP
```

RDP umożliwia graficzny dostęp zdalny do systemów Windows.

Zalecenia:

- nie wystawiaj RDP bezpośrednio do Internetu,
- używaj VPN lub Remote Desktop Gateway,
- stosuj MFA,
- ograniczaj dostęp na firewallu,
- monitoruj próby logowania.
## WinRM

```text
5985/TCP — HTTP
5986/TCP — HTTPS
```

WinRM umożliwia zdalne zarządzanie systemami Windows. Jest wykorzystywany między innymi przez:

```text
PowerShell Remoting
```
## VNC

```text
Port: 5900/TCP
```

VNC zapewnia zdalny dostęp do pulpitu.

Wiele implementacji VNC nie zapewnia wystarczającego szyfrowania, dlatego powinno być używane przez:

- VPN,
- tunel SSH,
- szyfrowany kanał.
# Transfer i udostępnianie plików

## FTP

```text
21/TCP — kanał sterujący
20/TCP — dane w trybie aktywnym
```

FTP nie szyfruje danych ani danych logowania. Bezpieczniejsze alternatywy:

- SFTP,
- SCP,
- FTPS.
## SFTP

```text
Port: 22/TCP
```

SFTP działa jako podsystem SSH. Zapewnia szyfrowany transfer plików.

> SFTP nie jest tym samym co FTP zabezpieczone TLS.
## SCP

```text
Port: 22/TCP
```

SCP umożliwia kopiowanie plików przez SSH.

Przykład:

```bash
scp file.txt user@server:/tmp/
```
## FTPS

FTPS to FTP zabezpieczone TLS. Najczęściej spotykane tryby:

```text
Explicit FTPS — zwykle port 21
Implicit FTPS — port 990
```
## TFTP

```text
Port: 69/UDP
```

TFTP to prosty protokół transferu plików.

Nie zapewnia:

- szyfrowania,
- silnego uwierzytelniania,
- zaawansowanej kontroli dostępu.

Typowe zastosowania:

- bootowanie urządzeń,
- przesyłanie konfiguracji,
- urządzenia sieciowe.
## SMB

```text
Port: 445/TCP
```

SMB umożliwia:

- udostępnianie plików,
- udostępnianie drukarek,
- komunikację w środowisku Windows,
- dostęp do udziałów sieciowych.

Przykład udziału:

```text
\\server\share
```

Starsze wersje SMB oraz NetBIOS mogą korzystać z portów `137–139`.
## NFS

```text
Port: 2049/TCP lub UDP
```

NFS służy do udostępniania plików w środowiskach Unix/Linux.

Błędna konfiguracja może umożliwić:

- dostęp do poufnych plików,
- zapis w udostępnionych katalogach,
- eskalację uprawnień.
# Poczta elektroniczna

## SMTP

```text
25/TCP  — komunikacja pomiędzy serwerami
587/TCP — wysyłanie poczty przez klientów
465/TCP — SMTP implicit TLS
```

SMTP służy do wysyłania wiadomości. Nie służy standardowo do pobierania wiadomości przez użytkownika.
## POP3

```text
110/TCP — POP3
995/TCP — POP3S
```

POP3 najczęściej pobiera wiadomości z serwera na urządzenie klienta.
## IMAP

```text
143/TCP — IMAP
993/TCP — IMAPS
```

IMAP przechowuje wiadomości na serwerze i synchronizuje je pomiędzy klientami.
## Porównanie protokołów pocztowych

| Protokół | Główna funkcja        |
| -------- | --------------------- |
| SMTP     | Wysyłanie poczty      |
| POP3     | Pobieranie poczty     |
| IMAP     | Synchronizacja poczty |
# Uwierzytelnianie i usługi katalogowe

## LDAP

```text
389/TCP lub UDP
```

LDAP służy do komunikacji z usługami katalogowymi.

Może być wykorzystywany do:

- wyszukiwania użytkowników,
- wyszukiwania grup,
- uwierzytelniania,
- odczytu informacji katalogowych.
## LDAPS

```text
636/TCP
```

LDAPS to LDAP zabezpieczony TLS.

Alternatywnym podejściem jest LDAP z użyciem mechanizmu StartTLS.
## Kerberos

```text
88/TCP i UDP
```

Kerberos jest protokołem uwierzytelniania opartym na biletach.

Jest intensywnie wykorzystywany w Active Directory.

Najważniejsze elementy:

- KDC,
- TGT,
- TGS,
- bilety usługowe.

Kerberos wymaga prawidłowej synchronizacji czasu.
## RADIUS

```text
1812/UDP — uwierzytelnianie
1813/UDP — accounting
```

RADIUS jest wykorzystywany między innymi przez:

- VPN,
- Wi-Fi przedsiębiorstw,
- urządzenia sieciowe,
- mechanizmy Network Access Control.
## TACACS+

```text
Port: 49/TCP
```

TACACS+ jest często używany do centralnego zarządzania dostępem administracyjnym do urządzeń sieciowych.

Rozdziela:

- authentication,
- authorization,
- accounting.
# Monitoring i logowanie

## SNMP

```text
161/UDP — zapytania
162/UDP — trapy
```

SNMP służy do monitorowania i zarządzania urządzeniami.

Przykładowe monitorowane wartości:

- wykorzystanie CPU,
- pamięć,
- stan interfejsów,
- liczba pakietów,
- błędy sieciowe.

SNMPv3 zapewnia lepsze bezpieczeństwo niż SNMPv1 i SNMPv2c.
## Syslog

```text
514/UDP lub TCP
6514/TCP — Syslog over TLS
```

Syslog służy do centralnego przesyłania logów.

Przykładowe źródła:

- serwery Linux,
- routery,
- firewalle,
- przełączniki,
- systemy IDS/IPS.
## NetFlow

NetFlow zbiera metadane o przepływach sieciowych.

Może zawierać:

- adres źródłowy,
- adres docelowy,
- porty,
- protokół,
- liczbę bajtów,
- czas trwania połączenia.

NetFlow nie przechowuje pełnej treści pakietów.
# Routing i infrastruktura sieciowa

## BGP

```text
Port: 179/TCP
```

BGP wymienia informacje o trasach pomiędzy systemami autonomicznymi. Jest podstawowym protokołem routingu publicznego Internetu.
## OSPF

OSPF działa bezpośrednio nad IP i nie korzysta z TCP ani UDP.

```text
Numer protokołu IP: 89
```

Jest używany jako wewnętrzny protokół routingu.
## RIP

```text
Port: 520/UDP
```

RIP jest starszym protokołem routingu wykorzystującym liczbę przeskoków jako metrykę.
## VRRP

VRRP umożliwia utworzenie wirtualnej, redundantnej bramy.

```text
Numer protokołu IP: 112
```
# VPN i tunelowanie

## IPsec

IPsec zabezpiecza komunikację na poziomie warstwy sieciowej.

Powiązane protokoły:

```text
IKE     — 500/UDP
NAT-T   — 4500/UDP
ESP     — protokół IP 50
AH      — protokół IP 51
```
## WireGuard

```text
Domyślnie: 51820/UDP
```

Port WireGuard jest konfigurowalny. WireGuard jest nowoczesnym i lekkim protokołem VPN.
## OpenVPN

Najczęściej spotykany port:

```text
1194/UDP
```

OpenVPN może działać również po TCP i na innych portach.
## L2TP

```text
Port: 1701/UDP
```

L2TP nie zapewnia samodzielnie szyfrowania.

Zwykle jest łączony z IPsec.
## PPTP

```text
1723/TCP
GRE — protokół IP 47
```

PPTP jest przestarzały i nie powinien być używany do zabezpieczania współczesnej komunikacji.
# Bazy danych

|Port|Usługa|Transport|
|--:|---|---|
|`1433`|Microsoft SQL Server|TCP|
|`1521`|Oracle Database|TCP|
|`3306`|MySQL/MariaDB|TCP|
|`5432`|PostgreSQL|TCP|
|`6379`|Redis|TCP|
|`9200`|Elasticsearch|TCP|
|`27017`|MongoDB|TCP|
## Zalecenia

Bazy danych nie powinny być bezpośrednio dostępne z publicznego Internetu. Dostęp należy ograniczać przy użyciu:

- firewalla,
- segmentacji sieci,
- VPN,
- list kontroli dostępu,
- silnego uwierzytelniania,
- TLS.

# Numery protokołów IP

Nie wszystkie protokoły korzystają z portów TCP lub UDP.

|Numer|Protokół|Zastosowanie|
|--:|---|---|
|`1`|ICMP|Diagnostyka IPv4|
|`2`|IGMP|Zarządzanie multicastem|
|`4`|IPv4 encapsulation|Tunelowanie IPv4|
|`6`|TCP|Transport połączeniowy|
|`17`|UDP|Transport bezpołączeniowy|
|`41`|IPv6 encapsulation|Tunelowanie IPv6|
|`47`|GRE|Tunelowanie|
|`50`|ESP|Szyfrowanie IPsec|
|`51`|AH|Integralność IPsec|
|`58`|ICMPv6|Diagnostyka IPv6|
|`89`|OSPF|Routing|
|`112`|VRRP|Redundancja routerów|
|`132`|SCTP|Alternatywny protokół transportowy|
Przykład:

```text
TCP używa numeru protokołu IP 6
UDP używa numeru protokołu IP 17
```
# Protokoły a model OSI

Przypisanie protokołów do warstw ma charakter uproszczony.

|Warstwa OSI|Przykładowe protokoły|
|--:|---|
|7 — aplikacji|HTTP, DNS, SMTP, FTP, SSH, SNMP|
|6 — prezentacji|TLS, kodowanie, kompresja|
|5 — sesji|RPC, NetBIOS Session Service|
|4 — transportowa|TCP, UDP, SCTP|
|3 — sieciowa|IPv4, IPv6, ICMP, IPsec|
|2 — łącza danych|Ethernet, ARP, VLAN, STP|
|1 — fizyczna|Przewody, światłowody, fale radiowe|
## Model TCP/IP

|Warstwa TCP/IP|Przykładowe protokoły|
|---|---|
|Aplikacji|HTTP, DNS, SSH, SMTP|
|Transportowa|TCP, UDP|
|Internetowa|IP, ICMP, IPsec|
|Dostępu do sieci|Ethernet, ARP, Wi-Fi|
# Filtry Wireshark

## Podstawowe protokoły

```wireshark
tcp
```

```wireshark
udp
```

```wireshark
icmp
```

```wireshark
dns
```

```wireshark
http
```

```wireshark
tls
```

```wireshark
ssh
```

```wireshark
smb2
```
## Filtrowanie po porcie

```wireshark
tcp.port == 443
```

```wireshark
udp.port == 53
```

Port źródłowy:

```wireshark
tcp.srcport == 22
```

Port docelowy:

```wireshark
tcp.dstport == 445
```
## Filtrowanie po adresie IP

```wireshark
ip.addr == 192.168.1.10
```

Tylko źródło:

```wireshark
ip.src == 192.168.1.10
```

Tylko cel:

```wireshark
ip.dst == 192.168.1.10
```
## DNS

```wireshark
dns.qry.name contains "example"
```

```wireshark
dns.flags.response == 0
```

```wireshark
dns.flags.response == 1
```
## HTTP

```wireshark
http.request
```

```wireshark
http.response
```

```wireshark
http.request.method == "POST"
```

```wireshark
http.host == "example.com"
```

## TCP

Nowe próby zestawienia połączenia:

```wireshark
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

Pakiety resetujące połączenie:

```wireshark
tcp.flags.reset == 1
```

Retransmisje:

```wireshark
tcp.analysis.retransmission
```
# Uwagi bezpieczeństwa

- `Telnet`, `FTP`, `HTTP` i standardowy `POP3` przesyłają dane bez domyślnego szyfrowania.
- Preferuj `SSH`, `SFTP`, `HTTPS`, `IMAPS`, `POP3S` i protokoły wykorzystujące TLS.
- Nie wystawiaj bezpośrednio do Internetu portów administracyjnych i baz danych.
- Ograniczaj dostęp przy użyciu firewalla i segmentacji sieci.
- Monitoruj nietypowe porty i niespodziewane usługi.
- Pamiętaj, że usługa może działać na niestandardowym porcie.
- Numer portu nie potwierdza jednoznacznie protokołu.
- Analizuj także treść pakietów, proces odpowiedzialny za połączenie i kontekst zdarzenia.
- Wyłączaj nieużywane protokoły i usługi.
- Starsze protokoły mogą nie obsługiwać nowoczesnego szyfrowania.
- W komunikacji administracyjnej stosuj MFA, VPN i listy dozwolonych adresów.
- Loguj i analizuj próby dostępu do portów `22`, `3389`, `445`, `5985` i `5986`.
# Szybka ściąga portów

```text
20/21   FTP
22      SSH, SFTP, SCP
23      Telnet
25      SMTP
53      DNS
67/68   DHCP
69      TFTP
80      HTTP
88      Kerberos
110     POP3
123     NTP
135     MS RPC
137-139 NetBIOS
143     IMAP
161/162 SNMP
179     BGP
389     LDAP
443     HTTPS
445     SMB
465     SMTPS
514     Syslog
587     SMTP Submission
636     LDAPS
993     IMAPS
995     POP3S
1433    MSSQL
1521    Oracle
1812    RADIUS
2049    NFS
3306    MySQL/MariaDB
3389    RDP
5060    SIP
5432    PostgreSQL
5900    VNC
5985    WinRM HTTP
5986    WinRM HTTPS
6379    Redis
6514    Syslog TLS
8080    HTTP Alternate
8443    HTTPS Alternate
9200    Elasticsearch
27017   MongoDB
```
# Najważniejsze zależności

```text
WWW:
HTTP  → 80/TCP
HTTPS → 443/TCP

Poczta:
SMTP  → wysyłanie
POP3  → pobieranie
IMAP  → synchronizacja

Zdalny dostęp:
SSH    → 22/TCP
RDP    → 3389/TCP/UDP
WinRM  → 5985/5986 TCP

Pliki:
FTP   → 20/21 TCP
SFTP  → 22/TCP
SMB   → 445/TCP
NFS   → 2049 TCP/UDP

Infrastruktura:
DNS   → 53 TCP/UDP
DHCP  → 67/68 UDP
NTP   → 123/UDP
SNMP  → 161/162 UDP
```