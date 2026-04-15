# Skany

Skany sieciowe to techniki rozpoznawcze wykorzystywane do zbierania informacji o hostach, portach, usługach i systemach operacyjnych. Sam skan nie zawsze oznacza atak, ale bardzo często stanowi **pierwszy etap rozpoznania przed właściwym atakiem**.

## Zadania ze Szloły Security

| Zadanie | Link |
|---|---|
| Scan | [Link](scan.pcap-analysis.md) |

## Inne pcapy


## Charakterystyka skanowania

- wiele połączeń do różnych portów w krótkim czasie,
- niewielka liczba pakietów na port,
- sekwencyjne lub szybkie przechodzenie po adresach IP,
- próby identyfikacji wersji usług,
- duża liczba połączeń zakończonych błędem lub resetem.

## Typy skanowania

- **host discovery** – wykrywanie aktywnych hostów,
- **port scanning** – identyfikacja otwartych portów,
- **service detection** – rozpoznawanie usług i wersji,
- **OS detection** – próba określenia systemu operacyjnego,
- **UDP scanning** oraz **TCP scanning**.

## Jak się bronić

Najważniejsze sposoby ograniczania skuteczności skanów:

- **firewall z zasadą deny by default**,
- **wyłączanie zbędnych usług i portów**,
- **segmentacja sieci**,
- **IDS/IPS** do wykrywania aktywności rozpoznawczej,
- **rate limiting** i ograniczanie prób połączeń,
- **ukrywanie szczegółów usług** – ograniczenie bannerów i wersji,
- **monitoring logów i ruchu sieciowego**,
- **kontrola ekspozycji usług do Internetu**.

