# Wyciąganie wniosków po incydencie (Lessons Learned Post-Incident Activity)

Cel fazy:  
Nie „odhaczyć” incydent i zapomnieć, tylko wyciągnąć z niego maksimum wiedzy, żeby:

- podobny atak następnym razem został wykryty szybciej,
    
- był mniej szkodliwy,
    
- a najlepiej – w ogóle się nie udał.
    

---

1. Co obejmuje faza „Lessons Learned”?

2. Podsumowanie incydentu (post-incident review / PIR)
    

- Co się stało? (timeline)
    
- Jak wykryliśmy incydent?
    
- Jak zareagowaliśmy?
    
- Co zadziałało dobrze, a co zawiodło?
    

3. Identyfikacja luk i problemów
    

- technicznych (brak logów, słabe reguły, brak integracji, dziura w EDR),
    
- procesowych (brak playbooka, niejasna eskalacja, chaos komunikacyjny),
    
- ludzkich (brak świadomości, brak szkoleń).
    

5. Ustalenie działań korygujących (action items)
    

- co zmieniamy w konfiguracji / regułach / narzędziach,
    
- co dopisujemy / poprawiamy w procedurach i playbookach,
    
- jakie szkolenia lub komunikaty dla użytkowników są potrzebne.
    

7. Aktualizacja „pamięci organizacji”
    

- nowe IOC/TTP trafiają do:
    

- reguł SIEM/EDR,
    
- list blokad (URL, IP, domeny),
    

- incydent trafia do bazy wiedzy (KB) jako case.
    

---

2. Jak wygląda typowe spotkanie „po incydencie”?

- Kto bierze udział:
    

- przedstawiciel SOC (L1/L2),
    
- IR lead / security,
    
- czasem admini systemów, właściciel biznesowy systemu, jeśli incydent był większy.
    

- Co omawiamy (w prostym układzie):
    

1.                  Timeline – krok po kroku:

- pierwszy sygnał (kiedy i skąd),
    
- moment potwierdzenia incydentu,
    
- działania containment,
    
- eradication & recovery,
    
- pełne przywrócenie.
    

2.                  Co zadziałało dobrze?

- które reguły / narzędzia / decyzje przyspieszyły reakcję.
    

3.                  Co poszło źle / mogło być lepiej?

- brak logów, spóźniona eskalacja, niejasny playbook, problemy komunikacyjne.
    

4.                  Konkretnie: co poprawiamy?

- lista action items z właścicielem i terminem.
    

---

3. Rola junior SOC w „Lessons Learned”

Junior SOC jest bardzo ważny, bo:

- był „na pierwszej linii” przy alercie,
    
- widzi praktyczne problemy: co było niejasne, czego brakowało.
    

Twoje zadania:

1. Dobre notatki w trakcie incydentu
    

- im lepiej opiszesz, co robiłeś i co widziałeś, tym łatwiej później to przeanalizować.
    

3. Udział w podsumowaniu (jeśli jesteś zaproszony)
    

- szczerze powiedzieć:
    

- co było dla Ciebie niejasne w playbooku,
    
- gdzie straciłeś czas (np. brak danych, dostępów),
    
- co by Ci ułatwiło poprawną ocenę alertu następnym razem.
    

5. Pomoc przy aktualizacji KB / playbooków
    

- dodanie nowego case’a,
    
- dopisanie dodatkowych kroków („sprawdź też X w SIEM, bo tego nam brakowało”),
    
- zapisanie nowych IOCs/TTP w odpowiednim miejscu.
    

7. Nauka na przyszłość (dla siebie)
    

- spisz sobie prywatne „lessons learned”:
    

- jakie wzorce zachowań hosta/sieci są podejrzane,
    
- jakie zapytania w SIEM okazały się najbardziej pomocne,
    
- jakich błędów już nie powtórzysz.
    

---

4. Przykładowe pytania, które warto zadać po incydencie

- Czy mogliśmy wykryć incydent wcześniej?
    

- jeśli tak – czego brakowało (reguły, logów, integracji)?
    

- Czy playbook był wystarczająco jasny dla L1?
    
- Czy ścieżka eskalacji była oczywista?
    
- Czy komunikacja (SOC ↔ admini ↔ biznes) działała sprawnie?
    
- Czy mamy już w regułach SIEM/EDR wszystkie znane IOCs z tego incydentu?
    
- Czy potrzebne są dodatkowe szkolenia / komunikacje dla użytkowników?
    

---

5. Czego NIE robić w fazie „Lessons Learned”

- Nie szukać winnych, tylko przyczyn.  
    Ta faza nie jest po to, żeby wskazać „kto zawalił”, tylko co systemowo nie zadziałało.
    
- Nie odkładać podsumowania „na kiedyś”.  
    Im później, tym więcej szczegółów wszyscy zapomną.  
    Idealnie: w ciągu kilku dni od zamknięcia incydentu.
    
- Nie kończyć incydentu bez żadnych zmian.  
    Jeśli po poważnym incydencie nie zmienia się nic:
    

- w regułach,
    
- w procedurach,
    
- w konfiguracji,  
    to znaczy, że organizacja niczego się nie nauczyła.
    



**