# Security Resources & SOC Glossary

Zbiór przydatnych stron, narzędzi, pojęć oraz krótkich notatek pomocnych w nauce cyberbezpieczeństwa, pracy analityka SOC, analizie alertów, OSINT, threat intelligence, phishingu oraz podstawach DFIR.

## Spis treści

* [Materiały do nauki](#materiały-do-nauki)
* [Źródła informacji security](#źródła-informacji-security)
* [Malware analysis i threat intelligence](#malware-analysis-i-threat-intelligence)
* [OSINT](#osint)
* [MITRE i threat-informed defense](#mitre-i-threat-informed-defense)
* [Pojęcia SOC i cyberbezpieczeństwo](#pojęcia-soc-i-cyberbezpieczeństwo)
* [Metryki SOC](#metryki-soc)
* [EDR](#edr)
* [SIEM, Splunk i ELK](#siem-splunk-i-elk)
* [Szybkie akronimy](#szybkie-akronimy)
* [Przydatne tipy — phishing](#przydatne-tipy--phishing)
* [Artykuły](#artykuły)


---

# Materiały do nauki

## Other — to familiarize

| Materiał              | Opis                                                                                              |
| --------------------- | ------------------------------------------------------------------------------------------------- |
| SOC Training Workbook | https://www.scribd.com/document/874669370/SOC-Training-Workbook-15-Simulated-Alerts-With-Analysis |
| All ports Cheat sheet | Ściąga z portów i protokołów sieciowych.                                                          |

---

# Artykuły

| Temat         | Link                                       |
| ------------- | ------------------------------------------ |
| What is OSINT | https://www.varonis.com/blog/what-is-osint |

---

# TryHackMe / lab resources

| Materiał                       | Link                                                | Opis                                                                                                        |
| ------------------------------ | --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| TryHackMe — APT28 Eviction Lab | https://static-labs.tryhackme.cloud/sites/eviction/ | Strona-lab z kontekstem i artefaktami kampanii APT28, przydatna do ćwiczeń analitycznych i budowy detekcji. |

## Best TryHackMe - SOC - rooms

* OSI Model Game
* OSI Model Game - Pro
* OSI Model - Quiz
* TCP Handshake - Practice
* Pyramid of Pain Practice

---

# Źródła informacji security

| Źródło                                  | Link                                                         | Opis                                                                                                                                               |
| --------------------------------------- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Krebs on Security                       | https://krebsonsecurity.com                                  | Blog Briana Krebsa opisujący realne incydenty, cyberprzestępczość, wycieki danych, kampanie phishingowe i działania grup przestępczych.            |
| The Hacker News                         | https://thehackernews.com                                    | Serwis z aktualnościami o podatnościach, kampaniach malware, atakach APT, exploitach oraz bezpieczeństwie aplikacji i infrastruktury.              |
| BleepingComputer                        | https://www.bleepingcomputer.com                             | Portal opisujący aktualne zagrożenia, ransomware, podatności, kampanie phishingowe oraz praktyczne informacje przydatne dla SOC i IR.              |
| The DFIR Report                         | https://thedfirreport.com/                                   | Bardzo wartościowe raporty opisujące prawdziwe włamania krok po kroku: initial access, lateral movement, persistence, C2, exfiltration i detekcje. |
| CISA KEV Catalog                        | https://www.cisa.gov/known-exploited-vulnerabilities-catalog | Katalog podatności aktywnie wykorzystywanych przez atakujących. Przydatny do priorytetyzacji patchowania i threat huntingu.                        |
| BleepingComputer — Supply Chain Attacks | https://www.bleepingcomputer.com/tag/supply-chain-attack/    | Zbiór artykułów dotyczących ataków na łańcuch dostaw, kompromitacji dostawców, bibliotek, aktualizacji i usług zewnętrznych.                       |
| CheckPoint Live Cyber Threat Map        | https://threatmap.checkpoint.com/                            | Interaktywna mapa pokazująca przykładową wizualizację globalnych cyberataków i trendów zagrożeń.                                                   |

---

# Malware analysis i threat intelligence

| Narzędzie / źródło                     | Link                                               | Opis                                                                                                                                                                                     |
| -------------------------------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| MalwareBazaar                          | https://bazaar.abuse.ch/                           | Repozytorium próbek malware i metadanych. Pozwala wyszukiwać próbki po hashach, rodzinach malware, tagach i typach plików. Przydatne do triage, wzbogacania IOC i nauki analizy malware. |
| MalShare                               | https://malshare.com/                              | Serwis umożliwiający wyszukiwanie i pobieranie próbek malware. Przydatny w laboratoriach analizy malware oraz przy porównywaniu hashy i rodzin zagrożeń.                                 |
| SOC Prime Threat Detection Marketplace | https://tdm.socprime.com/signup                    | Marketplace reguł detekcyjnych dla SIEM/EDR, w tym reguł Sigma. Przydatny do tworzenia i mapowania detekcji do MITRE ATT&CK.                                                             |
| ssdeep                                 | https://ssdeep-project.github.io/ssdeep/index.html | Narzędzie do fuzzy hashy, czyli porównywania podobieństwa plików. Pomaga grupować podobne próbki malware, nawet jeśli różnią się klasycznym hashem.                                      |
| OPSWAT MetaDefender Cloud              | https://metadefender.opswat.com/?lang=en           | Platforma do wielosilnikowego skanowania plików, URL i hashy. Przydatna do szybkiej oceny reputacji artefaktów.                                                                          |

---

# OSINT

| Narzędzie / źródło | Link                                     | Opis                                                                                                                                                   |
| ------------------ | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| OSINT Framework    | https://osintframework.com/              | Katalog narzędzi OSINT pogrupowanych według kategorii, np. domeny, adresy e-mail, social media, infrastruktura, malware i threat intelligence.         |
| Hunter.io          | https://hunter.io/                       | Narzędzie do wyszukiwania i weryfikacji adresów e-mail powiązanych z domeną. Przydatne przy analizie kampanii phishingowych i rozpoznaniu organizacji. |
| theHarvester       | https://github.com/laramies/theHarvester | Narzędzie OSINT do enumeracji domen, subdomen, adresów e-mail i innych artefaktów z wielu publicznych źródeł.                                          |
| ARIN               | https://www.arin.net/                    | Regional Internet Registry dla Ameryki Północnej. Przydatny do sprawdzania właścicieli adresów IP, zakresów sieci i informacji WHOIS.                  |

---

# MITRE i threat-informed defense

| Źródło                                   | Link                                                                              | Opis                                                                                                                                   |
| ---------------------------------------- | --------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| MITRE ATT&CK                             | https://attack.mitre.org/                                                         | Baza taktyk, technik i procedur atakujących. Standard używany do mapowania alertów, raportów, luk detekcyjnych i aktywności adversary. |
| MITRE D3FEND                             | https://d3fend.mitre.org/                                                         | Baza defensywnych technik bezpieczeństwa. Pomaga łączyć techniki ataku z możliwymi działaniami obronnymi.                              |
| MITRE CTID — Adversary Emulation Library | https://ctid.mitre.org/resources/adversary-emulation-library/                     | Biblioteka planów emulacji działań przeciwników. Przydatna do purple teamingu i walidacji detekcji.                                    |
| GitHub — Adversary Emulation Library     | https://github.com/center-for-threat-informed-defense/adversary_emulation_library | Repozytorium z materiałami MITRE CTID do emulacji zachowań grup zagrożeń.                                                              |
| MITRE ATLAS                              | https://atlas.mitre.org/                                                          | Baza wiedzy dotycząca ataków na systemy AI i machine learning.                                                                         |
| MITRE AADAPT                             | https://aadapt.mitre.org/                                                         | Zasoby MITRE związane z analizą i modelowaniem działań adversary.                                                                      |
| MITRE CALDERA                            | https://caldera.mitre.org/                                                        | Platforma do automatyzacji emulacji przeciwnika, testowania detekcji i ćwiczeń purple team.                                            |

---

# Pojęcia SOC i cyberbezpieczeństwo

## Mitigation — zapobieganie / ograniczanie skutków

Mitigation oznacza działania, których celem jest zapobieganie atakom lub ograniczenie ich skutków.

Przykłady:

* rozwiązania antyphishingowe,
* antywirusy,
* EDR,
* szkolenia użytkowników,
* polityki bezpieczeństwa,
* hardening systemów,
* segmentacja sieci.

---

## Detection — detekcja

Detection oznacza wykrywanie zagrożeń, które ominęły zabezpieczenia prewencyjne.

Przykłady źródeł detekcji:

* SIEM,
* EDR,
* IDS/IPS,
* logi systemowe,
* logi aplikacyjne,
* reguły Sigma/YARA/Snort,
* alerty z threat intelligence.

---

## EDR — Endpoint Detection and Response

EDR to narzędzie do monitorowania, wykrywania i reagowania na zagrożenia na urządzeniach końcowych, takich jak:

* laptopy,
* stacje robocze,
* serwery.

EDR zbiera dane o procesach, plikach, rejestrze, połączeniach sieciowych i działaniach użytkowników, a następnie pomaga analitykowi wykrywać oraz badać podejrzaną aktywność.

---

## Website defacement — podmiana witryny

Website defacement to atak na stronę internetową polegający na zmianie jej wyglądu lub zawartości.

Najczęściej oznacza, że atakujący uzyskał dostęp do serwera lub panelu administracyjnego i zastąpił oryginalną treść własnym komunikatem, grafiką lub złośliwym kodem.

Często występuje jako forma:

* hacktywizmu,
* cyberwandalizmu,
* demonstracji dostępu do systemu,
* kompromitacji publicznego serwisu [WWW](http://WWW).

---

## Supply Chain Attack — atak na łańcuch dostaw

Supply Chain Attack polega na kompromitacji aplikacji, biblioteki, aktualizacji lub usługi, której ufa wiele organizacji lub użytkowników.

Typowy przebieg:

1. Atakujący przejmuje komponent używany przez wiele ofiar.
2. Modyfikuje aplikację, bibliotekę lub mechanizm aktualizacji.
3. Użytkownicy instalują zainfekowaną wersję, ponieważ ufają dostawcy.
4. Malware trafia do wielu środowisk jednocześnie.

Przykłady:

* SolarWinds,
* 3CX.

---

## Zero-Day Attack — atak dnia zero

Zero-day to atak wykorzystujący podatność nieznaną producentowi lub taką, dla której nie istnieje jeszcze poprawka.

Cechy:

* luka nie jest publicznie załatana,
* tradycyjne zabezpieczenia mogą jej nie rozpoznawać,
* atakujący ma przewagę czasową,
* organizacje nie mają prostego sposobu na aktualizację systemu.

Przykłady:

* CVE-2021-44228 — Log4Shell,
* CVE-2019-0797 — zero-day w Windows,
* CVE-2020-0601 — CurveBall w Windows CryptoAPI.

---

## Misconfiguration — miskonfiguracja

Misconfiguration oznacza błędną konfigurację systemu, aplikacji, usługi lub infrastruktury, która tworzy lukę bezpieczeństwa.

Przykłady:

* otwarte porty,
* domyślne hasła,
* publicznie dostępne bucket storage,
* nadmierne uprawnienia,
* brak MFA,
* błędna konfiguracja CORS,
* brak aktualizacji,
* niebezpieczne ustawienia chmurowe.

---

## IDOR — Insecure Direct Object Reference

IDOR oznacza niezabezpieczone bezpośrednie odwołanie do obiektu.

Podatność występuje, gdy aplikacja pozwala użytkownikowi uzyskać dostęp do zasobu tylko przez zmianę identyfikatora, bez poprawnej kontroli uprawnień po stronie serwera.

Przykład:

```text
/invoice?id=123
/invoice?id=124
```

Jeżeli użytkownik może zobaczyć cudzą fakturę po zmianie `id`, aplikacja jest podatna na IDOR.

IDOR jest częścią kategorii Broken Access Control w OWASP Top 10.

---

## API — Application Programming Interface

API to interfejs umożliwiający komunikację między aplikacjami, systemami lub usługami.

Pozwala korzystać z funkcji lub danych systemu bez znajomości jego wewnętrznej implementacji.

### Internal API

API używane wewnątrz organizacji.

Zastosowanie:

* komunikacja między mikroserwisami,
* integracja wewnętrznych systemów,
* automatyzacja procesów,
* komunikacja backend-backend.

### External API

API udostępnione partnerom lub publicznie.

Wymaga szczególnej ochrony:

* autoryzacji,
* uwierzytelniania,
* limitów zapytań,
* walidacji danych,
* monitoringu,
* rate limitingu.

---

## True Positive

True Positive oznacza, że system bezpieczeństwa poprawnie wykrył realne zagrożenie.

Przykład:

EDR zgłasza malware na hoście i analiza potwierdza, że złośliwy plik rzeczywiście został uruchomiony.

---

## False Positive

False Positive oznacza, że system wygenerował alert mimo braku realnego zagrożenia.

Przykład:

Antywirus oznacza legalny plik jako podejrzany, mimo że plik jest bezpieczny.

---

## SOAR — Security Orchestration, Automation and Response

SOAR to technologia wspierająca automatyzację i koordynację działań zespołów bezpieczeństwa.

SOAR pomaga:

* automatyzować powtarzalne czynności,
* łączyć dane z wielu narzędzi,
* obsługiwać alerty według playbooków,
* przyspieszać reakcję na incydenty,
* standaryzować działania SOC,
* wspierać incident management i threat intelligence.

---

## 5W Investigation

Metoda 5W pomaga uporządkować analizę alertu.

| Pytanie       | Znaczenie                                                                  |
| ------------- | -------------------------------------------------------------------------- |
| Who / Kto     | Który użytkownik zalogował się, uruchomił polecenie lub pobrał plik        |
| What / Co     | Jakie dokładne działanie lub sekwencja zdarzeń zostały wykonane            |
| When / Kiedy  | Kiedy rozpoczęła się i zakończyła podejrzana aktywność                     |
| Where / Gdzie | Jakie urządzenie, adres IP lub strona internetowa były powiązane z alertem |
| Why / Czemu   | Uzasadnienie końcowego werdyktu analityka                                  |

Najważniejsze jest pytanie `Why`, ponieważ pokazuje tok rozumowania i argumenty stojące za decyzją.

---

## DFIR — Digital Forensics and Incident Response

DFIR oznacza informatykę śledczą i reagowanie na incydenty.

Obejmuje:

* zabezpieczanie dowodów,
* analizę systemów,
* analizę logów,
* analizę malware,
* odtwarzanie timeline,
* ustalanie przyczyny incydentu,
* containment,
* eradication,
* recovery,
* raport końcowy.

---

## Asset Inventory / Asset Lookup — wykaz aktywów

Asset inventory to lista zasobów organizacji.

Może obejmować:

* hosty,
* serwery,
* adresy IP,
* użytkowników,
* aplikacje,
* właścicieli systemów,
* krytyczność zasobów,
* lokalizację,
* role biznesowe.

Dla SOC asset inventory jest ważny, ponieważ pomaga określić, czy alert dotyczy zwykłej stacji roboczej, krytycznego serwera, kontrolera domeny czy systemu produkcyjnego.

---

## Fuzzy hashing — hashowanie podobieństwa

Fuzzy hashing to technika tworzenia odcisku pliku w taki sposób, aby można było ocenić podobieństwo dwóch plików, nawet jeśli nie są identyczne bajt po bajcie.

Klasyczne hashe, takie jak SHA-256, odpowiadają na pytanie:

```text
Czy to dokładnie ten sam plik?
```

Fuzzy hash odpowiada na pytanie:

```text
Czy te pliki są do siebie podobne?
```

Przykład:

Dwa dokumenty Word mogą zawierać tę samą złośliwą logikę makra, ale różnić się tytułem, kilkoma stringami lub dodatkowymi bajtami. SHA-256 będzie inny, ale fuzzy hash może wskazać wysokie podobieństwo.

---

# Metryki SOC

| Metryka               | Tłumaczenie                  | Skrót / wzór                               | Co opisuje                                                          |
| --------------------- | ---------------------------- | ------------------------------------------ | ------------------------------------------------------------------- |
| Alerts Count          | Liczba alertów               | `AC = całkowita liczba odebranych alertów` | Łączne obciążenie analityków SOC.                                   |
| False Positive Rate   | Wskaźnik fałszywych alarmów  | `FPR = False Positives / Total Alerts`     | Poziom szumu w alertach. Pokazuje, ile alertów jest niezasadnych.   |
| Alert Escalation Rate | Wskaźnik eskalacji alertów   | `AER = Escalated Alerts / Total Alerts`    | Pokazuje, ile spraw wymaga przekazania do wyższego poziomu analizy. |
| Threat Detection Rate | Wskaźnik wykrywania zagrożeń | `TDR = Detected Threats / Total Threats`   | Skuteczność zespołu SOC w wykrywaniu realnych zagrożeń.             |

---

# EDR

EDR — Endpoint Detection and Response — to zaawansowane rozwiązanie bezpieczeństwa służące do monitorowania, wykrywania i reagowania na zagrożenia na endpointach.

## Przykładowe rozwiązania EDR

* CrowdStrike Falcon,
* SentinelOne ActiveEDR,
* Microsoft Defender for Endpoint,
* OpenEDR,
* Symantec EDR.

## Co zbiera EDR

EDR może zbierać między innymi:

* procesy,
* drzewo procesów,
* argumenty linii poleceń,
* zmiany w rejestrze,
* modyfikacje plików,
* aktywność użytkowników,
* połączenia sieciowe,
* uruchamiane skrypty,
* zdarzenia związane z persystencją.

## Co daje EDR analitykowi

EDR prezentuje dane w uporządkowanej formie, np.:

* drzewo procesów,
* timeline aktywności,
* historia endpointu,
* powiązane IOC,
* alerty behawioralne,
* mapowanie do MITRE ATT&CK.

## Typowe mechanizmy detekcji EDR

* wykrywanie behawioralne,
* wykrywanie anomalii,
* dopasowywanie IOC,
* mapowanie do MITRE ATT&CK,
* machine learning,
* analiza pamięci,
* analiza procesów,
* analiza fileless malware.

## Telemetry — telemetria

Telemetria może być traktowana jak czarna skrzynka endpointu.

Zawiera dane potrzebne do:

* wykrywania zagrożeń,
* prowadzenia śledztwa,
* analizy timeline,
* korelacji zdarzeń,
* odtworzenia aktywności atakującego.

---

## Lateral Movement — ruch boczny

Lateral movement oznacza przemieszczanie się atakującego pomiędzy maszynami w sieci.

Po uzyskaniu dostępu do jednego hosta atakujący może próbować:

* przejąć kolejne konta,
* dostać się do innych hostów,
* uzyskać dostęp do serwerów,
* dotrzeć do kontrolera domeny,
* wykraść dane,
* utrzymać obecność w środowisku.

---

# SIEM, Splunk i ELK

## Parsing — parsowanie

Parsing oznacza rozbijanie surowego loga na pola.

Przykład pól:

* timestamp,
* user,
* src_ip,
* dst_ip,
* event_id,
* status,
* process_name,
* hostname.

Parsowanie pozwala łatwiej wyszukiwać, filtrować i korelować zdarzenia.

---

## Splunk

Splunk to platforma służąca do zbierania, indeksowania, wyszukiwania i analizy logów.

### Splunk Forwarder

Agent instalowany na hoście.

Zadanie:

* zbiera dane,
* monitoruje pliki logów,
* przesyła dane do Splunka.

### Splunk Indexer

Komponent odpowiedzialny za:

* odbiór danych,
* parsowanie,
* indeksowanie,
* przechowywanie danych,
* przygotowanie ich do wyszukiwania.

### Splunk Search Head

Interfejs użytkownika, w którym analityk może wyszukiwać dane za pomocą języka SPL.

Najczęściej używana aplikacja:

```text
Search & Reporting
```

---

## ELK / Elastic Stack

ELK, czyli Elastic Stack, to zestaw narzędzi do zbierania, przechowywania, wyszukiwania i wizualizacji dużych ilości danych.

Pierwotnie był używany głównie do monitorowania aplikacji, ale obecnie jest też stosowany w SOC jako elastyczna platforma analizy zdarzeń bezpieczeństwa.

## Komponenty Elastic Stack

| Komponent     | Opis                                                          |
| ------------- | ------------------------------------------------------------- |
| Elasticsearch | Silnik wyszukiwania i przechowywania danych.                  |
| Logstash      | Pipeline do przetwarzania, filtrowania i wzbogacania logów.   |
| Beats         | Lekkie agenty do zbierania i wysyłania danych z hostów.       |
| Kibana        | Interfejs do wizualizacji danych, dashboardów i wyszukiwania. |

---

# Szybkie akronimy

| Akronim       | Rozwinięcie                               | Opis                                                                               |
| ------------- | ----------------------------------------- | ---------------------------------------------------------------------------------- |
| OSI           | Open Systems Interconnection              | Model opisujący komunikację sieciową w siedmiu warstwach.                          |
| Encapsulation | Enkapsulacja                              | Dodawanie kolejnych nagłówków do danych podczas przechodzenia przez warstwy sieci. |
| Binary        | Dwójkowy                                  | System liczbowy oparty na wartościach 0 i 1.                                       |
| MAC           | Media Access Control                      | Adres sprzętowy interfejsu sieciowego.                                             |
| NIC           | Network Interface Card                    | Karta sieciowa.                                                                    |
| OSPF          | Open Shortest Path First                  | Protokół routingu, nowszy i szybszy niż RIP.                                       |
| RIP           | Routing Information Protocol              | Starszy protokół routingu oparty na liczbie przeskoków.                            |
| TCP           | Transmission Control Protocol             | Protokół połączeniowy zapewniający niezawodną transmisję danych.                   |
| UDP           | User Datagram Protocol                    | Protokół bezpołączeniowy, szybszy, ale bez gwarancji dostarczenia.                 |
| SIEM          | Security Information and Event Management | System do zbierania, korelacji i analizy zdarzeń bezpieczeństwa.                   |

---

# Przydatne tipy — phishing

## 1. Analizuj phishing kity i ich pliki

Jeżeli w zadaniu masz dostęp do phishing kitu, np. pliku `.zip` lub `.tar`, rozpakuj go w środowisku laboratoryjnym i przeskanuj pliki pod kątem adresów e-mail.

Przykład:

```bash
grep -r '@' .
```

Szczególnie sprawdzaj pliki typu:

* `submit`,
* `send.php`,
* `login.php`,
* `marvid`.

Często znajdują się tam:

* adres e-mail atakującego,
* domeny odbierające dane,
* webhooki,
* panele phishingowe,
* logi z przechwyconymi danymi.

---

## 2. Sprawdzaj linki i katalogi na domenie

Adresy URL z phishing maila często są bardzo dobrym źródłem informacji.

W bezpiecznym środowisku możesz sprawdzić strukturę ścieżek.

Przykład:

```text
http://fakewebsite.me/data/
http://fakewebsite.me/
```

W autoryzowanych laboratoriach można wykonać delikatne sprawdzenie katalogu:

```bash
curl http://fakewebsite.me/data/
```

Możliwe znaleziska:

* lista plików,
* logi,
* `log.txt`,
* `result.txt`,
* kopie formularzy,
* konfiguracje phishing kitu.

---

## 3. Czytaj dokładnie nagłówki wiadomości

Pola widoczne w kliencie poczty, takie jak `From` i `To`, nie wystarczają.

Należy sprawdzić pełne nagłówki wiadomości.

Szczególnie ważne pola:

| Pole        | Znaczenie                                                    |
| ----------- | ------------------------------------------------------------ |
| Return-Path | Adres zwrotny, często inny niż From.                         |
| Reply-To    | Adres, na który trafi odpowiedź użytkownika.                 |
| Received    | Ścieżka serwerów, przez które przechodziła wiadomość.        |
| SPF         | Weryfikacja uprawnienia serwera do wysyłki w imieniu domeny. |
| DKIM        | Podpis kryptograficzny wiadomości.                           |
| DMARC       | Polityka domeny dotycząca obsługi SPF i DKIM.                |

W CTF-ach oraz zadaniach szkoleniowych odpowiedzi często ukryte są w mniej oczywistych nagłówkach.

---

## 4. Szukaj ukrytych lub zakodowanych adresów i linków

Phisherzy często maskują informacje.

Sprawdzaj:

* różnicę między tekstem linku a faktycznym `href`,
* ciągi Base64,
* komentarze HTML,
* ukryte pola formularza,
* stopki wiadomości,
* osadzone skrypty.

Przykład dekodowania Base64:

```bash
echo 'aHR0cDovL2V4YW1wbGUuY29tLw==' | base64 -d
```

---

## 5. Analizuj załączniki pod kątem metadanych i ścieżek

Jeżeli phishing mail ma załącznik, np.:

* `.docx`,
* `.pdf`,
* `.html`,
* `.xls`,
* `.zip`,

należy przeanalizować go w środowisku laboratoryjnym.

Sprawdzenie typu pliku:

```bash
file suspicious.docx
```

Wyciąganie tekstu i metadanych:

```bash
strings suspicious.docx | grep -i '@'
```

Warto szukać:

* makr,
* osadzonych linków,
* metadanych dokumentu,
* adresów e-mail,
* domen C2,
* ścieżek do paneli phishingowych,
* ukrytych formularzy.


# Dodatkowe linki techniczne

| Źródło                         | Link                                             | Opis                                                        |
| ------------------------------ | ------------------------------------------------ | ----------------------------------------------------------- |
| Wireshark SMTP Display Filters | https://www.wireshark.org/docs/dfref/s/smtp.html | Lista pól i filtrów Wiresharka dla SMTP.                    |
| SMTP Codes                     | https://www.mailersend.com/blog/smtp-codes       | Opis kodów odpowiedzi SMTP.                                 |
| Wireshark IMF Display Filters  | https://www.wireshark.org/docs/dfref/i/imf.html  | Lista pól i filtrów Wiresharka dla Internet Message Format. |
