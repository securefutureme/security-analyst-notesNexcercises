## 1. Ludzie

**Zespoły i role bezpieczeństwa**

- Analitycy SOC – obsługa alertów, triage, eskalacja, podstawowe działania IR.
- Inżynierowie bezpieczeństwa – utrzymanie i rozwój narzędzi (SIEM, EDR, FW, logi).
- Threat Hunterzy – proaktywne szukanie zagrożeń, które nie zostały jeszcze wykryte alertami.

**Junior SOC powinien wiedzieć:**

- kto jest bezpośrednim przełożonym / liderem zmiany,
- do kogo eskaluje (L2/L3 / IR team),
- kto odpowiada za narzędzia, z których korzysta.

**Świadomość bezpieczeństwa w całej organizacji**

Wszyscy w organizacji powinni wiedzieć:

- jak rozpoznać podstawowe symptomy incydentu (np. podejrzane e-maile, nietypowe zachowanie systemu),
- że zgłoszenie podejrzenia jest właściwą reakcją, nie „przeszkadzaniem IT”.  

Szkolenia powinny być kierowane:

- nie tylko do działu security,
- nie tylko do managementu,
- ale do każdego pracownika (użytkownicy końcowi, HR, finanse, sprzedaż, itd.).

**Punkty kontaktowe i zgłaszanie incydentów**

- ***Kiedy coś zgłaszamy?***  
    np. nietypowe logowanie, podejrzany e-mail, dziwne okno logowania, nagły brak dostępu.    

- ***Jak zgłaszamy?***  
    dedykowany adres e-mail, numer telefonu, formularz, system zgłoszeń.  

- ***Komu zgłaszamy?***  
    SOC / helpdesk / service desk – zgodnie z procedurą.  


>**Ważne:**  
>Przepływ informacji: zgłoszenia nie mogą ginąć; ścieżka musi być prosta i znana.  
>Poufność - Informacje o incydentach nie powinny wychodzić poza organizację.  
>Komunikacja wewnętrzna dot. incydentów powinna odbywać się kanałami bezpiecznymi i szyfrowanymi.  
  
**„War room” i praca w trakcie incydentu**

- dobrze jest mieć zdefiniowaną przestrzeń roboczą („war room”) – fizyczną lub wirtualną:
	ograniczony dostęp,
    jasne zasady komunikacji,
    centralne miejsce podejmowania decyzji.   

- podczas incydentu ważne są notatki w czasie rzeczywistym (np. SharePoint)
- co, kiedy, na jakim systemie zostało zauważone,
- jakie działania wykonano (i z jakim skutkiem).

>Ważne:
> Notatek nie trzymamy „luzem” (np. na prywatnych notatnikach, nieszyfrowanych plikach).
> Najlepiej używać bezpiecznych dokumentów współdzielonych (np. w systemie ticketowym lub wewnętrznym repozytorium), z kontrolą dostępu.    

## 2. Narzędzia

**Systemy do śledzenia incydentów**

- System ticketowy / ITSM – miejsce, w którym:
- rejestrowane są zgłoszenia (w tym incydenty),
- przypisywane są zadania,
- śledzona jest historia działań.  
- IRT tools (Incident Response Tracking) – narzędzia lub moduły wspierające:
- rejestrację incydentów,
- statusy i etapy (np. Identification, Containment, …),
- przypisanie właścicieli,
- dokumentację decyzji.  

Junior SOC powinien umieć:

- poprawnie założyć i uzupełnić ticket IR,
- aktualizować go w miarę postępu prac (log działań).

**Narzędzia bezpieczeństwa i szyfrowania**

- Narzędzia szyfrujące – do ochrony:
	- komunikacji (np. szyfrowane komunikatory, e-maile),
	- plików z dowodami (artefakty, zrzuty pamięci, logi).  

- Nośniki danych – odpowiednio zabezpieczone
	- szyfrowane dyski/pendrive’y,
	- jasne zasady wynoszenia i przechowywania materiałów dowodowych.    

- Dedykowane komputery:
	- stacje do analizy malware / forensyki,
	- odseparowane od produkcyjnej sieci,
	- z odpowiednimi narzędziami (analiza logów, PCAP, itp.).

**AM + CMDB (Asset Management + Configuration Management DB)**

Żeby skutecznie reagować, trzeba wiedzieć, co chronimy.

- AM (Asset Management) – lista zasobów:  serwery, stacje robocze, urządzenia sieciowe, aplikacje, konta.  
- CMDB (Configuration Management Database) – baza konfiguracji:
	- kto jest właścicielem systemu,
	- gdzie stoi
	- jaki ma system operacyjny, wersję, IP, zależności
	  
Junior SOC powinien:
- wiedzieć, skąd wziąć informacje o hoście / usłudze,
- rozumieć, które systemy są krytyczne, a które mniej istotne. 

**Narzędzia zapobiegające (prewencja)**

- Systemy security – m.in.:
	- AV/EDR,
	- firewall, WAF, IDS/IPS
	- e-mail security, proxy, DLP, itp.       
- Świadomość, co jest chronione, a co nie:  
    - które segmenty sieci / systemy są objęte monitoringiem i ochroną,
    - gdzie są „dziury” (np. brak EDR, brak logów) – to wpływa na jakość detekcji i IR.
