
Cezar:

1. Odszyfruj: MUEJ{mufuneu_wytulu_dymn_jsmthu}

XOR

2. Odszyfruj: kYOJkrmop6asraCjqLattbuduq2wnainsbadoKe4squnobisu78= 3. Odszyfruj: keCJ8bnFtdSgyLbOtdid2a3Tncun0rb+oMS40avEodusyKfLsdu73A== 4. Zadanie z (*): Odszyfruj następujący obrazek w formacie .bmp: encrypted.bin

OTP:

5. Zadanie z (**): Wiedząc, że dane dwa obrazki BMP zostały zaszyfrowane za pomocą tego samego klucza OTP, odzyskaj flagę: otp1.bmp, otp2.bmp

RC4:

6. Odszyfruj dany ciag znaków za pomocą algorytmu RC4 i klucza „klucz_rc4”: U+GnITAr7SKRhK9nNoQdv5cAOvO21GuRa+tO7x5B0v5mwlnBGJfJwelEEQVh

AES:

7. Odszyfruj następującą wiadomosć, zaszyfrowaną algorytmem AES CBC z kluczem „bardzo_bezpieczny_klucz_aes32bit” oraz IV: „stala_wartosc_IV”: 69b02e6970088bcb35e5d31cae32bdb4d04244c2dba6c946bf8e33e0ac4827eb3c64746346ffa108588ab7b9ea30ac47a3ce9e015817dc987752bd715c79a593916b723b78b138f7b4c40d672434e78cfe27e6c587e6ada1809d27a1d447f717

8. Zaszyfruj następującą wiadomość algorytmem AES CBC z kluczem „bardzo_bezpieczny_klucz_aes32bit” oraz IV: „stala_wartosc_IV”: SAKP{aes_jest_unilateralnie_dobrym_szyfrem}

9. Zaszyfruj tę samą wiadomość z kluczem „bardzo_bezpieczny_klucz_aes32bit” oraz IV: „zmiennawartoscIV”: SAKP{aes_jest_unilateralnie_dobrym_szyfrem}

10. co możesz powiedzieć o różnicy między zaszyfrowanym tekstem z 7. i 8. oraz co możesz powiedzieć o różnicy między 8. i 9. – jaki wpływ ma wartość IV na ostateczny wygląd tekstu zaszyfrowanego?

11. Odszyfruj następującą wiadomość, zaszyfrowaną algorytmem AES ECB z kluczem „bardzo_bezpieczny_klucz_aes32bit”:

a2bf779808de7ca24ab425f01fee7755 d325c316085069321c6b22eaa88ca5d9 06b17646263be41f6299c93de094cd5a 1e7a9edc8b07bf71fc972276161f3f07

12. Teraz usuń z powyższej wiadomości 2 środkowe wiersze (bloki 128-bitowe) i odszyfruj, używając tego samego klucza. Czy przekaz wiadomości się zmienił? Jak może to wykorzystać atakujący?

13. Spróbuj tego samego dla następującej wiadomosci zaszyfrowanej algorytmem AES CBC z kluczem „bardzo_bezpieczny_klucz_aes32bit” oraz IV: „stala_wartosc_IV”:

99b3db5da1098485d32ca9e9eb3601dc 603548200e6df32afc260e8ebb073d2f ac911dbf8ce34f04cb0c55cc9792b83e ca04d3b768ddcd8a4f6d20c1a39a822d

jaki był efekt?

14. Odszyfruj tę sama wiadomość z punktu wyżej, używając klucza „bardzo_bezpieczny_klucz_aes32bit” i wartości IV „7374616c615f776172746f73636e7f6c” (zmień tryb na HEX). Co możesz powiedzieć o odszyfrowanej wiadomości? Czy wiesz, jak do tego doszło?

RSA:

15. Wygeneruj parę kluczy RSA-2048 16. Używajac wygenerowanej pary kluczy zaszyfruj następującą wiadomość za pomocą klucza publicznego: SAKP{RSA_jest_protokolem_szyfrowania_asymetrycznego} 17. Używając klucza prywatnego, odszyfruj wiadomość zaszyfrowaną wcześniej. 18: Odszyfruj następującą wiadomość, używając klucza prywatnego z pliku „private.pem” i schematu RSAES-PCKS1-V1_5: 66456ef90e0b1fbd98ec65b042adc1e427f251fbe125be9e90dbaba60683425a02fbb905568c476e6557f77d32217f81e2065a9a71d08a0fd37659382b03314cd314104721a60fcc965e035ddb993c055157e03a9d71ad926589ec2f0e500aedc66834c28775a8d28e0f24550ff691515841e149c1cbe3d7a63ca74c73a48ff3f91b899bd155ff236443cf60c5e1e16b61bf0f1810a5a4b4793fc9d4ac88a112ef2c870dc6f1731bc7fe2d0cbb5964350bab60f2811b40a7c75abc43853061b37f28f9274bc5469fddc62f17a40c8447365125db5e8100ea0e47f853bc5a359c6a91cb28e5481d01ebd4ce1870a2015d59b3ef8e419425e66a19c3d918b4ed11
