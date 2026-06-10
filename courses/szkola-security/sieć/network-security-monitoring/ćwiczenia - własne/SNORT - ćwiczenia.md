
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
