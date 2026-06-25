### Scenariusz incydentu

**Initech Corp**, średniej wielkości firma świadcząca usługi finansowe, niedawno wdrożyła nowy **firewall** oraz **system wykrywania włamań (IDS)** do monitorowania perymetru sieci. W ciągu ostatniego miesiąca analitycy bezpieczeństwa zauważyli nietypowe wzorce ruchu, jednak zespół **SOC** był przeciążony i nie przeprowadził dokładniejszej analizy. Jako nowy analityk bezpieczeństwa otrzymałeś zadanie przejrzenia logów perymetru z jednego miesiąca, aby ustalić, **jakie techniki zastosował przeciwnik** oraz **czy udało mu się naruszyć perymetr**.

(tutaj omawiane są pliki z Wirtualnej maszyny w TryHackMe)
Mamy trzy zestawy logów z okresu incydentu. Dostępne pliki to :

**Firewall Logs:** `firewall.log`  
**WAF Logs:** `ids_alerts.log`  
**VPN Logs:** `vpn_auth.log`

---
### Zasoby sieciowe (_Network Assets_)

Sieć Initech Corp zawiera następujące zasoby, które można wykorzystać jako punkt odniesienia podczas analizy:

**10.0.0.20 – FINANCE-SRV1**  
Rola: serwer plików / serwer finansowy (SMB)  
System: Windows Server  
Zespół: Finance IT  
Krytyczność: wysoka

**10.0.0.50 – VPN-GW**  
Rola: brama VPN  
System: Linux  
Zespół: NetOps  
Krytyczność: krytyczna

**10.0.0.51 – APP-WEB-01**  
Rola: wewnętrzna aplikacja / serwer WWW  
System: Linux  
Zespół: Apps Team  
Krytyczność: wysoka

**10.0.0.60 – WORKSTATION-60**  
Rola: stacja robocza pracownika  
System: Windows 10  
Zespół: Sales  
Krytyczność: średnia

**10.8.0.23 – VPN-CLIENT-ATTK**  
Rola: klient VPN przypisany dynamicznie (_ephemeral_)  
System: brak danych  
Zespół: brak danych  
Krytyczność: krytyczna

**10.0.1.10 – DMZ-WEB**  
Rola: serwer WWW w strefie DMZ  
System: Linux  
Zespół: NetOps  
Krytyczność: średnia

---
### Analiza logów

Istnieją dwa sposoby badania logów:

- **Metoda 1: ręczna analiza logów z użyciem narzędzi wiersza poleceń**  
- **Metoda 2: analiza logów z użyciem Splunka**

Zacznijmy od ręcznego przeglądu logów.

---
### Metoda 1: ręczna analiza logów

#### Podstawowe sprawdzenie logów firewalla

Polecenie: `head firewall.log`
```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ head firewall.log 
2025-08-25 00:47:46 ALLOW TCP [REDACTED]:60317 -> 10.0.0.50:443
2025-08-25 01:29:33 ALLOW TCP 203.0.113.100:62718 -> [REDACTED]:443
2025-08-25 01:42:12 ALLOW TCP 203.0.113.100:55875 -> [REDACTED]:80
2025-08-25 03:30:47 ALLOW TCP [REDACTED]:63035 -> [REDACTED]:80
2025-08-25 04:06:58 ALLOW TCP 192.0.2.115:65458 -> [REDACTED]:25
2025-08-25 05:51:36 ALLOW TCP 203.0.113.100:56035 -> [REDACTED]:53
2025-08-25 06:09:50 ALLOW TCP 198.51.100.92:63418 -> [REDACTED]:8080
2025-08-25 07:39:29 ALLOW TCP [REDACTED]:55955 -> [REDACTED]:8080
2025-08-25 08:24:34 ALLOW TCP 198.51.100.92:63475 -> [REDACTED]:8080
2025-08-25 08:57:21 ALLOW TCP 198.51.100.92:58636 -> 10.0.0.50:53
```
Przykładowy wynik pokazuje wpisy **ALLOW** dotyczące ruchu TCP pomiędzy adresami zewnętrznymi i hostami wewnętrznymi.

Polecenie:  `head ids_alerts.log`
```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ head ids_alerts.log 
2025-08-25 00:12:53 [**] [1:2003272:1] ET POLICY Suspicious HTTP [**] [Classification: Suspicious Activity] [Priority: 3] {TCP} 198.51.100.92:20127 -> [REDACTED]:22
2025-08-25 01:50:30 [**] [1:2003377:1] ET POLICY Suspicious HTTP [**] [Classification: Suspicious Activity] [Priority: 1] {TCP} 203.0.113.100:56603 -> [REDACTED]:25
2025-08-25 02:16:39 [**] [1:2003437:1] ET INFO Possible Benign Scan [**] [Classification: Suspicious Activity] [Priority: 3] {TCP} [REDACTED]:62546 -> [REDACTED]:21
2025-08-25 02:23:07 [**] [1:2003344:1] ET WEB_SERVER Possible SQL Injection [**] [Classification: Suspicious Activity] [Priority: 2] {TCP} 198.51.100.45:12396 -> [REDACTED]:22
2025-08-25 02:25:48 [**] [1:2003445:1] ET POLICY Suspicious HTTP [**] [Classification: Suspicious Activity] [Priority: 3] {TCP} 192.0.2.115:3952 -> [REDACTED]:22
2025-08-25 03:35:00 [**] [1:2003160:1] ET INFO Possible Benign Scan [**] [Classification: Suspicious Activity] [Priority: 1] {TCP} [REDACTED]:38760 -> [REDACTED]:443
2025-08-25 05:02:36 [**] [1:2003187:1] ET WEB_SERVER Possible SQL Injection [**] [Classification: Suspicious Activity] [Priority: 1] {TCP} 198.51.100.92:46776 -> [REDACTED]:3389
2025-08-25 06:04:26 [**] [1:2003179:1] ET INFO Possible Benign Scan [**] [Classification: Suspicious Activity] [Priority: 2] {TCP} 198.51.100.92:20632 -> 10.0.0.50:8080
2025-08-25 14:12:11 [**] [1:2003500:1] ET INFO Possible Benign Scan [**] [Classification: Suspicious Activity] [Priority: 2] {TCP} 192.0.2.115:30225 -> [REDACTED]:445
2025-08-25 15:30:03 [**] [1:2003354:1] ET POLICY Suspicious HTTP [**] [Classification: Suspicious Activity] [Priority: 3] {TCP} 203.0.113.100:27572 -> [REDACTED]:4444
```

W logach IDS widać alerty takie jak:

- **ET POLICY Suspicious HTTP**
- **ET INFO Possible Benign Scan**
- **ET WEB_SERVER Possible SQL Injection**

wraz z klasyfikacją, priorytetem i kierunkiem ruchu.

Polecenie: `head vpn_auth.log`

```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$  head vpn_auth.log 
2025-08-25 08:25:10 [REDACTED] alice SUCCESS assigned_ip=10.8.0.143
2025-08-25 08:27:38 203.0.113.100 svc_[REDACTED] SUCCESS assigned_ip=10.8.0.131
2025-08-25 14:57:10 203.0.113.10 svc_[REDACTED] SUCCESS assigned_ip=10.8.0.116
2025-08-25 23:04:53 203.0.113.10 jsmith SUCCESS assigned_ip=10.8.0.31
2025-08-26 03:36:17 198.51.100.92 svc_[REDACTED] SUCCESS assigned_ip=10.8.0.62
2025-08-26 08:55:14 [REDACTED] bob SUCCESS assigned_ip=10.8.0.126
2025-08-26 10:02:45 198.51.100.92 svc_[REDACTED] SUCCESS assigned_ip=10.8.0.81
2025-08-27 03:11:33 198.51.100.45 bob SUCCESS assigned_ip=10.8.0.163
2025-08-28 02:52:16 192.0.2.115 alice SUCCESS assigned_ip=10.8.0.132
2025-08-28 03:20:33 [REDACTED] svc_[REDACTED] SUCCESS assigned_ip=10.8.0.193
```

W logach VPN widoczne są zarówno poprawne logowania użytkowników, jak i przypisane im adresy IP z puli VPN.

---
#### Próba rozpoznania (_Reconnaissance Attempt_)

Na początku analizy warto sprawdzić **zablokowane żądania w logach firewalla**.

Polecenie: `cat firewall.log | grep "BLOCK" | head
`
```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat firewall.log | grep "BLOCK" | head
2025-08-26 12:12:47 BLOCK TCP 203.0.113.10:64292 -> 10.0.0.50:21
2025-08-27 03:18:28 BLOCK TCP [REDACTED]:61701 -> [REDACTED]:23
2025-08-27 11:56:20 BLOCK TCP 203.0.113.10:64952 -> 10.0.0.50:22
2025-08-27 22:52:00 BLOCK TCP 203.0.113.10:63686 -> [REDACTED]:445
2025-08-28 10:00:00 BLOCK TCP [REDACTED]:50000 -> [REDACTED]:4444
2025-08-28 10:02:30 BLOCK TCP [REDACTED]:50005 -> [REDACTED]:22
```

Analiza zablokowanych połączeń pokazuje, że zewnętrzny adres IP prowadził próby komunikacji z hostami wewnętrznymi na różnych portach, takich jak:

- **21**
- **22**
- **23**
- **445**
- **3389**

To wskazuje na **sondowanie usług wystawionych w sieci**.

Aby ustalić, który adres IP odpowiada za największą liczbę wpisów **BLOCK**, można użyć polecenia:

`cat firewall.log | grep "BLOCK" | cut -d' ' -f5 | cut -d: -f1 | sort -nr | uniq -c`

Wynik pokazuje, że jeden podejrzany adres IP wyróżnia się znacząco liczbą zablokowanych prób połączeń. To właśnie od niego warto rozpocząć dalszą korelację zdarzeń w innych logach. Następnie można sprawdzić, czy firewall **kiedykolwiek dopuścił ruch** pochodzący z tego podejrzanego adresu IP.

Polecenie: `cat firewall.log | grep [REDACTED] | grep "ALLOW"
`
```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat firewall.log | grep [REDACTED] | grep "ALLOW"
2025-08-26 00:17:58 ALLOW TCP [REDACTED]:61009 -> [REDACTED]:4444
2025-08-26 22:04:34 ALLOW TCP [REDACTED]:55996 -> 10.0.0.50:445
2025-08-27 21:04:23 ALLOW TCP [REDACTED]:53944 -> 10.0.0.50:22
2025-08-28 15:50:50 ALLOW TCP [REDACTED]:56123 -> [REDACTED]:3389
2025-08-30 20:26:23 ALLOW TCP [REDACTED]:61685 -> [REDACTED]:4444
2025-09-02 09:25:06 ALLOW TCP [REDACTED]:50550 -> 10.0.0.50:22  -----------
2025-09-22 15:46:02 ALLOW TCP [REDACTED]:59771 -> [REDACTED]:23
2025-09-22 17:22:11 ALLOW TCP [REDACTED]:49360 -> 10.0.0.50:22
```

Wyniki pokazują, że podejrzany adres IP uzyskał dostęp do wewnętrznych usług, m.in. na portach:

- **4444**
- **445**
- **22**
- **3389**
- **23**

To sugeruje, że atakujący **mógł uzyskać dostęp do sieci wewnętrznej przez exploitację**.

---
#### VPN Brute-force / Credential Access

Kolejnym krokiem jest analiza logów VPN pod kątem **nieudanych prób logowania**.

Polecenie: `cat vpn_auth.log | grep FAIL | cut -d' ' -f3 | sort -nr | uniq -c`

```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat vpn_auth.log | grep FAIL | cut -d' ' -f3 | sort -nr | uniq -c
118 [REDACTED]
1 203.0.113.100
1 198.51.100.92
1 198.51.100.45
```

Wyniki pokazują, że jeden podejrzany adres IP ma **wiele nieudanych prób logowania VPN**, podczas gdy inne adresy mają ich pojedyncze sztuki.

Następnie zawęża się analizę do tego konkretnego adresu IP: `cat vpn_auth.log | grep [REDACTED]`

```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat vpn_auth.log | grep [REDACTED]
2025-09-03 02:19:00 [REDACTED] svc_[REDACTED] FAIL
2025-09-03 02:19:10 [REDACTED] svc_[REDACTED] FAIL
2025-09-03 02:19:20 [REDACTED] svc_[REDACTED] FAIL
2025-09-03 02:19:30 [REDACTED] svc_[REDACTED] FAIL
--------
-----------
2025-09-03 02:19:40 [REDACTED] svc_[REDACTED] SUCCESS assigned_ip=[REDACTED]
2025-09-03 02:19:50 [REDACTED] svc_[REDACTED] SUCCESS assigned_ip=[REDACTED]
2025-09-04 16:45:24 [REDACTED] svc_[REDACTED] SUCCESS assigned_ip=10.8.0.181
2025-09-05 13:21:52 [REDACTED] jsmith SUCCESS assigned_ip=10.8.0.94
2025-09-09 17:54:00 [REDACTED] jsmith SUCCESS assigned_ip=10.8.0.187
2025-09-09 19:15:51 [REDACTED] jsmith SUCCESS assigned_ip=10.8.0.134
2025-09-10 12:24:20 [REDACTED] bob SUCCESS assigned_ip=10.8.0.39
```

Wyniki pokazują serię wielu wpisów **FAIL** dotyczących konta usługowego, po których następują wpisy **SUCCESS** wraz z przypisaniem adresu IP z puli VPN.

To oznacza, że:

- wykonano wiele prób logowania na konto usługowe
- po tych próbach nastąpiło skuteczne logowanie
- atakujący otrzymał wewnętrzny adres IP VPN

Pierwszy przypisany adres IP można następnie wykorzystać do dalszej analizy śladów aktywności w innych logach.

---
#### Ruch boczny (_Lateral Movement_)

Na tym etapie wiadomo już, że atakujący uzyskał **początkowy dostęp** i otrzymał **wewnętrzny adres IP**. Następnie należy sprawdzić logi firewalla pod kątem śladów ruchu bocznego z przejętego hosta.

Polecenie: `cat firewall.log | grep [REDACTED] | grep "ALLOW" | head`

```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat firewall.log | grep [REDACTED] | grep "ALLOW" | head 
2025-09-05 06:00:00 ALLOW TCP [REDACTED]:2000 -> [REDACTED]:22
2025-09-05 06:10:00 ALLOW TCP [REDACTED]:2001 -> [REDACTED]:445
2025-09-05 06:20:00 ALLOW TCP [REDACTED]:2002 -> [REDACTED]:22
2025-09-05 06:40:00 ALLOW TCP [REDACTED]:2004 -> [REDACTED]:3389
2025-09-05 07:30:00 ALLOW TCP [REDACTED]:2009 -> [REDACTED]:22
2025-09-05 08:00:00 ALLOW TCP [REDACTED]:2012 -> [REDACTED]:22
```

Wyniki pokazują, że przejęty host komunikuje się z maszynami wewnętrznymi:

- **10.0.0.20**
- **10.0.0.51**
- **10.0.0.60**

na portach:

- **22 (SSH)**
- **445 (SMB)**
- **3389 (RDP)**

To wskazuje na próbę rozpoznania i wykorzystania usług wewnętrznych.

Następnie warto przejść do logów IDS i sprawdzić, jakie reguły zostały uruchomione dla tego przejętego hosta.

Polecenie: `cat ids_alerts.log | grep [REDACTED] | head`

```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat ids_alerts.log | grep [REDACTED] | head    
2025-09-05 06:00:00 [**] [1:2000200:1] ET SCAN Possible SSH Scan [**] [Classification: Attempted Unauthorized Access] [Priority: 1] {TCP} [REDACTED]:2000 -> [REDACTED]:22
2025-09-05 06:10:00 [**] [1:2000201:1] ET EXPLOIT Possible MS-SMB Lateral Movement [**] [Classification: Attempted Unauthorized Access] [Priority: 1] {TCP} [REDACTED]:2001 -> [REDACTED]:445
2025-09-05 06:20:00 [**] [1:2000202:1] ET SCAN Possible SSH Scan [**] [Classification: Attempted Unauthorized Access] [Priority: 1] {TCP} [REDACTED]:2002 -> [REDACTED]:22
2025-09-05 06:30:00 [**] [1:2000203:1] ET EXPLOIT Possible RDP Brute Force [**] [Classification: Attempted Unauthorized Access] [Priority: 1] {TCP} [REDACTED]:2003 -> [REDACTED]:3389
2025-09-05 07:10:00 [**] [1:2000207:1] ET SCAN Possible SSH Scan [**] [Classification: Attempted Unauthorized Access] [Priority: 1] {TCP} [REDACTED]:2007 -> [REDACTED]:22
2025-09-05 07:20:00 [**] [1:2000208:1] ET EXPLOIT Possible RDP Brute Force [**] [Classification: Attempted Unauthorized Access] [Priority: 1] {TCP} [REDACTED]:2008 -> [REDACTED]:3389
2025-09-05 07:30:00 [**] [1:2000209:1] ET SCAN Possible SSH Scan [**] [Classification: Attempted Unauthorized Access] [Priority: 1] {TCP} [REDACTED]:2009 -> [REDACTED]:22
```

Alerty pokazują m.in.:

- **Possible SSH Scan**
- **Possible MS-SMB Lateral Movement**
- **Possible RDP Brute Force**

To sugeruje, że przejęty host próbuje wykorzystywać różne usługi na innych hostach wewnętrznych.

Szczególnie interesujący jest alert dotyczący **SMB lateral movement**. Aby zawęzić analizę do zdarzeń związanych z SMB, można użyć polecenia: `cat ids_alerts.log | grep -n [REDACTED] | grep 'SMB' | cut -d' ' -f6,7,8,9,10,19,21 | head`

```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat ids_alerts.log | grep -n [REDACTED] | grep 'SMB' | cut -d' ' -f6,7,8,9,10,19,21 | head
EXPLOIT Possible MS-SMB Lateral Movement [REDACTED]:2001 [REDACTED]:445
EXPLOIT Possible MS-SMB Lateral Movement [REDACTED]:2006 [REDACTED]:445
EXPLOIT Possible MS-SMB Lateral Movement [REDACTED]:2010 [REDACTED]:445
EXPLOIT Possible MS-SMB Lateral Movement [REDACTED]:2016 [REDACTED]:445
EXPLOIT Possible MS-SMB Lateral Movement [REDACTED]:2033 [REDACTED]:445
EXPLOIT Possible MS-SMB Lateral Movement [REDACTED]:2035 [REDACTED]:445
```

Wyniki potwierdzają liczne alerty: **EXPLOIT Possible MS-SMB Lateral Movement**. To potwierdza, że przejęty host **wykorzystywał usługę SMB**, co wskazuje na **udany ruch boczny**.

---
#### Beaconing C2

Skoro istnieją już dowody na ruch boczny, kolejnym krokiem jest poszukiwanie oznak **komunikacji C2**. W logach IDS można znaleźć alerty wskazujące bezpośrednio na **Possible C2 Beaconing**.

Polecenie: `cat ids_alerts.log | grep C2 | head
`
```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat ids_alerts.log | grep C2 | head
2025-09-11 01:00:00 [**] [1:2001000:1] ET TROJAN Possible C2 Beaconing [**] [Classification: A network Trojan was detected] [Priority: 1] {TCP} [REDACTED]:30000 -> [REDACTED]:4444
2025-09-11 07:00:00 [**] [1:2001001:1] ET TROJAN Possible C2 Beaconing [**] [Classification: A network Trojan was detected] [Priority: 1] {TCP} [REDACTED]:30001 -> [REDACTED]:4444
2025-09-11 13:00:00 [**] [1:2001002:1] ET TROJAN Possible C2 Beaconing [**] [Classification: A network Trojan was detected] [Priority: 1] {TCP} [REDACTED]:30002 -> [REDACTED]:4444
2025-09-12 13:00:00 [**] [1:2001006:1] ET TROJAN Possible C2 Beaconing [**] [Classification: A network Trojan was detected] [Priority: 1] {TCP} [REDACTED]:30006 -> [REDACTED]:4444
2025-09-12 19:00:00 [**] [1:2001007:1] ET TROJAN Possible C2 Beaconing [**] [Classification: A network Trojan was detected] [Priority: 1] {TCP} [REDACTED]:30007 -> [REDACTED]:4444
2025-09-13 01:00:00 [**] [1:2001008:1] ET TROJAN Possible C2 Beaconing [**] [Classification: A network Trojan was detected] [Priority: 1] {TCP} [REDACTED]:30008 -> [REDACTED]:4444
2025-09-13 07:00:00 [**] [1:2001009:1] ET TROJAN Possible C2 Beaconing [**] [Classification: A network Trojan was detected] [Priority: 1] {TCP} [REDACTED]:30009 -> [REDACTED]:4444
```

Wyniki pokazują wiele wpisów z klasyfikacją: **ET TROJAN Possible C2 Beaconing** w regularnych odstępach czasu, kierowanych do portu **4444**.

To bardzo mocno sugeruje komunikację pomiędzy przejętym hostem a serwerem **Command and Control**. Aby wyodrębnić host wewnętrzny odpowiedzialny za beaconing, można użyć dalszego filtrowania w logach IDS. 

**Commandline:** `cat ids_alerts.log | grep -n [REDACTED] | cut -d' ' -f6,7,8,9,10,19,22,23 | uniq -c | sort -nr | head
`
**Commandline:** `cat ids_alerts.log | grep -n [REDACTED]   | cut -d' ' -f6,7,8,9,10,19,22,23 | uniq -c | sort -nr | head

```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat ids_alerts.log | grep -n [REDACTED]  | cut -d' ' -f6,7,8,9,10,19,22,23 | sort -nr | uniq -c | sort -nr       
80 TROJAN Possible C2 Beaconing [**] {TCP} [REDACTED]:4444
32 INFO Possible HTTP POST Large {TCP} [REDACTED]:80
28 INFO Possible HTTP POST Large {TCP} [REDACTED]:8080
23 POLICY Suspicious HTTP [**] [Classification:
2 WEB_SERVER Possible SQL Injection [**] 10.0.0.50:53
2 WEB_SERVER Possible SQL Injection [**] 10.0.0.50:3389
2 WEB_SERVER Possible SQL Injection [**] [REDACTED]:8080
2 WEB_SERVER Possible SQL Injection [**] [REDACTED]:445
2 INFO Possible Benign Scan [**] 10.0.0.50:21
1 WEB_SERVER Possible SQL Injection [**] [REDACTED]:53
1 WEB_SERVER Possible SQL Injection [**] [REDACTED]:443
````

Wyniki pokazują, że jeden z hostów wewnętrznych generuje dużą liczbę alertów związanych z:

- **C2 Beaconing**
- **Suspicious HTTP**
- **Possible SQL Injection**

Statystyki alertów dodatkowo potwierdzają, że właśnie ten host jest prawdopodobnie **zainfekowanym systemem**, który utrzymuje łączność z zewnętrznym serwerem C2.

Analiza ta wskazuje, że:

- sieć wewnętrzna została skutecznie naruszona
- istnieje zewnętrzny adres IP pełniący rolę serwera C2
- przejęty host wysyła do niego regularne beacony

---

#### Próba eksfiltracji danych (_Data Exfiltration Attempt_)

Po ustaleniu obecności C2 i innych podejrzanych działań należy sprawdzić, czy pojawiają się oznaki **eksfiltracji danych**. W tym celu filtruje się logi firewalla dla przejętych hostów i analizuje ruch wychodzący do adresów zewnętrznych.

Polecenie: `cat firewall.log | grep [REDACTED] | cut -d' ' -f5,6,7 | uniq | sort
`
```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat firewall.log | grep [REDACTED]  | cut -d' ' -f5,6,7 | uniq | sort 
[REDACTED]:40000 -> [REDACTED]:8080
[REDACTED]:40001 -> [REDACTED]:8080
[REDACTED]:40002 -> [REDACTED]:8080
[REDACTED]:40003 -> [REDACTED]:80
[REDACTED]:40004 -> [REDACTED]:80
[REDACTED]:40005 -> [REDACTED]:80
[REDACTED]:40006 -> [REDACTED]:80
[REDACTED]:40007 -> [REDACTED]:80
[REDACTED]:40008 -> [REDACTED]:80
[REDACTED]:40009 -> [REDACTED]:8080
[REDACTED]:40010 -> [REDACTED]:80
[REDACTED]:40015 -> [REDACTED]:80
[REDACTED]:40016 -> [REDACTED]:80
[REDACTED]:40017 -> [REDACTED]:8080
[REDACTED]:40018 -> [REDACTED]:80
[REDACTED]:40019 -> [REDACTED]:8080
```

Wyniki pokazują, że przejęty host wysyła znaczną liczbę połączeń do zewnętrznego adresu IP na porty:

- **80**
- **8080**

To wskazuje na intensywny ruch wychodzący do systemu zewnętrznego. Następnie warto sprawdzić, jakie alerty generuje IDS dla tej aktywności.

**Polecenie: `cat ids_alerts.log | grep [REDACTED] | tail**`

```c
ubuntu@tryhackme:~/Desktop/Perimeter_logs/challenge$ cat ids_alerts.log | grep [REDACTED] | tail
2025-09-27 07:00:00 [**] [1:2002050:1] ET INFO Possible HTTP POST Large Upload [**] [Classification: Potential Data Exfiltration] [Priority: 2] {TCP} [REDACTED]:40050 -> [REDACTED]:8080
2025-09-27 11:00:00 [**] [1:2002051:1] ET INFO Possible HTTP POST Large Upload [**] [Classification: Potential Data Exfiltration] [Priority: 2] {TCP} [REDACTED]:40051 -> [REDACTED]:8080
2025-09-27 15:00:00 [**] [1:2002052:1] ET INFO Possible HTTP POST Large Upload [**] [Classification: Potential Data Exfiltration] [Priority: 2] {TCP} [REDACTED]:40052 -> [REDACTED]:80802025-09-28 07:00:00 [**] [1:2002056:1] ET INFO Possible HTTP POST Large Upload [**] [Classification: Potential Data Exfiltration] [Priority: 2] {TCP} [REDACTED]:40056 -> [REDACTED]:80
2025-09-28 11:00:00 [**] [1:2002057:1] ET INFO Possible HTTP POST Large Upload [**] [Classification: Potential Data Exfiltration] [Priority: 2] {TCP} [REDACTED]:40057 -> [REDACTED]:8080
2025-09-28 15:00:00 [**] [1:2002058:1] ET INFO Possible HTTP POST Large Upload [**] [Classification: Potential Data Exfiltration] [Priority: 2] {TCP} [REDACTED]:40058 -> [REDACTED]:80
2025-09-28 19:00:00 [**] [1:2002059:1] ET INFO Possible HTTP POST Large Upload [**] [Classification: Potential Data Exfiltration] [Priority: 2] {TCP} [REDACTED]:40059 -> [REDACTED]:8080
```

Wyniki pokazują alerty: **ET INFO Possible HTTP POST Large Upload**  / **Classification: Potential Data Exfiltration** - wskazujące na duże transfery wychodzące realizowane metodą **HTTP POST**.

To stanowi dowód na **próby eksfiltracji danych** z sieci wewnętrznej. 

Jeżeli analiza zostanie pogłębiona i odpowiednio skorelowana z innymi logami, można znaleźć jeszcze więcej podejrzanych aktywności związanych z tym incydentem.

---
### Metoda 2: analiza logów przez Splunka

Jako analityk SOC trzeba pamiętać, że ręczna analiza logów może stać się bardzo czasochłonna, zwłaszcza gdy pliki logów są duże. Dlatego na maszynie wirtualnej udostępniono również instancję **Splunka**, której można użyć do analizy.

**Zadania:**

**Przeanalizuj logi firewalla. Który zewnętrzny adres IP przeprowadził najwięcej działań rozpoznawczych?**

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-10.png)

**Odp. 203.0.113.45**

W logu firewalla, który host wewnętrzny był celem skanowania?

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-11.png)

**Odp. 10.0.0.20**

Która nazwa użytkownika była celem ataku w logach VPN?

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-12.png)

**Odp. svc_backup**

Jaki wewnętrzny adres IP został przypisany po udanym logowaniu VPN?

index="network_logs" sourcetype="vpn_logs" result=SUCCESS username=svc_backup| spath src_ip | search src_ip="203.0.113.45"

Ten filtr nam pokazuje czas, nazwę użytkownika, źródłowy adres IP i przypisany wewnętrzny adres IP dla udanego logowania VPN z adresu `203.0.113.45` na konto `svc_backup`.

![alt](/courses/tryhackme/soc-l1/networking/network-security-monitoring/Attachments/image-13.png)

**Odp. assigned_ip jako pierwsze pokazuje 10.8.0.23

Który port został użyty do prób ruchu bocznego przez SMB?`

SMB – używane porty sieciowe
- TCP 445 – wykorzystywany przez nowsze wersje SMB (SMBv2/v3) do komunikacji „Direct Host”, czyli bezpośrednio przez TCP/IP, bez NetBIOS.
- TCP 139 – używany przez starsze SMB (SMBv1), działające w oparciu o NetBIOS over TCP/IP (NBT).
- UDP 137 i UDP 138 – obsługują odpowiednio rozwiązywanie nazw NetBIOS oraz usługi datagramowe.
- UDP 443 – wykorzystywany przez nowoczesne wdrożenia SMB over QUIC w nowszych wersjach Windows Server.

<img width="1971" height="1471" alt="image" src="https://github.com/user-attachments/assets/34a549cb-4f49-43d6-b94f-01bb6e530985" />

**Odp. 445**


W logach IDS, który host wysyłał beacony do serwera C2?

Szukamy alertu "ET TROJAN Possible C2 Beaconing" w logach IDS, następnie patrzymy na "scr_ip":

<img width="2458" height="1548" alt="image" src="https://github.com/user-attachments/assets/867a5899-3f12-43f5-ac2d-25d3287f4a41" />

**Odp. 10.0.0.60**

Jaki adres IP został podczas analizy powiązany z infrastrukturą C2?

Tak jak wyżej - sprawdzamy "dst_ip"

**Odp. 198.51.100.77**

Który host wykazywał próby eksfiltracji danych?

Szukamy tutaj "alertów" z informacją "ET INFO Possible HTTP POST Large Upload".

<img width="2030" height="1376" alt="image" src="https://github.com/user-attachments/assets/0b4d4f2e-bc2d-4134-90b9-10659d2dfca6" />

**Odp. 10.0.0.51**
