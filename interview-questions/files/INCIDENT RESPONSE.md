#### How would you carry out the initial triage of the ticket, and on what basis would you escalate it to L2?  
Jakbyś dokonał bazowy triage ticketu i na jakiej podstawie byś go wyskalować do L2?

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
  
#### What steps would you take to validate whether an alert is a true positive or a false positive?

Jakie kroki byś podjął, aby potwierdzić, czy alert jest true positive czy false positive?

#### How would you investigate a suspicious PowerShell execution detected on an endpoint?

Jak byś zbadał podejrzane uruchomienie PowerShella wykryte na stacji końcowej?

#### What information would you collect first when investigating a potentially compromised user account?

Jakie informacje zebrałbyś w pierwszej kolejności podczas analizy potencjalnie przejętego konta użytkownika?

#### How would you respond to multiple failed login attempts followed by a successful login from an unusual location?

Jak byś zareagował na wiele nieudanych prób logowania, po których nastąpiło udane logowanie z nietypowej lokalizacji?

#### How would you analyze an alert related to possible phishing activity reported by an employee?

Jak byś przeanalizował alert dotyczący możliwego phishingu zgłoszonego przez pracownika?

#### What indicators would make you classify an event as a high-priority security incident?

Jakie wskaźniki sprawiłyby, że zaklasyfikowałbyś zdarzenie jako incydent bezpieczeństwa o wysokim priorytecie?

#### How would you investigate suspicious outbound network traffic from a workstation?

Jak byś zbadał podejrzany ruch wychodzący z komputera użytkownika?

#### What would you check if an endpoint is flagged for malware but the user reports no visible issues?

Co byś sprawdził, jeśli endpoint został oznaczony jako zainfekowany malware, ale użytkownik nie zgłasza żadnych widocznych problemów?

#### How would you determine whether lateral movement is taking place inside the environment?

Jak byś ustalił, czy w środowisku dochodzi do ruchu lateralnego?

#### What would be your immediate actions after detecting ransomware-related behavior on a host?

Jakie byłyby Twoje natychmiastowe działania po wykryciu zachowania wskazującego na ransomware na hoście?

#### How would you investigate a suspicious process creating unexpected child processes?

Jak byś zbadał podejrzany proces, który uruchamia nieoczekiwane procesy potomne?

#### What evidence would you document in the ticket to support escalation to the incident response team?

Jakie dowody udokumentowałbyś w tickecie, aby uzasadnić eskalację do zespołu incident response?

#### How would you handle an alert involving communication with a known malicious IP address?

Jak byś obsłużył alert dotyczący komunikacji ze znanym złośliwym adresem IP?

#### How would you prioritize two simultaneous incidents: a phishing report and a possible data exfiltration alert?

Jak byś ustalił priorytet dla dwóch jednoczesnych incydentów: zgłoszenia phishingu i alertu możliwej eksfiltracji danych?
  
  
  
  
  
  
  
  

  
