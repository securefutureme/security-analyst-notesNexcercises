
#### How can you protect yourself from Man-in-the-middle (on-path) attacks? →
Jak zabezpieczyć się przed atakiem Man-in-the-Middle (on-path)?

Ochrona przed MITM zależy od scenariusza, ale najważniejsze jest, żeby nawet jeśli ktoś wejdzie w środek ruchu, nie mógł go ani podejrzeć, ani podmienić.  
Po pierwsze, w aplikacjach wymuszam szyfrowanie i uwierzytelnienie – czyli TLS/HTTPS albo SSH – i zwracam uwagę na poprawną walidację certyfikatów. W środowiskach firmowych dodatkowo pomaga HSTS, a czasem mTLS, gdy chcemy mieć pewność co do obu stron.  
Po drugie, dbam o DNS, bo MITM często zaczyna się od przekierowania. Tam, gdzie to ma sens, stosuje się DNSSEC do weryfikacji odpowiedzi, a DNS over HTTPS albo DNS over TLS do ograniczenia podsłuchu samych zapytań.  
Po trzecie, jeśli jestem w niezaufanej sieci, np. publiczne Wi-Fi, to używam VPN i nie ignoruję ostrzeżeń przeglądarki o certyfikacie – to częsty sygnał próby podszycia.  
I na koniec, w samej sieci LAN ogranicza się klasyczne spoofingi, czyli ARP/DHCP – np. przez DHCP Snooping i Dynamic ARP Inspection na switchach żeby trudniej było w ogóle wejść w rolę ‘pośrednika’.

#### Co to jest DHCP Snooping?

#### Co to jest Dynamic ARP Inspection?

#### Co to jest DNSSEC ?

#### What Is Indicator of Compromise (IOCs)? →
Czym są wskaźniki kompromitacji (IOC)?
#### What is Indicators of Attack (IOAs)? → 
Czym są wskaźniki ataku (IOA)?

#### What is Cyber Threat Intelligence (CTI)? → 
Czym jest Cyber Threat Intelligence (CTI)?

#### What is TAXII in Cyber Threat Intelligence (CTI)? → 
Czym jest TAXII w kontekście CTI?

#### Name some of the Threat Intelligence Platforms →
 Podaj przykłady platform Threat Intelligence.
#### What are the types of Threat Intelligence? → 
Jakie są typy Threat Intelligence?
#### Can you describe SQL Injection? → 
Możesz opisać SQL Injection?

#### **What is ARP Spoofing / ARP Poisoning? How can it be detected?**  
Czym jest ARP Spoofing / ARP Poisoning i jak można go wykryć?

#### **What is a DNS Tunneling attack and what network indicators may suggest it?**  
Czym jest atak DNS Tunneling i jakie wskaźniki sieciowe mogą na niego wskazywać?

#### How would you identify Command and Control (C2) traffic in network logs?*
Jak zidentyfikować ruch Command and Control (C2) w logach sieciowych?

#### What is a DDoS attack and what are the most common signs of it in network monitoring?
Czym jest atak DDoS i jakie są jego najczęstsze oznaki w monitoringu sieciowym?**

#### **What is Port Scanning and how can a SOC analyst detect it?**  
Czym jest skanowanie portów i jak analityk SOC może je wykryć?

#### What is the difference between a brute-force attack and credential stuffing?
Jaka jest różnica między atakiem brute force a credential stuffing

#### What is network lateral movement and what logs can help detect it?
Czym jest lateral movement w sieci i które logi pomagają je wykryć?

#### How can you recognize data exfiltration attempts in network traffic?* 
Jak rozpoznać próbę eksfiltracji danych w ruchu sieciowym?

#### **What is a SYN Flood attack and how does it affect network availability?**  
Czym jest atak SYN Flood i jak wpływa on na dostępność sieci?

#### What are the common indicators of phishing-related network activity?
Jakie są typowe wskaźniki aktywności sieciowej związanej z phishingiem?
## Bezpieczeństwo aplikacji webowych (warstwa aplikacyjna)

#### What are the HTTP response codes? → 
Jakie są kody odpowiedzi HTTP?  

#### Explain OWASP Top 10 → 
Wyjaśnij, czym jest OWASP Top 10.  
#### What is SQL Injection? → 
Czym jest SQL Injection?  

#### Explain SQL Injection Types → 
Omów typy SQL Injection.  

#### How to prevent SQL injection vulnerability? → 
Jak zapobiegać podatności na SQL Injection?  
  
#### What is XSS and how XSS can be prevented? → 
Czym jest XSS i jak mu zapobiegać?  
#### Explain XSS Types → 
Omów typy XSS.  

#### What is IDOR? → 
Czym jest IDOR?  

#### What is RFI? → 
Czym jest RFI?  

#### What is LFI? → 
Czym jest LFI?  
#### What is difference between LFI and RFI? → 
Jaka jest różnica między LFI a RFI?  

#### What is CSRF? → 
Czym jest CSRF?  
#### What is WAF? → 
Czym jest WAF?

#### What is SSRF? →
Czym jest SSRF?

#### How can SSRF be detected and prevented? →
Jak wykrywać i jak zapobiegać SSRF?

#### What is Command Injection? →
Czym jest Command Injection?

#### What is the difference between SQL Injection and Command Injection? →
Jaka jest różnica między SQL Injection a Command Injection?

#### What is Path Traversal? →
Czym jest Path Traversal?

#### What is Broken Authentication? →
Czym jest Broken Authentication?

#### What is Broken Access Control? →
Czym jest Broken Access Control?

#### What are secure HTTP headers? →
Czym są bezpieczne nagłówki HTTP?

#### What is Content Security Policy (CSP)? →
Czym jest Content Security Policy (CSP)?
 