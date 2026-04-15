# DDoS

## Opis

DDoS (**Distributed Denial of Service**) to atak polegający na przeciążeniu usługi, serwera lub aplikacji przez bardzo dużą liczbę żądań pochodzących z wielu źródeł jednocześnie. Celem ataku nie jest zwykle uzyskanie dostępu do systemu, lecz **zakłócenie dostępności usługi** dla prawidłowych użytkowników.

## Cechy ataków DDoS:

- nagły wzrost ruchu sieciowego,
- duża liczba podobnych żądań,
- spadek wydajności lub niedostępność usługi,
- wzrost użycia CPU, RAM lub przepustowości,
- żądania pochodzące z wielu różnych adresów IP.

## Typy atakow DDoS

- **Volumetric attacks** – przeciążenie łącza dużą ilością ruchu,
- **Protocol attacks** – wykorzystanie słabości protokołów, np. SYN flood,
- **Application layer attacks** – przeciążenie aplikacji, np. przez dużą liczbę zapytań HTTP.

## Jak się bronić

Najczęściej stosowane metody ochrony przed DDoS:

- **rate limiting** – ograniczanie liczby żądań,
- **firewall i ACL** – filtrowanie niepożądanego ruchu,
- **WAF / reverse proxy / CDN** – ochrona aplikacji webowych,
- **systemy anty-DDoS** – wykrywanie i odfiltrowywanie ruchu atakującego,
- **load balancing** – rozłożenie ruchu na wiele instancji,
- **monitoring i alerting** – szybkie wykrywanie anomalii,
- **segmentacja usług** – ograniczenie wpływu ataku na całą infrastrukturę,
- **playbook reagowania** – gotowe procedury na wypadek incydentu.

## Zadania

| Zadanie | Link |
|---|---|
| Training | [Link](./training/training.pcap-analysis.md) | 
| Zadanie 1 | [Link](courses/szkola-security/sieć/powtorka-z-sieci/zadania%20-%20szkoła/DDoS/1/1.pcap-analysis.md) | 
| Zadanie 2 | [Link](courses/szkola-security/sieć/powtorka-z-sieci/zadania%20-%20szkoła/DDoS/2/2.pcap-analysis.md) | 
| Zadanie 3 | [Link](courses/szkola-security/sieć/powtorka-z-sieci/zadania%20-%20szkoła/DDoS/3/3.pcap-analysis.md) |
