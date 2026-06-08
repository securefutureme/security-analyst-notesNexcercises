
---
## Przykładowe reguły do ćwiczeń

### 1. Wykrycie ruchu ICMP

```text
alert icmp any any -> any any (msg:"LOCAL ICMP traffic detected"; sid:1000001; rev:1;)
```

Cel ćwiczenia:

- sprawdzić, czy Snort poprawnie czyta PCAP,
- wygenerować prosty alert,
- potwierdzić działanie `local.rules`.

---
### 2. Wykrycie ruchu HTTP

```text
alert tcp any any -> any 80 (msg:"LOCAL HTTP traffic detected"; sid:1000002; rev:1;)
```

Cel ćwiczenia:

- wykryć ruch TCP do portu 80,
- sprawdzić podstawowe dopasowanie po porcie docelowym.
### 3. Wykrycie User-Agenta sqlmap

```text
alert tcp any any -> any 80 (msg:"LOCAL SQLmap User-Agent detected"; content:"User-Agent|3A|"; nocase; http_header; content:"sqlmap"; nocase; http_header; sid:1000011; rev:1;)
```

Cel ćwiczenia:

- wykryć narzędzie sqlmap po nagłówku HTTP `User-Agent`,
- przećwiczyć `content`, `nocase` i `http_header`.

---
### 4. Wykrycie User-Agenta WPScan

```text
alert tcp any any -> any 80 (msg:"LOCAL WPScan User-Agent detected"; content:"User-Agent|3A|"; nocase; http_header; content:"WPScan"; nocase; http_header; sid:1000012; rev:1;)
```

Cel ćwiczenia:

- wykryć narzędzie WPScan po nagłówku HTTP,
- przećwiczyć analizę żądań HTTP.

---
### 5. Wykrycie directory traversal

```text
alert tcp any any -> any 80 (msg:"LOCAL Directory traversal sequence detected"; content:"../../"; http_uri; sid:1000013; rev:1;)
```

Cel ćwiczenia:

- wykryć próbę przejścia katalogów,
- przećwiczyć analizę URI.

---
### 6. Wykrycie XSS

```text
alert tcp any any -> any 80 (msg:"LOCAL Possible XSS script tag in URI"; content:"<script>"; nocase; http_uri; sid:1000014; rev:1;)
```

Cel ćwiczenia:

- wykryć prostą próbę XSS,
    
- sprawdzić dopasowanie ciągu znaków w URI.
    

---

### 7. Wykrycie parametru cmd=

```text
alert tcp any any -> any 80 (msg:"LOCAL Possible command parameter in URI"; content:"cmd|3D|"; nocase; http_uri; sid:1000015; rev:1;)
```

Cel ćwiczenia:

- wykryć podejrzany parametr `cmd=`,
    
- przećwiczyć zapis hex dla znaku `=`.
    

---

### 8. Wykrycie potencjalnego backdoora

```text
alert tcp any any -> any 80 (msg:"LOCAL Possible backdoor.php request"; content:"GET"; http_method; content:"backdoor.php"; http_uri; sid:1000016; rev:1;)
```

Cel ćwiczenia:

- wykryć żądanie GET do pliku `backdoor.php`,
    
- połączyć warunek na metodę HTTP i URI.
    

---

### 9. Wykrycie próby RCE z whoami

```text
alert tcp any any -> any 80 (msg:"LOCAL Possible RCE whoami in URI"; content:"|3D|whoami"; nocase; http_uri; sid:1000017; rev:1;)
```

Cel ćwiczenia:

- wykryć parametr zawierający `=whoami`,
    
- przećwiczyć prostą detekcję command injection / RCE.
    

---

## Scenariusz ćwiczenia praktycznego

### Krok 1. Przygotowanie katalogów

W katalogu sekcji SNORT tworzę strukturę:

```bash
mkdir -p pcaps screenshots logs
```

Przykład:

```text
SNORT/
├── README.md
├── pcaps/
├── screenshots/
└── logs/
```

---

### Krok 2. Pobranie PCAP

Pobieram plik `.pcap` z publicznego źródła do ćwiczeń traffic analysis.

Na potrzeby pierwszego ćwiczenia najlepiej wybrać PCAP zawierający ruch HTTP, ponieważ łatwiej testować reguły z `http_uri`, `http_header` i `http_method`.

---

### Krok 3. Szybki podgląd PCAP

Przed uruchomieniem Snorta sprawdzam, czy plik zawiera ruch:

```bash
tcpdump -r sample.pcap -nn -c 20
```

Jeśli chcę sprawdzić tylko HTTP:

```bash
tcpdump -r sample.pcap -nn 'tcp port 80' -c 20
```

---

### Krok 4. Dodanie pierwszej szerokiej reguły

Do pliku `local.rules` dodaję prostą regułę testową:

```text
alert tcp any any -> any 80 (msg:"LOCAL HTTP traffic detected"; sid:1000002; rev:1;)
```

---

### Krok 5. Sprawdzenie konfiguracji

```bash
sudo snort -T -c /etc/snort/snort_kurs.conf
```

Jeżeli test przejdzie poprawnie, można przejść dalej.

---

### Krok 6. Uruchomienie Snorta na PCAP

```bash
sudo snort -c /etc/snort/snort_kurs.conf -A console -q -r pcaps/sample.pcap
```

Jeżeli w PCAP znajduje się ruch HTTP na porcie 80, Snort powinien wygenerować alert.

---

### Krok 7. Zawężenie reguły

Po potwierdzeniu, że Snort działa, dodaję bardziej konkretną regułę, np.:

```text
alert tcp any any -> any 80 (msg:"LOCAL Possible command parameter in URI"; content:"cmd|3D|"; nocase; http_uri; sid:1000015; rev:1;)
```

Następnie ponownie uruchamiam test konfiguracji:

```bash
sudo snort -T -c /etc/snort/snort_kurs.conf
```

I analizuję PCAP:

```bash
sudo snort -c /etc/snort/snort_kurs.conf -A console -q -r pcaps/sample.pcap
```

---

### Krok 8. Dokumentacja wyniku

Do README dodaję:

- jakiego PCAP użyłem,
    
- jaką regułę napisałem,
    
- czy reguła wygenerowała alert,
    
- screenshot z konsoli,
    
- krótki wniosek.
    

Przykład opisu:

```text
Reguła wykryła żądanie HTTP zawierające parametr cmd= w URI. 
Taki parametr może wskazywać na próbę command injection albo testowanie aplikacji pod kątem RCE.
```

---

## Troubleshooting

### Brak alertów

Możliwe przyczyny:

- PCAP nie zawiera ruchu pasującego do reguły,
    
- reguła jest zbyt wąska,
    
- ruch jest na innym porcie niż 80,
    
- ruch HTTP jest zaszyfrowany,
    
- `local.rules` nie jest załadowany w konfiguracji Snorta,
    
- występuje błąd składni reguły.
    

Na start warto użyć bardzo szerokiej reguły:

```text
alert ip any any -> any any (msg:"LOCAL Any IP traffic detected"; sid:1000099; rev:1;)
```

Jeśli ta reguła działa, problem jest w logice konkretnej reguły, a nie w Snorcie.

---

### Błąd konfiguracji

Po każdej zmianie uruchamiam:

```bash
sudo snort -T -c /etc/snort/snort_kurs.conf
```

Jeśli Snort zwraca błąd, sprawdzam:

- średniki `;`,
    
- nawiasy `(` i `)`,
    
- cudzysłowy,
    
- unikalność `sid`,
    
- poprawność zmiennych takich jak `$HOME_NET` albo `$HTTP_PORTS`.
    

---

## Wnioski

Snort pozwala tworzyć własne reguły detekcyjne i sprawdzać je zarówno na ruchu live, jak i na zapisanych plikach PCAP.

Najważniejszy workflow pracy z własną regułą:

1. Dodać regułę do `local.rules`.
    
2. Sprawdzić konfigurację poleceniem `snort -T`.
    
3. Uruchomić Snorta na PCAP.
    
4. Sprawdzić alerty.
    
5. Zawęzić lub poprawić regułę.
    
6. Udokumentować wynik w repozytorium.
    

W praktyce SOC najważniejsze jest nie tylko napisanie reguły, ale też zrozumienie, dlaczego dana reguła wygenerowała alert i jaki ślad ataku został znaleziony w ruchu sieciowym.