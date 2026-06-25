# IDS – system wykrywania włamań

Jak wiemy, **firewalle** to rozwiązania bezpieczeństwa wdrażane zwykle na granicy sieci, aby chronić ruch przychodzący i wychodzący. Firewall sprawdza ruch w momencie zestawiania połączenia i blokuje go, jeśli narusza reguły bezpieczeństwa.

To jednak nie wystarcza. Potrzebny jest także mechanizm, który wykryje **aktywność połączenia, które przeszło przez firewall i już zostało zestawione**. Jeśli atakujący skutecznie ominie firewall, korzystając z połączenia wyglądającego legalnie, a następnie zacznie wykonywać złośliwe działania wewnątrz sieci, musi istnieć coś, co wykryje to odpowiednio wcześnie.

Do tego właśnie służy rozwiązanie bezpieczeństwa działające **wewnątrz sieci**, czyli **IDS (Intrusion Detection System)**.

## IDS na prostym przykładzie

Można to porównać do ochrony budynku:

- **firewall** działa jak strażnik przy wejściu, który sprawdza, kto wchodzi i wychodzi
- zawsze istnieje szansa, że złośliwa osoba przedostanie się do środka
- wtedy potrzebny jest kolejny mechanizm wykrycia zagrożenia już po wejściu do budynku

Taką rolę pełnią **kamery monitoringu**, rozmieszczone w całym obiekcie.  
**IDS działa podobnie do kamer monitoringu** — znajduje się „z boku”, obserwuje ruch sieciowy na podstawie **detekcji sygnaturowej** i **detekcji anomalii** oraz wykrywa nietypowy lub złośliwy ruch wewnątrz sieci i wychodzący z niej.

Po każdym wykryciu IDS generuje **alert** dla administratorów bezpieczeństwa.  
IDS **nie podejmuje działań blokujących** — jego zadaniem jest wyłącznie **powiadamianie** o wykrytej aktywności.
## Główne sposoby klasyfikacji IDS

IDS można klasyfikować na różne sposoby, ale jego podstawowy podział opiera się na:

- **sposobie wdrożenia**
- **trybie detekcji**

## Tryby wdrożenia (_Deployment Modes_)

### HIDS – Host Intrusion Detection System

**HIDS**, czyli host-based IDS, jest instalowany bezpośrednio na konkretnych hostach i odpowiada za wykrywanie zagrożeń związanych tylko z tym jednym systemem.
#### Cechy HIDS

- działa na poziomie pojedynczego hosta
- zapewnia bardzo szczegółową widoczność działań na tym hoście
- może wykrywać zagrożenia lokalne, których nie widać dobrze z poziomu samej sieci
#### Ograniczenia HIDS

- jest trudniejszy w zarządzaniu w dużych sieciach
- zużywa zasoby hosta
- wymaga osobnego utrzymania na każdym urządzeniu
### NIDS – Network Intrusion Detection System

**NIDS**, czyli network-based IDS, służy do wykrywania podejrzanych działań w całej sieci, niezależnie od konkretnego hosta. Monitoruje ruch sieciowy wszystkich urządzeń objętych obserwacją i wykrywa podejrzane wzorce aktywności.
#### Cechy NIDS

- monitoruje ruch sieciowy na poziomie sieci
- wykrywa aktywność obejmującą wiele hostów
- zapewnia scentralizowany widok detekcji w całej sieci
#### Znaczenie NIDS

NIDS jest szczególnie przydatny wtedy, gdy trzeba:

- wychwycić ruch lateralny
- wykryć skanowanie
- identyfikować komunikację z C2
- zauważyć anomalie w ruchu między systemami
## Tryby detekcji (_Detection Modes_)

### IDS sygnaturowy (_Signature-Based IDS_)

Każdy znany atak ma określony **wzorzec**, czyli **sygnaturę**. IDS sygnaturowy przechowuje takie sygnatury w swojej bazie danych. Jeśli w przyszłości pojawi się taki sam lub bardzo podobny atak, IDS rozpozna go na podstawie zapisanej sygnatury i zgłosi administratorom bezpieczeństwa.
#### Zalety

- szybkie wykrywanie znanych zagrożeń
- skuteczność wobec wcześniej zidentyfikowanych ataków
- niskie opóźnienie detekcji
#### Ograniczenia

- nie wykrywa **ataków zero-day**
- działa tylko wobec zagrożeń, których wzorce są już znane i zapisane w bazie

Im lepsza i bogatsza baza sygnatur, tym skuteczniejsze wykrywanie znanych zagrożeń.

### IDS anomaliowy (_Anomaly-Based IDS_)

Ten typ IDS najpierw uczy się **normalnego zachowania** sieci lub systemu, czyli tworzy **baseline**. Następnie wykrywa wszelkie odchylenia od tego normalnego wzorca.
#### Zalety

- potrafi wykrywać **ataki zero-day**
- nie opiera się wyłącznie na gotowych sygnaturach
- dobrze sprawdza się przy nowych lub nietypowych zagrożeniach
#### Ograniczenia

- może generować dużo **false positives**
- legalne działania użytkowników lub aplikacji mogą czasem wyglądać podejrzanie
- wymaga strojenia, aby ograniczyć nadmiar fałszywych alertów

Fałszywe alarmy można zmniejszyć przez **fine-tuning**, czyli ręczne doprecyzowanie, co w danym środowisku jest normalnym zachowaniem.
### IDS hybrydowy (_Hybrid IDS_)

**Hybrid IDS** łączy podejście sygnaturowe i anomaliowe, aby wykorzystać zalety obu metod.
#### Jak działa

- dla znanych zagrożeń używa detekcji sygnaturowej
- dla nowych i nietypowych zagrożeń wykorzystuje analizę anomalii
#### Zaleta

Zapewnia bardziej elastyczne i kompletne wykrywanie zagrożeń niż podejście oparte tylko na jednej metodzie.

## Kiedy który typ IDS ma sens

**IDS sygnaturowy** dobrze sprawdza się przy mniejszej powierzchni zagrożeń i wtedy, gdy ważne jest szybkie wykrywanie znanych ataków.

**IDS anomaliowy** i **IDS hybrydowy** są szczególnie przydatne w wykrywaniu nowoczesnych zagrożeń, w tym **ataków zero-day**, które pojawiają się coraz częściej i mogą powodować bardzo duże szkody w organizacjach

# Snort

**Snort** to jedno z najczęściej używanych rozwiązań **open-source IDS**, opracowane w **1998 roku**. Wykorzystuje **detekcję sygnaturową** oraz **detekcję anomalii** do identyfikowania znanych zagrożeń. Mechanizmy te są definiowane w **plikach reguł** narzędzia Snort.

W pakiecie Snorta znajduje się kilka **wbudowanych plików reguł**, które zawierają różne znane wzorce ataków. Dzięki temu wbudowane reguły Snorta potrafią wykrywać wiele rodzajów złośliwego ruchu od razu po instalacji.

Jednocześnie Snort można dostosować tak, aby wykrywał **konkretne typy ruchu sieciowego**, które nie są objęte domyślnymi regułami. Można więc:

- tworzyć **własne reguły**
- wyłączać wybrane **reguły wbudowane**, jeśli nie odnoszą się do zagrożeń istotnych dla danego systemu lub sieci
- definiować **własne reguły detekcyjne** zgodnie z wymaganiami środowiska

## Tryby pracy Snorta

## Różnica między:

- **Packet Sniffer mode**
- **Packet Logging mode**
- **NIDS mode**

| Tryb pracy                                  | Opis                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Użycie                                                                                                                                                                                                               |
| ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Packet sniffer mode**                     | Ten tryb odczytuje i wyświetla pakiety sieciowe bez wykonywania ich analizy. Tryb sniffera pakietów w Snorcie nie jest bezpośrednio związany z funkcją IDS, ale może być przydatny w monitorowaniu sieci i rozwiązywaniu problemów. W niektórych przypadkach administratorzy systemów muszą jedynie odczytać przepływ ruchu bez uruchamiania detekcji, aby zdiagnozować konkretny problem. Wtedy mogą użyć trybu packet sniffer. Tryb ten pozwala wyświetlać ruch sieciowy w konsoli albo zapisywać go do pliku.                                                           | Zespół sieciowy obserwuje problemy z wydajnością sieci. Aby je zdiagnozować, potrzebuje szczegółowego wglądu w ruch. W tym celu może wykorzystać tryb **packet sniffer** Snorta.                                     |
| **Packet logging mode**                     | Snort wykonuje detekcję ruchu sieciowego w czasie rzeczywistym i wyświetla wykrycia jako alerty w konsoli, aby administratorzy bezpieczeństwa mogli podjąć działania. W niektórych przypadkach ruch sieciowy musi jednak zostać zapisany do późniejszej analizy. Tryb **packet logging** pozwala logować ruch do pliku **PCAP** (standardowy format przechwytywania pakietów). Obejmuje to cały ruch sieciowy oraz wykrycia z nim związane. Tego typu logi mogą być później używane przez analityków śledczych do wykonania **root cause analysis** wcześniejszych ataków. | Zespół bezpieczeństwa musi rozpocząć dochodzenie po ataku sieciowym. Potrzebuje logów ruchu do przeprowadzenia **analizy przyczyny źródłowej**. Ruch zapisany przez tryb **packet logging** Snorta może w tym pomóc. |
| **Network Intrusion Detection System mode** | Tryb **NIDS** jest podstawowym trybem działania Snorta. Monitoruje on ruch sieciowy w czasie rzeczywistym i stosuje pliki reguł, aby wykrywać dopasowania do znanych wzorców ataków zapisanych jako sygnatury. Jeśli zostanie wykryte dopasowanie, generowany jest alert. To właśnie ten tryb zapewnia główną funkcjonalność systemu IDS.                                                                                                                                                                                                                                  | Zespół bezpieczeństwa musi aktywnie monitorować sieć lub systemy w celu wykrywania potencjalnych zagrożeń. Może wykorzystać do tego **tryb NIDS** Snorta.                                                            |

### Najważniejszy tryb z perspektywy IDS

Najbardziej istotne wykorzystanie Snorta jako **IDS** pochodzi z jego trybu **NIDS**.  
Mimo to Snort może pracować w każdym z opisanych wyżej trybów — zależnie od potrzeb operacyjnych, diagnostycznych albo śledczych.