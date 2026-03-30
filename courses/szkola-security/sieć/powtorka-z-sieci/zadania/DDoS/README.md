# DDoS

## Opis

DDoS (**Distributed Denial of Service**) to atak polegający na przeciążeniu usługi, serwera lub aplikacji przez bardzo dużą liczbę żądań pochodzących z wielu źródeł jednocześnie. Celem ataku nie jest zwykle uzyskanie dostępu do systemu, lecz **zakłócenie dostępności usługi** dla prawidłowych użytkowników.

Ataki DDoS mogą być prowadzone na różnych warstwach, w zależności od celu i techniki:

- **Volumetric attacks** – przeciążenie łącza dużą ilością ruchu,
- **Protocol attacks** – wykorzystanie słabości protokołów, np. SYN flood,
- **Application layer attacks** – przeciążenie aplikacji, np. przez dużą liczbę zapytań HTTP.

## Charakterystyka ataku

Typowe cechy ataków DDoS:

- nagły wzrost ruchu sieciowego,
- duża liczba podobnych żądań,
- spadek wydajności lub niedostępność usługi,
- wzrost użycia CPU, RAM lub przepustowości,
- żądania pochodzące z wielu różnych adresów IP.

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

| Zadanie | Link | Opis |
|---|---|---|
| Training | [Otwórz](./training/) | Wprowadzenie do analizy ruchu związanego z DDoS |
| Zadanie 1 | [Otwórz](./1/) | Identyfikacja podstawowych cech ataku |
| Zadanie 2 | [Otwórz](./2/) | Analiza wzorców ruchu i przeciążenia |
| Zadanie 3 | [Otwórz](./3/) | Zaawansowana analiza incydentu DDoS |

## Cel modułu

Celem tego modułu jest nauka rozpoznawania ataków DDoS w ruchu sieciowym oraz zrozumienie, jak wykrywać symptomy przeciążenia i jakie mechanizmy obronne stosuje się w praktyce.