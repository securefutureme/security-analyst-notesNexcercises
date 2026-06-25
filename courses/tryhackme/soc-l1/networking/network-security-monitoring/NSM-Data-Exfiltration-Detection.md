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
### Aktorzy zagrożeń i ich techniki eksfiltracji

| Threat Actor / Campaign    | Technika eksfiltracji                               | Opis                                                                                                             |
| -------------------------- | --------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| **APT29 (Cozy Bear)**      | **HTTPS przez legalne domeny**                      | Zaszyfrowane kanały HTTPS były używane do eksfiltracji danych z sieci rządowych.                                 |
| **FIN7**                   | **HTTP POST do serwerów C2**                        | Skradzione dane były osadzane w żądaniach HTTP POST, aby utrudnić wykrycie.                                      |
| **Lunar Spider (Zloader)** | **Szyfrowane kanały C2**                            | Atak utrzymywano przez około dwa miesiące, wykorzystując szyfrowane kanały i etapowe przygotowanie eksfiltracji. |
| **DarkSide Ransomware**    | **Podwójne wymuszenie: szyfrowanie + eksfiltracja** | Dane były kradzione przed zaszyfrowaniem systemów, a następnie atakujący grozili ich publicznym ujawnieniem.     |
| **APT10 (Cloud Hopper)**   | **Transfer chmura-do-chmury**                       | Dane były wykradane od dostawców usług zarządzanych z użyciem interfejsów API usług chmurowych.                  |
#### Typowe fazy związane z eksfiltracją:
##### Discovery / Collection
Atakujący lokalizuje wrażliwe pliki.
##### Staging / Compression
Atakujący agreguje, kompresuje, szyfruje albo koduje pliki, np. przy użyciu ZIP, RAR, 7z, tar, base64 lub steganografii.
##### Exfiltration transport
Transfer odbywa się przez sieć, nośniki wymienne, chmurę albo ukryte kanały komunikacji.
##### Comand & Control (C2) coordination
Kanał C2 koordynuje transfer i potwierdza jego odebranie.
## Techniki i wskaźniki

Wykrywanie eksfiltracji wymaga korelowania wskaźników z poziomu hosta i sieci, takich jak nietypowo duże lub częste transfery wychodzące, długie lub wysokozmiennościowe zapytania DNS, podejrzane linie poleceń procesów i połączenia sieciowe, aktywność API pamięci chmurowych, zdarzenia związane z nośnikami wymiennymi. Skuteczny triage SOC L1 koncentruje się na:

- hoście źródłowym / użytkowniku
- celu transferu
- wolumenie przesłanych danych
- tożsamości procesu / linii poleceń
- dowodach wspierających z logów proxy, DNS, flow, hosta i chmury

| Technika                           | Przykłady                                                                                                                                                                                                 | Główne wskaźniki ataku                                                                                                                        | Gdzie szukać                                                                                                             |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| **Sieciowe**                       | HTTP/HTTPS do S3, Azure Blob, webmaila; FTP/SFTP/SCP; tunelowanie DNS; ICMP i inne ukryte protokoły; własne TCP/UDP                                                                                       | Duże żądania POST, uploady do chmury, wysoki wolumen danych do jednego IP / ASN, skoki ruchu wychodzącego, długie nazwy hostów, zapytania TXT | Logi **proxy / web gateway**, **firewall / NGFW**, **NetFlow**, **DNS**                                                  |
| **Host-based**                     | PowerShell / Invoke-WebRequest, rclone, awscli, curl/wget, tworzenie archiwów ZIP/RAR, użycie nośników USB, ADS / ukryte strumienie                                                                       | Podejrzane procesy, połączenia sieciowe z hosta, tworzenie archiwów, odczyty plików przed połączeniem wychodzącym, użycie nośników wymiennych | **Sysmon / EDR**, **Windows Security** (4663/4656), **auditd**, historia shella w Linuxie, zdarzenia nośników wymiennych |
| **Eksfiltracja chmurowa**          | S3 PutObject / multipart upload, Azure Blob uploads, Google Cloud Storage `objects.insert`, zewnętrzne udostępnienia Drive / SharePoint                                                                   | Nietypowe uploady do storage’u, aktywność spoza normy dla kont usługowych, podejrzane adresy IP, niestandardowe operacje API                  | **CloudTrail**, **Azure Activity**, **GCP Audit Logs**, logi dostępu do storage’u                                        |
| **Ukryte techniki i kodowanie**    | Tunelowanie DNS, base64, chunked encoding, steganografia w obrazach / audio, dzielenie plików na wiele małych żądań (_low-and-slow_)                                                                      | Długie lub nietypowe zapytania DNS, wiele małych POST-ów, przerywane uploady, wzorce sugerujące ukrywanie danych                              | Logi **DNS**, logi **proxy**, korelacja z aktywnością procesów na hoście                                                 |
| **Insider i narzędzia współpracy** | Slack, Teams, Dropbox, Google Drive, Box; udostępnienia do użytkowników zewnętrznych; przejęte konta pracowników                                                                                          | Nietypowe udostępnienia, masowe pobrania, wysyłka plików poza organizację, aktywność z niecodziennych kont lub lokalizacji                    | Logi **audytowe**, zdarzenia udostępnień, logi pobrań plików, logi pocztowe                                              |
| **Ogólne IoA i sygnały triage**    | Duży ruch wychodzący do zewnętrznych IP / domen, nieznane domeny docelowe, podejrzane procesy i linie poleceń, wiele odczytów plików przed połączeniem wychodzącym, uploady wieloczęściowe / strumieniowe | Duży wolumen danych wychodzących, nietypowe cele komunikacji, korelacja odczytu plików z transferem, podejrzane procesy                       | Korelacja: **Proxy**, **Firewall**, **NetFlow**, **DNS**, **Sysmon / EDR** (Event ID 1/3/11), logi serwerów pocztowych   |

Eksfiltracja danych to zagrożenie o wysokim wpływie, które łączy metody oportunistyczne, legalne narzędzia oraz kreatywne ukryte kanały komunikacji w celu wyniesienia wrażliwych zasobów poza organizację. Skuteczna detekcja zależy mniej od pojedynczych alertów, a bardziej od szybkiej korelacji telemetryki hostowej, sieciowej i chmurowej, aby ustalić:

- kto uzyskał dostęp do danych
- co zostało przesłane
- w jaki sposób dane przygotowano do transferu
- dokąd zostały wysłane

### Trudne pojęcia

- **Eksfiltracja danych** – nieautoryzowane wynoszenie danych poza organizację.

- **Insider** – osoba z wewnątrz organizacji, która celowo lub nieumyślnie uczestniczy w naruszeniu bezpieczeństwa.

- **Dark web** – ukryta część Internetu, często wykorzystywana do nielegalnego handlu danymi i usługami.

- **Proxy / Web Gateway** – system pośredniczący w ruchu WWW, który może logować i filtrować transfery.

- **NGFW** – nowoczesny firewall oferujący bardziej zaawansowaną analizę niż klasyczna zapora.

- **Netflow** – dane podsumowujące komunikację sieciową, np. źródło, cel, czas trwania i wolumen.

- **Sysmon** – narzędzie rejestrujące szczegółowe zdarzenia systemowe i procesowe w Windows.

- **Auditd** – mechanizm audytu w systemach Linux.

- **ADS** (Alternate Data Streams) – alternatywne strumienie danych w NTFS, które mogą być używane do ukrywania informacji.

- **CloudTrail / Azure Activity / GCP Audit** – logi audytowe aktywności w usługach chmurowych AWS, Azure i Google Cloud.

- **IoA (Indicators of Attack)** – wskaźniki zachowań sugerujące aktywny atak, a nie tylko pojedynczy artefakt.

- **ASN** – autonomiczny system sieciowy identyfikujący operatora lub dużą sieć w Internecie.

- **Low-and-slow** – technika działania powoli i małymi porcjami, aby utrudnić wykrycie.


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
Można także szukać podejrzanych plików, filtrując po rozszerzeniach, takich jak: **PDF, csv, TXT**

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

Zadania

Ile połączeń było zaobserwowanych z konta gościa?

**ftp contains "guest"**

Zastosuj filtr; jaka jest nazwa pliku związanego z klientami, który został wyeksfiltrowany z konta root?

**ftp && frame.len > 90** -> Szukamy po FTP -> STOR -> nazwa pliku

Który wewnętrzny adres IP został wykryty jako wysyłający największy ładunek danych do zewnętrznego adresu IP?

**ftp && frame.len > 90** -> szukamy najwiekszej długości pakietu

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/30-image.png)

Jaka flaga jest ukryta w strumieniu FTP przesyłającym plik CSV do podejrzanego adresu IP?

**ftp contains "STOR" -> Szukamy po FTP -> DATA** 


# Eksfiltracja danych przez HTTP

**Eksfiltracja danych przez HTTP** polega na tym, że atakujący wyprowadza wrażliwe dane z sieci ofiary, używając **HTTP** jako kanału transportowego. HTTP jest często nadużywany, ponieważ **wtapia się w normalny ruch webowy**, może przechodzić przez **firewalle i proxy**, a dodatkowo może być **ukrywany** poprzez kodowanie, szyfrowanie lub tunelowanie.

To zadanie detekcyjne ma nauczyć analityków **SOC**, jak rozpoznawać oznaki eksfiltracji opartej na HTTP w:

- przechwyceniach pakietów (**Wireshark**)
- logach (**Splunk**)

oraz jak używać praktycznych zapytań i kroków dochodzeniowych.

## Dlaczego to jest ważne

- HTTP jest bardzo powszechny, więc atakujący ukrywają eksfiltrację w szumie legalnego ruchu webowego.
- Skuteczna detekcja pozwala zatrzymać wyciek danych i odtworzyć działania atakującego po kompromitacji.
- Organizacje muszą wykrywać i obsługiwać takie incydenty, aby chronić wrażliwe dane i spełniać wymagania compliance.

## Jak przeciwnicy wykorzystują HTTP do eksfiltracji danych

**POST uploads do zewnętrznych serwerów**  
Duże ilości danych są wysyłane do hostów kontrolowanych przez atakującego albo do pamięci chmurowych w treści żądań **POST**.

**GET requests z zakodowanymi danymi**  
Atakujący umieszcza małe fragmenty danych w **query stringach** albo segmentach ścieżki URL, co jest przydatne przy powolnej eksfiltracji typu **low-and-slow**.

**Wykorzystanie popularnych usług / CDN**  
Eksfiltracja jest ukrywana jako upload do popularnych usług albo do subdomen kontrolowanych przez atakującego pod wiarygodnie wyglądającymi domenami.

**Custom headers**  
Dane są umieszczane w nagłówkach, np. `X-Data: <base64>`, co może ominąć niektóre mechanizmy DLP oparte wyłącznie na prostym dopasowaniu ciągów znaków.

**Chunked transfer / multipart**  
Duże payloady są dzielone na wiele żądań, aby nie przekroczyć progów wykrywania opartych na rozmiarze.

**HTTPS/TLS tunneling**  
Szyfrowany kanał ukrywa właściwy payload. Wykrycie wymaga inspekcji TLS, analizy **SNI** albo detekcji opartej na metadanych.

**Staging przez usługi chmurowe**  
Atakujący wysyła dane np. do **Dropbox, GitHub, Gist**, a następnie pobiera je z zewnątrz.

**Przeciwnicy się dostosowują**  
Stosują podejście **low-and-slow**, szyfrowanie, kodowanie i legalne usługi, aby utrudnić wykrycie.

---
## Wskaźniki ataku (_IoAs_)

**Typowe wskaźniki sieciowe:**

- nietypowo duże żądania **HTTP POST** do zewnętrznych lub nieoczekiwanych hostów
- żądania HTTP do domen o **niskiej reputacji** albo rzadko spotykanych w normalnym ruchu
- częste małe żądania (_beaconing_) do tego samego hosta, po których następują duże uploady
- transfery **chunked** albo **multipart**, gdzie wiele żądań razem tworzy większy plik
### Analiza logów w Splunku

Aby rozpocząć, użyj następującego zapytania i upewnij się, że zakres czasu ustawiony jest na **All Time**

```
index="data_exfil" sourcetype="http_logs"
```

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/31-image.png)

To zapytanie pokaże logi typu `http_logs`. Ponieważ eksfiltracja może być realizowana przez metodę **POST**, zawężamy wyniki:

```
index="data_exfil" sourcetype="http_logs" method=POST
```

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/32-image.png)


Aby sprawdzić średnią, maksymalną i minimalną liczbę bajtów wysyłanych do poszczególnych domen, użyj:

```
index="data_exfil" sourcetype="http_logs" method=POST | stats count avg(bytes_sent) max(bytes_sent) min(bytes_sent) by domain | sort - count
```

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/33-image.png)

To pomaga zidentyfikować domeny, do których wysyłane są **duże ilości danych**.

**Odfiltrowanie legalnego ruchu i izolacja dużych payloadów POST**

Aby wyświetlić tylko żądania POST z większym payloadem, użyj:

```
index="data_exfil" sourcetype="http_logs" method=POST bytes_sent > 600 | table _time src_ip uri domain dst_ip bytes_sent | sort - bytes_sent
```

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/34-image.png)

Dotychczasowa analiza wskazuje na **jeden podejrzany wpis**, w którym duży fragment danych został wysłany do zewnętrznego źródła. Następnie należy skorelować to z plikiem PCAP.

### Analiza ruchu sieciowego - Filtrowanie ruchu HTTP

Najpierw zastosuj filtr na cały ruch HTTP:

| Notes                                                                                                   | Wireshark Filter |
| ------------------------------------------------------------------------------------------------------- | ---------------- |
| **Filtrowanie całego ruchu HTTP** – pokazuje wszystkie żądania i odpowiedzi HTTP w przechwyconym ruchu. | `http`           |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/35-image.png)

W wynikach widoczny jest ruch HTTP zawierający zarówno żądania **GET**, jak i **POST**.
### Filtrowanie żądań POST

Aby wyświetlić tylko żądania POST, użyj:

| Notes                                                                                               | Wireshark Filter                |
| --------------------------------------------------------------------------------------------------- | ------------------------------- |
| **Filtrowanie żądań POST** – pomaga skupić się na transferach, które mogą zawierać przesyłane dane. | `http.request.method == "POST"` |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/36-image.png)

### Filtrowanie żądań POST o większej długości ramki

Aby zawęzić wyniki do większych transferów, użyj:

| Notes                                                                                             | Wireshark Filter                                    |
| ------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| **POST z długością ramki większą niż 500** – pomaga ograniczyć liczbę wyników do większych żądań. | `http.request.method == "POST" and frame.len > 500` |
![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/37-image.png)

Nadal może być widoczny spory szum, więc warto zwiększyć próg.
### Dalsze zawężenie do dużych ramek

Zastosuj bardziej restrykcyjny filtr:

| Notes                                                                                                  | Wireshark Filter                                    |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------- |
| **POST z długością ramki większą niż 750** – pozwala wyłapać najbardziej podejrzane duże żądania HTTP. | `http.request.method == "POST" and frame.len > 750` |

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/38-image.png)

Ten filtr pokazuje już tylko **jeden wpis**, który wygląda tak samo jak ten znaleziony wcześniej w Splunku.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/39-image.png)

Następnie należy przejść do **HTTP Stream**, aby zobaczyć zawartość przesyłanego pliku.

**Zadania:**

**Który wewnętrzny, skompromitowany host został użyty do eksfiltracji tych wrażliwych danych?**

Do sprawdzenia tego musimy udać się do Wiresharka i zaaplikować "http.request.method == "POST" and frame.len > 750".

Odp. 192.168.1.103

**Jaka flaga jest ukryta w wyeksfiltrowanych danych?**

Follow -> HTTP Stream

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/40-image.png)

**Odp. THM{http_raw_3xf1ltr4t10n_succ3ss}**

# Eksfiltracja danych przez ICMP

**ICMP** to protokół warstwy sieciowej używany do diagnostyki i kontroli, np. przez **ping** lub komunikaty **TTL exceeded**. Ponieważ jest on często dozwolony przez firewalle i zwykle sprawdzany mniej rygorystycznie niż **TCP/UDP**, atakujący czasami wykorzystują go do **tunelowania** i **eksfiltracji danych**. Złośliwi aktorzy kodują dane w **payloadach ICMP** (np. echo request/reply, timestamp, info) i wysyłają je do zdalnego odbiorcy, którego kontrolują.

### Jak przeciwnicy wykorzystują ICMP do eksfiltracji

#### Najczęstsze techniki

**Tunelowanie w ICMP echo (type 8) / reply (type 0)**  
Atakujący umieszczają zakodowane fragmenty plików, np. w formacie **base64** albo **hex**, wewnątrz payloadu ICMP. Zdalny serwer zbiera te fragmenty i je dekoduje.

**Własne typy i kody ICMP**  
Wykorzystywane są niestandardowe typy ICMP lub niestandardowe kody, aby ominąć detekcję opartą na sygnaturach.

**Fragmentacja i składanie pakietów**  
Duże payloady są dzielone na wiele pakietów.

**Szyfrowanie i zaciemnianie**  
Payload może być szyfrowany albo kodowany, np. przy użyciu **base64**, żeby wyglądał jak losowe dane.
### Oznaki, że coś może być złośliwe

- utrzymujące się sesje ICMP do zewnętrznego hosta, który nie jest używany do legalnego monitoringu
- nietypowo duże payloady ICMP albo częsty ruch ICMP z payloadem większym niż typowy rozmiar pingu
- payloady ICMP zawierające dane o wysokiej entropii albo wzorce przypominające **base64** lub **hex**
- serie pakietów ICMP, po których nie następuje żaden inny legalny ruch aplikacyjny z tego samego hosta
### Wskaźniki ataku w Wiresharku

Podczas analizy pliku **pcap** w Wiresharku należy zwracać uwagę na:

**Wolumen ruchu ICMP**  
Jeden host wysyła dużą liczbę pakietów **ICMP echo request** do zewnętrznego adresu IP.

**Duży `frame.len` albo duży payload ICMP**  
Pingi z payloadem znacznie większym niż typowy, np. **powyżej 64 bajtów**.

**Nietypowe wartości `type/code`**  
Np. nietypowe użycie komunikatów **timestamp (13/14)** albo niestandardowych kodów.

**Regularność czasowa (periodyczność)**  
Pakiety ICMP wysyłane w równych odstępach czasu, z payloadem o podobnym rozmiarze.

**Fragmenty z ponownym składaniem**  
Wiele fragmentów ICMP pomiędzy tą samą parą adresów źródłowego i docelowego.

### Analiza ruchu

#### Filtrowanie całego ruchu ICMP

Poniższy filtr pokazuje wszystkie pakiety ICMP. Należy zwracać uwagę na **nietypowo częste** albo **duże** pakiety **ICMP Echo Request/Reply**.

**Filter:** `icmp`

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/41-image.png)

#### Izolowanie Echo Request

Następnie należy odfiltrować tylko pakiety **ICMP Echo Request**:

**Filter:** `icmp.type == 8`

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/42-image.png)

#### Analiza dużych pakietów ICMP

Teraz należy zawęzić wyniki do żądań ICMP o długości ramki większej niż 100:

**Filter:** `icmp.type == 8 and frame.len > 100`

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/43-image.png)

To pozwala oznaczyć pakiety z nietypowo dużym payloadem.  
Normalne pakiety **ping** mają zwykle około **74 bajtów** łącznie. Wszystko powyżej **100 bajtów** jest podejrzane.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/44-image.png)

To właściwie wystarcza.

ICMP jest prosty, dlatego każdą anomalię można stosunkowo łatwo wykryć przez analizę **rozmiaru ramki** i sprawdzenie, czy payload jest **większy niż zazwyczaj**.

Zadania:

Jaka flaga może być znaleziona w esfitrowanych danych ICMP?

**Filter**: `icmp.type == 8 and frame.len > 100`

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/45-image.png)

**Odp. THM{1cmp_3ch0_3xf1ltr4t10n_succ3ss}** 
