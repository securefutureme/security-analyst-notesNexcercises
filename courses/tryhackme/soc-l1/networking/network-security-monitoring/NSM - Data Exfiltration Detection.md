<<<<<<< Updated upstream
## Eksfiltracja danych
Eksfiltracja danych to nieautoryzowane przesyłanie danych z organizacji do zewnętrznego miejsca kontrolowanego przez przeciwnika. Może być działaniem celowym (insider) albo skutkiem działania malware lub przejętych poświadczeń.

Dlaczego przeciwnicy przeprowadzają eksfiltrację danych
Eksfiltracja danych polega na kradzieży wrażliwych informacji z sieci. Przeciwnicy robią to z kilku powodów:

#### Zysk finansowy
Skradzione dane, np. dane kart płatniczych lub dane osobowe, mogą zostać sprzedane w dark webie albo wykorzystane do oszustw.

#### Szpiegostwo
Aktorzy państwowi atakują własność intelektualną, tajemnice handlowe lub dane niejawne, aby uzyskać przewagę strategiczną.

#### Ransomware i wymuszenie
Atakujący kradną dane i grożą ich ujawnieniem, jeśli okup nie zostanie zapłacony.

#### Zakłócenie działania i sabotaż
Niektórzy przeciwnicy chcą zaszkodzić reputacji organizacji albo jej działalności poprzez ujawnienie danych wewnętrznych.

#### Utrzymanie dostępu i rozpoznanie
Wyeksfiltrowane dane pomagają atakującym lepiej zrozumieć środowisko i przygotować kolejne ataki.

#### Aktorzy zagrożeń i ich techniki eksfiltracji

Threat Actor / Campaign	Exfiltration Technique	Description
APT29 (Cozy Bear)	HTTPS przez legalne domeny	Zaszyfrowane kanały HTTPS były wykorzystywane do eksfiltracji danych z sieci rządowych.
FIN7	HTTP POST do serwerów C2	Skradzione dane były osadzane w żądaniach HTTP POST, aby utrudnić wykrycie.
Lunar Spider (Zloader)	Szyfrowane kanały C2	Utrzymywano dwumiesięczne włamanie przy użyciu szyfrowanych kanałów i etapowego przygotowywania eksfiltracji.
DarkSide Ransomware	Podwójne wymuszenie: szyfrowanie + eksfiltracja	Dane były kradzione przed zaszyfrowaniem systemów, a następnie atakujący grozili ich publicznym ujawnieniem.
APT10 (Cloud Hopper)	Transfer chmura-do-chmury	Dane były wykradane od dostawców usług zarządzanych z użyciem interfejsów API chmury.
Typowe fazy związane z eksfiltracją

#### Discovery / Collection
Atakujący lokalizuje wrażliwe pliki.

#### Staging / Compression
Atakujący agreguje, kompresuje, szyfruje albo koduje pliki, np. przy użyciu ZIP, RAR, 7z, tar, base64 lub steganografii.

#### Exfiltration transport
Transfer odbywa się przez sieć, nośniki wymienne, chmurę albo ukryte kanały komunikacji.

#### Command & Control (C2) coordination
Kanał C2 koordynuje transfer i potwierdza jego odebranie.

## Techniki i wskaźniki

Wykrywanie eksfiltracji wymaga korelowania wskaźników z poziomu hosta i sieci, takich jak nietypowo duże lub częste transfery wychodzące, długie lub wysokozmiennościowe zapytania DNS, podejrzane linie poleceń procesów i połączenia sieciowe, aktywność API pamięci chmurowych, zdarzenia związane z nośnikami wymiennymi. Skuteczny triage SOC L1 koncentruje się na:

- hoście źródłowym / użytkowniku
- celu transferu
- wolumenie przesłanych danych
- tożsamości procesu / linii poleceń
- dowodach wspierających z logów proxy, DNS, flow, hosta i chmury


Techniques	Examples	Indicator of Attack & where to look
Sieciowe	Wysyłanie danych przez HTTP/HTTPS do S3 / Azure Blob / webmaila, FTP/SFTP/SCP, tunelowanie DNS, ICMP / ukryte protokoły, własne TCP/UDP	Logi proxy / web gateway (duże POST-y, uploady do endpointów chmurowych), flow z firewalla / NGFW (dużo bajtów do jednego IP / ASN), netflow (skoki i transfery wychodzące), logi DNS (długie hostname’y, zapytania TXT).
Host-based	Powershell / Invoke-WebRequest, rclone, awscli, curl/wget, tworzenie archiwów (zip/rar), użycie nośników USB, ADS / ukryte strumienie	Sysmon / EDR (zdarzenia Process Create, Network Connect, File Create), Windows Security (4663/4656 object access), auditd / historia shella w Linuxie oraz zdarzenia nośników wymiennych.
Eksfiltracja chmurowa	S3 PutObject / multipart upload, uploady Azure Blob, Google Cloud Storage objects.insert, zewnętrzne udostępnienia Drive / SharePoint	CloudTrail / Azure Activity / GCP Audit, logi dostępu do storage’u w chmurze, nietypowa aktywność kont usługowych lub adresów IP.
Ukryte techniki i kodowanie	Tunelowanie DNS, kodowanie base64 lub chunked, steganografia w obrazach / audio, dzielenie plików na wiele małych żądań (low-and-slow)	Logi DNS, logi proxy z wieloma małymi POST-ami, korelacja przerywanych uploadów z podejrzaną aktywnością procesów.
Insider i narzędzia współpracy	Uploady lub udostępnienia przez Slack / Teams / Dropbox / Google Drive / Box do użytkowników zewnętrznych; przejęte konta pracowników	Logi audytowe (zdarzenia udostępniania, pobrania plików) oraz logi pocztowe.
Ogólne IoA i sygnały triage	Duży ruch wychodzący do zewnętrznych IP / domen, nieznane domeny docelowe, podejrzane procesy / linie poleceń, wiele odczytów plików przed połączeniem wychodzącym, uploady wieloczęściowe / strumieniowe	Korelacja: Proxy / Firewall / Netflow, DNS, Sysmon / EDR (EventID 1/3/11), logi serwerów pocztowych.

Eksfiltracja danych to zagrożenie o wysokim wpływie, które łączy metody oportunistyczne, legalne narzędzia oraz kreatywne ukryte kanały komunikacji w celu wyniesienia wrażliwych zasobów poza organizację. Skuteczna detekcja zależy mniej od pojedynczych alertów, a bardziej od szybkiej korelacji telemetryki hostowej, sieciowej i chmurowej, aby ustalić:

- kto uzyskał dostęp do danych
- co zostało przesłane
- w jaki sposób dane przygotowano do transferu
- dokąd zostały wysłane

Wyjaśnienie trudnych pojęć

Eksfiltracja danych – nieautoryzowane wynoszenie danych poza organizację.

- Insider – osoba z wewnątrz organizacji, która celowo lub nieumyślnie uczestniczy w naruszeniu bezpieczeństwa.

- Dark web – ukryta część Internetu, często wykorzystywana do nielegalnego handlu danymi i usługami.

- Proxy / Web Gateway – system pośredniczący w ruchu WWW, który może logować i filtrować transfery.

- NGFW – nowoczesny firewall oferujący bardziej zaawansowaną analizę niż klasyczna zapora.

- Netflow – dane podsumowujące komunikację sieciową, np. źródło, cel, czas trwania i wolumen.

- Sysmon – narzędzie rejestrujące szczegółowe zdarzenia systemowe i procesowe w Windows.

- Auditd – mechanizm audytu w systemach Linux.

- ADS (Alternate Data Streams) – alternatywne strumienie danych w NTFS, które mogą być używane do ukrywania informacji.

- CloudTrail / Azure Activity / GCP Audit – logi audytowe aktywności w usługach chmurowych AWS, Azure i Google Cloud.

- IoA (Indicators of Attack) – wskaźniki zachowań sugerujące aktywny atak, a nie tylko pojedynczy artefakt.

- ASN – autonomiczny system sieciowy identyfikujący operatora lub dużą sieć w Internecie.

- Low-and-slow – technika działania powoli i małymi porcjami, aby utrudnić wykrycie.
=======

**Eksfiltracja danych** to nieautoryzowane przesyłanie danych z organizacji do zewnętrznego miejsca kontrolowanego przez przeciwnika. Może być działaniem celowym (**insider**) albo skutkiem działania **malware** lub przejętych poświadczeń.

---
# Dlaczego przeciwnicy przeprowadzają eksfiltrację danych

Eksfiltracja danych polega na kradzieży wrażliwych informacji z sieci. Przeciwnicy robią to z kilku powodów:

**Zysk finansowy**  
Skradzione dane, np. dane kart płatniczych lub dane osobowe, mogą zostać sprzedane w dark webie albo wykorzystane do oszustw.

**Szpiegostwo**  
Aktorzy państwowi atakują własność intelektualną, tajemnice handlowe lub dane niejawne, aby uzyskać przewagę strategiczną.

**Ransomware i wymuszenie**  
Atakujący kradną dane i grożą ich ujawnieniem, jeśli okup nie zostanie zapłacony.

**Zakłócenie działania i sabotaż**  
Niektórzy przeciwnicy chcą zaszkodzić reputacji organizacji albo jej działalności poprzez ujawnienie danych wewnętrznych.

**Utrzymanie dostępu i rozpoznanie**  
Wyeksfiltrowane dane pomagają atakującym lepiej zrozumieć środowisko i przygotować kolejne ataki.

---
# Aktorzy zagrożeń i ich techniki eksfiltracji

| Kampania / Threat Actor    | Technika Eksfiltracji                               | Opis                                                                                                          |
| -------------------------- | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **APT29 (Cozy Bear)**      | **HTTPS przez legalne domeny**                      | Zaszyfrowane kanały HTTPS były wykorzystywane do eksfiltracji danych z sieci rządowych.                       |
| **FIN7**                   | **HTTP POST do serwerów C2**                        | Skradzione dane były osadzane w żądaniach HTTP POST, aby utrudnić wykrycie.                                   |
| **Lunar Spider (Zloader)** | **Szyfrowane kanały C2**                            | Utrzymywano dwumiesięczne włamanie przy użyciu szyfrowanych kanałów i etapowego przygotowywania eksfiltracji. |
| **DarkSide Ransomware**    | **Podwójne wymuszenie: szyfrowanie + eksfiltracja** | Dane były kradzione przed zaszyfrowaniem systemów, a następnie atakujący grozili ich publicznym ujawnieniem.  |
| **APT10 (Cloud Hopper)**   | **Transfer chmura-do-chmury**                       | Dane były wykradane od dostawców usług zarządzanych z użyciem interfejsów API chmury.                         |

---
# Typowoe fazy związane z eksfiltracją

**Discovery / Collection**  
Atakujący lokalizuje wrażliwe pliki.

**Staging / Compression**  
Atakujący agreguje, kompresuje, szyfruje albo koduje pliki, np. przy użyciu **ZIP, RAR, 7z, tar, base64** lub **steganografii**.

**Exfiltration transport**  
Transfer odbywa się przez sieć, nośniki wymienne, chmurę albo ukryte kanały komunikacji.

**Command & Control (C2) coordination**  
Kanał C2 koordynuje transfer i potwierdza jego odebranie.

---
# Techniki i wskaźniki

Wykrywanie eksfiltracji wymaga korelowania wskaźników z poziomu hosta i sieci, takich jak **nietypowo duże** lub **częste transfery wychodzące**, długie lub wysokozmiennościowe zapytania DNS, podejrzane linie poleceń procesów i połączenia sieciowe, aktywność API pamięci chmurowych, zdarzenia związane z nośnikami wymiennymi. Skuteczny triage SOC L1 koncentruje się na:

- hoście źródłowym / użytkowniku
- celu transferu
- wolumenie przesłanych danych
- tożsamości procesu / linii poleceń
- dowodach wspierających z logów proxy, DNS, flow, hosta i chmury

| Techniki                           | Przykłady                                                                                                                                                                                                 | IoC & gdzie szukać                                                                                                                                                                                                        |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Sieciowe**                       | Wysyłanie danych przez HTTP/HTTPS do S3 / Azure Blob / webmaila, FTP/SFTP/SCP, tunelowanie DNS, ICMP / ukryte protokoły, własne TCP/UDP                                                                   | Logi proxy / web gateway (duże POST-y, uploady do endpointów chmurowych), flow z firewalla / NGFW (dużo bajtów do jednego IP / ASN), netflow (skoki i transfery wychodzące), logi DNS (długie hostname’y, zapytania TXT). |
| **Host-based**                     | Powershell / Invoke-WebRequest, rclone, awscli, curl/wget, tworzenie archiwów (zip/rar), użycie nośników USB, ADS / ukryte strumienie                                                                     | Sysmon / EDR (zdarzenia Process Create, Network Connect, File Create), Windows Security (4663/4656 object access), auditd / historia shella w Linuxie oraz zdarzenia nośników wymiennych.                                 |
| **Eksfiltracja chmurowa**          | S3 PutObject / multipart upload, uploady Azure Blob, Google Cloud Storage objects.insert, zewnętrzne udostępnienia Drive / SharePoint                                                                     | CloudTrail / Azure Activity / GCP Audit, logi dostępu do storage’u w chmurze, nietypowa aktywność kont usługowych lub adresów IP.                                                                                         |
| **Ukryte techniki i kodowanie**    | Tunelowanie DNS, kodowanie base64 lub chunked, steganografia w obrazach / audio, dzielenie plików na wiele małych żądań (_low-and-slow_)                                                                  | Logi DNS, logi proxy z wieloma małymi POST-ami, korelacja przerywanych uploadów z podejrzaną aktywnością procesów.                                                                                                        |
| **Insider i narzędzia współpracy** | Uploady lub udostępnienia przez Slack / Teams / Dropbox / Google Drive / Box do użytkowników zewnętrznych; przejęte konta pracowników                                                                     | Logi audytowe (zdarzenia udostępniania, pobrania plików) oraz logi pocztowe.                                                                                                                                              |
| **Ogólne IoA i sygnały triage**    | Duży ruch wychodzący do zewnętrznych IP / domen, nieznane domeny docelowe, podejrzane procesy / linie poleceń, wiele odczytów plików przed połączeniem wychodzącym, uploady wieloczęściowe / strumieniowe | Korelacja: Proxy / Firewall / Netflow, DNS, Sysmon / EDR (EventID 1/3/11), logi serwerów pocztowych.                                                                                                                      |

---

Eksfiltracja danych to zagrożenie o **wysokim wpływie**, które łączy metody oportunistyczne, legalne narzędzia oraz kreatywne ukryte kanały komunikacji w celu wyniesienia wrażliwych zasobów poza organizację. Skuteczna detekcja zależy mniej od pojedynczych alertów, a bardziej od **szybkiej korelacji** telemetryki hostowej, sieciowej i chmurowej, aby ustalić:

- kto uzyskał dostęp do danych
- co zostało przesłane
- w jaki sposób dane przygotowano do transferu
- dokąd zostały wysłane

W kolejnych zadaniach zostaną omówione różne techniki wykorzystywane przez przeciwników do eksfiltracji danych oraz wskaźniki, które pomagają odtworzyć ślady ataku.


# Detekcja - Eksfiltracja przez tunelowanie DNS

**Eksfiltracja danych przez DNS** polega na nadużyciu **Domain Name System (DNS)** — protokołu, który normalnie jest dozwolony w sieciach — do przemycania danych zakodowanych wewnątrz zapytań i odpowiedzi DNS, tak aby firewalle i proxy webowe tego nie zauważyły. Ponieważ DNS jest zwykle dozwolony, a często także niefiltrowany albo przekazywany do publicznych resolverów, jest atrakcyjny jako **ukryty kanał komunikacji**.

---
## Tunelowanie DNS

**DNS (Domain Name System)** tłumaczy przyjazne dla człowieka nazwy domen, np. `example.com`, na adresy IP oraz obsługuje inne typy rekordów, takie jak **A, AAAA, TXT, MX, CNAME** itd.
### Kluczowe informacje

- zapytania DNS są **powszechne** — niemal każdy host wykonuje zapytania DNS
- DNS jest zazwyczaj **dozwolony przez firewalle i bramy**, co czyni go atrakcyjnym kanałem ukrytej komunikacji
- DNS używa głównie **UDP na porcie 53** do zapytań i odpowiedzi; **TCP** jest używany np. do transferów stref lub dużych odpowiedzi
### Dlaczego atakujący używają DNS do eksfiltracji

**Usługa zawsze aktywna**  
Zapytania DNS są rutynowe i często dozwolone na ruchu wychodzącym.

**Dobre ukrycie**  
Zapytania wyglądają jak zwykły ruch, jeśli nie są dokładnie analizowane.

**Elastyczny ładunek danych**  
Dane mogą być zakodowane w **subdomenach** albo w odpowiedziach typu **TXT**.

---
### Wskaźniki ataku

Podczas analizy ruchu DNS pod kątem możliwych oznak eksfiltracji danych należy zwracać uwagę na:

- dużą liczbę zapytań DNS wysyłanych do **jednej zewnętrznej domeny**, szczególnie jeśli liczba ta jest bardzo wysoka względem normy
- **długie etykiety subdomen** albo nietypowo długie pełne nazwy zapytań (**powyżej 60–100 znaków**)
- wysoką **entropię** lub wzorce przypominające **Base32 / Base64** w nazwie zapytania, np. dużo mieszanych liter, cyfr, znaków `-` i `=`
- rzadkie typy rekordów, np. **TXT** albo **NULL**, lub wiele dużych odpowiedzi TXT
- nietypowe zachowanie odpowiedzi, np. częste **NXDOMAIN** (gdy atakujący wykorzystuje eksfiltrację przez samo zapytanie, bez udzielania odpowiedzi), albo użycie **TCP / dużych fragmentów UDP** w DNS
- zapytania wysyłane w **regularnych odstępach czasu** (_beaconing_)

---
## Wykrywanie w Wiresharku

Poniżej znajdują się filtry wyświetlania **Wireshark**, komendy **tshark** oraz elementy, na które należy zwracać uwagę podczas analizy pliku `dns_exfil.pcap`.

## Krok 1: filtrowanie ruchu DNS

Najpierw zastosuj filtr na ruch DNS:

| Notes                                                                                    | Wireshark Filter |
| ---------------------------------------------------------------------------------------- | ---------------- |
| **Filtrowanie całego ruchu DNS** – pokazuje wszystkie pakiety DNS w przechwyconym ruchu. | `dns`            |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/11-image.png)

---
## Krok 2: filtrowanie zapytań DNS bez odpowiedzi

Następnie przefiltruj zapytania DNS bez odpowiedzi:

|Notes|Wireshark Filter|
|---|---|
|**Zapytania DNS bez odpowiedzi** – pozwalają zauważyć podejrzane zapytania, które nie otrzymują odpowiedzi, co może wskazywać na tunelowanie lub eksfiltrację.|`dns.flags.response == 0`|

W wynikach można zauważyć niektóre wpisy DNS z **dużą długością zapytania**.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/12-image.png)

---
## Krok 3: wyszukiwanie długich zapytań

Aby zawęzić wyniki, zastosuj filtr oparty na długości ramki:

| Notes                                                                                                        | Wireshark Filter        |
| ------------------------------------------------------------------------------------------------------------ | ----------------------- |
| **Wyszukiwanie długich zapytań DNS** – pomaga wyłapać podejrzane subdomeny i nietypowo długie nazwy zapytań. | `dns && frame.len > 70` |

Wynik pozwala zidentyfikować jedną konkretną **podejrzaną domenę**, która otrzymuje te nietypowo wyglądające zapytania DNS.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/13-image.png)

---
## Krok 4: filtrowanie po podejrzanej domenie

Po zidentyfikowaniu podejrzanej domeny można ją dodatkowo przefiltrować:

| Notes                                                                                                                         | Wireshark Filter                          |
| ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- |
| **Filtrowanie po podejrzanej domenie** – pokazuje wyłącznie ruch DNS związany z wybraną domeną, do której przesyłane są dane. | `dns && dns.qry.name contains <REDACTED>` |

Na tym etapie wygląda na to, że udało się poprawnie zidentyfikować próbę **tunelowania DNS**.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/14-image.png)
### Co można zaobserwować w ruchu sieciowym

- wiele **wewnętrznych hostów** zostało skompromitowanych
- wszystkie te hosty wysyłają dane w **częściach**, wykorzystując techniki tunelowania DNS
- zidentyfikowano **jedną zewnętrzną domenę**, która odbiera te zapytania DNS
## Analiza w Splunku

Otwórz instancję **Splunk** i w pasku wyszukiwania wpisz następujące zapytanie:

```
index=data_exfil sourcetype=DNS_logs
```

To zapytanie pokaże wyniki pasujące do `sourcetype=DNS_logs`.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/15-image.png)
### Na co zwracać uwagę

W logach DNS należy szukać:
- podejrzanie wyglądających domen
- domen z bardzo dużą liczbą zapytań
- aktywności pochodzącej od wielu hostów albo od jednego hosta, jeśli domena jest **niezaufana**
## Statystyki zapytań DNS według źródłowego adresu IP

Aby wyświetlić liczbę zapytań DNS generowanych przez każdy adres źródłowy, użyj:

```
index="data_exfil" sourcetype="DNS_logs" | stats count by src_ip
```

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/16-image.png)

## Identyfikowanie podejrzanych zapytań

Aby zobaczyć statystyki zapytań według samej wartości `query`, użyj:
```
index="data_exfil" sourcetype="dns_logs" | stats count by query | sort -count
```

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/17-image.png)

Wyniki bardzo wyraźnie pokazują **nietypowo wyglądające zapytania DNS** o dużym rozmiarze.
## Na co zwracać uwagę

- pojedyncze hosty generujące znacznie więcej zapytań DNS niż normalnie
- długie nazwy zapytań, wskazujące na **kodowanie danych w subdomenach**
## Filtrowanie długich zapytań

Aby zawęzić wyniki do zapytań dłuższych niż 30 znaków, użyj:

```
index="data_exfil" sourcetype="DNS_logs" | where len(query) > 30
```

To pozwala skutecznie odfiltrować najbardziej podejrzane, nietypowo wyglądające zapytania.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/18-image.png)
# Wnioski

Na podstawie poniższych wskaźników udało się zidentyfikować próby **eksfiltracji danych przez tunelowanie DNS**:

- **duża liczba zapytań DNS bez odpowiedzi**
- **duża długość zapytań DNS**

---
## **Zadania**

**Jaka podejrzana domena odbiera ruch DNS?**

Możemy to sprawdzić i w Wiresharku i w Splunku.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/20-image.png)

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/21-image.png)

Odp. `tunnelcorp.net`

**Ile podejrzanych wpisów ruchu / logów związanych z tunelowaniem DNS zaobserwowano?**

**Search Query:** `index="data_exfil" sourcetype="DNS_logs" | where len(query) > 30`

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/22-image.png)

**Odp. 315**

**Który lokalny adres IP wysłał największą liczbę podejrzanych żądań?**

Po zastosowaniu filtra w Splunku `index="data_exfil" sourcetype="DNS_logs" | where len(query) > 30`  wchodzimy do zakładki **src_ip.**

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/19-image.png)

**Odp: 192.168.1.103**

# Detekcja - Eksfiltracja przez FTP

**FTP (File Transfer Protocol)** to jeden z najstarszych protokołów służących do przesyłania plików pomiędzy klientem a serwerem w sieci **TCP/IP**. Atakujący wykorzystują go do wynoszenia dużych ilości danych z sieci, czasami przy użyciu **przejętych poświadczeń**, **błędnie skonfigurowanych serwerów** albo **tymczasowych kont**. Wykrywanie opiera się na połączeniu **inspekcji pakietów** (tylko FTP), **logów serwera**, **metadanych sesji SSH** oraz **analizy przepływów sieciowych, rozmiaru i wzorców ruchu**.

---
### Jak przeciwnicy wykorzystują FTP do eksfiltracji

- używają legalnych serwerów FTP (publicznych albo błędnie skonfigurowanych serwerów wewnętrznych) do przygotowania i transferu danych
- używają przejętych poświadczeń, np. kont usługowych lub kont użytkowników
- używają niestandardowych portów albo tunelowania, aby ukryć ruch wśród innej komunikacji
### Wskaźniki ataku

Na co zwracać uwagę:

- polecenia **USER** i **PASS** (poświadczenia przesyłane jawnym tekstem)
- polecenia **STOR** (upload) i **RETR** (download): powtarzające się albo duże transfery
- duże połączenia danych do nietypowych zewnętrznych adresów IP, szczególnie poza godzinami pracy
- otwieranie kanału danych na **portach efemerycznych** (**PASV**) połączone z dużym payloadem
## Analiza pliku `ftp-lab.pcap`

#### Izolowanie ruchu kontrolnego i danych FTP

Najpierw należy wyszukać sesje FTP przy użyciu poniższego filtra:

| Notes                                                                                              | Wireshark Filter |
| -------------------------------------------------------------------------------------------------- | ---------------- |
| **Izolowanie ruchu kontrolnego i danych FTP** – pokazuje ruch sterujący FTP oraz kanał danych FTP. | `ftp             |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/23-image.png)

Ten filtr pozwala wyizolować ruch kontrolny FTP.
### Wyszukiwanie poświadczeń

Następnie należy odfiltrować tylko próby logowania z użyciem poleceń **USER** i **PASS**:

| Notes                                                                                      | Wireshark Filter               |
| ------------------------------------------------------------------------------------------ | ------------------------------ |
| **Próby logowania USER/PASS** – pokazuje komendy logowania i hasła przesyłane w sesji FTP. | `ftp.request.command == "USER" |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/24-image.png)

Na podstawie wyników można szukać:

- podejrzanych nazw użytkowników
- słabych haseł

### Wyszukiwanie anomalii w nazwach plików lub poświadczeniach

Aby sprawdzić transfery plików, należy użyć filtra:

| Notes                                                                                | Wireshark Filter      |
| ------------------------------------------------------------------------------------ | --------------------- |
| **Wyszukiwanie polecenia STOR** – pokazuje przypadki wysyłania plików na serwer FTP. | `ftp contains "STOR"` |
|                                                                                      |                       |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/25-image.png)

Następnie kliknij prawym przyciskiem na pakiet i wybierz:

**Follow → TCP Stream**

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/26-image.png)

To pozwala obejrzeć zawartość strumienia TCP i lepiej zrozumieć, jakie dane były przesyłane.

Można także szukać podejrzanych plików, filtrując po rozszerzeniach, takich jak:

- **PDF**
- **csv**
- **TXT**

Przykład filtra dla plików CSV:

|Notes|Wireshark Filter|
|---|---|
|**Wyszukiwanie plików CSV w ruchu FTP** – pomaga zidentyfikować transfery potencjalnie wrażliwych danych tabelarycznych.|`ftp contains "csv"`|
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/27-image.png)

Wyniki pokazują, że podejrzany adres IP połączył się z użyciem konta **Guest** i przesłał pewne wrażliwe pliki **CSV** do podejrzanego zewnętrznego adresu IP.
### Identyfikowanie ruchu z dużym rozmiarem payloadu

Należy sprawdzić ruch o większej długości, używając filtra:

|Notes|Wireshark Filter|
|---|---|
|**Ruch FTP z dużą długością ramki** – pomaga wykrywać większe transfery danych, które mogą zawierać dokumenty lub archiwa.|`ftp && frame.len > 90`|
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/28-image.png)

Następnie należy sprawdzić zawartość w **TCP Stream**.

Wygląda na to, że dokument zawierający **wrażliwe informacje** był przesyłany do zewnętrznego adresu IP. Warto przeanalizować także inne strumienie, aby znaleźć więcej wskaźników świadczących o eksfiltracji wrażliwych dokumentów przez **protokół HTTP**.
>>>>>>> Stashed changes
