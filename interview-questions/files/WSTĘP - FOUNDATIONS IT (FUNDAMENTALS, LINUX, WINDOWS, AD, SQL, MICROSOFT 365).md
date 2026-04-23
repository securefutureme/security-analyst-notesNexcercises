#### NA CO UWAŻAĆ

**Nie powinno się mówić:**

1. Nigdy nie słyszałem o waszej firmie / produkcie itp.
  Podstawowy błąd. Zawsze powinniśmy się zapoznać z produktem przed przyjściem na rozmowę. Daje to nam naprawdę duży start w oczach rekrutującego, i zwiększa możliwość na lepszy rozwój rozmowy.
  
  2. Było to zawarte w moim CV.
     
To może zabrzmieć opryskliwie albo tak, jakbyś nie chciał rozmawiać. CV jest punktem wyjścia, ale rozmowa służy rozwinięciu doświadczeń, pokazaniu kontekstu i sposobu myślenia.

  **Lepiej powiedzieć:**  
„Tak, wspomniałem o tym w CV, ale chętnie rozwinę — w praktyce wyglądało to tak, że …”

  3. Nie mam żadnych pytań. (brak zadanych pytań do rekrutera).
  Może to wskazywac na brak zainteresowania firmą. Zwykle rekruterzy nie omawiają wszystkiego co się dzieje w firmie od razu, lepiej łapać ich za język, nawet jeżeli nam takie pytania się wydają nieważne.
  
Przykłady:

- „Jak wyglądają najczęstsze zgłoszenia na tym stanowisku?”
- „Jak wygląda współpraca między 1st line a 2nd line?”
- „Jakie są najważniejsze cele dla osoby na tym stanowisku w pierwszych miesiącach?”
  
4. **„W poprzedniej firmie wszystko było źle”**

5. „Nie znam tego narzędzia, ale to chyba nic trudnego”
   
**To należy mówić:**

6. **„Dbam o użytkownika, ale też trzymam się procesu.”**  
To bardzo dobra odpowiedź pod role 1st line / IT Support/SOC L1.

Przykład:  
„Staram się, żeby użytkownik czuł się zaopiekowany, ale jednocześnie ważne jest dla mnie działanie zgodnie z procesem, SLA i zasadami bezpieczeństwa.”
  
### FUNDAMENTALS

##### Jakie podstawy sieci są przydatne na takim stanowisku?
   
- SOC

-  **L1**
Na takim stanowisku najbardziej przydają się podstawy sieci, które pomagają szybko zrozumieć, gdzie może leżeć problem użytkownika. Mam na myśli przede wszystkim znajomość działania adresacji IP, różnicy między adresem IP publicznym i prywatnym, podstaw DNS i DHCP, bo bardzo często problemy z logowaniem, dostępem do zasobów albo działaniem aplikacji wynikają właśnie z tych obszarów.

Ważna jest też dla mnie umiejętność sprawdzenia podstawowej łączności, czyli czy urządzenie widzi sieć, czy ma poprawny adres IP, czy działa internet, VPN albo połączenie z zasobami firmowymi. Przydaje się też rozumienie, czym są porty, firewall i podstawowe zasady bezpieczeństwa, żeby umieć odróżnić problem użytkownika od blokady po stronie sieci lub polityk bezpieczeństwa.

Na pewno warto rozumieć, jak działa komunikacja między urządzeniem użytkownika, usługami Microsoft 365, Active Directory czy Entra ID. Dzięki temu można szybciej diagnozować incydenty, dobrze opisać zgłoszenie w systemie i w razie potrzeby sensownie przekazać je do 2nd line.

- L2

##### Czy możesz wymienić kilka najnowszych procesorów komputerowych?
Możemy wymienić tutaj **Intel Core Ultra 9 285K**, 24 rdzeniowy, dobry na sockety 1651, **AMD Ryzen 7 9800X3D** pod gaming (4.7 GHz pod AM5), możemy wymienić budżetowy **Ryzen 5 7600X** (4.7 Ghz pod AM5), albo inne z rodziny Ultra (Intel) takie jak Ultra 7 265KF (5.5ghz pod LGA 1851) albo  **i5-14600KF**.
##### Jakich narzędzi używasz/używałeś do identyfikowania i rozwiązywania problemów użytkowników?
Do identyfikowania i rozwiązywania problemów użytkowników najczęściej używałem Jira oraz ServiceNow, bo tam rejestrowałem zgłoszenia, sprawdzałem ich historię, priorytet i status. Przy problemach z kontami i dostępami korzystałem z Active Directory oraz Entra ID, żeby weryfikować użytkowników, grupy i uprawnienia. W przypadku tematów związanych z Microsoft 365 pracowałem też na portalach administracyjnych (admin center) Microsoft 365, żeby sprawdzić licencje, skrzynki, dostęp do usług i podstawową konfigurację. Dodatkowo korzystałem z bazy wiedzy w firmie jeżeli jest dostępna (KB) i dokumentacji technicznej dostępnej w internecie, żeby szybciej diagnozować powtarzające się problemy i trzymać się standardów zespołu.
##### Jaka jest idealna długość przeciętnej rozmowy z klientem?
Dla mnie idealna długość rozmowy z klientem to taka, która pozwala sprawnie zrozumieć problem i jasno powiedzieć, co dalej. Przy prostych zgłoszeniach zwykle jest to około 5–10 minut, ale nie skupiam się na samej długości rozmowy, tylko na skuteczności, jakości obsługi i dotrzymaniu SLA. Lepiej poświęcić minutę więcej i dobrze poprowadzić użytkownika, niż zakończyć rozmowę za szybko i zostawić problem nierozwiązany.
##### Wymień trzy kroki, które możesz podjąć, aby rozwiązać problem klienta związany z internetem.

Najpierw sprawdziłbym podstawy, czyli czy użytkownik ma aktywne połączenie z siecią, czy problem dotyczy tylko jednej osoby czy większej liczby użytkowników, i czy urządzenie jest poprawnie podłączone do Wi-Fi albo sieci LAN.

Drugi krok to wykonanie podstawowej diagnostyki, na przykład sprawdzenie adresacji IP poleceniem ipconfig, sprawdzenie czy DNS działa komendą nslookup, test połączenia z internetem i z zasobami wewnętrznymi komendą ping oraz bardziej radykalne rozwiązanie jak restart karty sieciowej albo urządzenia. Oczywiście są jeszcze takie komendy jak ipconfig /release | renew do zwolnienia i pobrania nowego agresu IP z routera, które też czasem rozwiązuje problem. Albo też flushdns - czyli wyczyszczenie pamięci podręcznej DNS.

Jeśli problem nadal występuje, sprawdziłbym zgłoszenia i ewentualne awarie po stronie infrastruktury, a w razie potrzeby przekazałbym sprawę do 2nd line z opisem wykonanych działań.
##### Jak podchodzisz do bezpieczeństwa IT w codziennej pracy supportowej (L1/L2)?

**L1**
W codziennej pracy supportowej podchodzę do bezpieczeństwa IT bardzo praktycznie i procesowo. Przede wszystkim dbam o to, żeby zawsze weryfikować tożsamość użytkownika przed wykonaniem wrażliwych działań, na przykład resetem hasła, nadaniem dostępu czy zmianą uprawnień. Trzymam się zasady minimalnych uprawnień i nie wykonuję działań poza procedurą. Zwracam też uwagę na podejrzane zgłoszenia, nietypowe zachowania użytkowników, phishing i wszelkie oznaki możliwego incydentu. Jeśli coś budzi wątpliwości, od razu eskaluję temat do odpowiedniego zespołu. Ważne jest dla mnie również poprawne rejestrowanie zgłoszeń w systemie, praca zgodnie z ITIL i dbanie o to, żeby nie udostępniać wrażliwych informacji osobom nieuprawnionym. Krótko mówiąc: bezpieczeństwo traktuję jako element każdej czynności supportowej, a nie osobny temat.

**L2**
##### Użytkownik mówi: „nie działa mi konto”. Od czego zaczynasz (L1/L2)?

L1
Zacząłbym od doprecyzowania, co dokładnie znaczy, że konto nie działa. Najpierw sprawdziłbym, czy problem dotyczy logowania do stacji roboczej, poczty, Microsoft 365, VPN czy innej aplikacji. Następnie zweryfikowałbym tożsamość użytkownika i sprawdził podstawowe rzeczy: czy login jest poprawny, czy konto nie jest zablokowane, wyłączone albo czy hasło nie wygasło. W kolejnym kroku sprawdziłbym konto w Active Directory lub Entra ID, na przykład status konta, blokady, ostatnie logowanie i ewentualne błędy synchronizacji. Jeśli problem dotyczy dostępu do konkretnych zasobów, sprawdziłbym też przypisane grupy i uprawnienia. Równolegle upewniłbym się, czy nie ma szerszego incydentu lub awarii wpływającej na więcej użytkowników.

L2
##### Co sprawdzasz wpierw, kiedy użytkownik zgłasza problemy z dźwiękiem?
Najpierw sprawdzam podstawowe rzeczy: czy dźwięk nie jest wyciszony? Czy klawisze funkcyjne nie zmutowały dźwięku? (czasami lapka na klawiszu może się nie palić). Czy głośniki są włączone i podłączone (jeżeli to stacjonarny)? Sprawdzam ustawienia odtwarzania dźwięku. Przy sprawdzeniu wszystkich podstawowych możliwości przechodzę do sprawdzenia/reinstalowania sterowników.
##### Co sprawdzasz, gdy reset hasła „się udał”, ale użytkownik nadal nie może się zalogować (L1/L2)?

Mapa myśli: **Brak logowania po resecie hasła**, → **czy wpisuje dobre hasło**  → Caps Lock / Num Lock / układ klawiatury  → **jakie konto**  → lokalne / domenowe / Microsoft / VPN / Azure AD  
→ **stan konta**  → zablokowane / wyłączone / wygasłe / wymuszona zmiana hasła  → **synchronizacja**  
→ AD / Azure AD / opóźnienie replikacji  → **gdzie próbuje się logować**  → komputer lokalny / domena / RDP / aplikacja / VPN  → **cache / stare poświadczenia**  → zapisane dane logowania / Credential Manager / sesja  → **problem nie z hasłem, tylko z dostępem**  → brak sieci, brak połączenia z domeną, MFA, polityka logowania

Zdania klucze:
- Najpierw sprawdzam, czy problem na pewno dotyczy **hasła**, a nie np. konta, domeny lub połączenia.
- Weryfikuję **Caps Lock, Num Lock i układ klawiatury**.
- Sprawdzam, czy użytkownik loguje się do **właściwego konta i właściwej domeny**.
- Potwierdzam, czy konto nie jest **zablokowane, wyłączone albo wygasłe**.
- Sprawdzam, czy hasło zostało poprawnie **zsynchronizowane**, np. między AD i Azure AD.
- Weryfikuję, czy urządzenie ma połączenie z **siecią / domeną / VPN**.
- Sprawdzam zapisane **stare poświadczenia** i cache logowania.
- Patrzę, czy nie ma wymuszenia typu **change password at next logon** albo problemu z MFA.
- Rozróżniam: problem z logowaniem do **Windows**, do **VPN**, do **maila** albo do **konkretnej aplikacji**.
  
###### Wersja interview 45–60 sekund
Jeśli reset hasła zakończył się sukcesem, a użytkownik nadal nie może się zalogować, zaczynam od podstaw. Najpierw sprawdzam, czy wpisuje właściwe hasło i czy nie ma problemu z Caps Lockiem, Num Lockiem albo układem klawiatury.  
Następnie weryfikuję, czy loguje się do poprawnego konta — na przykład lokalnego zamiast domenowego albo odwrotnie — i czy wybrana jest właściwa domena. Potem sprawdzam stan konta: czy nie jest zablokowane, wyłączone, wygasłe albo czy nie ma wymuszonej zmiany hasła przy następnym logowaniu.  
Jeśli środowisko jest domenowe lub hybrydowe, sprawdzam też synchronizację hasła między AD i Azure AD oraz to, czy komputer ma połączenie z siecią, domeną lub VPN. Na końcu weryfikuję zapisane stare poświadczenia, cache logowania albo to, czy problem nie dotyczy MFA lub konkretnej aplikacji, a nie samego konta Windows.
##### Co dzieje się po uruchomieniu komputera — od przycisku power do ekranu logowania?
Mapa myśli: Power On -> UEFI/BIOS -> POST -> Boot Device Selection -> Bootloader -> Ekran logowania OS
Zdania klucze: prąd do płyty głównej, pierwsza instrukcja procesora, stała pamięć flash, interfejs pomiędzy OS a hardware, sprawdzanie komponentów (jeżeli błąd=beep code), szukanie urządzeń rozruchowych, program ładujący, ładowanie jądra systemu (kernel) do RAM, inicjacja sterowników i usług.
##### Co to jest **swap/pagefile** i po co się go używa?
Mapa mysli: wydzielona partycja->swap->linux, ukryty plik->Windows-> pagefile.sys, technika, pamięć wirtualna, rozszerzenie RAM,  przestrzeń na HDD/SSD

Zdania klucze: efektywniejsza praca RAM, stabilność systemu, obsługa hibernacji, swapping in/out, lepiej nie wyłączać, brak może prowadzić do nagłych zamknięć aplikacji lub niestabilności.

##### Czym różni się **NTFS** od **FAT32**?

**System plików**  → **FAT32**  → starszy, prostszy  → bardzo szeroka kompatybilność  → limit pliku **4 GB**  
→ mniej funkcji bezpieczeństwa

**System plików**  → **NTFS**  → nowszy, domyślny w Windows  → obsługa dużych plików i partycji  → uprawnienia, szyfrowanie, journaling  → większa niezawodność i bezpieczeństwo

W praktyce supportowej powiedziałbym że jeśli liczy się kompatybilność, na przykład z telewizorem, BIOS-em albo starszym urządzeniem, FAT32 może być wygodny. Jeśli jednak komputer działa na Windows i potrzebujemy bezpieczeństwa, uprawnień, większej stabilności i obsługi dużych plików, lepszym wyborem jest NTFS.
##### Co to jest **system plików**? 
**Dysk / partycja**  → trzeba zorganizować dane  → **system plików**  → zasady zapisu i odczytu  
→ nazwy plików, foldery, metadane  → prawa dostępu, wolne miejsce, lokalizacja danych

**Zdania klucze:** System plików to sposób organizowania danych na dysku. - Dzięki niemu system operacyjny wie, gdzie plik jest zapisany i jak go odczytać. - Zarządza plikami, folderami, nazwami, uprawnieniami i wolnym miejscem. - Bez systemu plików dysk byłby tylko surową przestrzenią danych. - Przykłady: NTFS, FAT32, exFAT, ext4.

Wersja interview 30–45 sekund
System plików to struktura, która organizuje dane na nośniku, takim jak dysk HDD, SSD albo pendrive. Określa, jak pliki są zapisywane, nazywane, odczytywane i usuwane. Zarządza też folderami, metadanymi, wolnym miejscem i czasem uprawnieniami.  
Innymi słowy, bez systemu plików system operacyjny nie wiedziałby, gdzie znajduje się konkretny plik i jak go poprawnie otworzyć.

Z perspektywy IT Support system plików ma znaczenie praktyczne, bo wpływa na kompatybilność, limity rozmiaru plików, bezpieczeństwo i możliwość odzyskiwania danych po błędach. Dlatego przy diagnozie problemów z dyskiem albo kopiowaniem plików warto sprawdzić, jaki system plików jest używany.
##### Co oznacza, że system jest **64-bitowy**?
**Mapa myśli :** Architektura systemu → 64-bit → procesor przetwarza 64 bity naraz → większa przestrzeń adresowa → obsługa większej ilości RAM → możliwość uruchamiania aplikacji 64-bit → lepsza wydajność w nowszych systemach

**Zdania klucze:**  64-bit oznacza typ architektury procesora i systemu.  System może przetwarzać dane w blokach 64-bitowych.  Może obsłużyć więcej pamięci RAM niż 32-bit.  Lepiej współpracuje z nowoczesnymi aplikacjami.  Do działania wymaga procesora zgodnego z 64-bit.

**Wersja interview 30–45 sekund**  
System 64-bitowy oznacza, że procesor i system operacyjny są zaprojektowane do pracy na danych 64-bitowych. W praktyce najważniejsze jest to, że taki system może obsługiwać znacznie więcej pamięci RAM niż system 32-bitowy. Dzięki temu lepiej nadaje się do nowoczesnych komputerów i aplikacji. System 64-bitowy pozwala też uruchamiać programy 64-bitowe, które często są wydajniejsze i lepiej wykorzystują zasoby sprzętowe.

**Wersja „na plus” pod L1/L2**  
Z perspektywy IT Support sprawdziłbym zgodność między procesorem, systemem i aplikacją. Jeśli komputer ma dużo RAM, system 64-bitowy jest praktycznie konieczny, żeby tę pamięć wykorzystać. W troubleshootingu ma to znaczenie przy instalacji sterowników, zgodności programów i wyborze właściwej wersji aplikacji.

**Hak pamięciowy**  
**64-bit = więcej RAM + nowocześniejsze aplikacje**
##### Co to jest **zmienna środowiskowa PATH**?
**Mapa myśli :** Zmienne środowiskowe → PATH → lista folderów systemowych → szukanie plików wykonywalnych → uruchamianie komend bez pełnej ścieżki → cmd / terminal / PowerShell → ułatwienie pracy systemu i użytkownika

**Zdania klucze:**  PATH to zmienna środowiskowa systemu.  Zawiera listę folderów z programami.  
System szuka tam plików wykonywalnych.  Dzięki temu nie trzeba podawać pełnej ścieżki.  Ma znaczenie w CMD, PowerShell i terminalu.

**Wersja interview 30–45 sekund**  
PATH to zmienna środowiskowa, która zawiera listę katalogów, w których system szuka plików wykonywalnych. Dzięki temu użytkownik może uruchomić program lub komendę po samej nazwie, bez wpisywania pełnej ścieżki do pliku. Na przykład jeśli folder programu jest dodany do PATH, można uruchomić go bez przechodzenia do jego lokalizacji. To jest bardzo przydatne w wierszu poleceń, PowerShellu i przy narzędziach administracyjnych.

**Wersja „na plus” pod L1/L2**  
W supportcie PATH jest ważny, bo błędna konfiguracja może powodować, że komenda nie działa mimo poprawnej instalacji programu. Jeśli użytkownik dostaje komunikat, że polecenie nie jest rozpoznawane, sprawdziłbym, czy lokalizacja programu została dodana do PATH. To częsty problem przy Pythonie, Javie, Git czy narzędziach administracyjnych.

**Hak pamięciowy**  
**PATH = gdzie system szuka programów**
##### Czym różni się **proces** od **wątku**?

##### Co to jest **kernel** i za co odpowiada?

##### Co to jest **backup** i czym różni się od **archiwum**?

##### Dlaczego backup, którego nie da się odtworzyć, praktycznie nie istnieje?

##### Co to jest **RAID**? Wymień jego typy.

##### Dlaczego po zmianie w systemie czasem „trzeba wyczyścić cache”?

##### Czym różni się **maszyna wirtualna** od **kontenera**?

##### Co to jest **snapshot** i czy zastępuje backup?

##### Dlaczego restart czasem „naprawia” problem?

##### Co może oznaczać, że problem występuje tylko na jednym urządzeniu?

##### Jak odróżnić problem użytkownika od problemu systemowego(L1/L2)?

##### Co sprawdzasz jako pierwsze, gdy „nic nie działa”(L1/L2)?

##### Jak zawęzisz problem, jeśli objawy są ogólne?

##### Co oznacza „problem nie jest reprodukowalny”?

##### Dlaczego warto pytać: **od kiedy**, **u kogo**, **po jakiej zmianie**?

##### Co jest ważniejsze: szybka odpowiedź czy poprawna diagnoza?

##### Kiedy problem należy eskalować(SOC/L1)?

##### Jak opisać problem techniczny tak, żeby druga osoba mogła go zrozumieć i odtworzyć?
##### Dlaczego „u mnie działa” nie jest dobrą odpowiedzią?
#####  Co zrobić, gdy nie znasz odpowiedzi, ale musisz profesjonalnie poprowadzić zgłoszenie?\
##### Internet działa, ale Outlook nie — co to może oznaczać?
##### Użytkownik mówi, że „nie działa komputer” — jakie pytania zadasz najpierw?
##### Czy brak internetu zawsze oznacza problem z routerem?
##### Czy ping do IP wystarczy, żeby powiedzieć, że „sieć działa”?
##### Czy wyłączenie MFA poprawia bezpieczeństwo czy wygodę?
##### Czy administrator powinien mieć dostęp do wszystkiego?
##### Czy chmura automatycznie rozwiązuje problem backupów?
##### Czy antywirus gwarantuje bezpieczeństwo?
##### Czy szybkie zamknięcie ticketu oznacza dobrą obsługę?
##### Czy restart jest rozwiązaniem, czy tylko obejściem?
#####  Czy użytkownik zawsze poprawnie opisuje źródło problemu?
##### Co jest groźniejsze: brak dokumentacji czy zła dokumentacja?
##### Czy więcej uprawnień zawsze pomaga szybciej rozwiązywać problemy?
##### Co jest lepsze: obejście problemu czy trwałe rozwiązanie?
#####  Czy brak błędu oznacza, że problem nie istnieje?
##### Co to jest **cache** i po co się go stosuje?
#####  Co robisz, gdy użytkownik zgłasza, że zaginął plik?
### LINUX

##### Jak sprawdzić użycie dysku?
#####  Jak zrestartować usługę w Linuxie?
##### Co oznaczają uprawnienia `755`?
#####  Jaka jest rola `sudo`?
#####  Jak sprawdzić logi usługi?
#####  Jak sprawdzić adres IP?
##### Jak sprawdzić, czy port jest otwarty?
##### Co zrobisz przy błędzie `Permission denied`?
##### Jak podejdziesz do diagnozy niedziałającej usługi?
##### Czym różni się Linux od Windows z perspektywy administratora lub supportu?
##### Co to jest dystrybucja Linuxa? Jakie znasz przykłady?
##### Jaka jest różnica między katalogiem `/home`, `/root`, `/etc`, `/var`, `/tmp`?
#####  Co oznacza, że „wszystko w Linuksie jest plikiem”?
##### Jak sprawdzić, w jakim katalogu aktualnie się znajdujesz?
##### Jak wyświetlić pliki w katalogu, także ukryte?
#####  Jak przejść do innego katalogu?
##### Jak utworzyć, skopiować, przenieść i usunąć plik lub katalog?
##### Jak sprawdzić uprawnienia do pliku?
##### Co oznacza zapis typu `rwxr-xr--`?
#####  Jaka jest różnica między właścicielem, grupą i innymi użytkownikami?
##### Do czego służy `chmod`?
#####  Do czego służy `chown`?
##### Jaka jest różnica między kontem zwykłego użytkownika a rootem?
#####  Do czego służy `sudo`?
##### Jak dodać użytkownika do grupy?
##### Dlaczego zasada najmniejszych uprawnień jest ważna także w Linuxie?
#####  Jak sprawdzić, jakie procesy aktualnie działają?
##### Jaka jest różnica między `ps` a `top`?
#####  Jak zakończyć proces?
##### Co zrobić, gdy proces nie odpowiada?
##### Co to jest PID?
##### Jak sprawdzić status usługi w systemie?
##### Do czego służy `systemctl`?
##### Jak uruchomić, zatrzymać i zrestartować usługę?
#####  Co zrobisz, gdy usługa nie startuje po restarcie?
##### Gdzie w Linuxie zwykle szuka się logów?
##### Jak podejść do analizy problemu z niedziałającą usługą?
##### Do czego służy `journalctl`?
##### Jak sprawdzić ostatnie wpisy w logu?
#####  Jak śledzić log „na żywo”?
##### Co robisz, gdy użytkownik mówi, że „serwer działa wolno”?
#####  Jak sprawdzisz, czy problem dotyczy CPU, RAM, dysku czy sieci?
##### Jak sprawdzić adres IP maszyny?
##### Jak sprawdzić, czy host ma połączenie z siecią?
##### Do czego służy `ping`?
##### Do czego służy `traceroute` albo `tracepath`?
#####  Jak sprawdzić, czy DNS działa poprawnie?
##### Jak sprawdzić, czy dany port nasłuchuje?
##### Co oznacza, że usługa jest dostępna lokalnie, ale nie z innego hosta?
#####  Jakie mogą być przyczyny problemu z SSH?
##### Co sprawdzisz, gdy serwer „nie widzi internetu”?
#####  Jak sprawdzić ilość wolnego miejsca na dysku?
##### Jaka jest różnica między `df` a `du`?
#####  Co zrobisz, gdy kończy się miejsce na partycji?
##### Jak sprawdzisz największe katalogi lub pliki?
##### Co to jest montowanie systemu plików?
##### Co oznacza, że system plików jest zamontowany tylko do odczytu?
##### Jak zainstalować pakiet w Debianie/Ubuntu?
#####  Jak zainstalować pakiet w RHEL/CentOS/Alma/Rocky?
##### Jaka jest różnica między `apt` i `yum`/`dnf`?
#####  Jak sprawdzić, czy dany pakiet jest zainstalowany?
#####  Co zrobisz, gdy instalacja pakietu kończy się błędem zależności?
##### Do czego służy SSH?
#####  Jak połączyć się zdalnie z serwerem Linux?
#####  Jaka jest różnica między logowaniem hasłem a kluczem SSH?
##### Co sprawdzisz, gdy nie możesz zalogować się po SSH?
##### Dlaczego wyłączenie logowania rootem przez SSH bywa dobrą praktyką?
#####  Użytkownik mówi, że aplikacja nie działa. Od czego zaczynasz diagnostykę na serwerze Linux?
#####  Serwis www nie odpowiada — jakie są Twoje pierwsze 5 kroków?
##### Serwer działa bardzo wolno — jak zawężysz problem?
##### Nie działa DNS name resolution — co sprawdzisz?
##### Skończyło się miejsce na dysku w `/var` — co robisz?
##### Po restarcie usługa nie podniosła się automatycznie — jak to sprawdzisz?
##### Masz błąd „Permission denied” — jakie są możliwe przyczyny?
##### Aplikacja działa lokalnie, ale użytkownik nie może się z nią połączyć zdalnie — co sprawdzisz?
### WINDOWS

https://www.adaface.com/blog/windows-helpdesk-interview-questions/

##### Co sprawdzasz, gdy komputer z Windows działa bardzo wolno?
##### Jakie są najczęstsze przyczyny problemów z logowaniem do Windows?
#####  Co zrobisz, jeśli użytkownik widzi komunikat, że jego konto zostało zablokowane?
#####  Jak odróżnisz problem systemowy od problemu sprzętowego?
##### Jakie podstawowe narzędzia w Windows wykorzystujesz do diagnostyki problemów?
##### Do czego służy Event Viewer i kiedy go używasz?
##### Do czego służy Task Manager i jakie informacje można tam szybko sprawdzić?
##### Co sprawdzasz, gdy aplikacja w Windows się nie uruchamia?
##### Jak postąpisz, gdy użytkownik zgłasza, że komputer zawiesza się kilka razy dziennie?
##### Jakie są podstawowe kroki przy diagnozie problemu po aktualizacji Windows?
##### Co zrobisz, jeśli użytkownik nie może zalogować się do komputera domenowego?
##### Jaka jest różnica między kontem lokalnym a domenowym?
##### Co to jest profil użytkownika w Windows?
#####  Jakie objawy mogą wskazywać na uszkodzony profil użytkownika?
#####  Jak sprawdzić, czy problem z logowaniem wynika z hasła, sieci czy polityk?
##### Jakie mogą być przyczyny komunikatu „The trust relationship between this workstation and the primary domain failed”?
#####  Co to jest UAC i po co jest używane?
##### Jak postąpisz, gdy użytkownik potrzebuje uprawnień administratora lokalnego?
##### Jak bezpiecznie zweryfikujesz tożsamość użytkownika przed resetem hasła lub zmianą dostępu?
##### Jakie polecenia sieciowe w Windows znasz i do czego służą?
##### Kiedy użyjesz ipconfig, ping, nslookup i gpupdate?
##### Co sprawdzisz, gdy komputer ma internet, ale nie otwiera zasobów firmowych?
##### Jakie mogą być objawy problemu z DNS w Windows?
##### Co zrobisz, gdy użytkownik nie łączy się z VPN w Windowsie?
##### Jak sprawdzisz, czy problem dotyczy Wi-Fi, adaptera sieciowego czy systemu?
##### Jakie są najczęstsze przyczyny, że komputer „nie widzi sieci” w systemem Windows?
##### Co sprawdzasz, gdy Outlook w Windows nie synchronizuje poczty?
##### Jak postąpisz, gdy Teams nie chce się uruchomić na komputerze użytkownika?
#####  Jakie kroki wykonasz, gdy OneDrive nie synchronizuje plików?
#####  Co zrobisz, jeśli użytkownik ma Outlooka, ale nie widzi nowo nadanej skrzynki współdzielonej?
##### Jak odróżnisz problem aplikacji lokalnej od problemu po stronie usługi Microsoft 365?
##### Jakie podstawowe kroki wykonasz przy problemach z cache Outlooka lub Teams?
##### Co sprawdzasz, gdy po aktualizacji Windows przestała działać drukarka?
#####  Gdzie w Windows sprawdzisz problem ze sterownikiem?
#####  Co to jest Device Manager i kiedy go używasz?
##### Jak rozpoznać, że problem dotyczy sterownika, a nie samego urządzenia?
#####  Jakie mogą być przyczyny, że użytkownik nie może drukować?
##### Co sprawdzisz, gdy laptop nie wykrywa drugiego monitora?
##### Jakie podstawowe kroki wykonasz przy problemach z docking station?
##### akie podstawowe działania bezpieczeństwa są ważne na stanowisku 1st line w Windows?
#####  Jak rozpoznać możliwą infekcję lub niepożądane zachowanie systemu w Windowsie?
##### Co sprawdzisz, gdy Windows Defender zgłasza zagrożenie?
##### Do czego służy CMD, a do czego PowerShell?
##### Jakie proste komendy Windows warto znać na 1st line?
##### Co to jest services.msc i kiedy możesz z niego skorzystać?
##### Jak sprawdzisz, czy konkretna usługa systemowa działa poprawnie?
##### Jakie narzędzia w Windows wykorzystasz do sprawdzenia miejsca na dysku?
##### Co zrobisz, gdy użytkownik ma pełny dysk systemowy?
##### Jakie mogą być skutki braku miejsca na dysku dla działania Windows i aplikacji?
##### Kiedy warto użyć restartu usługi, a kiedy restartu całego komputera?
#####  Czym jest profil systemu Windows? Kiedy warto go usunąć i co zostanie usunięte?
#####  Użytkownik mówi: „Windows ciągle prosi mnie o hasło do służbowego konta” — jakie mogą być przyczyny?

### ACTIVE DIRECTORY

1. Czym jest Active Directory i do czego służy?
2. Jaka jest różnica między użytkownikiem, grupą i komputerem w AD?
3. Co to jest domena w Active Directory?
4. Czym różni się Active Directory od Entra ID?
5. Co to jest OU (Organizational Unit) i do czego się jej używa?
6. Po co tworzy się grupy w AD?
7. Jaka jest różnica między grupą security a distribution?
8. Co oznacza, że konto użytkownika jest zablokowane, wyłączone albo wygasłe?
9. Jakie są najczęstsze przyczyny problemów z logowaniem użytkownika w AD?
10. Jak wygląda bezpieczny proces resetu hasła użytkownikowi?
11. Jak sprawdziłbyś, czy użytkownik należy do właściwej grupy?
12. Co sprawdzasz, gdy użytkownik nie ma dostępu do folderu sieciowego?
13. Jak odróżniasz problem z hasłem od problemu z uprawnieniami?
14. Co to jest członkostwo w grupach i jak wpływa na dostęp?
15. Jakie informacje sprawdzisz w AD, gdy nowe konto użytkownika nie działa poprawnie?
16. Jakie mogą być skutki przeniesienia użytkownika do innego OU?
17. Co to jest GPO i do czego służy?
18. Jakie przykłady polityk mogą być ustawiane przez GPO?
19. Dlaczego ważne jest poprawne nazewnictwo i porządek w AD?
20. Jakie dane powinny znaleźć się w tickecie dotyczącym problemu z kontem AD?
21. Użytkownik mówi, że rano logował się normalnie, a teraz nie może. Jak podchodzisz do diagnozy?
22. Użytkownik twierdzi, że ma dostęp do aplikacji, ale nie do folderu współdzielonego. Co sprawdzasz?
23. Nowy pracownik nie może zalogować się pierwszego dnia pracy. Jakie kroki wykonasz?
24. Użytkownik po resecie hasła nadal nie może się zalogować. Co robisz dalej?
25. Konto zostało odblokowane, ale problem nadal występuje. Jakie mogą być przyczyny?
26. Użytkownik zgłasza brak dostępu po zmianie działu. Co sprawdzasz w AD?
27. Jak rozpoznasz, że problem może dotyczyć synchronizacji między AD a Entra ID?
28. Kiedy taki ticket rozwiążesz sam, a kiedy eskalujesz do 2nd line?
29. Jak wyjaśnisz użytkownikowi w prosty sposób, czym jest blokada konta?
30. Jakie ryzyka bezpieczeństwa widzisz przy pracy z kontami i hasłami użytkowników?
31. Co to jest Domain Controller?
32. Dlaczego replika danych w AD jest ważna?
33. Co może się stać, jeśli zmiana w AD nie jest od razu widoczna wszędzie?
34. Na czym polega zasada least privilege w kontekście AD?
35. Dlaczego nie powinno się nadawać uprawnień bezpośrednio użytkownikowi, jeśli można użyć grupy?
36. Jakie są różnice między środowiskiem on-prem AD a hybrydowym?
37. Dlaczego dokumentacja zmian w AD jest ważna?
38. Jakie typowe błędy popełnia 1st line przy zgłoszeniach dotyczących AD?
39. Jakie informacje powinieneś zebrać przed eskalacją problemu z AD?
40. Jak opisałbyś swoją rolę 1st line w pracy z Active Directory?
41. Jak sprawdzisz, czy komputer jest poprawnie dołączony do domeny?
42. Co to jest Group Policy i jaki ma wpływ na użytkownika lub komputer?
43. Jakie problemy użytkownik może odczuwać przez błędnie zastosowaną politykę GPO?
44. Jakim poleceniem możesz odświeżyć polityki grupowe?
45. Co sprawdzasz, gdy dyski sieciowe albo drukarki mapowane przez GPO się nie pojawiają?
46. Jakie mogą być przyczyny, że komputer nie widzi kontrolera domeny?
47. Jak sprawdzisz, na jakim koncie pracuje użytkownik i do jakich grup należy?
48. Kiedy problem z Windows należy eskalować do administratora AD/GPO?
### SQL

1. Czym różni się **baza danych** od zwykłego pliku Excel?
2. Co to jest **relacyjna baza danych**?
3. Czym różni się **SQL** od **NoSQL** na poziomie idei?
4. Co to jest **klucz główny**?
5. Po co używa się **indeksów** w bazie danych?
6. Czym różni się **DELETE** od **TRUNCATE**?
7. Co oznacza spójność danych?
8. Co to jest **replikacja**?
### ITIL / JIRA

[JIRA Explained Fast](https://www.youtube.com/results?search_query=jira+explained+in+5+minutes)

[ITIL Explained Fast](https://www.youtube.com/watch?v=AAQOJqBHz9w-)

#### **Sytuacyjne**

1. 10 pracowników zajmujących się wprowadzaniem danych zgłasza, że nie może się zalogować, recepcjonistka zapomniała laptopa i potrzebuje urządzenia zastępczego, a dyrektor generalny nie może otworzyć prezentacji na spotkanie, które rozpocznie się za 15 minut. Komu pomożesz w pierwszej kolejności?
   
   W pierwszej kolejności obsłużyłbym dziesięciu pracowników zajmujących się wprowadzaniem danych. To właśnie oni mają największy wpływ na działalność firmy, mimo że to dyrektor generalny jest osobą na najwyższym stanowisku
   
#### Czym różni się incident od service request?
#### Jak ustalasz priorytet zgłoszenia?
#### Kiedy eskalujesz zgłoszenie do 2nd line?
#### Jakie informacje powinny znaleźć się w dobrze opisanym tickecie?
#### Co wiesz o SLA?
#### Czym różni się bug, incident, problem i change?
#### Jak postępujesz z wieloma podobnymi zgłoszeniami od użytkowników?**
#### Co robisz, gdy użytkownik naciska na wyższy priorytet?
#### Jak zamykasz ticket, żeby było to zgodne z procesem i czytelne dla audytu?
#### Jakie są najważniejsze elementy poprawnie obsłużonego incydentu zgodnie z ITIL?
#### Jak odróżnisz incident od service request na praktycznych przykładach?
#### Co oznacza priorytetyzacja zgłoszeń i jakie dane są do niej potrzebne?
#### Jaka jest różnica między impact a urgency?
#### Jak wyznaczasz priority na podstawie impact i urgency?
#### Co to jest SLA i jak wpływa na pracę 1st line?
#### Co robisz, gdy widzisz, że zgłoszenie może nie zmieścić się w SLA?
#### Na czym polega ownership zgłoszenia w pracy service desk?
#### Kiedy zgłoszenie powinno być eskalowane do 2nd line?
#### Jakie informacje musisz przekazać przy eskalacji, żeby była jakościowa?
#### Jaka jest różnica między escalation functional a hierarchical?
#### Co to jest major incident i czym różni się od zwykłego incydentu?
#### Jak rozpoznasz, że kilka zgłoszeń może dotyczyć jednego większego incydentu?
#### Co to jest problem management i czym różni się od incident management?
#### Dlaczego dokumentacja i baza wiedzy są ważne w środowisku ITIL?
#### Jak powinno wyglądać poprawne zamknięcie zgłoszenia?

1. Jakie błędy najczęściej popełnia 1st line przy pracy w modelu ITIL?
2. Co to jest service request fulfillment i jakie zgłoszenia zwykle tam wpadają?
3. Jak postępujesz, gdy użytkownik naciska na zmianę priorytetu, ale biznesowo nie jest ona uzasadniona?
4. Jak pogodzisz szybkie zamykanie ticketów z jakością obsługi użytkownika?
5. Wymień kilka modeli opartych na ITIL, które zostały wdrożone w organizacjach.
6. Jakie informacje powinien zawierać dobrze opisany ticket w Jira?
7. Jak kategoryzujesz zgłoszenie w systemie ticketowym?
8. Na czym polega poprawne ustawienie typu zgłoszenia w Jira?
9. Jakie pola w tickecie są najważniejsze z punktu widzenia 1st line?
10. Jak aktualizujesz ticket w trakcie pracy, aby był czytelny dla innych zespołów?
11. Jak dokumentujesz wykonane kroki troubleshootingowe w Jira?
12. Co robisz, gdy ticket został źle przypisany lub źle sklasyfikowany?
13. Jak odróżnić ticket, który można rozwiązać od razu, od ticketu wymagającego eskalacji?
14. Jak korzystasz z komentarzy wewnętrznych i publicznych w systemie ticketowym?
15. Jakie błędy w opisie ticketów najbardziej utrudniają pracę 2nd line?
16. Jak pilnujesz SLA i terminów w systemie typu Jira?
17. Jak postępujesz z duplikatami zgłoszeń?
18. Jak połączysz kilka podobnych zgłoszeń w jedną logiczną obsługę incydentu?
19. Co robisz, gdy użytkownik nie odpowiada, a ticket pozostaje otwarty?
20. Jakie statusy ticketu najczęściej występują i co powinny oznaczać?
21. Kiedy zmieniasz assignee, a kiedy tylko dodajesz komentarz lub mention?
22. Jak opisać ticket tak, żeby inna osoba mogła od razu przejąć sprawę bez straty czasu?
23. Jak wykorzystujesz bazę wiedzy lub linked articles podczas pracy w Jira?
24. Jak raportować powtarzające się zgłoszenia, które mogą wskazywać na szerszy problem?
25. Jak wygląda dla Ciebie wzorcowy ticket od momentu rejestracji do zamknięcia?
26. Masz 10 nowych ticketów i 2 zbliżają się do naruszenia SLA — co robisz?
27. Użytkownik zgłasza brak dostępu, ale opis jest bardzo ogólny — jak poprowadzisz zgłoszenie?**
28. Widzisz 5 podobnych ticketów z różnych lokalizacji — jak zareagujesz?**
29. 2d line odrzuciło ticket z adnotacją “insufficient information” — co poprawiasz?**
30. Ticket został zamknięty, ale użytkownik wraca z tym samym problemem następnego dnia — jak to traktujesz?
31. Użytkownik twierdzi, że jego sprawa jest krytyczna, ale wpływ dotyczy tylko jednej osoby — jak odpowiadasz?
32. Nie możesz rozwiązać zgłoszenia, ale SLA się kończy — jakie działania podejmujesz?

### MICROSOFT 365 / ENTRA / OUTLOOK / TEAMS

1) Co robisz, gdy użytkownik nie może zalogować się do Microsoft 365?
2) Jaka jest różnica między Active Directory a Entra ID?
3) Co sprawdzasz, gdy użytkownik nie ma dostępu do zasobu (sieciowego, AD)?
4)  Jak przywrócić jedną bazę danych SQL Server lub jedną skrzynkę pocztową Exchange?
5) Co znaczą dla Ciebie litery PST? 
6) 1. Co wchodzi w skład Microsoft 365 i które usługi są najczęściej wspierane przez 1st line?
7. Jakie są najczęstsze problemy użytkowników w Microsoft 365?
8. Co sprawdzasz, gdy użytkownik nie może zalogować się do Microsoft 365?
9. Jak odróżnisz problem z kontem od problemu z usługą Microsoft 365?
10. Jakie mogą być przyczyny braku dostępu do aplikacji w Microsoft 365?
11. Co sprawdzisz, jeśli użytkownik ma przypisaną licencję, ale usługa nadal nie działa?
12. Jak wygląda Twoje podejście do troubleshootingu problemów z aktywacją usługi lub licencji?
13. Jak sprawdzisz, czy problem dotyczy jednego użytkownika czy większej awarii?
14. Co robisz, gdy użytkownik zgłasza, że „wczoraj działało, dziś nie działa”?
15. Jak dokumentujesz problem związany z Microsoft 365 w systemie ticketowym?
16. Czym różni się Active Directory od Entra ID?
17. Do czego służy Entra ID w organizacji?
18. Jakie najczęstsze problemy użytkownika mogą być związane z Entra ID?
19. Co sprawdzasz w Entra ID, gdy użytkownik nie może się uwierzytelnić?
20. Jak wyjaśnisz różnicę między authentication a authorization?
21. Jakie mogą być przyczyny zablokowania dostępu użytkownika do aplikacji w Entra ID?
22. Jaką rolę odgrywa MFA i jakie problemy użytkownicy zgłaszają najczęściej?
23. Co robisz, gdy użytkownik twierdzi, że nie otrzymuje promptu MFA?
24. Jak podchodzisz do resetu hasła lub odblokowania konta z perspektywy bezpieczeństwa?
25. Kiedy problem związany z Entra ID powinien zostać eskalowany do 2nd line?
26. Co sprawdzasz, gdy Outlook nie wysyła lub nie odbiera wiadomości?
27. Jakie mogą być przyczyny, że użytkownik nie widzi nowych maili?
28. Co zrobisz, gdy Outlook ciągle prosi o hasło?
29. Jak diagnozujesz problem z profilem Outlooka?
30. Jakie są typowe przyczyny problemów z kalendarzem w Outlooku?
31. Co sprawdzisz, gdy użytkownik nie widzi udostępnionej skrzynki lub kalendarza?
32. Jak postąpisz, gdy użytkownik zgłasza, że wiadomości trafiają do złego folderu?
33. Jakie mogą być przyczyny problemu z wyszukiwaniem maili w Outlooku?
34. Co robisz, gdy Outlook działa wolno albo się zawiesza?
35. Jak odróżnisz problem aplikacji Outlook od problemu po stronie konta lub Exchange Online?
36. Co sprawdzasz, gdy użytkownik nie może dodać skrzynki do Outlooka?
37. Jak pomógłbyś użytkownikowi, który zgłasza problem z zaproszeniami kalendarzowymi?
38. Co sprawdzasz, gdy użytkownik nie może zalogować się do Teams?
39. Jakie są najczęstsze problemy użytkowników w Microsoft Teams?
40. Co robisz, gdy w Teams nie działa mikrofon albo kamera?
41. Jak odróżniasz problem aplikacji Teams od problemu urządzenia?
42. Co sprawdzisz, gdy użytkownik nie widzi zespołu lub kanału?
43. Jakie mogą być przyczyny problemów z jakością połączeń w Teams?
44. Co zrobisz, gdy użytkownik nie może dołączyć do spotkania?
45. Jak pomógłbyś użytkownikowi, który nie widzi statusu innych osób lub obecności?
46. Co sprawdzisz, gdy użytkownik nie może udostępniać ekranu?
47. Jak diagnozujesz problem z czatem, jeśli wiadomości się nie wysyłają?
48. Co robisz, gdy Teams działa bardzo wolno albo nie ładuje się poprawnie?
49. Jakie podstawowe kroki wykonasz przed eskalacją problemu z Teams?
50. Użytkownik mówi: „Nie działa mi Teams, Outlook i OneDrive”. Od czego zaczynasz?
51. Użytkownik nie może zalogować się do Outlooka i Teams po zmianie hasła. Jak to analizujesz?
52. Użytkownik ma dostęp do poczty, ale nie ma dostępu do Teams. Jakie hipotezy bierzesz pod uwagę?
53. Użytkownik nie dostaje kodu MFA i nie może pracować. Jak poprowadzisz rozmowę i diagnostykę?
54. Użytkownik zgłasza, że nie widzi nowo nadanych uprawnień. Co sprawdzasz?
55. Jak obsłużysz zgłoszenie, w którym nie jesteś w stanie rozwiązać problemu od razu, ale użytkownik oczekuje szybkiej odpowiedzi?
56. Jakie informacje musisz zebrać zanim zaczniesz diagnozować problem w M365?
57. Jak ustalisz, czy problem jest lokalny, kontowy czy globalny?
58. Jakie kroki wykonujesz zawsze przed eskalacją?
59. Jak komunikujesz użytkownikowi, że problem wymaga dalszej analizy?
60. Co powinno znaleźć się w tickecie po zgłoszeniu dotyczącym Outlooka lub Teams?
### CHMURA / BACKUP / WIRTUALIZACJA

1. Co to jest **hypervisor**?
   - BYOD configuration issues?
1. Jak odzyskasz utracone pliki zgłoszone przez użytkownika?
2. Co to znaczy **on-premises** vs **cloud**?
3. Czym różni się **SaaS**, **PaaS** i **IaaS**?
4. Czy chmura oznacza, że „nie trzeba znać infrastruktury”?
5. Co to jest **wysoka dostępność**?
6. Czym różni się **skalowanie pionowe** od **poziomego**?
7. Co rozumiesz przez cloud computing?
8. Jaka jest różnica między rozwiązaniem on-premises a cloud?
9. Jakie znasz modele chmury: public, private, hybrid?
10. Jakie są główne zalety korzystania z chmury w środowisku firmowym?
11. Jakie ryzyka lub wyzwania wiążą się z chmurą?
12. Czym różni się SaaS, PaaS i IaaS?
13. Do której kategorii zaliczyłbyś Microsoft 365?
14. Czym różni się lokalne Active Directory od Entra ID w kontekście chmury?
15. Co to znaczy, że firma pracuje w modelu hybrydowym?
16. Jakie usługi użytkownika końcowego najczęściej działają dziś w chmurze?
17. Użytkownik nie może zalogować się do usługi chmurowej — co sprawdzasz najpierw?
18. Jak odróżnisz problem lokalny od problemu po stronie usługi chmurowej?
19. Co możesz sprawdzić, zanim eskalujesz problem z Microsoft 365?
20. Jakie mogą być przyczyny problemów z dostępem do aplikacji w chmurze?
21. Jakie znaczenie ma MFA w środowisku chmurowym?
22. Co zrobisz, jeśli użytkownik twierdzi, że “cloud nie działa”?
23. Jak dokumentowałbyś incydent związany z usługą chmurową w systemie ticketowym?
24. Kiedy problem z usługą chmurową powinien być potraktowany jako major incident?
25. Jakie informacje przekażesz do 2nd line przy eskalacji problemu z chmurą?
26. Jak upewnisz się, że problem dotyczy jednego użytkownika, a nie całej organizacji?
27. Dlaczego zarządzanie tożsamością jest tak ważne w środowisku chmurowym?
28. Co oznacza zasada least privilege?
29. Jakie zagrożenia bezpieczeństwa mogą występować w usługach chmurowych?
30. Dlaczego MFA jest ważniejsze w chmurze niż w wielu starszych środowiskach?
31. Jak zweryfikujesz użytkownika przed resetem hasła lub zmianą dostępu?
32. Co może oznaczać nietypowa próba logowania do konta użytkownika?
33. Jakie znaczenie mają role i grupy dostępu w środowisku cloud?
34. Dlaczego nie powinno się nadawać zbyt szerokich uprawnień?
35. Co zrobiłbyś, gdyby użytkownik zgłosił podejrzaną aktywność na koncie?
36. Jakie elementy bezpieczeństwa są wspólne dla pracy z chmurą i lokalną infrastrukturą?
37. Co to jest wirtualizacja?
38. Po co firmy używają wirtualizacji?
39. Czym jest maszyna wirtualna?
40. Czym różni się maszyna fizyczna od wirtualnej?
41. Co to jest hypervisor?
42. Jaka jest różnica między hypervisor type 1 i type 2?
43. Jakie platformy do wirtualizacji znasz?
44. Jakie są korzyści z uruchamiania wielu maszyn wirtualnych na jednym hoście?
45. Jakie są ograniczenia lub ryzyka wirtualizacji?
46. Co to jest snapshot maszyny wirtualnej?
47. Użytkownik zgłasza, że aplikacja działa bardzo wolno na środowisku wirtualnym — co bierzesz pod uwagę?
48. Jakie mogą być przyczyny niedostępności maszyny wirtualnej?
49. Co sprawdzisz, jeśli VM działa, ale użytkownik nie ma do niej dostępu?
50. Jak odróżnić problem z systemem operacyjnym od problemu z hostem wirtualizacyjnym?
51. Kiedy zgłoszenie dotyczące VM powinno zostać eskalowane?
52. Jakie informacje są przydatne przy zgłoszeniu awarii maszyny wirtualnej?
53. Co może powodować spadek wydajności środowiska wirtualnego?
54. Dlaczego ważne jest monitorowanie zasobów CPU, RAM i storage?
55. Co może się stać, jeśli host jest przeciążony?
56. Jakie problemy sieciowe mogą dotyczyć maszyn wirtualnych?
57. Jaka jest różnica między maszyną wirtualną w lokalnym data center a maszyną wirtualną w chmurze?
58. Co daje organizacji przeniesienie części zasobów do chmury?
59. Jakie typy problemów użytkownicy zgłaszają w środowisku hybrydowym?
60. Jak synchronizacja tożsamości może wpływać na dostęp do usług cloud?
61. Jakie wyzwania supportowe pojawiają się, gdy część systemów jest lokalnie, a część w chmurze?
62. Co zrobisz, jeśli użytkownik ma dostęp do zasobów lokalnych, ale nie do chmurowych?
63. Jak współpraca 1st line z 2nd line wygląda przy incydentach związanych z chmurą?
64. Jakie znaczenie ma dobra dokumentacja przy środowiskach hybrydowych?
65. Dlaczego znajomość podstaw wirtualizacji przydaje się nawet na 1st line?
66. Jak tłumaczyłbyś użytkownikowi technicznemu i nietechnicznemu problem związany z usługą w chmurze?
67. Użytkownik nie może zalogować się do Microsoft 365 po zmianie hasła — jak diagnozujesz problem?
68. Kilku użytkowników z różnych krajów zgłasza problem z Teams lub Outlook — co robisz?
69. Nowy pracownik nie ma dostępu do aplikacji chmurowych mimo aktywnego konta — jakie są możliwe przyczyny?
70. Maszyna wirtualna z aplikacją biznesową jest niedostępna — jak wygląda Twoje pierwsze działanie na 1st line?
71. Użytkownik zgłasza, że po pracy zdalnej nie widzi części zasobów — czy to bardziej kwestia sieci, tożsamości czy wirtualizacji?
72. Dostajesz zgłoszenie o wolnym działaniu systemu hostowanego na VM — jak je opiszesz i komu przekażesz?
73. Jak zareagujesz, jeśli podejrzewasz, że problem dotyczy awarii po stronie dostawcy usługi cloud?
74. Co robisz, jeśli nie jesteś pewien, czy problem leży po stronie użytkownika, urządzenia czy środowiska wirtualnego?

