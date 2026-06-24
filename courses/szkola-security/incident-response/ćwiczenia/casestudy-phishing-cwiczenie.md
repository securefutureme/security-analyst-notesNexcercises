# Co to ćwiczenie ma pokazać

Przeprowadzenie podstawowej analizy podejrzanej wiadomości oraz przygotowanie działań ograniczających skutki incydentu phishingowego.

## Scenariusz

Użytkownik zgłosił wiadomość zawierającą podejrzany link lub załącznik. Istnieje ryzyko wyłudzenia danych logowania albo uruchomienia złośliwego pliku.

## Zadania

1. Zabezpiecz wiadomość i jej nagłówki do dalszej analizy.

2. Sprawdź:
- adres nadawcy i domenę,
- SPF, DKIM i DMARC,
- linki i załączniki,
- treść oraz zastosowane techniki socjotechniczne.

3. Wyodrębnij IOC:
- domeny i adresy URL,
- adresy IP,
- hashe załączników,
- adresy nadawców.

4. Ustal, czy użytkownik:
- kliknął link,
- otworzył załącznik,
- podał dane logowania,
- uruchomił pobrany plik.

5. Zaproponuj działania:
- blokadę IOC,
- usunięcie wiadomości ze skrzynek,
- reset hasła i unieważnienie sesji,
- izolację hosta, jeśli uruchomiono malware.

6. Określ poziom ryzyka i decyzję o eskalacji.

## Rezultat

Krótki raport zawierający:

- ocenę wiadomości,
- zidentyfikowane IOC,
- wpływ na użytkownika i organizację,
- wykonane lub zalecane działania,
- końcową klasyfikację incydentu.

## Kryterium sukcesu

Wiadomość została poprawnie sklasyfikowana, IOC zablokowane, zakres incydentu ustalony, a potencjalnie przejęte konto lub urządzenie zabezpieczone.