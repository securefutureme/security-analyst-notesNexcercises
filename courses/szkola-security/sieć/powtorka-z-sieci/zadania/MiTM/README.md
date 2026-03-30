# MiTM

## Opis

MiTM (**Man-in-the-Middle**) to atak, w którym napastnik znajduje się pomiędzy dwiema komunikującymi się stronami i przechwytuje, analizuje lub modyfikuje przesyłane dane. Ofiara często nie jest świadoma, że komunikacja nie przebiega bezpośrednio.

## Charakterystyka ataku

- nietypowe odpowiedzi ARP,
- przekierowanie ruchu przez nieautoryzowany host,
- rozbieżności w odpowiedziach DNS,
- komunikacja przez podejrzany gateway,
- ostrzeżenia o certyfikatach,
- możliwość podglądu lub modyfikacji danych w transmisji.

## Typy ataków Man-in-the-Middle

- **ARP spoofing / ARP poisoning**,
- **DNS spoofing**,
- przejęcie sesji,
- podstawienie fałszywego punktu dostępowego,
- próby osłabienia szyfrowania lub wymuszenia komunikacji nieszyfrowanej.

## Jak się bronić

Podstawowe metody ochrony przed MiTM:

- **TLS / HTTPS / SSH / VPN** – szyfrowanie komunikacji,
- **weryfikacja certyfikatów** – sprawdzanie poprawności i zaufania,
- **HSTS** – wymuszanie bezpiecznego połączenia HTTPS,
- **Dynamic ARP Inspection** i **DHCP Snooping** na przełącznikach,
- **bezpieczne Wi-Fi** – WPA2/WPA3, najlepiej z kontrolą dostępu,
- **segmentacja sieci** – ograniczenie możliwości podsłuchu,
- **IDS/IPS** – wykrywanie prób spoofingu i anomalii,
- **świadomość użytkowników** – unikanie niezaufanych sieci i ignorowania alertów certyfikatów.

## Zadania

| Zadanie | Link |
|---|---|
| Training | [Link](/courses/szkola-security/sieć/powtorka-z-sieci/zadania/MiTM/training/training.pcap-analysis.md) | 
| Zadanie 1 | [Link](/courses/szkola-security/sieć/powtorka-z-sieci/zadania/MiTM/training/1.pcap-analysis.md) |
| Zadanie 2 | [Link](/courses/szkola-security/sieć/powtorka-z-sieci/zadania/MiTM/training/2.pcap-analysis.md) |
| Zadanie 3 | [Link](/courses/szkola-security/sieć/powtorka-z-sieci/zadania/MiTM/training/3.pcap-analysis.md) |
