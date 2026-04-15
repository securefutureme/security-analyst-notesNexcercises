
- Explain 2FA. →  
    Wyjaśnij, czym jest 2FA (uwierzytelnianie dwuskładnikowe).  
      
    2FA to uwierzytelnianie dwuskładnikowe, czyli logowanie z użyciem dwóch różnych składników potwierdzających tożsamość. Zwykle jest to: coś co znasz, coś co masz, coś czym jesteś (hasło, kod SMS, odcisk palca).  
      
    
- What are Encoding, Hashing, Encryption? → Czym są: kodowanie (encoding), hashowanie (hashing) i szyfrowanie (encryption)?
    

Encoding (kodowanie) - sposób zamiany danych do innego formatu, żeby systemy mogły je poprawnie przechowywać albo przesyłać.Nie służy do ukrywania informacji. Przykład: Base64.

Hashing (hashowanie) - jednokierunkowe przekształcenie danych do stałej długości skrótu. Nie da się tego normalnie odwrócić. Używa się tego np. do sprawdzania integralności albo przechowywania haseł. Przykład: SHA-256.

Encryption (szyfrowanie) - zabezpieczanie danych tak, żeby były nieczytelne bez odpowiedniego klucza. W przeciwieństwie do hashowania, szyfrowanie można odwrócić, jeśli mamy klucz. Przykład: AES.

- What are the differences between Hashing and Encryption? → Jakie są różnice między haszowaniem a szyfrowaniem?
    

Hashowanie -  operacja, która z dowolnych danych tworzy skrót o stałej długości. Taki skrót służy do porównywania lub weryfikacji danych, a nie do ich odzyskiwania, bo proces jest nieodwracalny. Np. system nie trzyma Twojego hasła tylko jego skrót, który jest sprawdzany przy logowaniu - porównuje hash wpisanego hasła z zapisanym hashem.  
Szyfrowanie -  zamienia dane na nieczytelną formę, którą można odszyfrować kluczem - ukrycie treści z możliwością odczytu. Np. gdy wysyłasz maila, treść jest szyfrowana, żeby ktoś jej nie odczytał. Odszyfrowana jest po drugiej stronie.

- Explain Salted Hashes → Wyjaśnij pojęcie „salted hashes” (hashe z solą).  
    Salted hashes to dodatkowe zabezpieczenie przy przechowywaniu haseł -  do hasła dodaje się losowy tekst, czyli sól (która jest losowa i unikalna), a dopiero potem oblicza hash. Taki tekst powoduje, że hash wygląda inaczej niż hash samego hasła. Eliminuje to problem, kiedy dwóch użytkowników miałoby to samo hasło (w wyniku którego byłby ten sam hash). W takim przypadku system dodaje inną “sól” by hash był inny od drugiego.  
      
    
- What is the difference between asymmetric encryption and symmetric? - Czym różni się szyfrowanie symetryczne od asymetrycznego?
    

Szyfrowanie symetryczne - używa tego samego klucza do szyfrowania i odszyfrowania.  
Szyfrowanie asymetryczne - używa parę kluczy - publicznego i prywatnego. Publiczny jest do szyfrowania, prywatny do odszyfrowania.   
Przykład: każdy może wrzucić list do skrzynki pocztowej (klucz publiczny), ale tylko właściciel ma klucz do jej otwarcia (klucz prywatny).

  

  
  

  
  
  
  
  
  
  
  
  
  

  
  

  
  

  
  
  
  
  
  

  
  