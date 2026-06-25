# NIST

[https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-61r2.pdf](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-61r2.pdf)

NIST SP 800-61r2 to przewodnik opisujący jak zbudować i prowadzić zdolność do obsługi incydentów bezpieczeństwa (Computer Security Incident Response Capability – CSIRC) w organizacji.

![[courses/szkola-security/incident-response/notatki/Attachments/1-image.png]]
#### Preparation (Przygotowanie)

- Przygotowanie procesów, narzędzi i ludzi do obsługi incydentów jak: 
- opracowanie i aktualizacja polityk/procedur IR,
- dobór narzędzi (SIEM, EDR, systemy ticketowe, forensyka),
- szkolenia, testy, ćwiczenia,
- działania prewencyjne (patching, hardening, awareness), które zmniejszają liczbę incydentów.
#### Detection & Analysis (Detekcja i analiza)

- Opis wektorów ataku, typowych objawów incydentu (signs),
- Źródła danych: logi systemowe, aplikacyjne, sieciowe, alerty z IDS/IPS, AV, EDR, informacje z zewnątrz (np. CERT-y).
- Jak prowadzić triage i analizę:
	a) korelacja wskaźników (precursors, indicators),
	b) dokumentowanie ustaleń (kto, co, kiedy, gdzie, jak),
	c) priorytetyzacja incydentów wg wpływu na biznes i łatwości odzyskania (impact & recoverability),
	d) zasady notyfikacji – kogo, kiedy, jak informować (wewnętrznie i zewnętrznie).  
#### Containment, Eradication & Recovery (Ograniczenie, usunięcie i odtworzenie)

- **Containment** – wybór strategii ograniczania skutków (krótko- vs długoterminowej), np.
	a) izolacja hostów,
	b) blokada kont, IP, domen, protokołów,
	c) zminimalizowanie wpływu na produkcję przy jednoczesnej kontroli incydentu.  

- **Evidence handling** – zbieranie i zabezpieczanie dowodów (logi, obrazy dysków, zrzuty pamięci) w sposób akceptowalny z punktu widzenia ewentualnych postępowań prawnych.
- **Eradication** – usuwanie przyczyny (malware, backdoory, podatności, złe konfiguracje).
- **Recovery** – bezpieczny powrót do normalnej pracy:
	a) przywracanie z backupów,
	b) patchowanie,
	c) monitoring post-incydentowy w celu wykrycia ponownej kompromitacji.

#### Post-Incident Activity (Działania po incydencie)

- Lessons learned – omówienie incydentu, co poszło dobrze, co źle, co poprawić.
    
- Wykorzystanie zebranych danych:
    

- tworzenie statystyk incydentów, trendów,
    
- aktualizacja polityk, procedur, reguł detekcji, konfiguracji narzędzi.  
      
    

- Retention – jak długo przechowywać dowody i dane incydentowe, z uwzględnieniem wymogów prawnych i wewnętrznych.
    

Dokument zawiera też checklistę obsługi incydentu jako praktyczne podsumowanie procesu. 

  
  
  
  
  
  
  
  

## SANS

[https://www.sans.org/media/score/504-incident-response-cycle.pdf  
  
](https://www.sans.org/media/score/504-incident-response-cycle.pdf)

Model PICERL – cykl Incident Response

Dokument przedstawia prosty, praktyczny model IR o nazwie PICERL:

Preparation – Identification – Containment –  
Eradication – Recovery – Lessons Learned

![[courses/szkola-security/incident-response/notatki/Attachments/2-image.png]]

#### Preparation (Przygotowanie)

- Ludzie: jasne role, kontakty, relacje.
    
- Dokumenty: polityki, procedury, plan komunikacji.
    
- Narzędzia: przygotowane narzędzia IR, „jump bag”, szkolenia i trening dla zespołu.
    

#### Identification (Identyfikacja)

- Budowanie świadomości i zasady „alert early”.
    
- Wykrywanie: nietypowe procesy, konta, uprawnienia, zdarzenia bezpieczeństwa.
    
- Użycie kanałów „out of band”, wskazanie Primary IR Handlera.
    
- Analiza logów, praca z nietypowymi plikami, zachowanie chain of custody.
    

#### Containment (Ograniczenie)

- „Stop the bleeding”: kategoryzacja, powiadomienie zarządu, odłączanie sieci (LAN), zrzuty pamięci, zmiana haseł.
    
- Krótkoterminowo: ustawienie filtrów FW/IDS, przegląd logów hostów, zabijanie backdoorów, wybór strategii zależnie od krytyczności.
    
- Długoterminowo: backup, praca „low profile”, współpraca z ISP, łatanie podatności, dokumentowanie działań, wydzielenie zainfekowanych VLAN, obrazowanie forensyczne.
    

  
  

#### Eradication (Usunięcie)

- Usuwanie artefaktów, stosowanie wszystkich łatek, blokowanie złośliwych IP („black hole IPs”).
    
- Poszukiwanie przyczyny źródłowej (root cause), dodatkowe filtry FW/IDS, szukanie innych punktów zaczepienia atakującego.
    
- Przywracanie z backupu, zmiany nazw DNS, w razie potrzeby wipe/format/rebuild, ponowne skanowanie i usuwanie malware.
    

#### Recovery (Odtworzenie)

- Powrót systemów do pracy (return to ops), monitorowanie oznak kompromitacji.
    
- Testowanie i dokumentowanie nowej „baseline”, formalna zgoda na powrót do produkcji.
    
- Automatyzacja – skrypty do wyszukiwania artefaktów atakującego.
    

#### Lessons Learned (Wnioski)

- Dokumentowanie incydentu, przegląd i komentarze wszystkich zainteresowanych stron.
    
- Finalizacja raportu, executive summary, identyfikacja wymaganych zmian i finansowania.
    
- Uzgodnienie raportu, poprawa procesów (nie szukanie winnych), aktualizacja procedur.
    

### Dane i narzędzia ważne w IR na poziomie enterprise

Druga strona ściągi opisuje, jakie dane zbierać i z jakich źródeł, aby skutecznie prowadzić IR w dużej organizacji.

#### Kluczowe źródła danych:

- Web proxy – często pomijane, a pomaga wykrywać:
    

skompromitowane hosty i połączenia C2,  
podejrzane/nieczytelne URL-e,  
nietypowe (często stare) User-Agent’y malware.

- DNS cache (hostów / wewnętrzny / zewnętrzny) – pozwala:
    

- zobaczyć, które systemy łączą się z „złymi” IP/domenami,
    
- zidentyfikować wcześniej nieznane zainfekowane hosty,
    
- korelować z listami złych domen/IP (blacklistami).  
      
    

- Netflow data (w tym FW/IPS) – użyteczne do:
    

- wykrywania beacon’ingu (powtarzalne połączenia co X sekund/godzin),
    
- obserwacji nieudanych prób połączeń,
    
- wychwytywania połączeń poza godzinami pracy,
    
- analizy dużych transferów wychodzących (np. >20 MB).
    

#### Przykładowe narzędzia do IR w środowisku enterprise:

- WMIC scripting – zdalne zbieranie danych z hostów (np. przez wmic /node:@systems.txt ...).
    
- SCCM reporting – raporty o inwentarzu, sterownikach, usługach itp.
    
- Kansa (PowerShell) – uruchamianie gotowych skryptów i zbieranie wyników z wielu hostów.
    
- Cyber-CPR – komercyjne narzędzie IR.
    
- Google Rapid Response (GRR) – darmowe narzędzie IR (Nix/OSX/Win), oparte na Pythonie, do zdalnego zbierania danych z hostów i centralnego zarządzania.
    

**