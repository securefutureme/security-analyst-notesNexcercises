
Dla każdego z 3 załączników odpowiedz na następujące pytania:

## **Próbka: Mail NEW ORDER FOR krain**

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/1-image.png)

1. **Czy dana wiadomość jest według ciebie phishingiem, czy bezpieczną wiadomością?** 

Według mnie tak - na pierwszy rzut oka wydaje się podejrzana, czytając domenę mailową - fisrtgreen a nie firstgreen. Pierwsza czerwona lampka.

Odp: Według mnie **wiadomość jest phishingiem.**

2. **Wymień wszystkie wskazówki, które wskazują według ciebie na to, że wiadomość jest phishingiem** 

- domena **fistrgreen.com**? załącznik [ krain[.]com ] (.htm i .html są używane do omijania filtrów URL).  
- Quote on the attached (odniesienie do załącznika bezpośrednio - socjotechnika (NEW ORDER)  
- Wiadomość od managera - pisownia bardzo "nieoficjalna i napisana na szybko" - chociaż akurat to może nie wykluczać.
- Czerwona flaga - zamówienie w postaci plików .htm? (zwykle się wysyła invoice w .pdf)

2. **Przeanalizuj nagłówki wiadomości:** 
   
a. Jaki był wynik testu SPF, DKIM i DMARC?

-  **SPF** - softfail
- **DMARC** -fail, 
- **DKIM** - fail

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/2-image.png)

b. Czy wiadomość jest zespoofowana, jeżeli tak to dlaczego i która technika spoofingu została zastosowana? 

Odp. Tak, wiadomość najprawdopodobniej jest spoofowana. Nagłówki pokazują 
**spf=softfail, dkim=fail i dmarc=fail**, więc wiadomość podszywa się pod domenę **fisrtgreen.com,** ale nie przechodzi mechanizmów potwierdzających, że została wysłana z autoryzowanego źródła. Zastosowana technika to najpewniej spoofing domeny nadawcy, obejmujący podszycie się pod adres **w** **polu From oraz Return-Path.**

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/3-image.png)

c. Jaki było oryginalny adres IP, z którego wysłano wiadomość?
Odp. **194[.]104[.]136[.]232**
![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/4-image.png)

4. Przeanalizuj załącznik wiadomości: 
   a. Jaka jest suma kontrolna MD5 i SHA-256 z załącznika?

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/9-image.png)
 
 Odp.
- MD5 - 3E26BC4D17DF91A5ABAE5F13B5F44C26
- **SHA-256:** 18d78c53f503b8a924617477f4c9b80ab74e5dc12732b487554b8e84df21fb91

b. Jakie techniki phishingowe stosuje załącznik? 

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/10-image.png)

Odp. 
- Załącznik udaje stronę **Microsoft SharePoint,** żeby wyglądać wiarygodnie. 
- Po otwarciu załącznika wyskakuje nam:
  a) **fałszywe okno logowania**, (przygotowana jako lokalny plik HTML otwierany bezpośrednio z komputera ofiary)
  b) **gotowy adres e-mail ofiary** (który mógł zostać osadzony bezpośrednio w pliku albo doładowany automatycznie przez prosty skrypt, np. z nazwy pliku, parametru w linku lub wcześniej przygotowanej wartości dla konkretnego odbiorcy.) 
  c) rozmyty plik Excela w tle, żeby przekonać użytkownika że po wpisaniu hasła otworzy dokument. 
- To klasyczna próba wyłudzenia danych logowania przez podszycie się pod znaną usługę.

**c. Do jakiej domeny wysyłane są poświadczenia (login i hasło)?**

Odp. **jodytravel.com**

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/11-image.png)

## Próbka: **phish_alert_iocp**

1. **Czy dana wiadomość jest według ciebie phishingiem czy bezpieczna wiadomością?
![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/12-image.png)
![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/13-image.png)

**Odp.** Wiadomość jest phishingiem.

2. **Wymień wszystkie wskazówki, które wskazują według ciebie na to, że wiadomość jest phishingiem**  

a) Załącznik .html  

b) Invoice Payment który trafia do spamu? (mamy napisane [SPAM] w treści)

c) Bardzo dziwny received-from (127.0.0.1 - loopback?)  

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/14-image.png)

d) Wygląda to jakby nadawca i odbiorca były takie same (FROM "kkolarik" TO "kelli kolarik")  

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/21-image.png)

e) Nadawca podszywa się pod **chg.com** ale technicznie pochodzi z hostów w AWS i z domeny znlc.jp, a nie z rzeczywistej infrastruktury firmowej chg.com.

3. **Przeanalizuj nagłówki wiadomości:**

**a. Jaki był wynik testu SPF, DKIM i DMARC?**  

- **spf=temperror** oznacza tymczasowy błąd uwierzytelniania SPF (Sender Policy Framework), czyli serwer odbierający e-mail nie mógł poprawnie zweryfikować nadawcy z powodu tymczasowego problemu z systemem DNS.

- **DMARC=temperror** (tak jak wyżej)  
- **DKIM=none**  (odbiorca nie może potwierdzic że została autentycznie wysłana przez domenę nadawcy)

**b. Czy wiadomość jest zespoofowana, jeżeli tak to dlaczego i która technika spoofingu została zastosowana?**

Nie jestesmy w stanie przeanalizować pod kątem bezpieczeństwa SPF/DMARC=temperror, możliwe, że DNS tego IP był zespoofowany.
Technika: Envelope-Path (podszycie się pod nadawcę) (return-path i From: są takie same - SPF się nie powiódł)  

c. Jaki było oryginalny adres IP z którego wysłano wiadomość?

**164[.]46[.]112[.]91**  

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/15-image.png)

4. **Przeanalizuj załącznik wiadomości:

**a. Jaka jest suma kontrolna MD5 i SHA-256 z załącznika?**  

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/16-image.png)

**b. Jakie techniki phishingowe stosuje załącznik?**  

Podszywanie się pod Microsoft  SSO - automatyczne uzupełnianie adresu mailowego + skopiowane grafiki i pliki CSS bezpośrednio z serwera Microsoft 

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/19-image.png)

**c. Do jakiej domeny wysyłane są poświadczenia (login i hasło)?**

**makivoice.online**

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/17-image.png)

W dodatku do potwierdzenia sprawdzony SPF record - manualnie:  

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/18-image.png)

## Próbka: Roehl Voicemail  

1. **Czy dana wiadomość jest według ciebie phishingiem czy bezpieczna wiadomością?**

**Odp.** Wiadomość jest phishingiem.

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/22-image.png)

2. **Wymień wszystkie wskazówki, które wskazują według ciebie na to, że wiadomość jest phishingiem**  

a) pusty email z załącznikiem
b) (.htm.htm - podwójne rozszerzenie pliku)
c) VOICE-NO_REPLY@Roehl[.]com < tashina.weigel@roehl[.]net> - niespójność nadawcy, nazwa wyświetlana i rzeczywisty adres nie są spójne
d) sam temat jest w sobie podejrzany (SILENTCODERSTIMEZONE - po wygooglowaniu do niczego nie prowadzi)
e) zwykle voicemail wygląda tak:

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/23-image.png)

2. **Przeanalizuj nagłówki wiadomości:**

**a. Jaki był wynik testu SPF, DKIM i DMARC?**

- **SPF** - softfail, 
- **DMARC** = fail; 
- **DKIM** = none, bo wiadomość nie jest podpisana

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/25-image.png)

**b. Czy wiadomość jest zespoofowana, jeżeli tak to dlaczego i która technika spoofingu została zastosowana?**

**Odp**. Tak, dlatego że nie przechodzi SPF nie jest podpisana DKIM i nie przechodzi DMARC.  
From i Recived są takie same: tashina.weigel@roehl[.]net 

**Technika**: podszycie się pod domenę nadawcy czyli spoofing adresu nadawcy / domeny (From spoofing).  

c. Jaki było oryginalny adres IP z którego wysłano wiadomość?

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/24-image.png)

**203[.]183[.]42[.]114**  

4. **Przeanalizuj załącznik wiadomości:**

**a. Jaka jest suma kontrolna MD5 i SHA-256 z załącznika?**

![alt](courses/szkola-security/phishing/zadania-szkola/Attachments/26-image.png)

**b. Jakie techniki phishingowe stosuje załącznik?**

Podobnie jak poprzednio, podszywanie się pod jakąś formę logowania, nie widać dokładnie jaką (kampania wygasła/źle wczytane pliki?).

  ![[courses/szkola-security/phishing/zadania-szkola/Attachments/28-image.png]]

c. Do jakiej domeny wysyłane są poświadczenia (login i hasło)?

Skonfigurować poprawnie... Inetsim? -> Do zrobienia