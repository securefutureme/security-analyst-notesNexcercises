
#### Explain 2FA. →  
Wyjaśnij, czym jest 2FA (uwierzytelnianie dwuskładnikowe).  

2FA to uwierzytelnianie dwuskładnikowe, czyli logowanie z użyciem dwóch różnych składników potwierdzających tożsamość. Zwykle jest to: coś co znasz, coś co masz, coś czym jesteś (hasło, kod SMS, odcisk palca).  

    
#### What are Encoding, Hashing, Encryption? → Czym są: kodowanie (encoding), hashowanie (hashing) i szyfrowanie (encryption)?

Encoding (kodowanie) - sposób zamiany danych do innego formatu, żeby systemy mogły je poprawnie przechowywać albo przesyłać.Nie służy do ukrywania informacji. Przykład: Base64.

Hashing (hashowanie) - jednokierunkowe przekształcenie danych do stałej długości skrótu. Nie da się tego normalnie odwrócić. Używa się tego np. do sprawdzania integralności albo przechowywania haseł. Przykład: SHA-256.

Encryption (szyfrowanie) - zabezpieczanie danych tak, żeby były nieczytelne bez odpowiedniego klucza. W przeciwieństwie do hashowania, szyfrowanie można odwrócić, jeśli mamy klucz. Przykład: AES.

#### What are the differences between Hashing and Encryption? → 
Jakie są różnice między haszowaniem a szyfrowaniem?

Hashowanie -  operacja, która z dowolnych danych tworzy skrót o stałej długości. Taki skrót służy do porównywania lub weryfikacji danych, a nie do ich odzyskiwania, bo proces jest nieodwracalny. Np. system nie trzyma Twojego hasła tylko jego skrót, który jest sprawdzany przy logowaniu - porównuje hash wpisanego hasła z zapisanym hashem.  
Szyfrowanie -  zamienia dane na nieczytelną formę, którą można odszyfrować kluczem - ukrycie treści z możliwością odczytu. Np. gdy wysyłasz maila, treść jest szyfrowana, żeby ktoś jej nie odczytał. Odszyfrowana jest po drugiej stronie.

#### Explain Salted Hashes → Wyjaśnij pojęcie „salted hashes” (hashe z solą).  
Salted hashes to dodatkowe zabezpieczenie przy przechowywaniu haseł -  do hasła dodaje się losowy tekst, czyli sól (która jest losowa i unikalna), a dopiero potem oblicza hash. Taki tekst powoduje, że hash wygląda inaczej niż hash samego hasła. Eliminuje to problem, kiedy dwóch użytkowników miałoby to samo hasło (w wyniku którego byłby ten sam hash). W takim przypadku system dodaje inną “sól” by hash był inny od drugiego.  

#### What is the difference between asymmetric encryption and symmetric? - Czym różni się szyfrowanie symetryczne od asymetrycznego?

Szyfrowanie symetryczne - używa tego samego klucza do szyfrowania i odszyfrowania.  
Szyfrowanie asymetryczne - używa parę kluczy - publicznego i prywatnego. Publiczny jest do szyfrowania, prywatny do odszyfrowania.   
Przykład: każdy może wrzucić list do skrzynki pocztowej (klucz publiczny), ale tylko właściciel ma klucz do jej otwarcia (klucz prywatny).

#### What is Base64 and is it secure? →
Czym jest Base64 i czy jest bezpieczne?

#### What is the difference between encoding and encryption? →
Jaka jest różnica między kodowaniem (encoding) a szyfrowaniem (encryption)?

#### Why is hashing used for storing passwords? →
Dlaczego hashowanie jest używane do przechowywania haseł?

#### What makes a good password hashing algorithm? →
Co sprawia, że algorytm hashowania haseł jest dobry?

#### What is the difference between MD5, SHA-1, and SHA-256? →
Jaka jest różnica między MD5, SHA-1 i SHA-256?

#### Why are MD5 and SHA-1 considered insecure? →
Dlaczego MD5 i SHA-1 są uznawane za niebezpieczne?

#### What is a hash collision? →
Czym jest kolizja haszy?

#### What is the purpose of salting in password hashing? →
Jaki jest cel stosowania soli (salt) przy hashowaniu haseł?

#### What is the difference between salt and pepper in cryptography? →
Jaka jest różnica między salt i pepper w kryptografii?

#### What is a digital signature and how does it work? →
Czym jest podpis cyfrowy i jak działa?

#### What is the difference between a digital signature and encryption? →
Jaka jest różnica między podpisem cyfrowym a szyfrowaniem?

#### What is a certificate in PKI? →
Czym jest certyfikat w infrastrukturze klucza publicznego (PKI)?

#### What is the role of a public key and a private key? →
Jaka jest rola klucza publicznego i klucza prywatnego?

#### What is TLS and why is it important? →
Czym jest TLS i dlaczego jest ważny?

#### What is the difference between data at rest and data in transit encryption? →
Jaka jest różnica między szyfrowaniem danych w spoczynku (data at rest) a szyfrowaniem danych w tranzycie (data in transit)?