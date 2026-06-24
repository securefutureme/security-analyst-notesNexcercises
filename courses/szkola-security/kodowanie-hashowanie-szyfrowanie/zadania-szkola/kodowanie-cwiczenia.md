
1. Rozpoznaj alfabet i rozkoduj ciąg znaków. 

**01010011 01000001 01001011 01010000 01111011 01100010 01101001 01101110 01100001 01110010 01111001 00110010 01010100 01100101 01111000 01110100 01111101**

Jest to zapis binarny (dwójkowy). Alfabet możemy znaleźć w internecie:
https://www.convertbinary.com/alphabet/

01010011 - S
01000001 - A
i tak dalej... 

**Inna metoda to CyberChef.** O wiele przyjemniejsza :)

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image.png)

**Odp. SAKP{binary2Text}**

2. Rozpoznaj alfabet i rozkoduj ciąg znaków. 466c61677b486578466f726573744865787d
   
**Jest to zapis hexadecymalny (szesnastkowy).** Tak jak poprzednio, możemy to rozwiązać literując to samodzielnie:
[https://www.convertbinary.com/alphabet/](https://www.eso.org/~ndelmott/ascii.html)

Capital F - 46
Lowercase L - l - 6c
i tak dalej... 

**Albo używając dekodera online/CyberChefa.** 

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image-2.png)

**Odp. Flag{HexForestHex}**

3. Rozpoznaj alfabet i rozkoduj ciąg znaków. TW9vbmNha2V7TmllX3dzenlzdGtvX2Jhc2VfY29fbWFfcGFkZGluZyF9
   
**Jest to zapis base64 - jest rodzaj kodowania transportowego, zmodyfikowanego pod kątem zwiększenia przenośności kodowania uuencode. Kodowanie to zostało zdefiniowane w dokumencie RFC 4648.**

https://base64.guru/learn/base64-characters

Z racji kompleksywności tego kodowania, najlepiej to odkodować CyberChefem bezpośrednio. 
![alt](image-11111.png)

**Odp. Mooncake{Nie_wszystko_base_co_ma_padding!}**

4. Rozpoznaj alfabet i rozkoduj ciąg znaków:

**353436633532346134643663373034353539376135323466363136643633373835373536353234653635366233353336353535343432346636313663366333353534366433313532346434363730353535393761346134663536333035353737353436653730363136313662333533363536353434363561353634353331333435343538373037323464343533353435353735383663346536353662366333363534353635323561346535353335373135333538373034653536343533303331353435383730353234643436373034353561343736383466353233303536333635343331343533393530353133643364**

Przypomina to kodowanie Hex. Pierwotny ciąg znaków zawiera wyłącznie znaki 0–9 i ma parzystą długość, co stanowi wyraźną wskazówkę, że jest to ciąg szesnastkowy.

By to rozwiązać, **zaczynijmy od "From Hex":**

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image-4.png)

jak widzimy, tutaj Hex  zostało zmienione na... Hex. Możemy oczywiście szukać dalej, i próbować odkodować dalej, ale w CyberChef mamy fajną funkcję, nazywa się **Magic**, która pozwala szybciej odszukiwać kilkukrotnie zakodowane informacje:

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image-5.png)

Dalej to nie wystarcza. Zmieniamy zatem **Depth**, tak długo, aż nie odkryjemy czegoś sensownego. 
Na podanym przykładzie udało się znaleźć informacje na **Depth: 6**
![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image-6.png)

**I tak mamy Hex -> Hex -> Base64 -> Base64 -> Hex -> Base64**

![[courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image-7.png]]

**Odp. Flag{Encoding_Combo_x32}**

5. Jaki ciąg znaków odpowiada wartościom Unicode \u672A\u6765\u306E\u5E73\u548C\u306F\u6226\u3063\u3066\u52DD\u3061\u3068\u308B\u3093\u3060\uFF01?

Wykonujemy prosty trik w Cyberchef **"Unescape Unicode Charcters"**

![[courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image-8.png]]

Odp. 未来の平和は戦って勝ちとるんだ！?
A jak sobie przetłumaczymy to: _We'll fight and win to bring peace to the future_! (DRAGONBALL FTW!)

6. Jakie emoji posiada codename U+1F6E1?

Możmy to sprawdzić online poprzez stronę: https://www.compart.com/en/unicode/
![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image-11.png)

Albo przez CyberChefa:

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image-12.png)

**Odp. Ὦ**

7. Jaki będzie adres URL jeśli zdekodujemy następujący punycode xn--scurityanalyst-0vl.com?

Zastosujemy do tego **"From Punycode"** w Cyberchefie - https://pl.wikipedia.org/wiki/Punycode

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image-13.png)

**Odp. sеcurityanalyst.com**

8. Rozpoznaj zastosowany w adresie znak użyty w celu zmylenia odbiorcy. Jaki jest kod unicode dla zastosowanego znaku?

Tutaj po prostu wklejamy "przekonwertowany" link na unicode:
![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania-szkola/Attachments/image-14.png)

**Odp. \u0435**