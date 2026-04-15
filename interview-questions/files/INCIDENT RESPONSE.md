
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
  

  
  
  
  
  
  
  
  

  
  