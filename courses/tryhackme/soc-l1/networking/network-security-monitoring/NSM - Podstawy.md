# Omówienie sieci
## Komponenty sieci – podstawowe elementy budujące sieć

Sieci stanowią **kręgosłup każdej nowoczesnej organizacji**. Serwery, stacje robocze, aplikacje i urządzenia bezpieczeństwa nie funkcjonują w izolacji — są ze sobą połączone, tworząc **jeden wspólny ekosystem**.

**Perymetr sieciowy** to miejsce, w którym ten wewnętrzny ekosystem jest oddzielony od zewnętrznego Internetu. To właśnie on bardzo często staje się **pierwszym celem atakujących**.

Sieć komputerowa nie jest przypadkowym zbiorem urządzeń. To **uporządkowana struktura**, w której zasoby sieciowe łączą się ze sobą, aby umożliwić **komunikację**, **współdzielenie zasobów** oraz **łączność między sobą i ze światem zewnętrznym**.


## Sieć dla małych przedsiębiorstw

Z perspektywy bezpieczeństwa wiedza o tym, **do czego służą poszczególne urządzenia** i **dlaczego są istotne**, pomaga szybciej identyfikować podejrzaną aktywność. Przyjrzyjmy się przykładowi **małej sieci przedsiębiorstwa** i omówmy jej najważniejsze komponenty, ich zastosowanie oraz znaczenie w kontekście bezpieczeństwa.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-2.png)
### Stacje robocze użytkowników (endpoints)

Pracownicy wykonują swoją codzienną pracę na **stacjach roboczych**, takich jak komputery PC i laptopy. Jednocześnie są one najczęstszym **punktem wejścia dla atakujących**, najczęściej za pośrednictwem **maili phishingowych** lub **złośliwych plików pobranych z sieci**.

**Przykład:**  
Mail phishingowy dostarcza malware na komputer pracownika działu finansowego.

**Dlaczego to ważne:**  
Endpointy są często **słabiej monitorowane**, ale ich kompromitacja może dać atakującemu **przyczółek**, z którego będzie mógł rozpocząć **ruch boczny** w sieci.

**Znaczenie:**  
Logi endpointów mogą ujawnić działanie **złośliwych procesów**, ale to logi sieciowe często jako pierwsze pokażą połączenia **C2 (Command and Control)**.

### Serwery plików i bazy danych

Te serwery przechowują najważniejszy zasób firmy, czyli **dane**.  
**Serwery plików** zapewniają scentralizowany dostęp do współdzielonych dokumentów, natomiast **serwery baz danych** zarządzają danymi strukturalnymi, takimi jak:

- dane klientów
- informacje kadrowe
- dane finansowe

**Znaczenie:**  
Atakujący często obierają te serwery za cel, ponieważ ich przejęcie oznacza dostęp do **wartościowych** lub **wrażliwych danych**.  
Operatorzy ransomware szczególnie chętnie atakują serwery plików, aby **zmaksymalizować skutki ataku**.  
Kampanie eksfiltracji danych często polegają na **potajemnym wynoszeniu danych** z tych serwerów poza sieć organizacji.

### Serwery aplikacyjne (WWW, poczta, VPN itp.)

Te serwery dostarczają usługi, z których pracownicy i klienci korzystają każdego dnia.

**Serwery WWW** – hostują firmowe strony internetowe i aplikacje webowe.  
**Serwery pocztowe** – obsługują komunikację firmową.  
**Bramy VPN** – umożliwiają bezpieczny zdalny dostęp do zasobów wewnętrznych.

**Znaczenie:**  
Ponieważ są to systemy **wystawione na zewnątrz**, serwery aplikacyjne są celami o wysokiej wartości. Atakujący stale je skanują w poszukiwaniu **luk w oprogramowaniu** lub **słabych konfiguracji**. Wykorzystanie jednej z takich słabości często daje im **pierwszy punkt zaczepienia** wewnątrz sieci.

Z perspektywy bezpieczeństwa trzeba monitorować:

- logi aplikacyjne
- alerty z firewalli
- sygnatury IDS

po to, aby identyfikować:

- próby exploitacji, np. **SQL injection** w aplikacji webowej
- próby logowania typu **brute force** do poczty lub usług VPN
- podejrzane zewnętrzne adresy IP komunikujące się z wrażliwymi aplikacjami

### Active Directory (AD) / serwery uwierzytelniania

**Active Directory** to fundament tożsamości w większości sieci przedsiębiorstw. Zarządza:

- użytkownikami
- grupami
- komputerami
- prawami dostępu

Pracownicy używają swoich poświadczeń AD do logowania się na komputerach, uzyskiwania dostępu do poczty, serwerów plików i aplikacji wewnętrznych.

**Znaczenie:**  
AD jest głównym komponentem kontrolującym wszystkie konta użytkowników i systemy w sieci.  
Atakujący często celują w AD w celu:

- **eskalacji uprawnień**
- **utrzymania dostępu**
- **ruchu bocznego**

Przejęcie jednego konta **domain admina** może doprowadzić do przejęcia całego przedsiębiorstwa.
Z perspektywy bezpieczeństwa należy monitorować logi uwierzytelniania pod kątem podejrzanych zachowań, takich jak:

- wielokrotne nieudane próby logowania (**password spraying**)
- nietypowe logowania z zewnętrznych adresów IP lub o nietypowych porach
- konta uzyskujące dostęp do systemów, z których normalnie nie powinny korzystać

---

### Routery i przełączniki (infrastruktura sieciowa)

**Routery** łączą różne sieci, przede wszystkim łącząc firmową sieć lokalną (**LAN**) z Internetem.  
**Przełączniki (switches)** łączą urządzenia w obrębie tej samej sieci, dzięki czemu komputery pracowników, drukarki i serwery mogą komunikować się ze sobą w sposób płynny. Urządzenia te stanowią **układ krążenia przedsiębiorstwa**.

**Znaczenie:**  
Choć routery i przełączniki zwykle nie są bezpośrednio wystawione na zewnątrz, ich przejęcie może dać atakującym możliwość:

- przechwytywania i modyfikowania ruchu (**Man-in-the-Middle**)
- tworzenia backdoorów przez przekierowywanie ruchu
- otwierania ukrytych kanałów komunikacji z Internetem

---

### Firewalle / urządzenia brzegowe/obwodowe

**Firewall** jest podstawową bramą bezpieczeństwa, która kontroluje ruch pomiędzy **zaufaną siecią wewnętrzną** a **niezaufanym Internetem**. Analizuje pakiety przychodzące i wychodzące, a następnie decyduje, czy je przepuścić, czy zablokować, zgodnie z ustalonymi regułami bezpieczeństwa.

**Urządzenia bezpieczeństwa brzegowego / sieciowego** są to systemy, które chronią granice sieci.

Nowoczesne firewalle realizują również:

- głęboką inspekcję aplikacji
- zapobieganie włamaniom
- wykrywanie malware

**Znaczenie:**

- chronią organizację przed bezpośrednią ekspozycją na Internet
- zapobiegają nieautoryzowanemu dostępowi do usług wewnętrznych, np. baz danych czy RDP
- logują każdą próbę połączenia — zarówno udaną, jak i zablokowaną

Takie logi bardzo często stanowią **najwcześniejszy wskaźnik ataków**, takich jak:

- skanowanie portów
- próby brute force
- próby exploitacji

# Widoczność sieciowa

**Widoczność sieciowa** jest kluczowa w cyberbezpieczeństwie. To zdolność do monitorowania i rozumienia tego, co dzieje się w całej sieci. To jedna z podstawowych zasad pracy analityka bezpieczeństwa: **nie da się chronić czegoś, czego nie widać**. Skuteczna widoczność umożliwia **wykrywanie zagrożeń**, **badanie incydentów** oraz utrzymanie **silnej postawy bezpieczeństwa**. Nie chodzi o śledzenie każdego pojedynczego pakietu, ale o posiadanie narzędzi pozwalających zbudować **jasny obraz sytuacji**. Bez tego jesteśmy ślepi na potencjalne zagrożenia.

Widoczność sieciowa pochodzi głównie z **dwóch podstawowych źródeł logów**. Trzeba rozumieć różnicę między nimi, aby skutecznie odtworzyć **oś czasu ataku**.

### Dlaczego widoczność jest kluczowa?

**Wyobraź sobie próbę zabezpieczenia domu bez okien i kamer bezpieczeństwa.** 

Nie wiedzielibyśmy, że ktoś próbuje się włamać, dopóki nie byłoby za późno. Widoczność sieciowa daje nam **„oczy” dla środowiska cyfrowego**. Bez niej złośliwe działania, takie jak **infekcje malware**, **nieautoryzowany dostęp** czy **eksfiltracja danych**, mogą pozostać całkowicie niezauważone.

Skuteczna widoczność pozwala analitykom bezpieczeństwa:

- **wykrywać anomalie** – zauważać nietypowe wzorce, które mogą wskazywać na atak;
- **badać incydenty** – odtwarzać przebieg ataku, aby zrozumieć, co się wydarzyło;
- **prowadzić threat hunting** – aktywnie szukać ukrytych przeciwników w sieci;
- **zapewniać zgodność** – spełniać wymagania regulacyjne dzięki logowaniu i monitorowaniu aktywności sieciowej;

Aby to osiągnąć, opieramy się głównie na **logach**, czyli zapisach zdarzeń zachodzących w sieci i na poszczególnych urządzeniach. Wyróżniamy dwie główne kategorie źródeł logów.

## Logi host-centryczne (_Host-Centric Logs_)

Logi host-centryczne są generowane przez **pojedyncze urządzenia (hosty)** w sieci, takie jak:

- serwery
- stacje robocze
- laptopy

Dają one szczegółowy, „bliski” widok tego, co dzieje się na konkretnej maszynie. Są niezbędne do zrozumienia **bezpośredniego wpływu ataku na system**.

### Kluczowe źródła logów host-centrycznych

**Logi systemu operacyjnego**  
Np. **Windows Event Logs**, **Linux syslog**, **logi macOS**. Rejestrują zdarzenia takie jak:

- logowania użytkowników
- tworzenie procesów
- uruchamianie usług
- nieudane próby logowania

**Logi aplikacyjne**  
Logi pochodzące z oprogramowania działającego na hoście, np.:

- serwery WWW (**Apache, Nginx**)
- bazy danych (**MySQL, MSSQL**)
- inne aplikacje

**Logi narzędzi bezpieczeństwa**  
Logi z:

- oprogramowania antywirusowego
- agentów **EDR**
- hostowych systemów wykrywania włamań (**HIDS**)

### Znaczenie logów host-centrycznych

Te logi są bardzo cenne przy odpowiadaniu na pytania takie jak:

**Szczegółowa analiza śledcza**  
Pozwalają zrozumieć dokładnie, jakie działania wykonał atakujący na przejętej maszynie, np. do jakich plików uzyskał dostęp, które zmodyfikował lub usunął.

**Śledzenie procesów i uruchomień**  
Pomagają wykryć tworzenie złośliwych procesów, wykonywanie nieautoryzowanych skryptów (np. **PowerShell**) oraz zmiany w usługach systemowych.

**Monitorowanie aktywności użytkowników**  
Pozwalają sprawdzić, kto się zalogował, kiedy to zrobił i jakich uprawnień używał. Jest to ważne zarówno przy wykrywaniu ataków zewnętrznych, jak i zagrożeń wewnętrznych.

**Ocena wpływu malware**  
Pozwalają potwierdzić, czy złośliwy plik został uruchomiony i jakie zmiany wprowadził w:

- rejestrze systemowym
- systemie plików
- działających usługach

---

### Logi sieciowo-centryczne (_Network-Centric Logs_)

O ile logi hostów pokazują, co dzieje się **na urządzeniu**, logi sieciowo-centryczne pokazują, co dzieje się **między urządzeniami**. Są generowane przez urządzenia sieciowe znajdujące się w sieci i monitorujące przepływający przez nią ruch.

**Co pokazują:**

- adresy IP źródłowe i docelowe
- porty
- protokoły
- podjętą akcję, np. **dozwolono** lub **zablokowano**

**Dlaczego są ważne:**  
Dają kluczowy kontekst: **kiedy**, **gdzie** i **w jaki sposób** coś się wydarzyło. Mogą ujawnić:

- początkowe próby rozpoznania wykonywane przez atakującego
- ruch boczny pomiędzy systemami
- próby eksfiltracji danych

Aby uzyskać pełny obraz, trzeba korelować oba typy logów. Można to ująć tak:

**Logi host-centryczne mówią, co wydarzyło się wewnątrz pokoju, a logi sieciowo-centryczne pokazują, kto wszedł do budynku i kto go opuścił.**

### Kluczowe źródła logów sieciowo-centrycznych

**Firewalle**  
Logi firewalli zawierają zapis każdego połączenia, które zostało **dozwolone** lub **zablokowane** zgodnie z wcześniej zdefiniowanymi regułami bezpieczeństwa. To pierwsze miejsce, do którego warto zajrzeć przy analizie **nieautoryzowanych prób połączeń z Internetu**.

**IDS/IPS**  
Systemy wykrywania i zapobiegania włamaniom monitorują ruch sieciowy pod kątem wzorców odpowiadających **znanym atakom** (sygnatury) lub **nietypowym zachowaniom** (anomalie). Ich logi są kluczowe przy wykrywaniu aktywnych ataków w czasie rzeczywistym.

**Routery i przełączniki**  
Choć nie logują w tradycyjnym sensie, urządzenia takie jak routery mogą generować **dane przepływu (flow data)**. Dane te podsumowują rozmowy sieciowe i pokazują:

- kto komunikował się z kim
- jak długo trwała komunikacja
- ile danych przesłano

To bardzo dobre źródło ogólnego obrazu aktywności sieciowej.

**Web proxy**  
Logi serwerów proxy są bardzo cenne w organizacjach, które kierują ruch webowy przez proxy. Rejestrują każdą odwiedzaną stronę, zapewniając widoczność w obszarach takich jak:

- zagrożenia webowe
- naruszenia polityk bezpieczeństwa
- próby eksfiltracji danych

**VPN**  
Urządzenia VPN zarządzają zdalnym dostępem pracowników. Ich logi pokazują:

- kto łączy się z siecią firmową
- skąd się łączy
- o której godzinie

To kluczowe dla monitorowania bezpieczeństwa połączeń zdalnych.

### Znaczenie logów sieciowo-centrycznych

Logi sieciowo-centryczne zapewniają **wysokopoziomowy, „ptasi” widok** ruchu przemieszczającego się pomiędzy urządzeniami i przez perymetr sieci. Są niezbędne do:

**Wczesnego wykrywania zagrożeń**  
Pozwalają identyfikować zagrożenia już na brzegu sieci, zanim zdążą przejąć endpoint. Obejmuje to m.in.:

- skanowanie portów
- próby brute force
- połączenia z adresów IP znanych jako złośliwe

**Identyfikowania komunikacji C2**  
Pomagają wykrywać wzorce komunikacji pomiędzy przejętym hostem wewnętrznym a zewnętrznym serwerem kontrolowanym przez atakującego.

**Śledzenia ruchu bocznego**  
Pozwalają obserwować przemieszczanie się atakującego z jednej przejętej maszyny na kolejną wewnątrz sieci.

**Wykrywania eksfiltracji danych**  
Pozwalają alarmować o nietypowo dużych lub podejrzanych transferach danych wychodzących z organizacji.

**Zapewniania szerokiego kontekstu**  
Umożliwiają zrozumienie skali ataku poprzez sprawdzenie, z jakimi innymi urządzeniami próbował komunikować się przejęty host.
# Perymetr sieciowy

**Perymetr sieciowy** (albo **obwód sieci**, **granica sieci**) to granica oddzielająca wewnętrzną sieć organizacji (**strefę zaufaną**, np. pracowników, serwery, aplikacje biznesowe) od zewnętrznego Internetu (**strefy niezaufanej**). To punkt, przez który dane **wchodzą do sieci** albo **ją opuszczają**. Można go porównać do **głównej bramy** albo **drzwi wejściowych** do chronionego budynku. Cały ruch przychodzący z Internetu musi przejść przez ten punkt, aby dostać się do sieci organizacji, a cały ruch wychodzący z sieci wewnętrznej również musi przez niego przejść, aby dostać się do Internetu. Perymetr sieciowy jest więc **pierwszą i najważniejszą linią obrony**.

- **Sieć wewnętrzna** to miejsce, w którym znajdują się systemy krytyczne dla biznesu.
- **Zewnętrzny Internet** jest pełen potencjalnych zagrożeń.
- **Perymetr** to kontrolowany punkt wejścia, przez który przechodzi cały ruch.

Zrozumienie perymetru, jego roli i sposobów jego ochrony jest bardzo ważne dla analityka bezpieczeństwa.

### Perymetr

Perymetr jest definiowany przez urządzenia sprzętowe znajdujące się na krawędzi sieci. W nowoczesnych środowiskach obejmuje on jednak także **wirtualne bramy**, **połączenia chmurowe** oraz **punkty zdalnego dostępu**.

Typowe elementy perymetru sieciowego to:

**Firewalle** – strażnicy filtrujący ruch pomiędzy siecią wewnętrzną a zewnętrzną.

**Routery / bramy sieciowe** – urządzenia kierujące ruchem i egzekwujące reguły dostępu.

**DMZ (Demilitarized Zone)** – buforowy segment sieci, w którym umieszcza się serwery wystawione publicznie, takie jak serwery WWW, pocztowe czy VPN.

**Bramy zdalnego dostępu / VPN** – bezpieczne punkty wejścia dla pracowników pracujących poza biurem.

![alt](courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-1.png)


### Znaczenie perymetru sieciowego

Perymetr sieciowy działa jak **strażnik bramy**, kontrolując to, co wchodzi do sieci i ją opuszcza. Nie jest to jedno urządzenie, ale raczej **zestaw mechanizmów bezpieczeństwa i komponentów sieciowych**, które współpracują, aby chronić zasoby wewnętrzne przed zagrożeniami zewnętrznymi. Każdy z tych komponentów pełni odrębną rolę w zarządzaniu, filtrowaniu i zabezpieczaniu przepływu danych pomiędzy siecią wewnętrzną i zewnętrzną.

Atakujący zawsze rozpoczynają rozpoznanie **z zewnątrz**. Perymetr jest zazwyczaj **pierwszą linią obrony** i często także **pierwszym miejscem**, w którym analitycy SOC zauważają oznaki złośliwej aktywności.

Jeżeli perymetr jest słaby albo błędnie skonfigurowany, atakujący mogą:

- wykorzystać wystawione usługi, np. **RDP, MySQL, SMB**, aby uzyskać dostęp
- prowadzić **skanowanie** i **rozpoznanie** w celu zmapowania sieci
- uruchamiać **ataki brute force** przeciwko usługom logowania
- używać kanałów **eksfiltracji danych** do przesyłania skradzionych informacji poza organizację

---

### Perymetr sieciowy w małym przedsiębiorstwie

Wyobraź sobie sieć małej firmy:

**Firewall** znajduje się pomiędzy Internetem a wewnętrzną siecią **LAN**.

**Serwer WWW** umieszczony jest w **DMZ**, aby klienci mogli korzystać ze strony internetowej firmy.

**Serwery wewnętrzne** — takie jak **AD, serwery plików i bazy danych** — znajdują się za firewallem i są dostępne wyłącznie dla pracowników.

Pracownicy spoza biura łączą się z siecią przez **bramę VPN**.

Taka architektura sprawia, że tylko **kontrolowany ruch** dociera do sieci wewnętrznej, a usługi publiczne pozostają odseparowane w **bezpieczniejszej strefie**.

Najczęściej w skład takiego środowiska wchodzą:

- **routery** – kierują ruchem sieciowym
- **firewalle** – analizują i filtrują ruch
- **DMZ (Demilitarized Zone)** – hostuje usługi publicznie dostępne
- **bramy VPN** – zapewniają bezpieczny dostęp zdalny

---

### Dlaczego to ma znaczenie

Perymetr jest **pierwszą linią obrony** przed zagrożeniami zewnętrznymi. Atakujący skanują adresy IP na perymetrze, szukając **otwartych portów** i **podatności**. Błędnie skonfigurowany albo słabo chroniony perymetr często prowadzi do:

- **nieautoryzowanego dostępu** (np. wystawiony **RDP/SSH**)
- **wycieków danych**
- **infekcji malware**

---

### Rola analityka bezpieczeństwa

Z perspektywy analityka bezpieczeństwa monitorowanie perymetru oznacza:

- przeglądanie logów firewalla pod kątem **połączeń zablokowanych i dozwolonych**
- identyfikowanie prób **skanowania** lub **ataków brute force**
- oznaczanie nietypowego ruchu wychodzącego, który może wskazywać na **beaconing malware** albo **eksfiltrację danych**
- rozumienie, **co powinno** i **czego nie powinno** być wystawione na perymetrze