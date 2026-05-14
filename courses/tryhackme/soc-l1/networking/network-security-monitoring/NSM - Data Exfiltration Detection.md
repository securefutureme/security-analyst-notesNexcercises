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
