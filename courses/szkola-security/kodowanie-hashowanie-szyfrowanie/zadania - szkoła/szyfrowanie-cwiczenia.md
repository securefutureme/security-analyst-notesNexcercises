
Cezar:

1. **Odszyfruj: MUEJ{mufuneu_wytulu_dymn_jsmthu}**

https://www.geeksforgeeks.org/ethical-hacking/caesar-cipher-in-cryptography/

Wykonujemy prosty operację w Cyberchefie -> **"ROT13"**
Jak widzimy, musieliśmy manualnie przeszukać ile "znaków" odszyfruje nam kod, który będzie miał sens.

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-15.png)
Możemy też użyć internetowego toola: https://cryptii.com/pipes/caesar-cipher/

**SAKP{salatka_cezara_jest_pyszna}**

XOR

2. Odszyfruj: kYOJkrmop6asraCjqLattbuduq2wnainsbadoKe4squnobisu78= 

https://en.wikipedia.org/wiki/XOR_cipher
XOR porównuje bity dwóch danych - klucz miesza dane. Ten sam klucz je odwraca. 

Tutaj widzimy że mamy jakiś Base64. Musimy go więc najpierw odszyfrować.

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-16.png)

Następnie bierzemy funkcję XOR Brute Force i odszyfrowujemy ją. Tutaj też mamy **crib** - **znany fragment tekstu**, którego CyberChef szuka w wyniku odszyfrowania. Pomaga odsiać "złe" klucze.
W skrócie - próbuje wielu kluczy i pokaże wyniki, w których pojawia się ten tekst.

Ustawiamy sobie sample lenght na 40, żeby zawęzić wyniki.

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-17.png)

Po przeszukaniu wyników, widzimy że najsensowniejszą odpowiedzią jest klucz c2.
Możemy też użyć criba (wiemy, że z poprzednich zadań powtarzają się odpowiedzi z SAKP).

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-18.png)

**Odp. SAKP{jednobajtowy_xor_jest_bezpieczny}**

3. Odszyfruj: keCJ8bnFtdSgyLbOtdid2a3Tncun0rb+oMS40avEodusyKfLsdu73A== 

Ponownie rozpoczynamy z tą samą metodą. 

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-19.png)

Jak widzimy, nie mamy żadnej zwrotki, także musimy zmienić key lenght na większy. Key length określa, **jak długi ma być klucz XOR, który CyberChef będzie próbował.** To zawęża brute force, bo CyberChef będzie wiedział, jakiego rozmiaru klucza szukać.

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-20.png)

Odp. Key = c2a1: **SAKP{dwubitowy_xor_jest_bezpieczniejszy}**

4. Zadanie z ( * ): Odszyfruj następujący obrazek w formacie .bmp: encrypted.bin

Do zadań dostaliśmy pliki do rozwiązania. Otwieramy je sobie w CyberChefie:

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-21.png)

Widzimy, że coś możemy rozczytać z początku. Musimy wyciągnąć pierwsze bajty klucza. Najlepiej je podejrzeć potem w Hex Editorze (jak użyłem **[https://hexed.it/](https://hexed.it/)**), można użyć programu HxD.

Standardowy plik BMP zaczyna się od sygnatury **`BM`**, czyli od dwóch bajtów `42 4D` w hexie. 
To jest jakiś punkt zaczepienia - podejrzewamy, że ten plik to zaszyfrowany BMP, więc  początek oryginalnego pliku powinien wyglądać właśnie jak na poniższym obrazku:

![alt](courses/szkola-security/kodowanie-hashowanie-szyfrowanie/zadania%20-%20szkoła/Attachments/image-22.png)

Wiedząc, że **dwa pierwsze bajty zaszyfrowanego pliku** to BM, robimy na nich operację **XOR**. Dzięki temu można sprawdzić, jakie znaki klucza musiały tam zostać użyte. 

![alt](image-25.png)

Klucz zaczyna się od liter **„ba”**. To był pierwszy fragment klucza.

Patrząc po pliku można zauważyć, że niektóre bajty powtarzają się często. Sugeruje to zwykle że w zaszyfrowanych danych są miejsca, gdzie oryginalny obraz miał dużo takich samych wartości, co w BMP się zdarza często.
**Innymi ujmując, prosty obraz BMP ma sporo powtarzalnych danych, więc jeśli został zaszyfrowany XOR-em, to też można próbować wyciągnąć z tego wzorce klucza.**

Zatem kopiujemy sobie początek bajtów, wkleimy je do CyberChefa, oraz przekonwertujemy z Hex.
Oczywiście możemy od razu przekonwertować to XOR. Mamy w drugim screen  shocie "clue" - niektóre słowa dają się odczytać (np. słowo klucz). Spróbujemy użyć XOR Brute Force, oraz od razu scribować tym słowem:

![alt](image-24.png)

Widać tutaj juz bardziej czytelniejszy klucz: _xor_jest_bezpiecznybardz_dlugi_klucz_xor_jest

Wiemy, że początek to "ba". Zatem tutaj początkiem będzie bardz, a dalej można to odczytać jako:
bardz_dlugi_klucz_xor_jest_bezpieczny. Użyjmy go do przekonwertowania obrazka do bmp. 

**Użyjemy do tego funkcji XOR (UTF-8) oraz Render Image.**

![alt](image-26.png)

**Odp. SAKP{short_xor_keys_can_be_easy_to_guess}**

OTP:
5.  Zadanie z ( ** ): Wiedząc, że dane dwa obrazki BMP zostały zaszyfrowane za pomocą tego samego klucza OTP, odzyskaj flagę: otp1.bmp, otp2.bmp
   
W tym zadaniu użyjemy operacji **XOR**, a następnie **Render Raw**.  W polu **Input** wklejamy dane z **pierwszego obrazka**.  
W operacji **XOR** w polu **Key** wpisujemy **cały ciąg szesnastkowy (hex)** pochodzący z **drugiego obrazka**.  

![alt](image-28.png)

Po wykonaniu operacji wynik wyświetlamy za pomocą **Render Raw**, aby poprawnie zobaczyć końcową zawartość.

![alt](image-27.png)

**Odp. SAKP{never_resue_one_time_pad_keys_never}** 

**RC4:**

6. Odszyfruj dany ciag znaków za pomocą algorytmu RC4 i klucza „klucz_rc4”: U+GnITAr7SKRhK9nNoQdv5cAOvO21GuRa+tO7x5B0v5mwlnBGJfJwelEEQVh

![alt](image-29.png)

**Odp. SAKP{bardzo_bezpieczny_tekstzaszyfrowany_rc4}**

AES:

7. Odszyfruj następującą wiadomosć, zaszyfrowaną algorytmem AES CBC z kluczem „bardzo_bezpieczny_klucz_aes32bit” oraz IV: „stala_wartosc_IV”: 69b02e6970088bcb35e5d31cae32bdb4 d04244c2dba6c946bf8e33e0ac4827eb3c64746346ffa108588ab7b9ea30ac47a3ce9e015817dc987752bd715c79a593916b723b78b138f7b4c40d672434e78cfe27e6c587e6ada1809d27a1d447f717

![alt](image-30.png)

**Odp. SAKP{aes_jest_uniwersalnym_szyfrem_symetrycznym_uzywanym_przez_rzady_na_calym_swiecie}**


8. Zaszyfruj następującą wiadomość algorytmem AES CBC z kluczem „bardzo_bezpieczny_klucz_aes32bit” oraz IV: „stala_wartosc_IV”: SAKP{aes_jest_unilateralnie_dobrym_szyfrem}

![alt](image-31.png)

**Odp. 69b02e6970088bcb35e5d31cae32bdb4 8508856ce5cf40817c3f82e2108b73d57c50363397ba2f06430853fdb09f9ed3**

9. Zaszyfruj tę samą wiadomość z kluczem „bardzo_bezpieczny_klucz_aes32bit” oraz IV: „zmiennawartoscIV”: SAKP{aes_jest_unilateralnie_dobrym_szyfrem}

![alt](image-32.png)

**Odp. a6558dae8082c55ea8a0c4af6805f75d3e598e8740d436c540438bfedc21d5bbd13fbda5a711b686fec4f329ff4873cb**

10. Co możesz powiedzieć o różnicy między zaszyfrowanym tekstem z 7. i 8. oraz co możesz powiedzieć o różnicy między 8. i 9. – jaki wpływ ma wartość IV na ostateczny wygląd tekstu zaszyfrowanego?

**Odp.** 
**W 7 i 8 pierwszy blok jest taki sam - 69b02e6970088bcb35e5d31cae32bdb4. Ten sam początek wiadomości oraz użyto tego samego IV.** 
**W 8 i 9 pierwszy blok jest różny, co pokazuje nam zmianę IV oraz całego szyfru.** 
Wnioskek - stały IV jest niebezpieczny do używania, bo pokazuje podobieństwa między wiadomościami.

11. Odszyfruj następującą wiadomość, zaszyfrowaną algorytmem AES ECB z kluczem „bardzo_bezpieczny_klucz_aes32bit”:
**a2bf779808de7ca24ab425f01fee7755 d325c316085069321c6b22eaa88ca5d9 06b17646263be41f6299c93de094cd5a 1e7a9edc8b07bf71fc972276161f3f07**

![alt](image-33.png)

**Odp.SAKP{tryb_AESECB_nie_jest_bezpiecznym_trybem_nie_uzywaj_go}**

12. Teraz usuń z powyższej wiadomości 2 środkowe wiersze (bloki 128-bitowe) i odszyfruj, używając tego samego klucza. Czy przekaz wiadomości się zmienił? Jak może to wykorzystać atakujący?

![alt](image-34.png)

**Odp. Atakujący może używać tego do zmieniania treści wiadomości w taki sposób, by nas zmylić (instrukcje np. do czegoś może zmienić z "tak" na "nie").**
**SAKP{tryb_AESECB_uzywaj_go}**

13. Spróbuj tego samego dla następującej wiadomosci zaszyfrowanej algorytmem AES CBC z kluczem „bardzo_bezpieczny_klucz_aes32bit” oraz IV: „stala_wartosc_IV”:
**99b3db5da1098485d32ca9e9eb3601dc 603548200e6df32afc260e8ebb073d2f ac911dbf8ce34f04cb0c55cc9792b83e ca04d3b768ddcd8a4f6d20c1a39a822d**

Jaki był efekt?

![alt](image-35.png)

**Odp.SAKP{tryb_CBCnie_pozwala_na_manipulacje_szyfrogramem}**

14. Odszyfruj tę sama wiadomość z punktu wyżej, używając klucza „bardzo_bezpieczny_klucz_aes32bit” i wartości IV „7374616c615f776172746f73636e7f6c” (zmień tryb na HEX). Co możesz powiedzieć o odszyfrowanej wiadomości? Czy wiesz, jak do tego doszło?

![alt](image-36.png)
Odp. **SAKP{tryb_CBC____pozwala_na_manipulacje_szyfrogramem}**

**Nasza odszyfrowana wiadomość zmieniła przesłanie. Wynika to z tego że wartość IV jest w trybie CBC XORowana z pierwszym blokiem tekstu jawnego i dopiero potem przesyłana do algorytmu blokowego**

**RSA:**

15. **Wygeneruj parę kluczy RSA-2048** 

Mamy kilka sposobów na generowanie kluczy RSA-2048

- toole w internecie - https://cryptotools.net/rsagen
- używając CyberChefa -> Generate RSA Key Pair
- OpenSSL / Putty itp. 
  
![alt](image-37.png)

![alt|430](image-38.png)
![alt|430](image-40.png)
![alt](image-39.png)
![alt](image-41.png)

16. **Używajac wygenerowanej pary kluczy zaszyfruj następującą wiadomość za pomocą klucza publicznego: SAKP{RSA_jest_protokolem_szyfrowania_asymetrycznego}** 

Najpierw kopiujemy sobie jedną parę kluczy wygenerowanych w poprzednim zadaniu. 
Następnie kopiujemy klucz publiczny i wklejamy go np. do CyberChefa -> RSA Encrypt i szyfrujemy wiadomość.

![alt|697](image-43.png)

16. **Używając klucza prywatnego, odszyfruj wiadomość zaszyfrowaną wcześniej.** 

Robimy operację odwrotną dla sprawdzenia, czy klucze działają.

![alt|697](image-44.png)

17. **Odszyfruj następującą wiadomość, używając klucza prywatnego z pliku „private.pem” i schematu RSAES-PCKS1-V1_5:** 

66456ef90e0b1fbd98ec65b042adc1e427f251fbe125be9e90dbaba60683425a02fbb905568c476e6557f77d32217f81e2065a9a71d08a0fd37659382b03314cd314104721a60fcc965e035ddb993c055157e03a9d71ad926589ec2f0e500aedc66834c28775a8d28e0f24550ff691515841e149c1cbe3d7a63ca74c73a48ff3f91b899bd155ff236443cf60c5e1e16b61bf0f1810a5a4b4793fc9d4ac88a112ef2c870dc6f1731bc7fe2d0cbb5964350bab60f2811b40a7c75abc43853061b37f28f9274bc5469fddc62f17a40c8447365125db5e8100ea0e47f853bc5a359c6a91cb28e5481d01ebd4ce1870a2015d59b3ef8e419425e66a19c3d918b4ed11

By wykonać to zadanie, użyjemy CyberChefa. Plik private.pem można otworzyć w notatniku i przekopiować treść klucza prywatnego do programu. Jako, że widzimy tutaj kod Hex, musimy go wpierw odszyfrować, a dopiero użyć odszyfrowanie za pomocą  RSA.

![alt|697](image-45.png)