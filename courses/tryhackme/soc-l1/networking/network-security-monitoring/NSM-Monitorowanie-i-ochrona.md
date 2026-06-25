
**Monitorowanie perymetru** oznacza wykorzystywanie **firewalli**, **systemów IDS/IPS** oraz **kontroli dostępu** do analizowania ruchu, ograniczania ekspozycji i egzekwowania reguł bezpieczeństwa. Dzięki temu analitycy bezpieczeństwa mogą:

- **wykrywać wczesne etapy ataków**, takie jak skanowanie portów czy próby brute force
- **identyfikować błędne konfiguracje**, które pozostawiają wrażliwe usługi wystawione na zewnątrz
- **rozpoznawać anomalie w ruchu wychodzącym**, które mogą wskazywać na malware lub eksfiltrację danych

## Monitorowanie perymetru w praktyce

Poniżej znajdują się przykładowe scenariusze pokazujące, jak ważne jest monitorowanie perymetru.
### Scenariusz 1: sprawdzanie portów (_Port Scanning_)

Atakujący testuje sieć, aby sprawdzić, które porty są otwarte, a które zamknięte, podczas gdy firewall wykonuje swoje zadanie i blokuje połączenia.

## Log firewalla

```c
2025-09-22 08:30:04 ALLOW TCP 198.51.100.45:49876 -> 10.0.0.51:80
2025-09-22 08:30:05 BLOCK TCP 203.0.113.10:50001 -> 10.0.0.20:21
2025-09-22 08:30:06 BLOCK TCP 203.0.113.10:50002 -> 10.0.0.20:22
2025-09-22 08:30:07 ALLOW TCP 192.0.2.115:51235 -> 10.0.0.50:443
2025-09-22 08:30:08 BLOCK TCP 203.0.113.10:50003 -> 10.0.0.20:23
2025-09-22 08:30:09 BLOCK TCP 203.0.113.10:50004 -> 10.0.0.20:25
2025-09-22 08:30:10 ALLOW TCP 198.51.100.92:51111 -> 10.0.0.50:443
2025-09-22 08:30:11 BLOCK TCP 203.0.113.10:50005 -> 10.0.0.20:53
```
#### Analiza logu

Ten sam zewnętrzny adres IP (**203.0.113.10**) próbuje w krótkim czasie połączyć się z wieloma portami na tej samej maszynie wewnętrznej.

**Werdykt:**  
To klasyczny **port scan**. Atakujący szuka otwartej usługi, którą mógłby zaatakować.

---
### Scenariusz 2: atak na serwer WWW (_SQL Injection_)

Firmowa strona internetowa jest atakowana. System **IDS** dostarcza więcej szczegółów niż firewall, ponieważ identyfikuje także **typ ataku**.

#### Logi WAF (_Web Application Firewall_)

```c
timestamp=2025-09-22T09:14:44Z src_ip=192.0.2.130 action=ALLOW request="GET /index.html"
timestamp=2025-09-22T09:14:45Z src_ip=198.51.100.92 action=ALLOW request="GET /products.php?id=9"
timestamp=2025-09-22T09:14:46Z src_ip=[REDACTED] action=BLOCK request="GET /search.php?q=<script>alert('XSS')</script>" rule_id=941100 attack_type="XSS"
timestamp=2025-09-22T09:14:47Z src_ip=192.0.2.140 action=ALLOW request="GET /css/style.css"
timestamp=2025-09-22T09:15:42Z src_ip=[REDACTED] action=BLOCK request="GET /../../../../etc/passwd" rule_id=930120 attack_type="Directory Traversal"
...
.....
```

#### Analiza logu

Ten log pokazuje mieszankę akcji **ALLOW** i **BLOCK**. Analityk może od razu odfiltrować wpisy z `action=BLOCK`, aby szybko znaleźć zagrożenia. WAF wykonuje najtrudniejszą część pracy, ponieważ nie tylko blokuje żądanie, ale także wskazuje **dlaczego** zostało ono uznane za złośliwe.

-  Alert `attack_type="SQL Injection"` wskazuje, że atakujący próbuje wydobyć informacje z bazy danych.  
- Alert `attack_type="XSS"` oznacza próbę wstrzyknięcia złośliwego skryptu.  
- Alert `attack_type="Directory Traversal"` pokazuje próbę odczytu wrażliwych plików serwera.

**Werdykt:**  
WAF skutecznie identyfikuje i blokuje wiele typów ataków webowych pochodzących z podejrzanego adresu IP. To alert o **wysokim poziomie pewności**, wskazujący, że atakujący aktywnie atakuje stronę internetową.

### Scenariusz 3: odgadywanie hasła (_VPN Brute-Force_)

Atakujący próbuje odgadnąć hasło użytkownika, aby uzyskać zdalny dostęp do sieci. Powoduje to duży szum w logach uwierzytelniania.

#### Log bramy VPN

```c
2025-09-22 10:12:11 FAILED_AUTH TCP [REDACTED]:31245 -> 10.0.0.1:443 (user 'admin')  
2025-09-22 10:12:15 FAILED_AUTH TCP [REDACTED]:31248 -> 10.0.0.1:443 (user 'admin')  
2025-09-22 10:12:21 SUCCESS_AUTH TCP 198.51.100.88:41233 -> 10.0.0.1:443 (user 'b.jones')  
2025-09-22 10:12:08 FAILED_AUTH TCP [REDACTED]:31249 -> 10.0.0.1:443 (user 'guest')  
2025-09-22 10:12:09 FAILED_AUTH TCP [REDACTED]:31250 -> 10.0.0.1:443 (user 'user')
```

#### Analiza logu

Log jest wypełniony zdarzeniami **FAILED_AUTH** i **SUCCESS_AUTH**.  
Kilka udanych logowań z różnych adresów IP jest zjawiskiem normalnym.  
Problemem jest jednak **duża liczba nieudanych prób logowania**.

Aby znaleźć atak, analityk powinien filtrować lub grupować logi według **źródłowego adresu IP**. Po wykonaniu tego kroku szybko okaże się, że jeden podejrzany użytkownik lub adres odpowiada za setki nieudanych prób logowania w bardzo krótkim czasie.

**Werdykt:**  
Jeden podejrzany adres IP prowadzi atak **brute force** przeciwko bramie VPN. Atakujący próbuje używać listy popularnych nazw użytkowników, takich jak **admin**, **root**, **test** itd., aby znaleźć prawidłowe konto i je przejąć. Rozproszone udane logowania są normalnym ruchem generowanym przez legalnych pracowników.

---

## Kluczowe wnioski

Zadaniem analityka jest **oddzielenie normalnego ruchu od aktywności podejrzanej**.

Należy zwracać uwagę na podejrzane wzorce:

- **powtarzające się próby z jednego źródła do wielu celów** = skanowanie
- **powtarzające się próby z jednego źródła do jednego celu** = brute forcing
- **ruch pojawiający się w idealnych, regularnych odstępach czasu** = beaconing malware

**Kontekst ma kluczowe znaczenie.**  
Alert z IDS, który wyjaśnia, **dlaczego** coś zostało oznaczone jako zagrożenie, jest znacznie cenniejszy niż zwykły wpis firewalla o zablokowanym połączeniu.

Monitorowanie perymetru sieciowego jest **pierwszym krokiem do wykrywania ataków**.


## TRYHACKME - Zadania

- Przeanalizuj logi firewalla. Który adres IP wykonuje skanowanie portów?

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-6.png)

Mamy tu klasyczny przykład skanu portów, tak jak było to zaprezenowane wcześniej. Mamy tutaj dużo logów z blokadą TCP, gdzie jasno widać, że atakujący próbuje zeskanować porty, by sprawdzić które są otwarte a które zamknięte.

**Odp: 203.0.113.10**

- W logach **WAF** – który pojedynczy źródłowy adres IP odpowiada za wszystkie zablokowane ataki webowe?

![alt|697](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-5.png)
Możemy to ładnie wygrepować - szukamy samych logów gdzie firewall zablokował połączenie. No i też widzimy, co atakujący próbował zrobić.
**Odp. 198.51.100.12**

- W logach **VPN** – ile nieudanych prób ataku **brute force** odnotowano?

**Łatwo możemy to policzyć komendą: cat vpn_logs.txt | grep -c "FAILED_AUTH"**

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-7.png)

- Który podejrzany adres IP został wykryty podczas próby przeprowadzenia ataku **brute force** na bramę VPN?

Robimy podobną komendę, tylko bez count :)

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-8.png)

**Odp: 45.137.22.13**