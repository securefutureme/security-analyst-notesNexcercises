Pytania:

1 Analizujesz podejrzane zachowanie. Widzisz w logach taką komendę: powershell -enc 
cABvAHcAZQByAHMAaABlAGwAbAAgAC0AZQBuAGMAIABjAEEAQgB2AEEASABjAEEAWgBRAEIAeQBBAEgATQBBAGEAQQBCAGwAQQBHAHcAQQBiAEEAQQBnAEEAQwAwAEEAWgBRAEIAdQBBAEcATQBBAEkAQQBCAGoAQQBFAEUAQQBRAGcAQgAyAEEARQBFAEEAUwBBAEIAagBBAEUARQBBAFcAZwBCAFIAQQBFAEkAQQBlAFEAQgBCAEEARQBnAEEAVABRAEIAQgBBAEcARQBBAFEAUQBCAEMAQQBHAHcAQQBRAFEAQgBIAEEASABjAEEAUQBRAEIAaQBBAEUARQBBAFEAUQBCAG4AQQBFAEUAQQBRAHcAQQB3AEEARQBFAEEAVwBnAEIAUgBBAEUASQBBAGQAUQBCAEIAQQBFAGMAQQBUAFEAQgBCAEEARQBrAEEAUQBRAEIAQwBBAEcAcwBBAFEAUQBCAEkAQQBHAE0AQQBRAFEAQgBSAEEARwBjAEEAUQBnAEIAMgBBAEUARQBBAFIAUQBCAEYAQQBFAEUAQQBVAGcAQgAzAEEARQBFAEEATgBBAEIAQgBBAEUAVQBBAFIAUQBCAEIAQQBGAGMAQQBVAFEAQgBDAEEARgBJAEEAUQBRAEIARgBBAEUAawBBAFEAUQBCAGsAQQBFAEUAQQBRAGcAQgBDAEEARQBFAEEAUgBRAEIAagBBAEUARQBBAFkAUQBCADMAQQBFAEkAQQBRAGcAQgBCAEEARQBVAEEAYQB3AEIAQgBBAEYARQBBAFUAUQBCAEMAQQBFAEkAQQBRAFEAQgBEAEEASABNAEEAUQBRAEIAUgBBAEYARQBBAFEAZwBCAEUAQQBFAEUAQQBSAFEAQgBGAEEARQBFAEEAVQBRAEIAUgBBAEUASQBBAGEAQQBCAEIAQQBFAFkAQQBSAFEAQgBCAEEARgBFAEEAWgB3AEIAQwBBAEcAOABBAFEAUQBCAEYAQQBFAFUAQQBRAFEAQgBTAEEASABjAEEAUQBRAEIAMwBBAEUARQBBAFIAUQBCAEYAQQBFAEUAQQBWAEEAQgBCAEEARQBJAEEAYgBnAEIAQgBBAEUAVQBBAFMAUQBCAEIAQQBFADAAQQBRAFEAQgBDAEEARQBJAEEAUQBRAEIARgBBAEcATQBBAFEAUQBCAE4AQQBFAEUAQQBRAGcAQgBDAEEARQBFAEEAUgB3AEIATgBBAEUARQBBAFUAUQBCAFIAQQBFAEkAQQBRAGcAQgBCAEEARQBRAEEAWQB3AEIAQgBBAEYARQBBAFUAUQBCAEMAQQBFAFEAQQBRAFEAQgBGAEEARQBVAEEAUQBRAEIAUgBBAEYARQBBAFEAZwBCAHAAQQBFAEUAQQBSAGcAQgBGAEEARQBFAEEAVQBRAEIAbgBBAEUASQBBAE0AZwBCAEIAQQBFAFUAQQBSAFEAQgBCAEEARgBNAEEAUQBRAEIAQwBBAEUAbwBBAFEAUQBCAEYAQQBFAFUAQQBRAFEAQgBYAEEARwBjAEEAUQBnAEIAUwBBAEUARQBBAFIAUQBCAEYAQQBFAEUAQQBXAGcAQgAzAEEARQBJAEEAUQBnAEIAQgBBAEUAVQBBAFkAdwBCAEIAQQBHAEUAQQBkAHcAQgBDAEEARQBJAEEAUQBRAEIARwBBAEcAcwBBAFEAUQBCAFYAQQBGAEUAQQBRAGcAQgBEAEEARQBFAEEAUwBBAEIAUgBBAEUARQBBAFUAUQBCAFIAQQBFAEkAQQBSAEEAQgBCAEEARQBRAEEAVQBRAEIAQgBBAEYARQBBAFUAUQBCAEMAQQBHAHMAQQBRAFEAQgBGAEEARQBVAEEAUQBRAEIAUgBBAEcAYwBBAFEAZwBBAHcAQQBFAEUAQQBSAFEAQgBGAEEARQBFAEEAVQB3AEIAQgBBAEUASQBBAFEAZwBCAEIAQQBFAFUAQQBSAFEAQgBCAEEAQQA9AD0A

Zidentyfikuj, co robi tajemnicza komenda. Postaraj się ułożyć recepturę dekodowania za pomocą cyberchefa i zapisać ją do pliku. Następnie otwórz cyberchefa w nowej karcie przyklej komendę kolejny raz i załaduj zapisaną recepturę dekodującą.

- najpierw wklejamy do CyberChefa. Widzimy tutaj encoding Base64.
![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-56.png)

- nastepnie zapisujemy do pliku (najpierw usuwamy początek "powershell -enc")
![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-58.png)

- otwieramy plik w nowej karcie, i tak samo ucinamy końcówkę (albo używamy Regural expressions).
![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-57.png)

- kontynuujemy "zapętlanie" aż wyskoczy nam wynik (sekwencja tutaj się powtarza)

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-59.png)

**Odp. whoami > iam.tmp; more iam.tmp**

2. Wykonaj 3 wybrane przez siebie przykłady z repozytorium [https://github.com/mattnotmax/cyberchef-recipes](https://github.com/mattnotmax/cyberchef-recipes)

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-60.png)

**a) przykład 1.**

[**Recipe 12: Big Number Processing**](https://github.com/mattnotmax/cyberchef-recipes?tab=readme-ov-file#recipe-12---big-number-processing)

W tej recepcje możemy użyć prostego zestawu operacji, aby zamienić 38-cyfrowy numer seryjny X509SerialNumber na jego odpowiednik szesnastkowy jako numer seryjny certyfikatu X.509. 

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/1-image.png)

Skrótowo opis: normalizacja numerów seryjnych certyfikatów między różnymi formatami
Przkłady użycia: analiza phishingu albo malware z własnym certyfikatem - z pcapa albo logów, gdy wyciągamy numer seryjny certyfikatu, ale np. format się nam nie zgadza z tym, co pokazuje sandbox albo narzędzie do analizy, ta recepta pozwala nam szybko ujednolicić format i połączyć fakty.

**b) przykład 2.**

[**Recipe 36: Create a CyberChef Password Generator**](https://github.com/mattnotmax/cyberchef-recipes?tab=readme-ov-file#recipe-36---create-a-cyberchef-password-generator)

Ta recepta jest fajnym pomysłem na stworzenie nowych haseł, dla siebie, czy też userów.

**Przykład:**
Passphrase number: 33
Passphrase words: 5
Passphrase max lenght: 22

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/2-image.png)


**c) przykład 3.**
**[Recipe 43 - Magento skimmer deobfuscation](## Recipe 43 - Magento skimmer deobfuscation)**

Dobry przykład do szybkiego wyciągania najważniejszych wskaźników kompromitacji z zaciemnionego JavaScriptu, nie wykonując pełnej ręcznej analizy od początku - np. jeżeli mamy JavaScript z wieloma ciągami np. `\x68\x74\x74\x70...` to przez tą receptę szybko możemy wyciągnąć:

- domeny
- nazwy pliku JS
- ścieżkę endpointu
- URL do exfiltracji

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/3-image.png)

## Inne przykłady

**SOON**