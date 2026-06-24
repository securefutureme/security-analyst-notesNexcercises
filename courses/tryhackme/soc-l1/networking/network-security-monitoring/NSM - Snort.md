Zanim przejdziemy głębiej do **Snorta** i analizy ruchu, warto krótko omówić, czym są **IDS (Intrusion Detection System)** oraz **IPS (Intrusion Prevention System)**. Infrastrukturę sieciową można skonfigurować tak, aby korzystała z obu tych rozwiązań, ale przed ich użyciem trzeba dobrze rozumieć różnice między nimi.

# Przypomnienie
### Intrusion Detection System (IDS)

**IDS** to **pasywne rozwiązanie monitorujące**, służące do wykrywania możliwych złośliwych działań, podejrzanych wzorców, nietypowych incydentów oraz naruszeń polityk bezpieczeństwa. Dla każdego podejrzanego zdarzenia generuje **alert**.

####  Dwa główne typy IDS

**Network Intrusion Detection System (NIDS)**  
NIDS monitoruje przepływ ruchu z różnych obszarów sieci. Jego celem jest analiza ruchu w całej podsieci. Jeśli wykryje dopasowanie do sygnatury, tworzy alert.

**Host-based Intrusion Detection System (HIDS)**  
HIDS monitoruje przepływ ruchu z pojedynczego urządzenia końcowego. Jego celem jest analiza ruchu tylko na tym urządzeniu. Jeśli wykryje dopasowanie do sygnatury, tworzy alert.

### Intrusion Prevention System (IPS)

**IPS** to **aktywne rozwiązanie ochronne**, służące do zapobiegania możliwym złośliwym działaniom, podejrzanym wzorcom, anomaliom i naruszeniom polityk bezpieczeństwa. Odpowiada za **zatrzymanie / zablokowanie / przerwanie** podejrzanego zdarzenia natychmiast po jego wykryciu.
#### Cztery główne typy IPS

**Network Intrusion Prevention System (NIPS)**  
NIPS monitoruje przepływ ruchu z różnych obszarów sieci. Jego celem jest ochrona ruchu w całej podsieci. Jeśli wykryje dopasowanie do sygnatury, połączenie zostaje zakończone.

**Behaviour-based Intrusion Prevention System (Network Behaviour Analysis – NBA)**  
Systemy behawioralne monitorują ruch z różnych obszarów sieci. Ich celem jest ochrona ruchu w całej podsieci. Jeśli wykryją anomalię, połączenie zostaje zakończone.

System **Network Behaviour Analysis** działa podobnie do **NIPS**. Różnica polega na tym, że systemy behawioralne wymagają **okresu uczenia** (_baselining_), aby poznać normalny ruch i odróżniać go od ruchu złośliwego. Dzięki temu mogą skuteczniej wykrywać **nowe i nieznane zagrożenia**.

System musi najpierw nauczyć się, co jest **normalne**, aby później wykrywać to, co **nienormalne**. Okres uczenia jest bardzo ważny, bo pomaga ograniczyć **false positives**. Jeśli jednak w trakcie uczenia dojdzie do naruszenia bezpieczeństwa, wyniki będą bardzo problematyczne. Równie ważne jest właściwe nauczenie systemu rozpoznawania legalnych działań.

**Wireless Intrusion Prevention System (WIPS)**  
WIPS monitoruje przepływ ruchu w sieci bezprzewodowej. Jego celem jest ochrona ruchu bezprzewodowego i zatrzymywanie możliwych ataków wychodzących z tej warstwy. Jeśli wykryje sygnaturę, połączenie zostaje zakończone.

**Host-based Intrusion Prevention System (HIPS)**  
HIPS aktywnie chroni ruch pochodzący z pojedynczego urządzenia końcowego. Jego celem jest analiza ruchu na konkretnym urządzeniu. Jeśli wykryje sygnaturę, połączenie zostaje zakończone.

Mechanizm działania **HIPS** jest podobny do **HIDS**. Różnica polega na tym, że **HIDS** tylko generuje alerty, a **HIPS** dodatkowo zatrzymuje zagrożenie przez przerwanie połączenia.

## Techniki detekcji i zapobiegania

Istnieją trzy główne techniki detekcji i zapobiegania używane w rozwiązaniach IDS i IPS:

| Technique           | Approach                                                                                                                                                                                                                          |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Signature-Based** | Ta technika opiera się na regułach identyfikujących konkretne wzorce znanych złośliwych zachowań. Model ten pomaga wykrywać **znane zagrożenia**.                                                                                 |
| **Behaviour-Based** | Ta technika identyfikuje nowe zagrożenia o nowych wzorcach, które omijają sygnatury. Model porównuje zachowania znane / normalne z zachowaniami nieznanymi / nienormalnymi, co pomaga wykrywać **wcześniej nieznane zagrożenia**. |
| **Policy-Based**    | Ta technika porównuje wykryte działania z konfiguracją systemu i politykami bezpieczeństwa. Model ten pomaga wykrywać **naruszenia polityk bezpieczeństwa**.                                                                      |
# Działanie Snorta

Przejdźmy teraz do **Snorta**. Oficjalny opis mówi, że:

Snort może być wdrożony **inline**, aby zatrzymywać pakiety. Ma trzy podstawowe zastosowania:

- jako **sniffer pakietów**, podobnie jak `tcpdump`
- jako **logger pakietów**, przydatny do debugowania ruchu sieciowego
- jako pełnoprawny **system wykrywania i zapobiegania włamaniom**

Snort można pobrać i skonfigurować zarówno do użytku prywatnego, jak i biznesowego.

**Snort** to **otwartoźródłowy, regułowy system NIDS/NIPS**. Został stworzony i jest nadal rozwijany przez **Martina Roesha**, społeczność open-source oraz zespół **Cisco Talos**.

## Możliwości Snorta

Snort oferuje m.in.:

- analizę ruchu na żywo
- wykrywanie ataków i prób rozpoznania
- logowanie pakietów
- analizę protokołów
- alertowanie w czasie rzeczywistym
- moduły i pluginy
- preprocesory
- wsparcie wieloplatformowe (**Linux i Windows**)
## Tryby pracy Snorta

Snort ma trzy główne tryby działania:

**Sniffer Mode**  
Odczytuje i wyświetla pakiety IP w konsoli.

**Packet Logger Mode**  
Loguje wszystkie pakiety IP — przychodzące i wychodzące — które pojawiają się w sieci.

**NIDS / NIPS Mode**  
Loguje lub odrzuca pakiety uznane za złośliwe zgodnie z regułami zdefiniowanymi przez użytkownika.