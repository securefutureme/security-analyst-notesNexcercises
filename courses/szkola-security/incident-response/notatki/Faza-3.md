# Ograniczenie zagrożenia (contaiment)

Cel fazy:  
Zatrzymać „krwawienie” – czyli ograniczyć rozprzestrzenianie się ataku i dalsze szkody, zanim przejdziemy do usuwania zagrożenia (Eradication) i odtwarzania systemów (Recovery).

Dla junior SOC ważne jest jedno:  
robisz tylko takie działania, które są opisane w playbookach / procedurach i mieszczą się w Twoich uprawnieniach.

DWA PYTANIA: CZY JEST POTRZEBNY CONTAIMENT I CZY MAMY DO TEGO UPRAWNIENIA?

  
  

1. Zasady ogólne

- Najpierw bezpieczeństwo, potem wygoda  
    Lepiej na chwilę „wyłączyć” użytkownika lub host, niż pozwolić atakowi pójść dalej.
    
- Nie niszcz dowodów  
    Nie usuwaj logów, nie rób formatów czy pełnych czyszczeń na własną rękę. To przychodzi później (Eradication/Recovery).
    
- Działaj według playbooków  
    Zawsze sprawdź, czy istnieje playbook dla danego typu incydentu (phishing, malware na endpoint, podejrzane logowanie, itp.).
    
- Loguj wszystko, co robisz  
    Godzina, co zrobiłeś, na którym hoście/kodzie użytkownika.
    

---

2. Typowe działania containment (z perspektywy junior SOC)

a) Endpoint (stacja robocza / serwer)

- Izolacja hosta w EDR  
    – host traci łączność z siecią (poza komunikacją z EDR).
    
- Zabicie złośliwego procesu  
    – jeśli playbook na to pozwala.
    
- Tymczasowa blokada konta użytkownika  
    – np. przy podejrzeniu przejęcia konta.
    

Zawsze odnotuj:

- nazwę hosta,
    
- konto użytkownika,
    
- dokładny czas izolacji/blokady.
    

b) Sieć

Jeśli masz takie uprawnienia (albo przekazujesz do kogoś, kto ma):

- Blokada IP / domeny / URL w firewallu, proxy, secure web gateway.
    
- Odcięcie wybranego segmentu / VLAN (zwykle robi to zespół sieciowy na prośbę IR/SOC).
    

Junior SOC zwykle:zgłasza potrzebę blokady wg playbooka (np. do NetOps / L2),dostarcza konkretne dane: IP, domeny, URL, porty.

c) E-mail

- Blokada nadawcy / domeny / URL w bramie pocztowej.
    
- Usunięcie (purge) wiadomości z innych skrzynek (jeśli system na to pozwala).
    
- Oznaczenie maila jako złośliwego w systemie, żeby reguły antyspam/antiphishing mogły go rozpoznawać w przyszłości.  
    Pamiętaj o defangingu adresów i URL, jeśli wklejasz je do ticketa / notatek.
    

---

3. Co jest oczekiwane od junior SOC?

W fazie „Ograniczenie zagrożenia” od junior SOC oczekuje się, że:

1. Rozpozna, że to już czas na containment, a nie tylko analizę  
    – np. potwierdzone uruchomienie malware, aktywne C2, wyciek danych.
    
2. Uruchomi właściwy playbook  
    – np. „Malware na endpoint”, „Phishing – użytkownik kliknął link”, „Konto przejęte”.
    
3. Wykona standardowe kroki, do których ma uprawnienia, np.:
    

- izolacja hosta w EDR,
    
- otwarcie zgłoszenia do zespołu sieci / mail / AD z prośbą o blokadę,
    
- powiadomienie IR lead / L2 zgodnie z procedurą.
    

5. Udokumentuje każde działanie w systemie ticketowym:
    

- co, kiedy, na czym, na czyje polecenie.
    

---

4. Czego NIE robić jako junior SOC w containment

- Nie formatuj / nie reinstaluj hosta na własną rękę – to jest część Eradication/Recovery.
    
- Nie wyłączaj logowania / monitoringu – nawet jeśli generuje dużo logów, w incydencie to często klucz do późniejszej analizy.
    
- Nie kontaktuj się zewnętrznie z mediami / klientami / partnerami  
    – komunikacja zewnętrzna jest zadaniem managementu / PR / wyznaczonych osób.
    
- Nie uzgadniaj „na gębę” zmian z użytkownikami  
    – wszystko przez ticket / ustalone kanały.
    

**