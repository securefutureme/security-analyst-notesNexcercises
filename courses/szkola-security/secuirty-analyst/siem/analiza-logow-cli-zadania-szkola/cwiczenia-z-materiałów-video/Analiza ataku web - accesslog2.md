 
**Ułożenie timeline ataku z datami i godzinami** 

1. Pierwszy kontakt z serwerem atakującego 

Wiemy, że IP atakującego to 1.3.3.7. Sprawdzamy więc pierwszy kontakt komendą **cat access.log | grep "1.3.3.7" | head -5**

![alt](courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/1-image.png)

**Odp. 6/Jan/2022:10:07:22 +0100**

2. Wejście atakującego na serwer 

Filtrujemy "wp-login" komendą **cat access.log | grep "wp-login" | grep "1.3.3.7" | head -5**

![alt](courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/2-image.png)

**Odp. 16/Jan/2022:10:09:57 +0100

3. IP atakującego 
   
Filtrujemy wszystkie adresy:

![[courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/4-image.png]]

Potem, możemy użyć komendy **cat access.log | grep 'cmd=' | cut -d" " -f2** do przefiltrowania logów, gdzie wystąpiło słowo "cmd" (sugerowalne dla ataku) by upewnić się, który IP atakował.

![[courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/3-image.png]]

**Odp. 1.3.3.7** 

4. Rozpoczęcie WPscanu przez atakującego 

**Filtrujemy sobie frazę "wp-scan" cat access.log | grep "absolutnie_nie_wpscan" | head -n10; w celu odnalezienia pierwszego wpisu.**

![[courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/5-image.png]]

**Odp. 16/Jan/2022:10:09:55 +0100**  

5. **Próby dostępu do logowania/rejestracji:**

![alt](courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/2-image.png)

- `wp-login.php` to standardowy plik WordPressa obsługujący **logowanie**,
- parametr `action=register` zmienia działanie tej strony na **formularz rejestracji nowego użytkownika**,
- więc to żądanie pokazuje, że ktoś próbował sprawdzić, czy w aplikacji da się **założyć konto**.
  
**Odp. GET /wp-login.php?action=register**

6. **Pierwsze POST /wp-login.php od atakującego** 

cat access.log | grep "POST /wp-login.php" | grep "1.3.3.7" | head -5

![alt](courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/7-image.png)

**Odp. 16/Jan/2022:10:10:06 +0100**

7. **Pierwsze wyciągnięcie plików z serwera**
   
**cat access.log | grep "upload" | grep "1.3.3.7" | head -5**

![alt](courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/9-image.png)

**Odp. 16/Jan/2022:10:09:57 +0100]**

8. **Pierwsze użycie komendy** (na serwerze)

**cat access.log | grep "cmd" | grep "1.3.3.7" | head -5**

![alt](courses/szkola-security/secuirty-analyst/siem/analiza-logow-cli-zadania-szkola/cwiczenia-z-materiałów-video/Attachments/10-image.png)

**Odp. 16/Jan/2022:10:15:02 +0100**