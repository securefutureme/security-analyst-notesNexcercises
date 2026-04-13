
# Atakujący i rozpoznanie sieci

Jak omówiono w poprzednim zadaniu, atakujący rozpoczynają atak od próby odkrycia zasobów organizacji, które są dostępne z publicznego Internetu (**attack surface**, czyli **powierzchnia ataku**). W tej fazie rozpoznania atakujący próbują ustalić m.in. następujące informacje:

- do jakich zasobów mogą uzyskać dostęp
- jakie są adresy **IP**, porty, systemy operacyjne i usługi działające na tych zasobach
- jakie wersje usług są uruchomione
- czy któraś z usług ma podatność, którą można wykorzystać

Krótko mówiąc, atakujący próbują znaleźć **punkt wejścia**, który pozwoli im wykorzystać słabości sieci.

# Obrońcy i rozpoznanie sieci

Z drugiej strony również obrońcy czasami uruchamiają oprogramowanie wykonujące działania związane z rozpoznaniem sieci. W trakcie takiej aktywności chcą oni osiągnąć następujące cele:

- zinwentaryzować zasoby organizacji i upewnić się, że wszystkie są udokumentowane
- upewnić się, że niepotrzebne adresy IP, porty ani usługi nie są wystawione, a to, co działa, jest rzeczywiście potrzebne
- upewnić się, że podatności zostały załatane lub przynajmniej te, które można wykorzystać, zostały zabezpieczone

Krótko mówiąc, obrońcy starają się **maksymalnie zmniejszyć powierzchnię ataku**

# Wyzwanie w wykrywaniu rozpoznania sieci

Jak można zauważyć, zarówno atakujący, jak i obrońcy wykonują działania rozpoznawcze. Podobne działania prowadzą również różne organizacje badawcze, roboty indeksujące, wyszukiwarki i inne podmioty mapujące zasoby dostępne w Internecie. Zespoły **SOC** muszą więc umieć odróżnić **dobre rozpoznanie** od **złośliwego rozpoznania**.

Aby ograniczyć ten problem, zespoły SOC często stosują następujące techniki:

- tworzą **allowlisty** dla znanych wewnętrznych i nieszkodliwych zewnętrznych skanerów, tak aby nie generować alertów dla tych źródeł
- integrują **Threat Intelligence** z mechanizmami detekcji i oznaczają aktywność skanowania tylko wtedy, gdy pochodzi ona ze źródeł znanych jako złośliwe lub podejrzane

Ponieważ takie podejście może jednak pominąć część złośliwej aktywności skanującej, niektóre zespoły wykorzystują **Threat Intelligence** do **podnoszenia poziomu ważności alertów**, zamiast ograniczać się wyłącznie do ich uruchamiania na tej podstawie. Dodatkowo wdrażają ogólne reguły wykrywające **zachowania charakterystyczne dla skanowania**, o których będzie mowa w kolejnych zadaniach..

# Zachowania związane z rozpoznaniem sieci

Podczas omawiania zachowań związanych z **rozpoznaniem sieci** zespół **SOC** może natrafić na aktywność mającą na celu mapowanie hostów w docelowej sieci. Taka aktywność może przyjmować następujące formy.

#### Zewnętrzna aktywność skanująca

Analityk SOC może zaobserwować aktywność skanującą prowadzoną **spoza sieci organizacji**, skierowaną przeciwko maszynom znajdującym się wewnątrz sieci, głównie przeciwko **publicznie dostępnym zasobom na perymetrze**. W takim typie ataku analityk zauważy, że **źródłowy adres IP** jest adresem zewnętrznym, a **adres docelowy** należy do organizacji.

Taki typ skanowania wskazuje, że atak nadal znajduje się w fazie **Reconnaissance** w cyklu życia **MITRE ATT&CK**. Oznacza to, że atakujący **nie ma jeszcze przyczółka wewnątrz sieci** i prowadzi wstępne rozpoznanie, aby znaleźć możliwości uzyskania **początkowego dostępu** do środowiska.

**[Reconnaissance w frameworku MITRE ATT&CK](https://attack.mitre.org/tactics/TA0043/)**

Ten rodzaj skanowania występuje na początkowych etapach ataku, a ponieważ atakujący nie osiągnął jeszcze żadnego trwałego dostępu do sieci, jest to skanowanie o **niskim poziomie ważności**. W odpowiedzi na zewnętrzną aktywność skanującą analityk SOC może **zablokować obraźliwe adresy IP** na firewallu perymetrowym organizacji. Trzeba jednak pamiętać, że atakujący może wrócić ponownie, **ukrywając lub zmieniając swój adres IP**.

#### Wewnętrzna aktywność skanująca

Drugim typem skanowania, który może zaobserwować analityk SOC, jest aktywność **wewnętrzna-do-wewnętrznej**. W takim przypadku analityk zauważy, że zarówno **źródłowy**, jak i **docelowy adres IP** są prywatnymi adresami należącymi do sieci organizacji. Oznacza to, że skanowanie rozpoczyna się **wewnątrz organizacji** i obejmuje zasoby znajdujące się w tej samej sieci.

Taki typ skanowania wskazuje, że atak przeszedł już do fazy **Discovery** w cyklu życia **MITRE ATT&CK**. W niektórych innych frameworkach może to być również określane jako **wewnętrzne rozpoznanie**, co sugeruje, że atakujący **ma już przyczółek w sieci** i przygotowuje się do **ruchu bocznego**.

[**Discovery w frameworku MITRE ATT&CK**](https://attack.mitre.org/tactics/TA0007/)

Ponieważ ten rodzaj skanowania wskazuje, że atakujący **znajduje się już wewnątrz sieci**, jest to alert o **wysokim poziomie ważności**. Po upewnieniu się, że nie jest to jakaś autoryzowana aktywność, analityk SOC powinien **eskalować alert** i rozpocząć **proces Incident Response**. W takiej sytuacji samo zablokowanie źródłowego adresu IP na firewallu nie będzie wystarczające. Konieczne będzie **głębsze dochodzenie dotyczące systemu** oraz przeprowadzenie **analizy przyczyny źródłowej (root cause analysis)**.

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-14.png)
# Identyfikowanie skanowania wewnętrznego i zewnętrznego

Zobaczmy teraz, jak aktywność skanująca wygląda w logach firewalla.

Mamy kilka plików **CSV**, które zostały wyeksportowane z rozwiązania **SIEM**. Chociaż logi zawierają jeden plik z uproszczonym, oczyszczonym wynikiem, pozostałe mogą wydawać się trudniejsze do odczytania. Tak właśnie często wyglądają realne pliki logów po wyeksportowaniu z urządzeń bezpieczeństwa.

Można użyć polecenia **head**, aby podejrzeć zawartość plików.

**Przykład użycia polecenia `head`:**

**head -n2 log-session-1.csv**

Przykładowy wynik:

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-15.png)
Gdy już zapoznamy się z zawartością pliku, możemy użyć narzędzia **cut** z separatorem `,`
aby filtrować poszczególne kolumny w plikach CSV. Trzeba jednak pamiętać, że ponieważ **data zawiera przecinek**, należy odpowiednio uwzględnić to podczas ustalania numerów kolumn.

**Zadania:**

**Który plik zawiera logi pokazujące wewnętrzną aktywność skanującą?**

log-session-2.csv 
![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-16.png)
Mamy tutaj trzy pliki excelowe do przeanalizowania. Wewnętrzna aktywność skanująca to taka, gdzie docelowe i źródłowy IP jest prywatny oraz są nie-routowalne – działają tylko w sieci lokalnej i nie są dostępne bezpośrednio z Internetu. Tutaj mamy jasno na dłoni, które IP są prywatne.

Szybka referencja: https://pl.wikipedia.org/wiki/Adres_prywatny

**Ile wpisów logów występuje dla wewnętrznego adresu IP wykonującego wewnętrzną aktywność skanującą?**

Trzeba przefiltrować sobie jedną z kolumn i dodać je do siebie. 

Możemy zrobić to komendą **cut -d ","** **-f1 | uniq -c** 

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-17.png)

**Jaki zewnętrzny adres IP wykonuje zewnętrzną aktywność skanującą?**

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-18.png)