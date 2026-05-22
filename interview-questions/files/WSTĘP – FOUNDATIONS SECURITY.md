#### Authentication vs authorization (uwierzytelnianie vs autoryzacja)
_**Bardzo popularne pytanie na rozmowach (starter)**_

**Uwierzytelnienie** - wtedy, kiedy udowadniamy, że my to my. W skrócie - proces weryfikacji tożsamości przed przyznaniem dostępu.  
Uwierzytelnianie ma trzy czynniki - to co wiemy (hasło, PIN), to co mamy (token, karta) i to czym jesteś (biometria, rozpoznanie twarzy). Mogą być jedno, dwu albo kilkuskładnikowe (MFA).  
  
**Autoryzacja** - czyli - do czego masz konkretnie dostęp?. W skrócie - określenie poziomu dostępu użytkownika.  
Przykład: admin zwykle ma dostęp do wszystkiego, HR ma tylko dostęp do folderu grupy HR, ale już nie ma do Sales, uczeń może zobaczyć swoje oceny, ale nie innych uczniów, jako klient banku masz dostęp do swojego konta, ale np. nie możesz zmienić już software którego bank używa itd.


#### How do you keep yourself updated with information security? →  Jak dbasz o bieżące aktualizowanie wiedzy z zakresu bezpieczeństwa informacji?  

Tutaj możemy mieć kilkanaście opcji do wyboru.  
“Obserwuję niebezpiecznika na różnych kanałach, w tym na ich stronie, czytał artykuły z HackerNews i HackRead”  
TIP: Można poczytać kilka artykułów przed rozmową żeby bardziej być w temacie.



#### What are Black Hat, White Hat and Gray Hat Hackers? → Kim są hakerzy typu black hat, white hat i gray hat?  
Hakerzy black hat to zwykle hakerzy, którzy się włamują do systemów nielegalnie, bez pozwolenia, wykorzystując znane podatności lub zero-daye. Zwykle są tymi “złymi” hakerami, włamując się do systemów dla swojego zysku.

Hakerzy white hat to hakerzy, którzy pracują legalnie i włamują się do systemów za pozwoleniem firmy, by potem robić z tego raporty, które będą miały na celu poprawę bezpieczeństwa serwerów/stron/aplikacji. Zwykle są certyfikowani - znani też jako etyczni hakerzy.  
  
Gray hat to hakerzy, którzy są mieszanką czarnych i białych - włamują się do systemów nielegalnie, ale nie robią tego ze złych zamiarów - nie są wynajęci, ale włamują się do systemów, by potem przekazywać te informacje do firm (za drobną opłatą) by załatać podatność (coś jak Bounty Hunter).

#### Do you know any programming language? →  Czy znasz jakiś język programowania?    
**TIP:** przy tym pytaniu lepiej odpowiedzieć zgodnie z obecnym stanem znajomości języków programowania.

#### How can you define Blue Team and Red Team basically? →  Jak w podstawowy sposób zdefiniujesz Blue Team i Red Team?  

Blue Team to drużyna “broniąca” a Red Team “atakująca” systemy informatyczne.  

#### Explain Vulnerability, Risk and Threat →  Wyjaśnij różnicę między: podatnością (vulnerability), ryzykiem (risk) i zagrożeniem (threat).
    
Podatność to “słabość” czy też “luka” w systemie, w ich procedurach, w kontrolach zarządczych czy też w implementacji - która może być wykorzystana i wyeksploatowana przez hakerów.  
Ryzyko to duże będa skutki, jeśli zagrożenie będzie realne (wpływ na biznes/operacje) oraz jak bardzo jest prawdopodobne, że do tego dojdzie  
Zagrożenie to każda sytuacja, która może realnie zaszkodzić organizacji czy ludziom bo ktoś wykorzystał system w niewłaściwy sposób (uzyska dostęp do uprawnień których nie powinien mieć, zniszczy dane itp.)

#### What is compliance? - Czym jest compliance (zgodność z wymaganiami/standardami)?  

Compliance jak sama nazwa wskazuje, jest to działanie w wymaganiami, które obowiązują w danej firmie albo gdy narzuca je regulacja czy rząd. Są to polityki, procedury i kontrole które muszą wdrożone.  

#### What is MITRE ATT&CK? -> Czym jest MITRE ATT&CK?  
Jest to globalne knowledge base która opisuje jak atakujący operują w praktyce - jakie mają cele/taktyki i jakie mają techniki, są one oparte na rzeczywistych obserwacjach kampanii atakujących. W SOC używamy je jako język do modelowania zagrożeń, mapowania detekcji, opisu incydentów czy też analizy luk w kontrolach/detekcjach.  
      
#### Do you have any project that we can look at? →  Czy masz projekt, który możemy obejrzeć / przeanalizować?  
TIP: najlepiej wymienić te projekty, które mają jakieś odzwierciedlenie dla pozycji na którą startujesz.

#### Could you share some general endpoint security product categories? → Podaj podstawowe kategorie produktów do ochrony endpointów.  
Antiwirus, EDR (Endpoint Detection and Response), XDR(Extended Detection and Response) , DLP (Data Loss Prevention), ale też Firewall czy MDM.  
      
#### What is CIA triad? →  
Czym jest triada CIA?  
Jest to podstawowy model w cybersecurity, używanych przy dla ochrony systemów i informacji.  

C to confidentiality, czyli dostęp do danych mają określone osoby;  
I to Integrity czyli że dane są poprawne i nie zostały zmienione w sposób nieautoryzowany;  
A to Availability czyli dane i usługi są dostępne wtedy, kiedy są potrzebne dla uprawnionych użytkowników;  

Jakie przykłady w cyberbezpieczeństwie byś wymienił dla każdego z nich?  

**Confidentiality** - środki kontrolne np. Least privelige, MFA, szyfrowanie dysku, segmentacja sieci  
**Integrity**  - mogą być to np. mechanizmy kontroli danych (checksum). change management (bo dobrze zrobiony zapobiega niekontrolowanym zmianom)  
**Availability** - jako środki kontrolne możemy dać? Backupy, ochrona DDoS, Disaster Recovery itp.  
  
#### What is AAA? →  
Czym jest AAA (Authentication, Authorization, Accounting)?  

Autentykacja, autoryzacja i audyt, to model kontroli dostępu. Czyli w zadajemy sobie pytania: kim jest ( ta osoba która chce wejść - hasło, MFA itd.)? do czego ma prawo (role,grupy) ? i co robiła lub zamierza zrobić w systemie (to wiemy poprzez logi). W SOC możemy to podzielić  na:  

Authentication: wykrywanie przejęć kont (nietypowe logowania, MFA fatigue, impossible travel).  
Authorization: wykrywanie nadużyć uprawnień (eskalacja, dostęp do zasobów spoza roli).  
Accounting: rekonstrukcja zdarzeń w incydencie (timeline, co zostało dotknięte/wykradzione).  

#### What is Cyber Kill Chain? →  
Czym jest model Cyber Kill Chain?  

Model Cyber Kill Chain, jest to model etapów ataku na endpoint/system, który opisuje drogę atakującego - od rozpoznania do celu, np. w pierwszej fazie mamy rekonesans, czyli atakujący zbiera informację, prowadząc OSINT, social engineering etc., następnie atakujący dostarcza malware/payload  np. poprzez phishing/USB. Po tej fazie zwykle następuje wykonanie złego na kodzie ofiary, i w dalszych procesach uruchomienie dalszych faz np. C2, poprzez połączenie się z hostem atakującego. Po tej fazie atakujący zwykle eksploatuje system ofiary do swoich celów. W SOC używamy tego by jak najszybciej przerwać ten “łańcuch”, najlepiej przed fazą dostarczania (wykrywanie phishingu), lub też wykrywamy exploita przez nietypowe procesy, albo odcinamy C2 po anomaliach DNS/proxy  

#### What is OSINT?→  
Czym jest OSTINT?  

**OSINT** - czyli Open Source Inteligence, jest to tzw. biały wywiad, czyli zebranie wszystkich informacji na temat ofiary, za pomocą ogólnie dostępnych informacji w internecie. Może być to zebranie danych z portali społecznościowych, for, baz danych czy mediów. Jest to zwykle etyczne działanie, praktykowane przez detektywów, dziennikarzy itp.  

#### Explain True Positive and False Positive. →  
Wyjaśnij pojęcia: True Positive i False Positive.

**True Positive** - w luźnym znaczeniu jest to “prawdziwie pozytywny”, czyli taki alert albo sygnał, który jeżeli został wywołany przez jakąś regułę, jest realnym zagrożeniem. Czyli np. jeżeli mamy regułę na SQL injection, i faktycznie alert został wygenerowany przez wykonanie prawdziwego adresu URL z payloadem w środku. (np. ma w sobie OR 1=1)  
  
**False Positive** - “fałszywie pozytywny” czyli fałszywy alarm. W skrócie, jest to alert, który został wygenerowany np. przez regułę, ale jest ona czymś spodziewanym, i ten alert nie niesie za sobą żadnego zagrożenia. Np. brute force alert wywołany przez zwykłego użytkownika po wpisaniu kilka razy błędnego hasła.

#### What is the difference between SOC L1 and L2?. →  
Jaka byś wytłumaczył różnicę pomiędzy SOC L1 a L2?  

L1 to pierwsza linia obrony. Obserwują kolejkę w poszukiwaniu alertów i przez to “filtrują” szum od realnych problemów. Zajmują się wyłapywaniem false positive, by odciążyć L2. Zbierają podstawowe IoC do alertów i eskalują problemy, które wyglądają poważnie.  

L2 to następna linia obrony - bada incydenty, łączy fakty, ocenia ryzyko zagrożenia i szuka przyczyny. Prowadzi trudniejsze incydenty, wykonuje działania prewencyjne i naprawcze w obliczu zagrożenia.  
    
#### What is the difference between event, alert and incident? →  
Jaka jest różnica między eventem, alertem i incidentem?  

**Event** (wydarzenie - zwykle zaplanowane) - jest to każde zarejestrowane zdarzenie w systemie, i nie musi oznaczać zagrożenia, np. logowanie, uruchomienie procesu, błąd usługi, usługa została uruchomiona.  

**Alert** (powiadomienie) -event lub zestaw eventów, które spełniły regułę i zostały uznane za podejrzane lub warte uwagi, np. 10 nieudanych logowań w 2 minuty, wykrycie malware przez EDR, logowanie z nietypowej lokalizacji.  

**Incident** - (zdarzenie - niespodziewane) - potwierdzone naruszenie bezpieczeństwa albo realny problem wymagający obsługi, np. konto zostało przejęte, ktoś wykradł dane z serwera, stacja robocza została zainfekowana ransomware.  
#### What would you describe “defence in depth”? →  
Jakbyś opisał “defense in depth (dogłębna/warstwowa obrona)”?  

**Defence in depth** to sposób działania, gdzie nie polegamy tylko na jednym zabezpieczeniu, tylko budujemy kilka warstw ochronnych.  
Jeżeli jedna warstwa zawiedzie - kolejne mogą dalej utrudnić, wykryć lub zatrzymać atak.  
Przykłady to np. w firmie możemy mieć kilka takich warstw: firewall (który blokuje niechciany ruch z sieci), SIEM (wykrwanie incidentów), MFA (utrudnia przejęcie konta) itd.  


#### What is the principle of least privilege, and where does it most often “break” in practice? → 
Co to jest zasada najmniejszych uprawnień (least privilege) i gdzie najczęściej “wywala się” w praktyce?

Least privilege jest jak zasada ograniczonego zaufania - każdy użytkownik, system, aplikacja albo konto serwisowe dostaje tylko takie uprawnienia, jakie są niezbędne do jego funkcjonowania - żadne inne uprawnienia nie wchodzą w grę.  
Ogranicza to skutki błędów, przejęcia kont, nadużyć czy też malware. Z założenia mało dostępu - mała szanse dla atakującego na rozszerzenia pola działań.  
Najczęściej “wywala się” w codziennej praktykach i złych nawykach: zbyt szerokie prawa użytkowników, wspólne konta, brak porządków po zmianach ról, API/tokeny z pełnymi uprawnieniami itp. 

#### How do you communicate with the system owner when you need to quickly confirm “is this normal behavior”?→  
Jak komunikujesz się z ownerem systemu, kiedy potrzebujesz szybko potwierdzić „czy to normalne zachowanie”?  

"Witam, jestem SOC Analyst, widzę nietypowe zachowanie na serwerze/aplikacji i potrzebuję potwierdzenia, czy jest to zaplanowana aktywność.” - następnie podaję twarde fakty (co się wydarzyło, kiedy, host). 

Np. “Cześć, mamy alert z hosta PL-12332. O 10:14 uruchomiono cmd.exe z parametrami pobierającymi plik z wewnętrznego zasobu sieciowego. Użytkownik: k.woźniak. Czy to element normalnej administracji lub wdrożenia?”

#### What information would you consider ‘must have’ before closing an alert as a false positive →  
Jakie informacje uznałbyś za konieczne, zanim zamkniesz alert jako false positive?  

Nie zamykam alertu jako false positive, dopóki nie mam twardych dowodów, takich jak:  
Co wywołało zdarzenie (reguła, IoC, typ detekcji),  
Pełny kontekst zdarzenia (kto, z jakiego hosta, konta, jakie IP, do czego się łączył)  
Czy aktywność jest biznesowo uzasadniona (znane narzędzie, admin task, skaner)  
Potwierdzenie z innych źródeł logów (np. alert z SIEMa, ale potwierdzenie z VPN logs, EDR, firewall, maile)  
Brak innych znaków złośliwych działań (np. alert uruchomionego cmd.exe bez innych podejrzanych działań)  
Potwierdzenie historyczne (czy ten użytkownik/host zwykle tak działa)  
Reputacja, czyli upewnienie się np. czy plik który został sklasyfikowany jako malware to nie autentyczny plik systemowy.  

#### What are your sources of knowledge when you encounter a technique/alert you do not know?→  
Jakie są Twoje źródła wiedzy, gdy trafiasz na technikę/alert, którego nie znasz?  
      
W takim przypadku najpierw korzystam ze wszystkich wewnętrznych źródeł, takie jak przeglądanie wcześniejszych incydentów (najszybciej się dowiemy po tym jak ktoś wcześniej rozwiązał zadanie), firmowe “Knowledge Base”. playbooki i runbooki (o ile istnieją), dokumentacja narzędzi, które używam w firmie.  
Następnie sięgam po źródła zewnętrzne, takie jak MITRE ATT&CK (żeby zrozumieć technikę, jeżeli istnieje), VirusTotal (często można się spotkać z opisem do jakiej techniki należy to malware), inne jak Microsoft Learn, Splunk docs itp.  

#### What is telemetry? - 
Co to jest telemetria?  

**Telemetria** jest to ciągłe zbieranie i analiza danych o zdarzeniach IT w czasie rzeczywistym. Pozwala na wykrywanie, monitorowanie oraz analizę zdarzeń użytkowników, co pomaga w detekcji i prewencji ataków.  Zwykle zbieramy dane z EDRów, SIEMów czy NDRów.  

#### What are the typical telemetry sources used in a SOC (without going into Event IDs)? →  
Jakie są typowe źródła telemetrii wykorzystywane w SOC (bez wchodzenia w Event IDs)?

Typowymi źródłami telemetrii są logi systemowe (Linux,Windows), bezpieczeństwa (z EDRów, AV, firewall), sieciowe (z firewalli, routerów), zapytania DNS, proxy, z bram pocztowych, logowania (z AD albo Azure AD), aplikacyjne (błędy aplikacji, nieutoryzowany dostęp), serwerowe, chmurowe, z IDSów i IPSów, z NDRów.
#### How would you explain the difference between a “control” and a “requirement”? → 
Jak wytłumaczysz różnicę między „control” (kontrolą) a „requirement” (wymaganiem)?

Kontrola to jest sposób, w jaki to wymaganie realizujemy albo sprawdzamy.  
Przykład: Szyfrowanie dysków, DLP, ACL-e, segmentacja sieci.  
Wymaganie to jest coś, co musi zostać spełnione.  
Przykład: Dane muszą być chronione przed nieautoryzowanym dostępem.
#### How do you understand “severity” vs “priority” in the context of incidents? →  
Jak rozumiesz „severity” vs „priority” w kontekście incydentów?  

**Severity** - to jak poważny jest incident - czyli jego realny wpływ techniczny i biznesowy.  
**Priority** -  jak szybko i w jakiej kolejności trzeba się nim zająć.

Przykład: Malware na komputerze testowym, odizolowanym od sieci.  
Severity będzie średnie. Priority będzie niskie lub średnie  
Zagrożenie istnieje, ale ryzyko dla organizacji jest ograniczone.  
#### What is an attack surface? →  
Co to jest attack surface?

W krótkich słowach: wszystko, co da się zaatakować. Jest to całkowity zbiór wszystkich rzeczy w IT, przez które atakujący może spróbować dostać się do systemów albo je wykorzystać.  
Przykład: człowiek (social engineering), poczta email (phishing), oprogramowanie (niezałatane podatności)
#### What is a “security baseline”, and who usually maintains it? →  
Co to jest „security baseline” (linia bazowa bezpieczeństwa) i kto go zwykle utrzymuje?

Security baseline jest to bazowy, wymagany zestaw bezpiecznych ustawień konfiguracji dla systemu, urządzenia lub aplikacji. Zwykle narzuca on jak coś powinno być skonfigurowane żeby ograniczyć ryzyko oraz zachować jednolitość w całej organizacji.   
Utrzymywany jest zwykle przez drużyny cyberbezpieczeństwa razem z administratorami systemowymi (IT Operations), dodatkowo GRC (governance, risk management and compliance) pomaga w definiowaniu wymagań.  
  
Przykład: Linux baseline (wyłączony root login po SSH, tylko klucze, auditd/logging)  
Windows workstation baseline: włączony firewall, BitLocker, wyłączone lokalne konto gościa, ograniczone makra Office, automatyczne aktualizacje

#### What do you do if you don’t have enough data to assess an alert (missing logs / missing context)? →  
Co robisz, jeśli nie masz pełnych danych do oceny alertu (brak logów / brak kontekstu)?

Gdybym spotkał się z takim problemem - na pewno bym starał się zweryfikować co tylko się da. Można by było wysłać prośbę o dosłanie logów (do teamów z sieci, sysadminów, endpoint security). Spisałbym co dokładnie brakuje (logi z jakiego źródła?, danych z EDR, informacji o hoście, użytkowniku, czas zdarzenia). Sprawdziłbym dokładnie dostępne narzędzia jak SIEM, EDR, firewall (do których mam dostęp) w poszukiwaniu brakującego kontekstu. Sprawdziłbym też poprzednie alerty. Jeżeli dalej nie miałbym pewności, udokumentował bym te ograniczenia i ocenił ryzyko, a potem wyskalowane do odpowiedniego teamu.

**Przykład: Brak logów z firewalla**

1. Alert mówi o podejrzanym połączeniu wychodzącym, ale nie ma pełnych logów sieciowych.
2. Sprawdzam EDR na stacji, DNS logs, proxy i historię procesu.
3. Jeśli nadal brak potwierdzenia, zaznaczam, że analiza jest ograniczona przez brak telemetry i pytam o dosłanie logów lub eskaluję do zespołu sieciowego.  
#### What is a false negative and why can it be more dangerous than a false positive? →  
Co to jest false negative i dlaczego bywa groźniejszy niż false positive?  

**False negative** (fałszywie negatywny) to przypadek, gdy system mówi, że wszystko jest w porządku, a rzeczywiście zagrożenie istnieje. W skrócie - atak został przeoczony.  
False positive (fałszywie pozytywny) z kolei to przypadek, gdzie system zgłasza problem, ale nic złego się nie dzieje.  
  
**False negative** jest groźniejszy niż false positive dlatego, że daje fałszywe poczucie ochrony. Jako analitycy nie możemy nawet zareagować odpowiednio szybko, bo system nic nie zgłosił, incident trwa, a atakujący może robić co chce.  
  
Przykład false negative: malware działa na stacji roboczej, ale AV/EDR go nie wykrywa, albo nietypowy ruch do C2 wygląda „normalnie” i SIEM nie generuje alertu.  
Przykład false positive: użytkownik loguje się z innej lokalizacji przez VPN i system uznaje to za „impossible travel”.

