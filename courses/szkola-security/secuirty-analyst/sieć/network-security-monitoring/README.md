# Network Security Monitoring

Network Security Monitoring (NSM) to ciągłe pozyskiwanie, przetwarzanie i analiza danych sieciowych w celu wykrywania, badania i reagowania na zagrożenia. Dane te obejmują m.in. pełne pakiety, metadane przepływów (flow) oraz logi z elementów infrastruktury. NSM jest więc procesem i zdolnością operacyjną, a nie tylko pojedynczym narzędziem.

W praktyce w SOC NSM służy do:

* wykrywania podejrzanych zachowań na bazie ruchu i metadanych,
* dostarczania kontekstu do incydentów (np. „kto z kim rozmawiał”, „kiedy”, „jakim protokołem”, „jak dużo danych”),
* wsparcia threat huntingu,
* walidacji alertów z innych źródeł (EDR/SIEM).

# Pozyskiwanie ruchu sieciowego – metody

## a) Port Mirroring / SPAN

SPAN (Switched Port Analyzer), znany też jako port mirroring, to funkcja przełącznika/routera umożliwiająca skopiowanie ruchu z wybranych portów/VLANów na port docelowy, do którego podpinamy sensor lub analizator. Cisco opisuje to wprost jako mechanizm wysyłania kopii ruchu do interfejsu analizującego.

### Plusy

* Zwykle brak potrzeby fizycznego rozcinania łączy.
* Relatywnie szybkie do wdrożenia w środowiskach enterprise.
* Niskie ryzyko wpływu na ruch produkcyjny przy poprawnej konfiguracji.

### Minusy

* Ryzyko przesycenia portu mirrorującego (utrata pakietów).
* Zależność od konfiguracji i zmian po stronie sieci (np. maintenance).
* W praktyce mniej „pewne” źródło danych niż dobrze dobrany TAP.

Dodatkowo warto pamiętać o wariantach zdalnych (np. ERSPAN), jeśli architektura to wspiera.



## b) Network TAP

TAP to urządzenie wpięte „w tor” transmisji, które tworzy kopię ruchu do celów monitoringu. Warianty pasywne (szczególnie światłowodowe) mogą działać bez zasilania do utrzymania linku, a wiele rozwiązań jest projektowanych tak, by utrata zasilania nie przerywała ruchu produkcyjnego.

### Plusy

* Wysoka wiarygodność danych (mniejsze ryzyko pominięć niż w SPAN).
* Brak możliwości „przypadkowego” wyłączenia zdalnego.
* Zwykle mniej ryzykowna konfiguracja logiczna.

### Minusy

* Wymaga fizycznej ingerencji w infrastrukturę.
* W zależności od typu TAP i medium, trzeba uwzględnić ryzyko operacyjne podczas instalacji.

## c) Zbieranie bezpośrednio na urządzeniach końcowych

To podejście obejmuje:

* agenty hostowe,
* telemetrię systemową i sieciową,
* rozwiązania eBPF/agentless na poziomie hosta (w zależności od platformy).

### Plusy

* Może być jedyną realistyczną opcją w części środowisk chmurowych lub silnie rozproszonych.
* Brak potrzeby specjalnych urządzeń inline.

### Minusy

* Obciążenie hosta.
* Ryzyko sabotażu po przejęciu maszyny.
* Ograniczony wgląd w ruch, który nie przechodzi przez dany host.

Warto rozumieć relację pojęć:

* NSM to szeroka praktyka operacyjna monitorowania bezpieczeństwa w sieci.
* NDR (Network Detection & Response) to kategoria narzędzi, które realizują NSM w sposób zautomatyzowany, zwykle z naciskiem na behawioralną analizę ruchu i wykrywanie anomalii

# Najczęstsze źródła danych

## a) Full packet capture (full content data)

Pełne zrzuty ruchu – każdy pakiet, z nagłówkami i payloadem, zapisywany np. w plikach .pcap / .pcapng. To „złoty standard” dowodu sieciowego, pozwalający odtworzyć całe rozmowy, wyciągać pliki, badać szczegóły ataku itp.

### Plusy

* Maksymalny poziom szczegółowości – można wrócić do dokładnej treści komunikacji.
* Świetne do analizy powłamaniowej / forensics.

### Minusy

* Bardzo duże zużycie przestrzeni dyskowej.
* Ciężkie do automatycznego przetwarzania na dużą skalę – wymaga selekcji, indeksowania, rotacji.

## b) Extracted content

Zrekonstruowane, „wysokopoziomowe” obiekty z ruchu: pliki, obrazy, dokumenty, załączniki, strumienie HTTP itp. Narzędzia NSM/NDR oraz Zeek potrafią automatycznie wyciągać takie artefakty z pełnego ruchu.

### Plusy

* Bezpośredni dostęp do plików / obiektów – można wrzucać do sandboxa, AV, Yary
* Brak problemu z fragmentacją na poziomie pakietów – dostajesz „gotowy” obiekt.

### Minusy

* Rozmiar nadal może być duży (szczególnie przy dużej liczbie pobieranych plików).
* Zwykle brak pełnych danych z niższych warstw (brak pełnego kontekstu L2/L3/L4 – IP/MAC itd. – jeśli nie powiążesz tego z innymi logami).

## c) Session data (flow / connection data)

Dane o przepływach – kto z kim rozmawiał, kiedy, jak długo, ile bajtów/pakietów, jaki protokół, jakie flagi TCP itd. Przykłady: NetFlow/IPFIX, logi z Zeek conn.log.

W literaturze „session data” i „connection data” często używa się zamiennie – np. w Zeek conn.log to klasyczne session/connection data.

### Plusy

* Zajmuje znacznie mniej miejsca niż pełne PCAP, łatwe do indeksowania i analiz hurtowych
* Idealne do szybkiego odpowiadania na pytania typu „kto z kim gadał i jak bardzo”.

### Minusy

* Brak treści przesyłanych danych (nie odtworzysz plików, stron WWW).

## d) Transactional data (transaction data)

Podobne do session data, ale skupione na konkretnej transakcji w warstwie aplikacji (L7): request–response.

Przykłady: logi HTTP/DNS/SMTP, Zeek http.log, dns.log, gdzie jedno zdarzenie opisuje jedno zapytanie i odpowiedź (metoda, URI, kod odpowiedzi, user-agent itd.).

### Plusy

* Mało danych, lekkie i bardzo przydatne analitycznie (widzisz konkretne żądania i odpowiedzi).
* Zwykle zawiera podstawowe informacje z niższych warstw (adresy IP, porty).

### Minusy

* Brak detali z warstw L2/L3/L4 ponad podstawowe pola.
* Nie zobaczysz całego payloadu, tylko streszczenie transakcji.

## e) Statistical data

Dane zagregowane/statystyczne opisujące ruch: rozkład protokołów, liczba sesji w czasie, „top talkers”, histogramy rozmiarów pakietów itp. Przykłady: statystyki z Wiresharka („Statistics”), dane agregowane z narzędzi typu nfdump, capinfos itd. 

### Plusy

* Bardzo mały rozmiar, idealne do trendów, baseline’ów, wykrywania anomalii na wysokim poziomie.
* Ułatwia korelowanie aktywności (np. skok ruchu DNS, nagły wzrost jednego protokołu).

### Minusy

* Brak wglądu w pojedyncze przepływy lub konkretne transakcje – służy raczej do „gdzie kopać dalej”, a nie pełnej analizy.

## g) Metadata

Szeroko rozumiane „dane o danych”, czyli dodatkowy kontekst przypisany do powyższych typów:

* informacje o hoście (asset data, rola systemu, właściciel),
* geolokalizacja IP, informacje o reputacji, tagi z systemów TI,
* identyfikatory użytkowników, systemów, reguł, sensorów itd.
* whois, passive dns, certificate transparency;

### Plusy

* Drastycznie zwiększa wartość analityczną danych - pozwala uzyskać dodatkowe informacje o danej aktywności (łatwiej łączyć fakty i korelować zdarzenia).
* Ułatwia pivotowanie między różnymi typami danych NSM.

### Minusy

* Wymaga spójnego modelu danych i procesów wzbogacania (enrichment), inaczej „śmieci w środku = śmieci na wyjściu”.
* Wymaga integracji z różnymi serwisami

## h) Alarmy

* są kluczowym elementem monitoringu
* dają impuls do rozpoczęcia śledztwa
* mogą być generowana przez IDS bądź narzędia SIEM
* same w sobie nie są wystarczające do skutecznego monitoringu
* posiadają też dużą historyczną wartość

# Kiedy NSM jest najbardziej efektywny

* Jak jest nieszyfrowana komunikacja (niektórzy mówią, że NSM wychodzi z użytku
* Jak mamy dobrze skonfigurowany NSM
* Jak mamy dobrze spozycjonowane czujki

# Umiejscowienie NSM w sieci

* umiejscowienie czujek w sieci mocno wpływa na to co widzimy na monitoringu a co nam umyka
* ruch nie przechodzący przez czujkę nie będzie widoczny
* adresy IP zmodyfikowane przez NAT nie będą widoczne
* serwery proxy również mogą wpływać na brak widoczności IP docelowych i źrodłowych
* jeśli masz zasoby, sensory powinny być przy każdym istotnym punkcie wejścia/wyjścia (ingress/egress)
* W praktyce wybierasz miejsca o największej koncentracji ruchu (traffic convergence), a nie każdy port osobno.

## Krawędź internetu (Internet edge / WAN edge)

Za firewallem / przed firewallem, w zależności od celu:

* przed FW – widzisz cały ruch przychodzący,
* za FW – ruch już przefiltrowany, bliżej realnych hostów.

To podstawowy punkt monitorowania ruchu do/z internetu.

## DMZ i strefy z systemami wystawionymi na zewnątrz

Segment z serwerami www, VPN, reverse proxy itp.

Daje wgląd w ataki na usługi publiczne i ewentualny ruch „przeskakujący” do sieci wewnętrznej.

## Core / agregacja ruchu w sieci wewnętrznej

Przełączniki core / dystrybucyjne, gdzie zbiegają się VLAN-y użytkowników i serwerów.

Pozwala widzieć zarówno ruch „north–south” (do/z internetu) jak i część „east–west” (pomiędzy segmentami).

## Segmenty z systemami krytycznymi

AD, DNS, bazy danych, systemy finansowe, OT/ICS, IoT itd.

CIS rekomenduje umieszczanie pasywnych sensorów szczególnie w pobliżu krytycznych zasobów i stref wysokiego ryzyka, bo tam najczęściej będzie lateral movement.
