# Likwidacja i powrót do działania operacyjnego

**

Cel fazy:  
Nie tylko „wyczyścić alert”, ale usunąć rzeczywistą przyczynę incydentu tak, żeby atakujący nie mógł wrócić w ten sam sposób.

---

1. Co zwykle dzieje się w fazie Eradication?

Typowe działania (zwykle wykonywane przez IR / adminów / inżynierów):

- Usunięcie malware i artefaktów
    

- złośliwe pliki, skrypty, web shelle, podejrzane usługi, zadania harmonogramu itd.
    

- Usunięcie mechanizmów persystencji
    

- wpisy w Run Keys / Startup,
    
- złośliwe usługi, zadania, plug-iny.
    

- Usunięcie nieautoryzowanych kont / kluczy / access tokens
    

- konta lokalne/domenowe, klucze SSH, API keys, itp.
    

- Załatanie podatności / naprawa błędnych konfiguracji
    

- aplikacja/system, przez który doszło do włamania, musi zostać naprawiony.
    

Ważne:  
Eradication to nie tylko skan AV – to upewnienie się, że wektor wejścia jest zamknięty, a „tylne drzwi” usunięte.

---

2. Rola junior SOC w Eradication

Junior SOC zazwyczaj nie:

- reinstaluje systemów z własnej inicjatywy,
    
- nie robi „wipe & rebuild” produkcji.
    

Ale może / powinien:

1. Przekazać jasne informacje zespołom technicznym
    

- jakie hosty są dotknięte,
    
- jakie IOCs (pliki, procesy, domeny, IP) wykryto,
    
- jakie były dotychczasowe działania (containment).
    

3. Wspierać weryfikację „czystości” hostów po działaniach technicznych:
    

- brak nowych alertów z EDR/AV,
    
- brak podejrzanych procesów / połączeń w SIEM,
    
- logi wyglądają normalnie (brak beaconingu, prób C2, anomalii).
    

5. Uzupełniać i porządkować dokumentację w tickecie incydentu:
    

- co zostało usunięte,
    
- kto i kiedy wykonał dane działania,
    
- jakie IOCs mogą trafić do nowych reguł detekcji.
    

---

3. Czego NIE robić w Eradication jako junior SOC

- Nie kasować „na ślepo” plików tylko po nazwie bez konsultacji z IR / adminem – można „zabić” krytyczną aplikację.
    
- Nie usuwać logów – to dowody i podstawa późniejszej analizy.
    
- Nie kończyć incydentu tylko dlatego, że AV „coś usunął” – zawsze trzeba spojrzeć na root cause i persystencję.
    

  
  
  

---

Powrót do działania operacyjnego (Recovery)

Cel fazy:  
Bezpiecznie przywrócić systemy do normalnej pracy, zminimalizować ryzyko ponownej kompromitacji i upewnić się, że środowisko jest stabilne.

---

1. Co zwykle dzieje się w fazie Recovery?

Typowe działania (głównie po stronie adminów / inżynierów):

- Przywracanie systemów z backupu lub rebuild / reimage maszyn.
    
- Rekonfiguracja systemów
    

- włączenie dodatkowych zabezpieczeń,
    
- twardnienie konfiguracji (hardening).
    

- Stopniowe zdejmowanie containmentu
    

- przywrócenie hosta do sieci,
    
- odblokowanie kont, reguł FW – tylko tam, gdzie to bezpieczne.
    

- Testy działania
    

- czy usługa działa,
    
- czy użytkownicy mogą normalnie pracować.
    

- Podwyższony monitoring po incydencie
    

- wzmocnione reguły SIEM/EDR dla dotkniętych hostów,
    
- obserwowanie pod kątem ponownych prób ataku.
    

---

2. Rola junior SOC w Recovery

Junior SOC:

1. Monitoruje środowisko po przywróceniu systemów
    

- czy na „naprawionych” hostach nie pojawiają się:
    

- nowe alerty EDR,
    
- podejrzane logowania,
    
- nietypowy ruch sieciowy.
    

3. Aktualizuje ticket incydentu
    

- które systemy przywrócono,
    
- kiedy zdjęto izolację / blokady,
    
- od kiedy system jest uznany za produkcyjny.
    

5. Zgłasza od razu anomalie „po powrocie”
    

- jeśli coś wygląda jak powrót tego samego ataku (np. te same domeny, procesy) – natychmiastowa eskalacja.
    

  
  

---

3. Czego NIE robić w Recovery jako junior SOC

- Nie naciskać na przyspieszenie powrotu „za wszelką cenę” – „szybko” nie może być ważniejsze niż „bezpiecznie”.
    
- Nie zakładać, że po reboocie jest po problemie – reboot ≠ recovery.
    
- Nie zmieniać reguł detekcji „żeby nie było alertów” – wyciszanie sensownych alertów po incydencie to przepis na powtórkę ataku.
    

---

4. Podsumowanie dla junior SOC

W fazach Likwidacja zagrożenia (Eradication) i Powrót do działania (Recovery):

- Twoja rola to głównie:
    

- przekazywanie pełnego obrazu (co się stało, gdzie, jakie IOCs),
    
- współpraca z adminami / IR,
    
- weryfikacja, że środowisko faktycznie wygląda „na zdrowe” po ich działaniach,
    
- rzetelna dokumentacja w ticketach.
    



**