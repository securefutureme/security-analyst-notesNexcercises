# SQL Injection
### 1. Cel i definicja  

`modyfikacja`

Krótki opis techniki ataku:  
czym jest brute force
jaki jest cel atakującego,  
na jaką warstwę działa (web app, auth, proxy, API, sesja, upload, itp.).
  
### 2. Mechanizm działania ataku

`modyfikacja`

Opis krok po kroku:  
1. [Krok 1]  
2. [Krok 2]  
3. [Krok 3]  
4. [Efekt końcowy]  
  
### 3. Warianty techniki  

`modyfikacja`
  
### 4. Artefakty i telemetria  

`modyfikacja`
Gdzie ten atak najczęściej zostawia ślady:  

- access log webserwera,  
- error log webserwera,  
- logi aplikacyjne / auth,  
- WAF / reverse proxy / load balancer,  
- IDS / NDR / SIEM,  
- PCAP / analiza pakietów.  
  
### 5. Co analityk zobaczy w logach  
### Apache / Nginx / reverse proxy  
- [Typowe wpisy]  
- [Statusy HTTP]  
- [Powtarzalne URI]  
- [Wzorzec User-Agent / IP / Referrer]  
  
### Zeek / Suricata / Snort  
- [Typowe eventy]  
- [Pola do korelacji]  
- [Zachowanie sieciowe]  
  
### Splunk / SIEM  
- [Zapytanie / dashboard / korelacja]  
- [Wskaźniki wolumetryczne]  
- [Odchylenie od baseline]  
  
### Wireshark / PCAP  
- [Co filtrować]  
- [Jakie pola sprawdzić]  
- [Jak odróżnić ruch ręczny od automatycznego]  
  
## 6. Wskaźniki kompromitacji i heurystyki detekcyjne 

- [IOC / IOA 1]  
- [IOC / IOA 2]  
- [IOC / IOA 3]  
- [Anomalia czasowa]  
- [Anomalia wolumetryczna]  
- [Anomalia behawioralna]  
  
## 7. Triage SOC L1 / L2  
### L1  
- [Co sprawdzić najpierw]  
- [Jak potwierdzić]  
- [Kiedy eskalować]  
  
### L2  
- [Głębsza analiza]  
- [Korelacja z innymi źródłami]  
- [Ocena skuteczności ataku]  
- [Zakres incydentu]  
  
## 8. Wpływ biznesowy i ryzyko  

- [Skutek techniczny]  
- [Skutek dla użytkownika]  
- [Skutek dla organizacji]  
- [Poziom ryzyka]  
  
## 9. Mitigacje i hardening  

- [Mitigacja 1]  
- [Mitigacja 2]  
- [Mitigacja 3]  
- [Detekcja]  
- [Prewencja]  
- [Monitoring po wdrożeniu]  
  
## Źródła / referencje  
- [Źródło 1]  
- [Źródło 2]  
- [Źródło 3]