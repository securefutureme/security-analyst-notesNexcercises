# INTERVIEW QUESTIONS

## PRESECURITY - 100 PYTAŃ (FUNDAMENTALS, LINUX, WINDOWS, AD, SQL)  


## WSTĘP – NAJWAŻNIEJSZE POJĘCIA I PODSTAWY 

- How do you keep yourself updated with information security? → 
    

Jak dbasz o bieżące aktualizowanie wiedzy z zakresu bezpieczeństwa informacji?  
Tutaj możemy mieć kilkanaście opcji do wyboru.  
“Obserwuję niebezpiecznika na różnych kanałach, w tym na ich stronie, czytał artykuły z HackerNews i HackRead”  
TIP: Można poczytać kilka artykułów przed rozmową żeby bardziej być w temacie.

- Authentication vs authorization (uwierzytelnianie vs autoryzacja)  
    Bardzo popularne pytanie na rozmowach (starter)
    

Uwierzytelnienie - wtedy, kiedy udowadniamy, że my to my. W skrócie - proces weryfikacji tożsamości przed przyznaniem dostępu.  
Uwierzytelnianie ma trzy czynniki - to co wiemy (hasło, PIN), to co mamy (token, karta) i to czym jesteś (biometria, rozpoznanie twarzy). Mogą być jedno, dwu albo kilkuskładnikowe (MFA).  
  
Autoryzacja - czyli - do czego masz konkretnie dostęp?. W skrócie - określenie poziomu dostępu użytkownika.  
Przykład: admin zwykle ma dostęp do wszystkiego, HR ma tylko dostęp do folderu grupy HR, ale już nie ma do Sales, uczeń może zobaczyć swoje oceny, ale nie innych uczniów, jako klient banku masz dostęp do swojego konta, ale np. nie możesz zmienić już software którego bank używa itp.

  
  
  

- What are Black Hat, White Hat and Gray Hat Hackers? → 
    

Kim są hakerzy typu black hat, white hat i gray hat?  
Hakerzy black hat to zwykle hakerzy, którzy się włamują do systemów nielegalnie, bez pozwolenia, wykorzystując znane podatności lub zero-daye. Zwykle są tymi “złymi” hakerami, włamując się do systemów dla swojego zysku.

Hakerzy white hat to hakerzy, którzy pracują legalnie i włamują się do systemów za pozwoleniem firmy, by potem robić z tego raporty, które będą miały na celu poprawę bezpieczeństwa serwerów/stron/aplikacji. Zwykle są certyfikowani - znani też jako etyczni hakerzy.  
  
Gray hat to hakerzy, którzy są mieszanką czarnych i białych - włamują się do systemów nielegalnie, ale nie robią tego ze złych zamiarów - nie są wynajęci, ale włamują się do systemów, by potem przekazywać te informacje do firm (za drobną opłatą) by załatać podatność (coś jak Bounty Hunter).

- Do you know any programming language? →  
    Czy znasz jakiś język programowania?  
    Tutaj lepiej nie zmyślać, powiedzieć że w szkole miałem C++ i podstawy pythona (lata temu). Obecnie bez praktyki.  
      
    
- How can you define Blue Team and Red Team basically? →  
    Jak w podstawowy sposób zdefiniujesz Blue Team i Red Team?  
    Blue Team to drużyna “broniąca” a Red Team “atakująca” systemy informatyczne.  
      
    
- Explain Vulnerability, Risk and Threat →  
    Wyjaśnij różnicę między: podatnością (vulnerability), ryzykiem (risk) i zagrożeniem (threat).
    

Podatność to “słabość” czy też “luka” w systemie, w ich procedurach, w kontrolach zarządczych czy też w implementacji - która może być wykorzystana i wyeksploatowana przez hakerów.  
Ryzyko to duże będa skutki, jeśli zagrożenie będzie realne (wpływ na biznes/operacje) oraz jak bardzo jest prawdopodobne, że do tego dojdzie  
Zagrożenie to każda sytuacja, która może realnie zaszkodzić organizacji czy ludziom bo ktoś wykorzystał system w niewłaściwy sposób (uzyska dostęp do uprawnień których nie powinien mieć, zniszczy dane itp.)

- What is compliance?  
    Czym jest compliance (zgodność z wymaganiami/standardami)?  
    Compliance jak sama nazwa wskazuje, jest to działanie w wymaganiami, które obowiązują w danej firmie albo gdy narzuca je regulacja czy rząd. Są to polityki, procedury i kontrole które muszą wdrożone.  
      
    

  

- What is MITRE ATT&CK?  
    Czym jest MITRE ATT&CK?  
    Jest to globalne knowledge base która opisuje jak atakujący operują w praktyce - jakie mają cele/taktyki i jakie mają techniki, są one oparte na rzeczywistych obserwacjach kampanii atakujących. W SOC używamy je jako język do modelowania zagrożeń, mapowania detekcji, opisu incydentów czy też analizy luk w kontrolach/detekcjach.  
      
    
- Do you have any project that we can look at? →  
    Czy masz projekt, który możemy obejrzeć / przeanalizować?  
    Obecnie (na 14.01) posiadam jeden projekt na GitHubie, w którym analizowałem maile phishingowe.  
      
    
- Could you share some general endpoint security product categories? →  
    Podaj podstawowe kategorie produktów do ochrony endpointów.  
    Antiwirus, EDR (Endpoint Detection and Response), XDR(Extended Detection and Response) , DLP (Data Loss Prevention), ale też Firewall czy MDM.  
      
    
- What is CIA triad? →  
    Czym jest triada CIA?  
    Jest to podstawowy model w cybersecurity, używanych przy dla ochrony systemów i informacji.  
    C to confidentiality, czyli dostęp do danych mają określone osoby;  
    I to Integrity czyli że dane są poprawne i nie zostały zmienione w sposób nieautoryzowany;  
    A to Availability czyli dane i usługi są dostępne wtedy, kiedy są potrzebne dla uprawnionych użytkowników;  
    Jakie przykłady w cyberbezpieczeństwie byś wymienił dla każdego z nich?  
    Confidentiality - środki kontrolne np. Least privelige, MFA, szyfrowanie dysku, segmentacja sieci  
    Integrity  - mogą być to np. mechanizmy kontroli danych (checksum). change management (bo dobrze zrobiony zapobiega niekontrolowanym zmianom)  
    Availability - jako środki kontrolne możemy dać? Backupy, ochrona DDoS, Disaster Recovery itp.  
      
    
- What is AAA? →  
    Czym jest AAA (Authentication, Authorization, Accounting)?  
    Autentykacja, autoryzacja i audyt, to model kontroli dostępu. Czyli w zadajemy sobie pytania: kim jest ( ta osoba która chce wejść - hasło, MFA itd.)? do czego ma prawo (role,grupy) ? i co robiła lub zamierza zrobić w systemie (to wiemy poprzez logi). W SOC możemy to podzielić  na:  
    Authentication: wykrywanie przejęć kont (nietypowe logowania, MFA fatigue, impossible travel).  
    Authorization: wykrywanie nadużyć uprawnień (eskalacja, dostęp do zasobów spoza roli).  
    Accounting: rekonstrukcja zdarzeń w incydencie (timeline, co zostało dotknięte/wykradzione).  
      
    
- What is Cyber Kill Chain? →  
    Czym jest model Cyber Kill Chain?  
    Model Cyber Kill Chain, jest to model etapów ataku na endpoint/system, który opisuje drogę atakującego - od rozpoznania do celu, np. w pierwszej fazie mamy rekonesans, czyli atakujący zbiera informację, prowadząc OSINT, social engineering etc., następnie atakujący dostarcza malware/payload  np. poprzez phishing/USB. Po tej fazie zwykle następuje wykonanie złego na kodzie ofiary, i w dalszych procesach uruchomienie dalszych faz np. C2, poprzez połączenie się z hostem atakującego. Po tej fazie atakujący zwykle eksploatuje system ofiary do swoich celów. W SOC używamy tego by jak najszybciej przerwać ten “łańcuch”, najlepiej przed fazą dostarczania (wykrywanie phishingu), lub też wykrywamy exploita przez nietypowe procesy, albo odcinamy C2 po anomaliach DNS/proxy  
      
    
- What is OSINT?→  
    Czym jest OSTINT?  
    OSINT - czyli Open Source Inteligence, jest to tzw. biały wywiad, czyli zebranie wszystkich informacji na temat ofiary, za pomocą ogólnie dostępnych informacji w internecie. Może być to zebranie danych z portali społecznościowych, for, baz danych czy mediów. Jest to zwykle etyczne działanie, praktykowane przez detektywów, dziennikarzy itp.  
      
    
- Explain True Positive and False Positive. →  
    Wyjaśnij pojęcia: True Positive i False Positive.
    

True Positive - w luźnym znaczeniu jest to “prawdziwie pozytywny”, czyli taki alert albo sygnał, który jeżeli został wywołany przez jakąś regułę, jest realnym zagrożeniem. Czyli np. jeżeli mamy regułę na SQL injection, i faktycznie alert został wygenerowany przez wykonanie prawdziwego adresu URL z payloadem w środku. (np. ma w sobie OR 1=1)  
  
False Positive - “fałszywie pozytywny” czyli fałszywy alarm. W skrócie, jest to alert, który został wygenerowany np. przez regułę, ale jest ona czymś spodziewanym, i ten alert nie niesie za sobą żadnego zagrożenia. Np. brute force alert wywołany przez zwykłego użytkownika po wpisaniu kilka razy błędnego hasła.

- What is the difference between SOC L1 and L2?. →  
    Jaka byś wytłumaczył różnicę pomiędzy L1 a L2?  
      
    L1 to pierwsza linia obrony. Obserwują kolejkę w poszukiwaniu alertów i przez to “filtrują” szum od realnych problemów. Zajmują się wyłapywaniem false positive, by odciążyć L2. Zbierają podstawowe IoC do alertów i eskalują problemy, które wyglądają poważnie.  
      
    L2 to następna linia obrony - bada incydenty, łączy fakty, ocenia ryzyko zagrożenia i szuka przyczyny. Prowadzi trudniejsze incydenty, wykonuje działania prewencyjne i naprawcze w obliczu zagrożenia.  
      
    
- What is the difference between event, alert and incident? →  
    Jaka jest różnica między event, alert i incident?  
      
    Event (wydarzenie - zwykle zaplanowane) - jest to każde zarejestrowane zdarzenie w systemie, i nie musi oznaczać zagrożenia, np. logowanie, uruchomienie procesu, błąd usługi, usługa została uruchomiona.  
    Alert (powiadomienie) -event lub zestaw eventów, które spełniły regułę i zostały uznane za podejrzane lub warte uwagi, np. 10 nieudanych logowań w 2 minuty, wykrycie malware przez EDR, logowanie z nietypowej lokalizacji.  
    Incident - (zdarzenie - niespodziewane) - potwierdzone naruszenie bezpieczeństwa albo realny problem wymagający obsługi, np. konto zostało przejęte, ktoś wykradł dane z serwera, stacja robocza została zainfekowana ransomware.  
      
    
- What would you describe “defence in depth”? →  
    Jakbyś opisał “defense in depth (dogłębna/warstwowa obrona)”?  
    Defence in depth to sposób działania, gdzie nie polegamy tylko na jednym zabezpieczeniu, tylko budujemy kilka warstw ochronnych.  
    Jeżeli jedna warstwa zawiedzie - kolejne mogą dalej utrudnić, wykryć lub zatrzymać atak.  
    Przykłady to np. w firmie możemy mieć kilka takich warstw: firewall (który blokuje niechciany ruch z sieci), SIEM (wykrwanie incidentów), MFA (utrudnia przejęcie konta) itd.  
      
    
- What is the principle of least privilege, and where does it most often “break” in practice? → Co to jest zasada najmniejszych uprawnień (least privilege) i gdzie najczęściej “wywala się” w praktyce?
    

Least privilege jest jak zasada ograniczonego zaufania - każdy użytkownik, system, aplikacja albo konto serwisowe dostaje tylko takie uprawnienia, jakie są niezbędne do jego funkcjonowania - żadne inne uprawnienia nie wchodzą w grę.  
Ogranicza to skutki błędów, przejęcia kont, nadużyć czy też malware. Z założenia mało dostępu - mała szanse dla atakującego na rozszerzenia pola działań.  
Najczęściej “wywala się” w codziennej praktykach i złych nawykach: zbyt szerokie prawa użytkowników, wspólne konta, brak porządków po zmianach ról, API/tokeny z pełnymi uprawnieniami itp. 

- How do you communicate with the system owner when you need to quickly confirm “is this normal behavior”?→  Jak komunikujesz się z ownerem systemu, kiedy potrzebujesz szybko potwierdzić „czy to normalne zachowanie”?  
      
    - “Cześć, widzę nietypowe zachowanie na serwerze/aplikacji i potrzebuję potwierdzenia, czy jest to zaplanowana aktywność.” - następnie podaję twarde fakty (co się wydarzyło, kiedy, host). 
    

Np. “Cześć, mamy alert z hosta PL-12332. O 10:14 uruchomiono cmd.exe z parametrami pobierającymi plik z wewnętrznego zasobu sieciowego. Użytkownik: k.woźniak. Czy to element normalnej administracji lub wdrożenia?”

- What information would you consider ‘must have’ before closing an alert as a false positive →  
    Jakie informacje uznałbyś za konieczne, zanim zamkniesz alert jako false positive?  
      
    Nie zamykam alertu jako false positive, dopóki nie mam twardych dowodów, takich jak:  
    Co wywołało zdarzenie (reguła, IoC, typ detekcji),  
    Pełny kontekst zdarzenia (kto, z jakiego hosta, konta, jakie IP, do czego się łączył)  
    Czy aktywność jest biznesowo uzasadniona (znane narzędzie, admin task, skaner)  
    Potwierdzenie z innych źródeł logów (np. alert z SIEMa, ale potwierdzenie z VPN logs, EDR, firewall, maile)  
    Brak innych znaków złośliwych działań (np. alert uruchomionego cmd.exe bez innych podejrzanych działań)  
    Potwierdzenie historyczne (czy ten użytkownik/host zwykle tak działa)  
    Reputacja, czyli upewnienie się np. czy plik który został sklasyfikowany jako malware to nie autentyczny plik systemowy.  
      
    
- What are your sources of knowledge when you encounter a technique/alert you do not know?→  
    Jakie są Twoje źródła wiedzy, gdy trafiasz na technikę/alert, którego nie znasz?  
      
    W takim przypadku najpierw korzystam ze wszystkich wewnętrznych źródeł, takie jak przeglądanie wcześniejszych incydentów (najszybciej się dowiemy po tym jak ktoś wcześniej rozwiązał zadanie), firmowe “Knowledge Base”. playbooki i runbooki (o ile istnieją), dokumentacja narzędzi, które używam w firmie.  
    Następnie sięgam po źródła zewnętrzne, takie jak MITRE ATT&CK (żeby zrozumieć technikę, jeżeli istnieje), VirusTotal (często można się spotkać z opisem do jakiej techniki należy to malware), inne jak Microsoft Learn, Splunk docs itp.  
      
    
- What is telemetry? - Co to jest telemetria?  
    Telemetria jest to ciągłe zbieranie i analiza danych o zdarzeniach IT w czasie rzeczywistym. Pozwala na wykrywanie, monitorowanie oraz analizę zdarzeń użytkowników, co pomaga w detekcji i prewencji ataków.  Zwykle zbieramy dane z EDRów, SIEMów czy NDRów.  
      
    
- What are the typical telemetry sources used in a SOC (without going into Event IDs)? →  
    Jakie są typowe źródła telemetrii wykorzystywane w SOC (bez wchodzenia w Event IDs)?
    

Typowymi źródłami telemetrii są logi systemowe (Linux,Windows), bezpieczeństwa (z EDRów, AV, firewall), sieciowe (z firewalli, routerów), zapytania DNS, proxy, z bram pocztowych, logowania (z AD albo Azure AD), aplikacyjne (błędy aplikacji, nieutoryzowany dostęp), serwerowe, chmurowe, z IDSów i IPSów, z NDRów.

- How would you explain the difference between a “control” and a “requirement”? →  
    Jak wytłumaczysz różnicę między „control” (kontrolą) a „requirement” (wymaganiem)?
    

Kontrola to jest sposób, w jaki to wymaganie realizujemy albo sprawdzamy.  
Przykład: Szyfrowanie dysków, DLP, ACL-e, segmentacja sieci.  
Wymaganie to jest coś, co musi zostać spełnione.  
Przykład: Dane muszą być chronione przed nieautoryzowanym dostępem.

- How do you understand “severity” vs “priority” in the context of incidents? →  
    Jak rozumiesz „severity” vs „priority” w kontekście incydentów?  
      
    Severity - to jak poważny jest incident - czyli jego realny wpływ techniczny i biznesowy.  
    Priority -  jak szybko i w jakiej kolejności trzeba się nim zająć.  
    Przykład: Malware na komputerze testowym, odizolowanym od sieci.  
    Severity będzie średnie. Priority będzie niskie lub średnie  
    Zagrożenie istnieje, ale ryzyko dla organizacji jest ograniczone.  
      
    
- What is an attack surface? →  
    Co to jest attack surface?
    

W krótkich słowach: wszystko, co da się zaatakować. Jest to całkowity zbiór wszystkich rzeczy w IT, przez które atakujący może spróbować dostać się do systemów albo je wykorzystać.  
Przykład: człowiek (social engineering), poczta email (phishing), oprogramowanie (niezałatane podatności)

- What is a “security baseline”, and who usually maintains it? →  
    Co to jest „security baseline” (linia bazowa bezpieczeństwa) i kto go zwykle utrzymuje?
    

Security baseline jest to bazowy, wymagany zestaw bezpiecznych ustawień konfiguracji dla systemu, urządzenia lub aplikacji. Zwykle narzuca on jak coś powinno być skonfigurowane żeby ograniczyć ryzyko oraz zachować jednolitość w całej organizacji.   
Utrzymywany jest zwykle przez drużyny cyberbezpieczeństwa razem z administratorami systemowymi (IT Operations), dodatkowo GRC (governance, risk management and compliance) pomaga w definiowaniu wymagań.  
  
Przykład: Linux baseline (wyłączony root login po SSH, tylko klucze, auditd/logging)  
Windows workstation baseline: włączony firewall, BitLocker, wyłączone lokalne konto gościa, ograniczone makra Office, automatyczne aktualizacje

- What do you do if you don’t have enough data to assess an alert (missing logs / missing context)? →  
    Co robisz, jeśli nie masz pełnych danych do oceny alertu (brak logów / brak kontekstu)?
    

Gdybym spotkał się z takim problemem - na pewno bym starał się zweryfikować co tylko się da. Można by było wysłać prośbę o dosłanie logów (do teamów z sieci, sysadminów, endpoint security). Spisałbym co dokładnie brakuje (logi z jakiego źródła?, danych z EDR, informacji o hoście, użytkowniku, czas zdarzenia). Sprawdziłbym dokładnie dostępne narzędzia jak SIEM, EDR, firewall (do których mam dostęp) w poszukiwaniu brakującego kontekstu. Sprawdziłbym też poprzednie alerty. Jeżeli dalej nie miałbym pewności, udokumentował bym te ograniczenia i ocenił ryzyko, a potem wyskalowane do odpowiedniego teamu.

Przykład:Brak logów z firewalla

1. Alert mówi o podejrzanym połączeniu wychodzącym, ale nie ma pełnych logów sieciowych.
    
2. Sprawdzam EDR na stacji, DNS logs, proxy i historię procesu.
    
3. Jeśli nadal brak potwierdzenia, zaznaczam, że analiza jest ograniczona przez brak telemetry i pytam o dosłanie logów lub eskaluję do zespołu sieciowego.  
      
    

- What is a false negative and why can it be more dangerous than a false positive? →  
    Co to jest false negative i dlaczego bywa groźniejszy niż false positive?  
      
    False negative (fałszywie negatywny) to przypadek, gdy system mówi, że wszystko jest w porządku, a rzeczywiście zagrożenie istnieje. W skrócie - atak został przeoczony.  
      
    False positive (fałszywie pozytywny) z kolei to przypadek, gdzie system zgłasza problem, ale nic złego się nie dzieje.  
      
    False negative jest groźniejszy niż false positive dlatego, że daje fałszywe poczucie ochrony. Jako analitycy nie możemy nawet zareagować odpowiednio szybko, bo system nic nie zgłosił, incident trwa, a atakujący może robić co chce.  
      
    Przykład false negative: malware działa na stacji roboczej, ale AV/EDR go nie wykrywa, albo nietypowy ruch do C2 wygląda „normalnie” i SIEM nie generuje alertu.  
    Przykład false positive: użytkownik loguje się z innej lokalizacji przez VPN i system uznaje to za „impossible travel”.
    

  
  
  
  
  

## SIECI 

- What is Firewall? → 
    

Czym jest firewall (zapora sieciowa)?  
Firewall jest urządzeniem bądź programem które zawiera zbiór reguł, blokujących lub pozwalających na określony ruch sieciowy.

  

- What is OSI Model? Explain each layer. → 
    

Czym jest model OSI? Omów każdą warstwę.  
Model OSI jest modelem opisowym - w jaki sposób dane przechodzą przez sieć. Każda posiada swoje informacje, czyli nagłówki. Zmiana zerów i jedynek w solidne dane nazywamy enkapsulacją. I odwrotnie, rozbijanie danych na zera i jedynki to dekapsulacja. Dzieli się na 7 warstw:  
  
7. Aplikacji - w tej warstwie jest wszystko to co my widzimy na ekranie, czyli co widzi aplikacja - przeglądarka itp. - mamy tutaj protokoły jak HTTP, SMTP etc.Są tu dane aplikacyjne (data), które występują we wszystkich 3 warstwach od góry.  
  
8. Prezentacji  - tutaj zachodzi wszystkie procesy standaryzacji, żeby było zrozumiane dla wszystkich aplikacji i systemów. Czyli procesy szyfrowania danych, kodowanie, kompresja itp.  
9. Sesji - przy każdym połączeniu musi być i sesja, w tej warstwie jest utrzymywane połączenie logiczne  
  
10. Transportowa - odpowiada za to, jak dane są przesyłane między dwoma urządzeniami, czyli czy chcemy je mieć dokładne i wolne, lub niedokładne i szybkie, mówimy tu o protokołach TCP i UDP, czyli np. TCP będzie wybrane przy pobieraniu danych (i przy TCP mamy wybór odpowiednich portów, HTTP, SMTP), a UDP np. w streamowaniu wideo, gdzie jak pojedyncze piksele nie dotrą, to nic wielkiego się nie stanie. W TCP mamy część danych nazywanych segmentami a w UDP datagramy.  
  
11. Sieciowa - w tej warstwie decyduje się, jaką drogą pakiety dotrą do celu oraz jakie dane są przesyłane pomiędzy sieciami. Komunikacja odbywa się na poziomie adresów IP. Czyli cały routing odbywa się tutaj. Ta warstwa decyduje o wysyłaniu pakietów z adresu źródłowego do adresu docelowego w miarę najkrótszym czasie. Równiez tutaj się odbywa adresacja IP.  
  
12. Łącza danych - tutaj zachodzi komunikacja w tej samej sieci LAN, switche, adresy MAC itp. Jest dodana ramka (frame) z fizycznymi adresami MAC, żeby dane widziały gdzie iść. 

13. Fizyczna - w tej warstwie zachodzi bezpośrednia komunikacja pomiędzy urządzeniami, poprzez kable itp, czyli wymiana bitów pomiędzy urządzeniami.

  
  
  
  

- What is Three-Way Handshake? →
    

Czym jest trzyetapowy handshake (TCP three-way handshake)?

Three-Way handshake to metoda która opisuje wymianę komunikacji pomiędzy hostami, które używają TCP. Three-way, bo ma trzy “segmenty” - klient wysyła segment z flagą SYN (oraz ze swoim numerem ISN), że chce się połączyć, dostaje zwrotkę od hosta B SYN+ACK acknowledge - “przyjęliśmy Twoją prośbe i odsyłamy swój ISN”, a klient odsyła ACK, z potwierdzeniem ISN serwera.Przez to też TCP jest wolniejszy ale bardziej niezawodny, co szybki i stratny UDP. Mniej znane flagi - RST - resetuje połączenie, PSH - push, wymusza przesyłanie pakietu.  
  

- What is TCP/IP Model? Explain the difference between OSI and TCP/IP model. → Czym jest model TCP/IP? Wyjaśnij różnice między modelem OSI a TCP/IP.
    

Model TCP/IP jest modelem praktycznym, który w przeciwieństwie do OSI (modelu referencyjnego), ma realne przełożenie jak dane są przesyłane w Internecie. Przede wszystkim jest zorientowany na zestaw protokołów i stanowi podstawę Internetu. Model OSI pozwala na zrozumienie funkcji - ma charakter dydaktyczny. Przedstawiany jest w czterech warstwach,  
(4)Aplikacyjna - udostępnia użytkownikom możliwość korzystania z usług sieciowych (HTTPS, IMAP, POP3, DNS, SSH)  
(3) Transportowa - której głównym zadaniem jest sprawna obsługa komunikacji pomiędzy urządzeniami,  
(2) Sieciowa - której głównym zadaniem jest znalezienie najkrótszej i najszybszej drogi do urządzenia docelowego przez sieć rozległą,  
(1 ) Dostępu do sieci - kodowanie danych na jezyk maszynowy, przekazywanie do medium transmisyjnego, adresacja (MAC).  
Jakbyśmy mieli porównać modele, OSI rozdziela warstwę aplikacyjną modelu TCP/IP na trzy (aplikacyjną, sesji i prezentacji). Tak samo jak rozdziela dostępu do sieci na dwa - na fizyczną i łącza danych.  
  

- What is ARP? 
    

Czym jest ARP (Address Resolution Protocol)?  
ARP to protokół (łącza danych - data link layer) który powiązuje adresy MAC i IP w jedną całość. Mamy tak zwane ARP cache, jakby “notes wewnętrzny” w którym urządzenie zapisuje które IP odpowiada danemu adresowi MAC. Zwykle działa na zasadzie ARP request (zapytanie) i ARP Reply (odpowiedź).  
W skrócie: urządzenie, żeby wysłać dane do danego IP musi znać adres MAC. Sprawdza swoją tablicę ARP, jeżeli nic tam nie znajduje, wysyła ARP request w broadcascie (do wszystkich urządzeń w sieci lokalnej). Każde urzadzenie otrzymuje zapytanie, ale tylko te właściwe odpowiada ARP Reply. Ta informacja trafia do ARP cache.  
  

- What is DHCP?  
    Czym jest DHCP ?  
    Dynamic Host Configuration Protocol, jest to protokół warstwy aplikacji, odpowiedzialny za dynamiczne przydzielanie adresów IP do hosta. Wyobraźmy sobie, że musimy za każdym razem przydzielać adresy IP naszym kartom sieciowym. DHCP przydziela też maski podsieci, bramę domyślną, serwer DNS itp.  
    Reguła DORA - czyli jak działa DHCP - Discover, Offer, Request, Ack, czyli klient najpierw pyta o serwer DHCP w sieci, potem serwer proponuje adresację, potem klient prosi o przydzielenie tej adresacji, i na koniec dostaje zatwierdzenie od serwera. DHCP przydziela adres na określony czas i host go odnawia  
    W SOC możemy się spotkać z Rogue DHCP (fałszywy serwer może przekierować ruch przez złośliwą bramę).  
    

- Co to jest segmentacja sieci i jaki ma wpływ na bezpieczeństwo?
    

Segmentacja sieci jest nic innego dzieleniem infrastruktury na strefy o różnym poziomie zaufania (strefa DMZ, VLANy itd),  w celu większej kontroli nad nią (poprzez ACL, mikrosegmentację, firewall).  
Ma duży wpływ na bezpieczeństwo, np. ogranicza ruch boczny (nawet jak atak na hosta sie uda, nie będzie tak łatwo się dostać do kolejnego), zmniejsza “pole rażenia” przy ataku, czyli z danej podsieci już nie będzie tak łatwo się dostać dalej, no i też możemy łatwiej kontrolować co się dzieje stawiając punkty kontrolne, jest tak łatwiej logować i przez to analizować co się dzieje podczas ataków.  
  

- Przykład ataku lub problemu, który sklasyfikujesz jako atak na warstwę L3 powiedz po czym to poznasz w logach/pcap.
    

  

- Przykład ataku lub problemu, który sklasyfikujesz jako atak na warstwę L4 powiedz po czym to poznasz w logach/pcap.
    

  

- Przykład ataku lub problemu, który sklasyfikujesz jako atak na warstwę L6 powiedz po czym to poznasz w logach/pcap.
    

  

- Przykład ataku lub problemu, który sklasyfikujesz jako atak na warstwę L7 i powiedz po czym to poznasz w logach/pcap.
    

  

- Przykład ataku lub problemu, który sklasyfikujesz jako atak na warstwę L2 powiedz po czym to poznasz w logach/pcap.
    

  

- How would you describe HTTPS protocol? - Jakbyś opisał protokół HTTPS?  
    Jest to bezpieczniejszy przykład HTTP, który pozwala przeglądarce połączyć się ze stroną. Różnica z HTTP jest taka że ma dodatkową warstwę szyfrowania - dzięki czemu dane jak hasła czy numery kart nie są widoczne dla osób po drodze. HTTPS najpierw tworzy szyfrowane połączenie, a dopiero potem wysyła dane.  
    Przykład: logujemy się do banku. Przy HTTP może podejrzeć dane na tej samej sieci, przy HTTPS są te dane szyfrowane.  
      
    
- Where does the address 127.0.0.1 lead to? - Gdzie prowadzi adres 127.0.0.1?  
    Jest to adres używany do komunikacji komputera z samym sobą (lokalny). Można go użyć do np. połączenia z programem uruchomionym na tym samym komputerze na konkretnym porcie. 
    

  

### PROTOCOLS

##   
PHISHING

## ANALIZA MALWARE I ANALIZA EVENT LOGÓW (15)

- What is the name of the software that compiles written code? → 
    

Jak nazywa się oprogramowanie, które kompiluje kod źródłowy?

Oprogramowanie nazywa się kompilator, czyli tłumaczenie kodu źródłowego na kod maszynowy.  
  

- What is the name of the software that translates machine codes into assembly language? → Jak nazywa się oprogramowanie tłumaczące kod maszynowy na język asemblera?
    

Nazywamy to disassembler, który bierzy kod maszynowy i rekonstruuje go do postaci instrukcji assemblera.  
  

- What is the difference between static and dynamic malware analysis? → 
    

Jaka jest różnica między statyczną a dynamiczną analizą malware?

Analiza statyczna opiera się na analizowaniu próbki nie uruchamiając jej - analizując tylko to co mamy, czyli hashe, typ pliku,  certyfikaty, ciągi znaków (w toolu PEID, strings), czasami dekompilację kodu. Pozwala zidentyfikować typ zagrożenia i jego podstawowe IoC.  
Analiza dynamiczna opiera się na aktywnym wykonaniu kodu w odpowiednim do tego przystosowanym sandboxie i zobaczenie na własne oczy co dokładnie takie malware robi, używając do tego też tooli jak Process Monitor, Process Explorer, Wireshark itp.  
  

- What if malware “bricks  your computer and you are not able to analyze what malware did?  
    Co jeśli malware "zbrickuje" komputer i nie jesteśmy w stanie przeanalizować co taki malware robi?
    

Jako, że takie próbki zawsze testujemy w labowych warunkach, takie jak VM/sandbox z ograniczoną siecią, telemetryką i możliwością snapshot/rollback, są oczywiście sposoby na destrukcyjne malware. 

Jeśli próbka „zbrickuje” system, po prostu cofam snapshot i odtwarzam środowisko, a artefakty zbieram z logów/monitoringu (proc/file/network) oraz z obrazu dysku/pamięci, jeśli zdążyłem je zrzucić.  
Gdy malware celowo niszczy system lub wykrywa VM, robimy analizę statyczną (strings, importy, unpacking) albo odpalamy w innym, bardziej kontrolowanym środowisku (np. odizolowany host, inny hypervisor) i ograniczamy jego uprawnienia, żeby zminimalizować skutki.  
  

  
  
  

- How does malware achieve persistence on Windows? → 
    

W jaki sposób malware uzyskuje trwałość (persistence) w systemie Windows?

Poprzez ustawienie sobie “autostartu” przy uruchamianiu, albo innego mechanizmu przy którym malware będzie startowało przy starcie, np. zaplanowane działania w Task Scheduler, Usługi w Windowsie (services), Folder Startup, GPO w środowiskach domenowych, Run Once w rejestrze HKLM.

  

- Which event logs are available default on Windows?  
    Jakie dzienniki zdarzeń są domyślnie dostępne w systemie Windows?  
      
    
- With which security Event ID can the Successfully RDP connection be detected?  
    Za pomocą jakiego identyfikatora zdarzenia (Event ID) w dzienniku Security można wykryć udane połączenie RDP?  
      
    
- With which event id can failed logons be detected?  
    Za pomocą jakiego identyfikatora zdarzenia (Event ID) można wykryć nieudane logowania?  
      
    
- Which field of which event should I look at so that I can detect RDP logons?  
    Na które pole w jakim zdarzeniu powinienem patrzeć, aby wykryć logowania RDP?
    

  

- Po czym poznasz, że plik jest spakowany/obfuskowany (packer) i co wtedy robisz?
    
- Jak rozpoznasz, że malware wykonuje C2, i jakie IOC zbierzesz?
    

  

- Jak odróżnisz „droppera” od „payloadu”?
    

  

- Jakie różnice w podejściu masz do: trojana, ransomware, infostealera?
    

  

- Jak z logów wyciągniesz: kto, skąd, kiedy, na jakie konto, jakim mechanizmem się zalogował?  
      
    
- Jak rozpoznasz, że to konto jest service account i czy jego zachowanie jest nietypowe?
    

  
  
  
  
  
  
  
  
  
  
  
  
  

### KODOWANIE, HASHOWANIE, KRYPTOGRAFIA

- Explain 2FA. →  
    Wyjaśnij, czym jest 2FA (uwierzytelnianie dwuskładnikowe).  
      
    2FA to uwierzytelnianie dwuskładnikowe, czyli logowanie z użyciem dwóch różnych składników potwierdzających tożsamość. Zwykle jest to: coś co znasz, coś co masz, coś czym jesteś (hasło, kod SMS, odcisk palca).  
      
    
- What are Encoding, Hashing, Encryption? → Czym są: kodowanie (encoding), hashowanie (hashing) i szyfrowanie (encryption)?
    

Encoding (kodowanie) - sposób zamiany danych do innego formatu, żeby systemy mogły je poprawnie przechowywać albo przesyłać.Nie służy do ukrywania informacji. Przykład: Base64.

Hashing (hashowanie) - jednokierunkowe przekształcenie danych do stałej długości skrótu. Nie da się tego normalnie odwrócić. Używa się tego np. do sprawdzania integralności albo przechowywania haseł. Przykład: SHA-256.

Encryption (szyfrowanie) - zabezpieczanie danych tak, żeby były nieczytelne bez odpowiedniego klucza. W przeciwieństwie do hashowania, szyfrowanie można odwrócić, jeśli mamy klucz. Przykład: AES.

- What are the differences between Hashing and Encryption? → Jakie są różnice między haszowaniem a szyfrowaniem?
    

Hashowanie -  operacja, która z dowolnych danych tworzy skrót o stałej długości. Taki skrót służy do porównywania lub weryfikacji danych, a nie do ich odzyskiwania, bo proces jest nieodwracalny. Np. system nie trzyma Twojego hasła tylko jego skrót, który jest sprawdzany przy logowaniu - porównuje hash wpisanego hasła z zapisanym hashem.  
Szyfrowanie -  zamienia dane na nieczytelną formę, którą można odszyfrować kluczem - ukrycie treści z możliwością odczytu. Np. gdy wysyłasz maila, treść jest szyfrowana, żeby ktoś jej nie odczytał. Odszyfrowana jest po drugiej stronie.

- Explain Salted Hashes → Wyjaśnij pojęcie „salted hashes” (hashe z solą).  
    Salted hashes to dodatkowe zabezpieczenie przy przechowywaniu haseł -  do hasła dodaje się losowy tekst, czyli sól (która jest losowa i unikalna), a dopiero potem oblicza hash. Taki tekst powoduje, że hash wygląda inaczej niż hash samego hasła. Eliminuje to problem, kiedy dwóch użytkowników miałoby to samo hasło (w wyniku którego byłby ten sam hash). W takim przypadku system dodaje inną “sól” by hash był inny od drugiego.  
      
    
- What is the difference between asymmetric encryption and symmetric? - Czym różni się szyfrowanie symetryczne od asymetrycznego?
    

Szyfrowanie symetryczne - używa tego samego klucza do szyfrowania i odszyfrowania.  
Szyfrowanie asymetryczne - używa parę kluczy - publicznego i prywatnego. Publiczny jest do szyfrowania, prywatny do odszyfrowania.   
Przykład: każdy może wrzucić list do skrzynki pocztowej (klucz publiczny), ale tylko właściciel ma klucz do jej otwarcia (klucz prywatny).

  

  
  

  
  
  
  
  
  
  
  
  
  

  
  

  
  

  
  
  
  
  
  

  
  

##   
SIEM

- What is SIEM? → Czym jest SIEM?
    

Jest to system, który zbiera, standaryzuje i analizuje logi oraz zdarzenia bezpieczeństwa z wielu źródeł, takich jak firewallów, serwerów, EDRów i aplikacji. Przykład: Splunk, Microsoft Sentinel, Elastic Security, ArcSight  
  

- Explain Security Misconfiguration →  
    Wyjaśnij pojęcie błędnej konfiguracji bezpieczeństwa (security misconfiguration).  
      
    
- What is Port Scanning? → Czym jest skanowanie portów?  
      
    

  
  

###   
  
NETWORK SECURITY MONITORING

  

Could you share some general network security product names? → Podaj przykładowe rozwiązania/produkty z obszaru bezpieczeństwa sieci.  
  

What are HIDS and NIDS? → Czym są HIDS i NIDS?  
  

What is the key difference between IDS and IPS? → Jaka jest kluczowa różnica między IDS a IPS?

  
  
  
  
  
  
  
  
  
  
  

##   
ATAKI ORAZ IDENTYFIKACJA ZAGROŻEŃ SIECIOWYCH 

- How can you protect yourself from Man-in-the-middle (on-path) attacks? →
    

 Jak zabezpieczyć się przed atakiem Man-in-the-Middle (on-path)?

Ochrona przed MITM zależy od scenariusza, ale najważniejsze jest, żeby nawet jeśli ktoś wejdzie w środek ruchu, nie mógł go ani podejrzeć, ani podmienić.  
Po pierwsze, w aplikacjach wymuszam szyfrowanie i uwierzytelnienie – czyli TLS/HTTPS albo SSH – i zwracam uwagę na poprawną walidację certyfikatów. W środowiskach firmowych dodatkowo pomaga HSTS, a czasem mTLS, gdy chcemy mieć pewność co do obu stron.  
Po drugie, dbam o DNS, bo MITM często zaczyna się od przekierowania. Tam, gdzie to ma sens, stosuje się DNSSEC do weryfikacji odpowiedzi, a DNS over HTTPS albo DNS over TLS do ograniczenia podsłuchu samych zapytań.  
Po trzecie, jeśli jestem w niezaufanej sieci, np. publiczne Wi-Fi, to używam VPN i nie ignoruję ostrzeżeń przeglądarki o certyfikacie – to częsty sygnał próby podszycia.  
I na koniec, w samej sieci LAN ogranicza się klasyczne spoofingi, czyli ARP/DHCP – np. przez DHCP Snooping i Dynamic ARP Inspection na switchach żeby trudniej było w ogóle wejść w rolę ‘pośrednika’.

  

- Co to jest DHCP Snooping?
    

  

- Co to jest Dynamic ARP Inspection?
    

  

- Co to jest DNSSEC ?
    

  

- What Is Indicator of Compromise (IOCs)? → 
    

Czym są wskaźniki kompromitacji (IOC)?

  

- What is Indicators of Attack (IOAs)? → 
    

Czym są wskaźniki ataku (IOA)?

  

- What is Cyber Threat Intelligence (CTI)? → 
    

Czym jest Cyber Threat Intelligence (CTI)?

  

- What is TAXII in Cyber Threat Intelligence (CTI)? → 
    

Czym jest TAXII w kontekście CTI?

  

- Name some of the Threat Intelligence Platforms →
    

 Podaj przykłady platform Threat Intelligence.

  

- What are the types of Threat Intelligence? → 
    

Jakie są typy Threat Intelligence?

  

- Can you describe SQL Injection? → 
    

Możesz opisać SQL Injection?

##   
Bezpieczeństwo aplikacji webowych (warstwa aplikacyjna)

What are the HTTP response codes? → Jakie są kody odpowiedzi HTTP?  
  

Explain OWASP Top 10 → Wyjaśnij, czym jest OWASP Top 10.  
  

What is SQL Injection? → Czym jest SQL Injection?  
  

Explain SQL Injection Types → Omów typy SQL Injection.  
  

How to prevent SQL injection vulnerability? → Jak zapobiegać podatności na SQL Injection?  
  

What is XSS and how XSS can be prevented? → Czym jest XSS i jak mu zapobiegać?  
  

Explain XSS Types → Omów typy XSS.  
  

What is IDOR? → Czym jest IDOR?  
  

What is RFI? → Czym jest RFI?  
  

What is LFI? → Czym jest LFI?  
  

What is difference between LFI and RFI? → Jaka jest różnica między LFI a RFI?  
  

What is CSRF? → Czym jest CSRF?  
  

What is WAF? → Czym jest WAF?

  
  
  
  

## INCIDENT RESPONSE

- How would you carry out the initial triage of the ticket, and on what basis would you escalate it to L2? → Jakbyś dokonał bazowy triage ticketu i na jakiej podstawie byś go wyskalować do L2?
    

Przy analizie ticketu zawsze zaczynamy od sprawdzenia, co wywołało alert (czyli nasze IoC - indicator of compromise) - co się wydarzyło, gdzie i czego dotyczy:  
- reguły  
- żródło logów  
- czas zdarzenia  
- jaki host  
- jaki użytkownik  
- adresy IP  
- procesy,  
- hashe  
- nazwę detekcji  
- czy alert dotyczy endpointa, konta, maila czy ruchu sieciowego  
- jaki ma to wpływ na naszą firmę,  
  
Następnie kategoryzuję ticket: priorytet, zakres i ryzyko. Potem próbuję potwierdzić, czy są oznaki podejrzanego działania, czy tylko nietypowe, ale legalne zachowanie (np. kilka nieprawidłowych logowań od znanego użytkownika). Następnie sprawdzam też inne tickety, które mogą pochodzić od tych samych kont, użytkowników czy IP, by zobaczyć czy alert to nie false positive.  
Jeżeli jest false positive, to opisuję i zamykam ticket.  
  
Jeżeli jest to ticket wysokiego ryzyka, gdzie potrzebna jest głębsza analiza, brakuje pewności, zagrożenie może być poważne albo wpływ obejmuje więcej niż jeden system lub użytkownika, zbieram wszystkie informacje i wysyłam ticket do L2. Czyli nie jako ochrona dla mnie “na wszelki wypadek” tylko gdy są konkretne przesłanki do zagrożenia bezpieczeństwa.  
  

  
  
  
  
  
  
  
  

  
  
  

##   
NARZĘDZIA

### SNORT

###   
ZEEK

###   
WIRESHARK

- Masz plik PCAP i masz wykonać wstępną analizę ruchu. Co zrobisz, żeby:  
    a) znaleźć 3-way handshake TCP,  
    - szukamy flag SYN->SYN/ACK->FIN - w takiej sekwencji (możemy użyć filtra tcp.flag)  
    - Jeśli jest tylko SYN bez odpowiedzi albo retransmisje, to może wskazywać na problem sieciowy, filtrowanie lub skanowanie.  
      
    b) określić protokół warstwy aplikacyjnej,  
    - Najpierw otwieram pcap w Wireshark i używam Statistics ->Protocol Hierarchy.  
    - potem weryfikuję przez kolumnę Protocol - filtrowanie po ruchu np. http, dns, tls  
    - analizuję porty i zawartości pakietów (Follow TCP/UDP Stream) jeśli protokół nie został rozpoznany automatycznie  
      
    c) ustalić, czy w ruchu przesłano dane logowania  
    - możemy użyć “Follow TCP stream” na pierwszym pakiecie, żeby zobaczyć całą sesję i sprawdzić czy przypadkiem hasła nie zostały przesłany jawnym tekstem.  
      
    d) sprawdzić, czy da się odzyskać przesłany plik?
    

- najpierw sprawdzamy filtr tcp.dstport == 20  - protokół FTP na 20 jest od transferu danych. Szukamy pakietów które mogą wskazywać o transferze plików (wielkość pakietów ma znaczenie)
    
- jeżeli w pakiecie znajdziemy coś świadczącego o rozszerzeniu pliku .txt .pdf itd. wycinamy dane i zapisujemy do pliki (oczywiście jak nie jest zaszyfrowany).
    
- alternatywnie File - > Export Objects 
    

### TSHARK

  

### SPLUNK

  
  
  

### AUTORUNS - ANALIZA MALWARE

  

### BURP

  

### CYBERCHEF

  

### HASHCAT

  
**

