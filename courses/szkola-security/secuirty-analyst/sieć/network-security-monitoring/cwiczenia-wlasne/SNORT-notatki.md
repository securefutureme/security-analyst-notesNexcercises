# Overview - Po co to robię?

W tej notatce chciałbym pokazać praktyczne przećwiczenie działania Snorta jako systemu IDS/IPS oraz narzędzia do analizy plików PCAP.

Tutaj mogę znaleźć:

- czym jest Snort,
- w jakich trybach może działać,
- jak wygląda podstawowa składnia reguły,
- jak dodać własną regułę do `local.rules`,
- jak sprawdzić poprawność konfiguracji,
- jak uruchomić Snorta na pliku `.pcap`,
- jak odczytać alerty wygenerowane przez własne reguły.

---

## Czym jest Snort?

Snort to open-source system IDS/IPS przeznaczony do analizy ruchu sieciowego w sieciach IP.

Może działać jako:

- **NIDS** - pasywnie monitoruje ruch sieciowy i generuje alerty,
- **IPS inline** - działa w torze ruchu i może blokować pakiety,
- **narzędzie do analizy PCAP** - analizuje wcześniej zapisany ruch z pliku `.pcap`.

W kontekście SOC Snort jest przydatny, ponieważ pozwala wykrywać znane wzorce ataków na podstawie reguł sygnaturowych.

---

## Tryby pracy Snorta

### Sniffer mode

Snort działa jak prosty sniffer pakietów i wyświetla ruch na ekranie.

Przykład:

```bash
sudo snort -i <interfejs> -q -v
```

Opcje:

- `-i <interfejs>` - interfejs sieciowy, np. `eth0`, `ens33`,
- `-q` - tryb quiet, mniej komunikatów systemowych,
- `-v` - pokazuje nagłówki pakietów,
- `-d` - pokazuje payload, czyli dane aplikacyjne.

Przykład z payloadem:

```bash
sudo snort -i <interfejs> -q -v -d
```

### Packet logger mode

Snort zapisuje przechwycony ruch do plików, aby można było przeanalizować go później.
Ten tryb jest przydatny, gdy chcemy zebrać ruch z interfejsu i wrócić do niego w późniejszym czasie.

---
### Network IDS mode

Snort analizuje ruch sieciowy z interfejsu albo z pliku PCAP, porównuje go z regułami i generuje alerty.

Przykład analizy pliku PCAP:

```bash
sudo snort -c /etc/snort/snort_kurs.conf -A console -q -r <plik.pcap>
```

Opcje:

- `-c` - wskazuje plik konfiguracyjny Snorta,
- `-A console` - wypisuje alerty na konsolę,
- `-q` - tryb quiet,
- `-r` - odczyt ruchu z pliku PCAP.

### IPS inline mode

W trybie IPS Snort działa aktywnie w torze ruchu i może blokować pakiety.

W takim trybie reguły mogą używać akcji takich jak:

- `drop`,
- `reject`,
- `sdrop`.

W tym ćwiczeniu skupiam się głównie na trybie IDS i analizie plików PCAP.

---
## Budowa reguły Snorta

Podstawowa składnia reguły:

```text
[action] [protocol] [src_ip] [src_port] [direction] [dst_ip] [dst_port] ([options])
```

Przykład:

```text
alert tcp any any -> any 80 (msg:"HTTP traffic detected"; sid:1000001; rev:1;)
```

Elementy reguły:

|Element|Znaczenie|
|---|---|
|`alert`|akcja - wygeneruj alert|
|`tcp`|protokół|
|`any any`|dowolny adres źródłowy i dowolny port źródłowy|
|`->`|kierunek ruchu|
|`any 80`|dowolny adres docelowy na porcie 80|
|`msg`|komunikat alertu|
|`sid`|unikalny identyfikator reguły|
|`rev`|rewizja reguły|

---
## Akcje w regułach

Najważniejsze akcje:

- `alert` - wygeneruj alert i przepuść ruch,
- `log` - tylko zaloguj dopasowanie,
- `drop` - w trybie IPS upuść pakiet i zaloguj zdarzenie,
- `sdrop` - w trybie IPS upuść pakiet bez logowania,
- `reject` - odrzuć połączenie i zaloguj zdarzenie,
- `pass` - przepuść ruch i nie sprawdzaj go dalej innymi regułami.

W praktyce IDS najczęściej używana będzie akcja:

```text
alert
```
## Protokoły

Snort może analizować między innymi:

- `tcp`,
- `udp`,
- `icmp`,
- `ip`.

Przykład dla ICMP:

```text
alert icmp any any -> any any (msg:"ICMP traffic detected"; sid:1000001; rev:1;)
```

---
## Adresy IP w regułach

Przykłady:

```text
192.168.1.10
192.168.1.0/24
any
[192.168.1.10,192.168.1.20,10.0.0.5]
```

Można też używać zmiennych zdefiniowanych w pliku konfiguracyjnym Snorta:

```text
var HOME_NET 192.168.1.0/24
var EXTERNAL_NET !$HOME_NET
```

Przykład użycia zmiennych:

```text
alert tcp $EXTERNAL_NET any -> $HOME_NET 80 (msg:"External HTTP traffic"; sid:1000002; rev:1;)
```

Zaprzeczenie:

```text
!$HOME_NET
!192.168.1.10
```

---
## Porty w regułach

Przykłady:

```text
80
1:1024
any
[80,8080,8000]
!80
```

Można też używać zmiennych:

```text
portvar HTTP_PORTS [80,8080,8000]
```

Przykład:

```text
alert tcp any any -> any $HTTP_PORTS (msg:"HTTP traffic"; sid:1000003; rev:1;)
```

---
## Kierunek ruchu

Jednokierunkowo:

```text
SRC -> DST
```

Dwukierunkowo:

```text
SRC <> DST
```

Przykład:

```text
alert tcp any any -> any 80 (msg:"Request to HTTP server"; sid:1000004; rev:1;)
```

Ta reguła sprawdza ruch tylko w kierunku od źródła do celu.

---
## Opcje reguł

Opcje znajdują się w nawiasach:

```text
(msg:"..."; sid:1000001; rev:1; content:"...";)
```

Najważniejsze opcje:

|Opcja|Znaczenie|
|---|---|
|`msg`|komunikat widoczny w alercie|
|`sid`|unikalny identyfikator reguły|
|`rev`|rewizja reguły|
|`content`|szukany ciąg znaków lub bajtów|
|`nocase`|ignorowanie wielkości liter|
|`http_header`|szukanie w nagłówkach HTTP|
|`http_uri`|szukanie w URI HTTP|
|`http_method`|szukanie w metodzie HTTP|
Własne reguły powinny mieć `sid` od `1000000` wzwyż.

---
## Content matching

Przykład wyszukiwania tekstu ASCII:

```text
content:"blue";
```

Przykład wyszukiwania bajtów hex:

```text
content:"|62 6c 75 65|";
```

To odpowiada tekstowi:

```text
blue
```

Można też mieszać tekst i hex:

```text
content:"b|6c 75|e";
```

Zaprzeczenie:

```text
content:!"blue";
```

Przykład bez rozróżniania wielkości liter:

```text
content:"get /"; nocase;
```

---
## Ważna uwaga o HTTPS

Reguły wykorzystujące `http_uri`, `http_header` albo `http_method` dobrze działają na ruchu HTTP widocznym w treści pakietów.

W przypadku zwykłego zaszyfrowanego HTTPS Snort nie zobaczy pełnego URI ani nagłówków HTTP, jeśli ruch nie został wcześniej odszyfrowany.

Dlatego w ćwiczeniach z PCAP najłatwiej testować reguły na ruchu HTTP albo na takich plikach PCAP, gdzie interesujące dane są widoczne w plaintext.

---
## Plik local.rules

Własne reguły można dopisywać w pliku:

```bash
/etc/snort/rules/local.rules
```

Przykład prostej reguły ICMP:

```text
alert icmp any any -> any any (msg:"LOCAL ICMP traffic detected"; sid:1000001; rev:1;)
```

Znaczenie:

- `alert` - wygeneruj alert,
- `icmp` - analizuj ruch ICMP,
- `any any -> any any` - dowolne źródło i dowolny cel,
- `msg` - komunikat alertu,
- `sid` - identyfikator własnej reguły,
- `rev` - rewizja reguły.

---
## Sprawdzenie konfiguracji

Po każdej zmianie w regułach warto sprawdzić konfigurację:

```bash
sudo snort -T -c /etc/snort/snort_kurs.conf
```

Jeśli konfiguracja jest poprawna, Snort powinien zakończyć test bez błędów.

---
## Uruchomienie Snorta na pliku PCAP

Przykład:

```bash
sudo snort -c /etc/snort/snort_kurs.conf -A console -q -r sample.pcap
```

Jeżeli reguły dopasują się do ruchu w pliku PCAP, alerty pojawią się w konsoli.
