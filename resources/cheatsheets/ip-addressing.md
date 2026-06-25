# Subnetting - shortcut

![[resources/cheatsheets/Attachments/2-image.png]]

https://pbxbook.com/other/ipcheat.html
https://www.aelius.com/njh/subnet_sheet.html

## Spis treści

Szybka ściąga dotycząca adresów IPv4, masek podsieci, notacji CIDR, zakresów prywatnych oraz obliczania podsieci.

- [[#Podstawy IPv4]]
- [[#Klasy adresów IPv4]]
- [[#Notacja CIDR]]
- [[#Najważniejsze zakresy adresów]]
	- [[#Link-local / APIPA]]
	- [[#Prywatne adresy IPv4]]
	- [[#Loopback]]
	- [[#Adres nieokreślony]]
	- [[#Broadcast ograniczony]]
	- [[#Multicast]]
	- [[#Carrier-Grade NAT]]
	- [[#Adresy dokumentacyjne]]
- [[#Tabela CIDR]]
- [[#Subnetting sieci /8]]
- [[#Subnetting sieci /16]]
- [[#Subnetting sieci /24]]
- [[#Rozmiary bloków]]
- [[#Jak obliczyć podsieć]]
- [[#Przydatne wzory]]
- [[#Przydatne polecenia]]

---

# Podstawy IPv4

Adres IPv4 składa się z **32 bitów**, podzielonych na cztery oktety po 8 bitów:

```text
192.168.1.10
```

Postać binarna:

```text
11000000.10101000.00000001.00001010
```

Każdy oktet może przyjmować wartość od:

```text
0–255
```

Adres wraz z maską CIDR:

```text
192.168.1.10/24
```

oznacza, że:

- pierwsze `24` bity identyfikują sieć,
- pozostałe `8` bitów identyfikuje hosta.

# Klasy adresów IPv4

> Klasy adresów są rozwiązaniem historycznym. Współczesne sieci używają notacji CIDR, która zastąpiła tradycyjny podział klasowy.

|Klasa|Początkowe bity|Zakres pierwszego oktetu|Zakres adresów|Historyczna maska|
|---|---|--:|---|---|
|A|`0`|`1–126`|`1.0.0.0–126.255.255.255`|`255.0.0.0` (`/8`)|
|B|`10`|`128–191`|`128.0.0.0–191.255.255.255`|`255.255.0.0` (`/16`)|
|C|`110`|`192–223`|`192.0.0.0–223.255.255.255`|`255.255.255.0` (`/24`)|
|D|`1110`|`224–239`|`224.0.0.0–239.255.255.255`|Multicast|
|E|`1111`|`240–255`|`240.0.0.0–255.255.255.255`|Zarezerwowane|
## Ważne wyjątki

- `0.0.0.0/8` ma znaczenie specjalne.
- `127.0.0.0/8` jest przeznaczone dla interfejsu loopback.
- `255.255.255.255` jest adresem ograniczonego broadcastu.
- Klasy D i E nie są standardowymi zakresami adresów hostów.

---
# Notacja CIDR

CIDR — **Classless Inter-Domain Routing** — określa liczbę bitów należących do części sieciowej adresu.

Przykład:

```text
192.168.10.0/24
```

Maska:

```text
255.255.255.0
```

Liczba bitów hosta:

```text
32 - 24 = 8
```

Liczba wszystkich adresów:

```text
2^8 = 256
```

Standardowa liczba użytecznych hostów:

```text
256 - 2 = 254
```

**Dwa adresy są zwykle zarezerwowane:**

- pierwszy adres — adres sieci,
- ostatni adres — adres broadcast.

---
# Najważniejsze zakresy adresów

## Prywatne adresy IPv4

Adresy prywatne nie są routowane bezpośrednio w publicznym Internecie.

|Zakres|CIDR|Liczba adresów|
|---|---|--:|
|`10.0.0.0–10.255.255.255`|`10.0.0.0/8`|16 777 216|
|`172.16.0.0–172.31.255.255`|`172.16.0.0/12`|1 048 576|
|`192.168.0.0–192.168.255.255`|`192.168.0.0/16`|65 536|

Przykładowe adresy prywatne:

```text
10.10.10.5
172.16.20.15
192.168.1.100
```

> Nie cały zakres `172.0.0.0/8` jest prywatny. Prywatny jest wyłącznie zakres `172.16.0.0/12`.
## Link-local / APIPA

```text
169.254.0.0/16
```

Zakres:

```text
169.254.0.0–169.254.255.255
```

System może przypisać sobie taki adres automatycznie, jeśli nie otrzyma konfiguracji z serwera DHCP.

Przykład:

```text
169.254.25.81
```

Pojawienie się adresu APIPA często wskazuje na:

- brak dostępu do serwera DHCP,
- problem z interfejsem sieciowym,
- błąd konfiguracji VLAN,
- problem z połączeniem fizycznym lub bezprzewodowym.
## Loopback

Cały zakres loopback:

```text
127.0.0.0/8
```

Najczęściej używany adres:

```text
127.0.0.1
```

Nazwa:

```text
localhost
```

Test lokalnego stosu TCP/IP:

```bash
ping 127.0.0.1
```

Ruch wysłany na adres loopback nie opuszcza lokalnego hosta.
## Adres nieokreślony

```text
0.0.0.0
```

Może oznaczać:

- brak przypisanego adresu,
- wszystkie lokalne interfejsy,
- trasę domyślną w zapisie `0.0.0.0/0`.

Przykład nasłuchiwania na wszystkich interfejsach:

```text
0.0.0.0:8080
```
## Broadcast ograniczony

```text
255.255.255.255
```

Adres służy do wysyłania komunikatu do wszystkich hostów w lokalnym segmencie sieci.

Routery zazwyczaj nie przekazują takiego ruchu dalej.

## Multicast

```text
224.0.0.0/4
```

Zakres:

```text
224.0.0.0–239.255.255.255
```

Multicast umożliwia wysyłanie danych do grupy odbiorców.

Przykłady:

```text
224.0.0.1 — wszystkie hosty w lokalnej podsieci
224.0.0.2 — wszystkie routery w lokalnej podsieci
```

## Carrier-Grade NAT

```text
100.64.0.0/10
```

Zakres wykorzystywany przez operatorów internetowych do współdzielenia publicznych adresów IPv4 pomiędzy wielu klientów.

Zakres:

```text
100.64.0.0–100.127.255.255
```

## Adresy dokumentacyjne

Zakresy przeznaczone do przykładów, dokumentacji i laboratoriów:

```text
192.0.2.0/24
198.51.100.0/24
203.0.113.0/24
```

Nie powinny być używane jako rzeczywiste publiczne adresy usług.

---
# Tabela CIDR

|  CIDR | Maska             | Liczba adresów | Użyteczne hosty |
| ----: | ----------------- | -------------: | --------------: |
|  `/8` | `255.0.0.0`       |     16 777 216 |      16 777 214 |
|  `/9` | `255.128.0.0`     |      8 388 608 |       8 388 606 |
| `/10` | `255.192.0.0`     |      4 194 304 |       4 194 302 |
| `/11` | `255.224.0.0`     |      2 097 152 |       2 097 150 |
| `/12` | `255.240.0.0`     |      1 048 576 |       1 048 574 |
| `/13` | `255.248.0.0`     |        524 288 |         524 286 |
| `/14` | `255.252.0.0`     |        262 144 |         262 142 |
| `/15` | `255.254.0.0`     |        131 072 |         131 070 |
| `/16` | `255.255.0.0`     |         65 536 |          65 534 |
| `/17` | `255.255.128.0`   |         32 768 |          32 766 |
| `/18` | `255.255.192.0`   |         16 384 |          16 382 |
| `/19` | `255.255.224.0`   |          8 192 |           8 190 |
| `/20` | `255.255.240.0`   |          4 096 |           4 094 |
| `/21` | `255.255.248.0`   |          2 048 |           2 046 |
| `/22` | `255.255.252.0`   |          1 024 |           1 022 |
| `/23` | `255.255.254.0`   |            512 |             510 |
| `/24` | `255.255.255.0`   |            256 |             254 |
| `/25` | `255.255.255.128` |            128 |             126 |
| `/26` | `255.255.255.192` |             64 |              62 |
| `/27` | `255.255.255.224` |             32 |              30 |
| `/28` | `255.255.255.240` |             16 |              14 |
| `/29` | `255.255.255.248` |              8 |               6 |
| `/30` | `255.255.255.252` |              4 |               2 |
| `/31` | `255.255.255.254` |              2 |              2* |
| `/32` | `255.255.255.255` |              1 |         1 adres |

* `/31` jest wykorzystywane przede wszystkim na łączach point-to-point. W takim przypadku oba adresy mogą być użyte przez końce połączenia.
  
- `/32` oznacza pojedynczy adres hosta, a nie standardową podsieć wielohostową.

---
# Subnetting sieci /8

Poniższa tabela pokazuje podział tradycyjnej sieci `/8` na mniejsze podsieci.

|CIDR|Maska|Liczba podsieci względem `/8`|Adresy w podsieci|Użyteczne hosty|
|--:|---|--:|--:|--:|
|`/8`|`255.0.0.0`|1|16 777 216|16 777 214|
|`/9`|`255.128.0.0`|2|8 388 608|8 388 606|
|`/10`|`255.192.0.0`|4|4 194 304|4 194 302|
|`/11`|`255.224.0.0`|8|2 097 152|2 097 150|
|`/12`|`255.240.0.0`|16|1 048 576|1 048 574|
|`/13`|`255.248.0.0`|32|524 288|524 286|
|`/14`|`255.252.0.0`|64|262 144|262 142|
|`/15`|`255.254.0.0`|128|131 072|131 070|
|`/16`|`255.255.0.0`|256|65 536|65 534|

---
# Subnetting sieci /16

Poniższa tabela pokazuje podział tradycyjnej sieci `/16`.

|CIDR|Maska|Liczba podsieci względem `/16`|Adresy w podsieci|Użyteczne hosty|
|--:|---|--:|--:|--:|
|`/16`|`255.255.0.0`|1|65 536|65 534|
|`/17`|`255.255.128.0`|2|32 768|32 766|
|`/18`|`255.255.192.0`|4|16 384|16 382|
|`/19`|`255.255.224.0`|8|8 192|8 190|
|`/20`|`255.255.240.0`|16|4 096|4 094|
|`/21`|`255.255.248.0`|32|2 048|2 046|
|`/22`|`255.255.252.0`|64|1 024|1 022|
|`/23`|`255.255.254.0`|128|512|510|
|`/24`|`255.255.255.0`|256|256|254|

---
# Subnetting sieci /24

Poniższa tabela pokazuje podział jednej sieci `/24`.

|CIDR|Maska|Liczba podsieci względem `/24`|Adresy w podsieci|Użyteczne hosty|Krok|
|--:|---|--:|--:|--:|--:|
|`/24`|`255.255.255.0`|1|256|254|256|
|`/25`|`255.255.255.128`|2|128|126|128|
|`/26`|`255.255.255.192`|4|64|62|64|
|`/27`|`255.255.255.224`|8|32|30|32|
|`/28`|`255.255.255.240`|16|16|14|16|
|`/29`|`255.255.255.248`|32|8|6|8|
|`/30`|`255.255.255.252`|64|4|2|4|
|`/31`|`255.255.255.254`|128|2|2*|2|
|`/32`|`255.255.255.255`|256|1|1 adres|1|

---
# Rozmiary bloków

**Najczęściej używane wartości maski**

|Wartość maski|Bity binarne|Rozmiar bloku|
|--:|---|--:|
|`0`|`00000000`|256|
|`128`|`10000000`|128|
|`192`|`11000000`|64|
|`224`|`11100000`|32|
|`240`|`11110000`|16|
|`248`|`11111000`|8|
|`252`|`11111100`|4|
|`254`|`11111110`|2|
|`255`|`11111111`|1|
 **Wzór na rozmiar bloku**

```text
256 - wartość oktetu maski
```

**Przykład dla `/27`:**

```text
Maska: 255.255.255.224
Krok:  256 - 224 = 32
```

**Podsieci zaczynają się więc co 32 adresy:**

```text
0
32
64
96
128
160
192
224
```

---
# Jak obliczyć podsieć

### 1. Ustal maskę

Przykład:

```text
/26 = 255.255.255.192
```
### 2. Oblicz krok

```text
256 - 192 = 64
```
### 3. Wypisz początki bloków

```text
0
64
128
192
```

Daje to podsieci:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```
### 4. Znajdź blok zawierający adres

Dla adresu:

```text
192.168.1.130/26
```

liczba `130` znajduje się w przedziale:

```text
128–191
```
### 5. Wyznacz adresy

```text
Adres sieci:       192.168.1.128
Pierwszy host:     192.168.1.129
Ostatni host:      192.168.1.190
Adres broadcast:   192.168.1.191
```
## Przykład obliczenia

Dany adres:

```text
10.10.10.70/27
```
### Krok 1 — maska

```text
/27 = 255.255.255.224
```
### Krok 2 — rozmiar bloku

```text
256 - 224 = 32
```
### Krok 3 — zakresy podsieci

```text
0–31
32–63
64–95
96–127
128–159
160–191
192–223
224–255
```

Adres `70` znajduje się w zakresie:

```text
64–95
```
### Wynik

|Element|Adres|
|---|---|
|Adres IP|`10.10.10.70`|
|Maska|`255.255.255.224`|
|CIDR|`/27`|
|Adres sieci|`10.10.10.64`|
|Pierwszy host|`10.10.10.65`|
|Ostatni host|`10.10.10.94`|
|Broadcast|`10.10.10.95`|
|Wszystkie adresy|32|
|Użyteczne hosty|30|

---
# Przydatne wzory

## Liczba bitów hosta

```text
32 - długość prefiksu CIDR
```

Przykład:

```text
/27 → 32 - 27 = 5 bitów hosta
```
## Liczba wszystkich adresów

```text
2^(liczba bitów hosta)
```

Przykład:

```text
2^5 = 32 adresy
```
## Standardowa liczba użytecznych hostów

```text
2^(liczba bitów hosta) - 2
```

Przykład:

```text
32 - 2 = 30 hostów
```
## Liczba podsieci

Jeżeli sieć bazowa `/24` została podzielona na `/27`:

```text
2^(27 - 24) = 2^3 = 8 podsieci
```

---
# Przydatne polecenia

## Windows

Wyświetlenie konfiguracji sieciowej:

```powershell
ipconfig
```

Szczegółowa konfiguracja:

```powershell
ipconfig /all
```

Tablica routingu:

```powershell
route print
```

Test loopback:

```powershell
ping 127.0.0.1
```

Test bramy domyślnej:

```powershell
ping 192.168.1.1
```
## Linux

Wyświetlenie adresów:

```bash
ip address
```

Krótka wersja:

```bash
ip -br address
```

Tablica routingu:

```bash
ip route
```

Sprawdzenie konkretnego adresu:

```bash
ip route get 8.8.8.8
```
## Kalkulatory

Popularne narzędzia konsolowe:

```bash
ipcalc 192.168.1.130/26
```

```bash
sipcalc 192.168.1.130/26
```

Przykładowy wynik powinien zawierać:

```text
Network address
Broadcast address
Network mask
Host range
Number of usable hosts
```
# Szybka ściąga

```text
/24 = 255.255.255.0   = 256 adresów = 254 hosty
/25 = 255.255.255.128 = 128 adresów = 126 hostów
/26 = 255.255.255.192 = 64 adresy   = 62 hosty
/27 = 255.255.255.224 = 32 adresy   = 30 hostów
/28 = 255.255.255.240 = 16 adresów  = 14 hostów
/29 = 255.255.255.248 = 8 adresów   = 6 hostów
/30 = 255.255.255.252 = 4 adresy    = 2 hosty
/31 = 255.255.255.254 = 2 adresy    = łącza point-to-point
/32 = 255.255.255.255 = pojedynczy adres
```

Najczęstsze kroki podsieci:

```text
128, 64, 32, 16, 8, 4, 2, 1
```

Najczęstsze wartości oktetu maski:

```text
128, 192, 224, 240, 248, 252, 254, 255
```
