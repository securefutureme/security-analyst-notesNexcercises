## PROTOKOŁY SIECIOWE — pytania teoretyczne (15)

#### What is the difference between TCP and UDP, and in what scenarios is each preferred? →
Jaka jest różnica między TCP i UDP oraz w jakich scenariuszach preferuje się każdy z nich?

#### What is the purpose of the TCP flags SYN, ACK, FIN, RST, and PSH? →
Jakie jest przeznaczenie flag TCP: SYN, ACK, FIN, RST i PSH?

#### What is the difference between HTTP and HTTPS from a security perspective? →
Jaka jest różnica między HTTP i HTTPS z perspektywy bezpieczeństwa?

#### How does DNS work, and why is it often abused by attackers? →
Jak działa DNS i dlaczego jest często wykorzystywany przez atakujących?

#### What is the difference between a recursive DNS query and an iterative DNS query? →
Jaka jest różnica między rekursywnym a iteracyjnym zapytaniem DNS?

#### What are the most common DNS record types and what are they used for? →
Jakie są najczęstsze typy rekordów DNS i do czego służą?

#### What is ARP, and why can it be a security risk in local networks? →
Czym jest ARP i dlaczego może stanowić ryzyko bezpieczeństwa w sieciach lokalnych?

#### What is the difference between ICMP and TCP/UDP, and what is ICMP used for? →
Jaka jest różnica między ICMP a TCP/UDP i do czego służy ICMP?

#### What is DHCP and what security issues can be associated with it? →
Czym jest DHCP i jakie problemy bezpieczeństwa mogą być z nim związane?

#### What is the role of NAT, and how can it affect network visibility during investigations? →
Jaka jest rola NAT i jak może on wpływać na widoczność ruchu podczas dochodzeń?

#### What is the difference between FTP, FTPS, and SFTP? →
Jaka jest różnica między FTP, FTPS i SFTP?

#### How do SMTP, POP3, and IMAP differ, and where are they used? →
Czym różnią się SMTP, POP3 i IMAP oraz gdzie są używane?

#### What is TLS, and at which stage of a connection is it established? →
Czym jest TLS i na jakim etapie połączenia jest ustanawiany?

#### Why are ports important in network communication, and what is the difference between well-known, registered, and dynamic ports? →
Dlaczego porty są ważne w komunikacji sieciowej i jaka jest różnica między portami well-known, registered i dynamic?

## PROTOKOŁY SIECIOWE — pytania praktyczne (10)

#### You see repeated outbound DNS requests to random-looking subdomains of the same domain. What could this indicate and how would you investigate it? →
Widzisz powtarzające się wychodzące zapytania DNS do losowo wyglądających subdomen tej samej domeny. Co to może oznaczać i jak to zbadasz?

#### A host is sending many SYN packets but receives very few completed connections. What might this suggest? →
Host wysyła wiele pakietów SYN, ale bardzo mało połączeń zostaje w pełni zestawionych. Co to może sugerować?

#### You observe a large volume of ICMP traffic between internal hosts. How would you determine whether it is normal or suspicious? →
Obserwujesz duży wolumen ruchu ICMP między hostami wewnętrznymi. Jak ustalisz, czy to normalne czy podejrzane?

#### A user reports that a legitimate website opens, but the browser warns about an invalid certificate. What would you check first? →
Użytkownik zgłasza, że otwiera prawidłową stronę, ale przeglądarka ostrzega o nieprawidłowym certyfikacie. Co sprawdzisz najpierw?

#### During packet analysis, you notice multiple ARP replies without corresponding ARP requests. What could this mean? →
Podczas analizy pakietów zauważasz wiele odpowiedzi ARP bez odpowiadających im zapytań ARP. Co to może oznaczać?

#### A workstation suddenly starts making outbound connections over uncommon ports. How would you triage this activity? →
Stacja robocza nagle zaczyna wykonywać połączenia wychodzące przez nietypowe porty. Jak przeprowadzisz triage tej aktywności?

#### You detect DNS responses with very low TTL values during an investigation. Why might that matter? →
Podczas dochodzenia wykrywasz odpowiedzi DNS z bardzo niskimi wartościami TTL. Dlaczego może to mieć znaczenie?

#### An internal machine is communicating with many external IPs over UDP on a regular interval. What possibilities would you consider? →
Wewnętrzna maszyna komunikuje się z wieloma zewnętrznymi adresami IP po UDP w regularnych odstępach czasu. Jakie hipotezy rozważysz?

#### You need to determine whether suspicious traffic is data exfiltration over HTTP/HTTPS. What protocol-level indicators would you look for? →
Musisz ustalić, czy podejrzany ruch to eksfiltracja danych przez HTTP/HTTPS. Jakich wskaźników na poziomie protokołu będziesz szukać?

#### An employee cannot access email, and logs show issues related to SMTP and IMAP connections. How would you approach troubleshooting from a SOC perspective? →
Pracownik nie może uzyskać dostępu do poczty, a logi pokazują problemy związane z połączeniami SMTP i IMAP. Jak podejdziesz do troubleshootingu z perspektywy SOC?