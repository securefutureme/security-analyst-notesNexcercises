
- How can you protect yourself from Man-in-the-middle (on-path) attacks? →
    

 Jak zabezpieczyć się przed atakiem Man-in-the-Middle (on-path)?

Ochrona przed MITM zależy od scenariusza, ale najważniejsze jest, żeby nawet jeśli ktoś wejdzie w środek ruchu, nie mógł go ani podejrzeć, ani podmienić.  
Po pierwsze, w aplikacjach wymuszam szyfrowanie i uwierzytelnienie – czyli TLS/HTTPS albo SSH – i zwracam uwagę na poprawną walidację certyfikatów. W środowiskach firmowych dodatkowo pomaga HSTS, a czasem mTLS, gdy chcemy mieć pewność co do obu stron.  
Po drugie, dbam o DNS, bo MITM często zaczyna się od przekierowania. Tam, gdzie to ma sens, stosuje się DNSSEC do weryfikacji odpowiedzi, a DNS over HTTPS albo DNS over TLS do ograniczenia podsłuchu samych zapytań.  
Po trzecie, jeśli jestem w niezaufanej sieci, np. publiczne Wi-Fi, to używam VPN i nie ignoruję ostrzeżeń przeglądarki o certyfikacie – to częsty sygnał próby podszycia.  
I na koniec, w samej sieci LAN ogranicza się klasyczne spoofingi, czyli ARP/DHCP – np. przez DHCP Snooping i Dynamic ARP Inspection na switchach żeby trudniej było w ogóle wejść w rolę ‘pośrednika’.

  

- Co to jest DHCP Snooping?
    

  

- Co to jest Dynamic ARP Inspection?
    

  

- Co to jest DNSSEC ?
    

  

- What Is Indicator of Compromise (IOCs)? → 
    

Czym są wskaźniki kompromitacji (IOC)?

  

- What is Indicators of Attack (IOAs)? → 
    

Czym są wskaźniki ataku (IOA)?

  

- What is Cyber Threat Intelligence (CTI)? → 
    

Czym jest Cyber Threat Intelligence (CTI)?

  

- What is TAXII in Cyber Threat Intelligence (CTI)? → 
    

Czym jest TAXII w kontekście CTI?

  

- Name some of the Threat Intelligence Platforms →
    

 Podaj przykłady platform Threat Intelligence.

  

- What are the types of Threat Intelligence? → 
    

Jakie są typy Threat Intelligence?

  

- Can you describe SQL Injection? → 
    

Możesz opisać SQL Injection?

##   
Bezpieczeństwo aplikacji webowych (warstwa aplikacyjna)

What are the HTTP response codes? → Jakie są kody odpowiedzi HTTP?  
  

Explain OWASP Top 10 → Wyjaśnij, czym jest OWASP Top 10.  
  

What is SQL Injection? → Czym jest SQL Injection?  
  

Explain SQL Injection Types → Omów typy SQL Injection.  
  

How to prevent SQL injection vulnerability? → Jak zapobiegać podatności na SQL Injection?  
  

What is XSS and how XSS can be prevented? → Czym jest XSS i jak mu zapobiegać?  
  

Explain XSS Types → Omów typy XSS.  
  

What is IDOR? → Czym jest IDOR?  
  

What is RFI? → Czym jest RFI?  
  

What is LFI? → Czym jest LFI?  
  

What is difference between LFI and RFI? → Jaka jest różnica między LFI a RFI?  
  

What is CSRF? → Czym jest CSRF?  
  

What is WAF? → Czym jest WAF?
 