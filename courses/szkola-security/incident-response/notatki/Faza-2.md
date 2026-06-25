# Identyfikacja, Wykrywanie i Analiza

Celem tej fazy jest wychwycenie potencjalnych incydentów, odróżnienie ich od szumu (false positive) oraz podjęcie decyzji, czy mamy do czynienia z:

- zwykłym zdarzeniem (event),
    
- podejrzanym zdarzeniem wymagającym obserwacji,
    
- incydentem bezpieczeństwa, który trzeba dalej obsłużyć w ramach IR.
    

---

1. Co obejmuje ta faza?

- Przyjęcie sygnału – alert, zgłoszenie użytkownika, info z zewnątrz.
    
- Wstępny triage – szybka ocena, czy alert ma sens.
    
- Analiza techniczna – logi, artefakty, kontekst.
    
- Klasyfikacja – event vs incident, poziom ważności, pilność.
    
- Decyzja – zamknięcie jako FP, eskalacja, albo przejście do Containment.
    

2. Skąd biorą się sygnały (źródła detekcji)?

- SIEM
    

- alerty z reguł korelacyjnych (np. wiele nieudanych logowań, podejrzane logowania VPN, nietypowy ruch sieciowy).
    

- EDR / AV
    

- wykrycie malware, podejrzanych procesów, exploitów, działań użytkownika.
    

- Systemy e-mail security
    

- phishing, spam, złośliwe załączniki, podejrzane linki.
    

- Firewall / IDS / WAF / Proxy
    

- skanowanie portów, próby exploitów, nietypowe HTTP(S)/DNS.
    

- Zgłoszenia użytkowników / helpdesk
    

- „Komputer dziwnie działa”, „dostałem podejrzany mail”, „widzę dziwny komunikat logowania”.
    

- Zewnętrzne źródła
    

- threat intel, CERT, vendorzy, informacje o nowej kampanii/włamaniu.
    

3. Typowy workflow dla SOC L1 w fazie Identyfikacji

I. – Przyjęcie alertu / zgłoszeniaOtwórz ticket / sprawdź, czy już istnieje.

- Zanotuj podstawowe dane:
    

- kto (użytkownik, host, konto),
    
- co (rodzaj alertu),
    
- kiedy (czas wystąpienia),
    
- skąd (jakie narzędzie wygenerowało alert).
    

  

II.  – Szybki triage (czy warto inwestować czas?)

Pytania pomocnicze:

- Czy reguła alertu jest znana z dużej liczby false positive?
    
- Czy to jest krytyczny system / użytkownik (serwer produkcyjny, admin, VIP)?
    
- Czy to jest jednorazowe zdarzenie, czy część większego wzorca (np. seria podobnych alertów)?
    

Na tym etapie nie analizujesz jeszcze bardzo głęboko, tylko oceniasz, czy alert:

- wygląda na oczywisty FP (np. testowe skanowanie z wewnętrznego narzędzia, znana „szumowa” reguła),
    
- czy jednak zasługuje na pełną analizę.
    

III.  – Analiza techniczna (zależnie od typu)

a) Alert na endpoint (EDR/AV)

- proces i ścieżkę pliku,
    
- rodzica procesu (parent process),
    
- użytkownika, na którym działa,
    
- powiązane działania:
    

- nowe pliki,
    
- połączenia sieciowe,
    
- zmiany w rejestrze (Windows).
    

b) Alert sieciowy (FW/IDS/Proxy)

- źródłowy i docelowy IP/port,
    
- domenę/URL (pamiętaj o defangingu, jeśli kopiujesz do notatek),
    
- ilość przesyłanych danych,
    
- czy IP/domena jest znana jako malicious (TI, VT, wewnętrzne listy).
    

c) Alert związany z kontem / logowaniem (AD, VPN, SSO)

- lokalizacja (geografia, nietypowy kraj / ASN),
    
- typ logowania (interaktywny, RDP, VPN),
    
- pora dnia (nietypowe godziny),
    
- korelację z innymi logami (np. błędy logowania → nagły sukces).
    

d) Alert mailowy (phishing / malware)

- nadawcę (From, Reply-To, domena, SPF/DKIM/DMARC, jeśli masz),
    
- temat i treść (język, pilność, błędy, pretekst),
    
- linki – zawsze defangowane (http → hxxp, . → [.]),
    
- załączniki – typ pliku, nazwa, analiza (sandbox, AV, EDR, hash).  
      
      
    

IV. – Korelacja i kontekst

- Sprawdź w SIEM, czy:
    

- są inne alerty dla tego samego hosta / użytkownika,
    
- w podobnym czasie wystąpiły inne podejrzane zdarzenia.
    

- Sprawdź w EDR, czy:
    

- host generował inne podejrzane procesy / połączenia.
    

- Sprawdź w AM/CMDB:
    

- co to za system?
    
- jaki ma poziom krytyczności?
    
- kto jest właścicielem biznesowym?
    

V.  – Decyzja: event vs incident i eskalacja

- Jeśli wszystko wskazuje na fałszywy alarm –  
    → zamykasz jako FP, dokumentując, dlaczego.
    
- Jeśli zdarzenie jest podejrzane, ale niejednoznaczne –  
    → możesz oznaczyć jako „do obserwacji”, przekazać do L2 lub wpisać w notatkach do kolejnych alertów.
    
- Jeśli masz silne przesłanki, że to naruszenie bezpieczeństwa –  
    → klasyfikujesz jako incydent, eskalujesz wg ścieżki (IR lead / L2/L3),  
    → przechodzimy do fazy Containment.
    

Kluczem jest konsekwentna klasyfikacja i dobra dokumentacja.

VI.  – Dokumentacja

- wpisz do ticketu:
    

- jakie logi sprawdziłeś,
    
- jakie zapytania/filtry użyłeś,
    
- jakie były wyniki,
    
- dlaczego podjąłeś taką decyzję (FP / incident / eskalacja).
    

Dzięki temu:

- ktoś inny może kontynuować Twoją pracę,
    
- łatwiej wyciągnąć wnioski przy lessons learned,
    
- budujesz swój „repozytorium przypadków”.
    

---

4. Co jest „nietypowym zachowaniem”? (przykłady)  
Żeby coś uznać za abnormal behaviour, dobrze mieć w głowie proste wzorce. Przykłady:

Host / endpoint

- procesy uruchamiane z nietypowych lokalizacji (%TEMP%, %APPDATA%, C:\Users\Public\ itd.),
    
- Word/Excel uruchamiające cmd.exe / powershell.exe,
    
- nowy plik EXE pojawiający się zaraz po otwarciu maila.
    

Sieć

- host, który nagle wysyła duże ilości danych na zewnętrzny adres,
    
- regularne, powtarzalne połączenia do jednego IP/domeny (beaconing),
    
- DNS z dużą liczbą zapytań do dziwnie wyglądających domen.
    

Konto/użytkownik

- logowania z nietypowych lokalizacji (kraj, miasto, ASN),
    
- wiele nieudanych logowań → nagłe udane logowanie,
    
- logowanie w godzinach nietypowych dla użytkownika (np. 3:00 w nocy).
    

E-mail

- nadawca niby znany, ale dziwna domena (np. micros0ft.com),
    
- temat/treść wymuszające pośpiech („pilne”, „suspended”, „ostatnie ostrzeżenie”),
    
- niespodziewane załączniki, prośba o makra lub logowanie się do „panelu”.
    

---

5. Dobre praktyki dla junior SOC w fazie Identyfikacji

- Nie klikaj podejrzanych linków i załączników „normalnie” – używaj:
    

- defangingu,
    
- sandboxów / środowisk analitycznych.
    

- Zawsze zapisuj swoje kroki – nawet przy FP.
    
- Pivotuj – z jednego alertu przechodź do innych logów (host, konto, IP, domena).
    
- Korzystaj z playbooków, ale myśl – playbook mówi co zrobić, Ty decydujesz, co ma sens w danej sytuacji.
    
- Eskaluje się wcześniej, nie za późno – jeśli coś wygląda źle i przekracza Twoje kompetencje lub uprawnienia, podnieś rękę.
    

**