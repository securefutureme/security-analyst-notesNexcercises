https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/default.aspx

Szybka ściąga najważniejszych zdarzeń Windows Security Event Log wykorzystywanych podczas monitoringu, threat huntingu i Incident Response.

> Sam identyfikator zdarzenia nie jest dowodem incydentu. Zawsze należy sprawdzić host, użytkownika, adres IP, proces, czas zdarzenia oraz powiązane logi.

---
# Spis treści

- [[#Najważniejsze zasady]]
- [[#Priorytetowe zdarzenia SOC]]
- [[#Logowanie i uwierzytelnianie]]
- [[#Typy logowania]]
- [[#Procesy i wykonanie kodu]]
- [[#Persystencja]]
- [[#Konta i grupy]]
- [[#Kerberos i NTLM]]
- [[#Rejestr, pliki i zasoby]]
- [[#Sieć i firewall]]
- [[#Active Directory]]
- [[#Integralność logów i systemu]]
- [[#Korelacje zdarzeń]]
- [[#Pozostałe zdarzenia]]
- [[#Dodatkowe źródła logów]]
- [[#Szybka lista]]

---
# Najważniejsze zasady

## Event ID nie wystarcza

Podczas analizy sprawdzaj:

- `Computer` — host generujący zdarzenie,
- `SubjectUserName` — konto wykonujące operację,
- `TargetUserName` — konto będące celem operacji,
- `IpAddress` — źródłowy adres IP,
- `WorkstationName` — nazwa stacji źródłowej,
- `LogonType` — sposób logowania,
- `ProcessName` — proces odpowiedzialny za zdarzenie,
- `ParentProcessName` — proces nadrzędny,
- `CommandLine` — pełne argumenty procesu,
- `ObjectName` — plik, rejestr lub obiekt,
- `TaskName` — nazwa zadania harmonogramu,
- `ServiceName` — nazwa zainstalowanej usługi,
- `Status` i `SubStatus` — przyczyna błędu logowania.

## Wymagana konfiguracja audytu

Nie wszystkie zdarzenia są rejestrowane domyślnie. Ich dostępność zależy między innymi od:

- Advanced Audit Policy,
    
- roli hosta,
    
- ustawień domenowych,
    
- konfiguracji SACL,
    
- logowania linii poleceń procesów,
    
- konfiguracji Windows Filtering Platform.
    

---

# Priorytetowe zdarzenia SOC

## Najważniejsze zdarzenia do monitorowania

|Event ID|Znaczenie|Dlaczego jest ważne|
|--:|---|---|
|`1102`|Wyczyszczono dziennik audytu|Możliwa próba usunięcia śladów|
|`4624`|Udane logowanie|Analiza dostępu i lateral movement|
|`4625`|Nieudane logowanie|Brute force, password spraying|
|`4648`|Użyto jawnie podanych poświadczeń|RunAs, PsExec, lateral movement|
|`4672`|Przydzielono specjalne uprawnienia|Logowanie konta uprzywilejowanego|
|`4688`|Utworzono nowy proces|Podstawowe źródło detekcji wykonania kodu|
|`4697`|Zainstalowano usługę|Persystencja lub zdalne wykonanie|
|`4698`|Utworzono zadanie harmonogramu|Typowa metoda persystencji|
|`4702`|Zmieniono zadanie harmonogramu|Modyfikacja istniejącej persystencji|
|`4719`|Zmieniono politykę audytu|Możliwa próba wyłączenia monitoringu|
|`4720`|Utworzono konto użytkownika|Podejrzane nowe konto|
|`4724`|Zresetowano hasło konta|Możliwe przejęcie konta|
|`4728`|Dodano członka do grupy globalnej|Eskalacja uprawnień w domenie|
|`4732`|Dodano członka do grupy lokalnej|Dodanie do lokalnych Administratorów|
|`4740`|Konto zostało zablokowane|Brute force lub błędna konfiguracja|
|`4768`|Zażądano biletu Kerberos TGT|Analiza uwierzytelniania Kerberos|
|`4769`|Zażądano biletu usługi Kerberos|Kerberoasting i lateral movement|
|`4771`|Nieudana preautoryzacja Kerberos|Password spraying, błędne hasła|
|`4776`|Walidacja poświadczeń NTLM|Logowania domenowe przy użyciu NTLM|
|`4657`|Zmieniono wartość rejestru|Persystencja i zmiany konfiguracji|
|`4663`|Uzyskano dostęp do obiektu|Dostęp do plików lub katalogów|
|`4946`|Dodano regułę Windows Firewall|Możliwe otwarcie dostępu do usługi|
|`5156`|Zezwolono na połączenie sieciowe|Widoczność połączeń procesów|
|`5157`|Zablokowano połączenie sieciowe|Próba niedozwolonej komunikacji|
|`5136`|Zmieniono obiekt Active Directory|Zmiany kont, grup, GPO i konfiguracji|
|`5140`|Uzyskano dostęp do udziału sieciowego|Dostęp SMB|
|`5145`|Sprawdzono dostęp do pliku w udziale|Szczegółowy monitoring SMB|
|`5379`|Odczytano poświadczenia Credential Manager|Możliwy credential access|
|`6416`|System rozpoznał nowe urządzenie|Podłączenie USB lub innego sprzętu|

---

# Logowanie i uwierzytelnianie

## 4624 — udane logowanie

```text
An account was successfully logged on
```

Najważniejsze pola:

- `TargetUserName`,
    
- `TargetDomainName`,
    
- `LogonType`,
    
- `IpAddress`,
    
- `WorkstationName`,
    
- `AuthenticationPackageName`,
    
- `LogonProcessName`,
    
- `ProcessName`.
    

Szczególnie interesujące przypadki:

- logowanie administracyjne z nowego IP,
    
- logowanie poza godzinami pracy,
    
- logowanie konta serwisowego interaktywnie,
    
- logowanie typu `3` z nietypowego hosta,
    
- logowanie typu `10` na serwerze przez RDP,
    
- logowanie po serii zdarzeń `4625`.
    

---

## 4625 — nieudane logowanie

```text
An account failed to log on
```

Może wskazywać na:

- brute force,
    
- password spraying,
    
- błędne hasło zapisane w usłudze,
    
- wygasłe poświadczenia,
    
- próbę użycia nieistniejącego konta.
    

Najważniejsze pola:

- `TargetUserName`,
    
- `LogonType`,
    
- `IpAddress`,
    
- `WorkstationName`,
    
- `Status`,
    
- `SubStatus`,
    
- `FailureReason`.
    

### Przykładowa detekcja

```text
Wiele zdarzeń 4625
→ różne konta
→ jeden adres IP
→ krótki przedział czasu
```

Możliwy password spraying.

---

## 4648 — logowanie przy użyciu jawnych poświadczeń

```text
A logon was attempted using explicit credentials
```

Powstaje między innymi przy użyciu:

- `runas`,
    
- mapowania udziału sieciowego,
    
- narzędzi administracyjnych,
    
- PsExec,
    
- skryptów korzystających z innych poświadczeń.
    

Sprawdź:

- konto źródłowe,
    
- konto docelowe,
    
- proces,
    
- serwer docelowy,
    
- powiązane `4624`.
    

---

## 4672 — specjalne uprawnienia dla nowego logowania

```text
Special privileges assigned to new logon
```

Wskazuje, że sesja otrzymała uprawnienia administracyjne, np.:

- `SeDebugPrivilege`,
    
- `SeBackupPrivilege`,
    
- `SeRestorePrivilege`,
    
- `SeTakeOwnershipPrivilege`.
    

Zdarzenie może być normalne dla kont systemowych i administratorów.

Alarmujące jest, gdy:

- dotyczy nietypowego użytkownika,
    
- występuje po logowaniu z zewnętrznego IP,
    
- pojawia się bezpośrednio po utworzeniu lub zmianie konta.
    

---

## Pozostałe zdarzenia sesji

|Event ID|Znaczenie|
|--:|---|
|`4634`|Sesja została zakończona|
|`4647`|Użytkownik zainicjował wylogowanie|
|`4778`|Ponownie połączono sesję RDP|
|`4779`|Rozłączono sesję RDP|
|`4800`|Stacja robocza została zablokowana|
|`4801`|Stacja robocza została odblokowana|
|`4825`|Odmówiono dostępu przez Remote Desktop|

---

# Typy logowania

Pole `LogonType` występuje między innymi w zdarzeniach `4624` i `4625`.

|Logon Type|Nazwa|Przykład|
|--:|---|---|
|`2`|Interactive|Logowanie lokalne przy klawiaturze|
|`3`|Network|SMB, zdalny dostęp do zasobu|
|`4`|Batch|Zadanie harmonogramu|
|`5`|Service|Uruchomienie usługi|
|`7`|Unlock|Odblokowanie stacji|
|`8`|NetworkCleartext|Poświadczenia przesłane w formie możliwej do odtworzenia|
|`9`|NewCredentials|`runas /netonly`|
|`10`|RemoteInteractive|RDP|
|`11`|CachedInteractive|Logowanie z użyciem zapisanych danych domenowych|
|`12`|CachedRemoteInteractive|Buforowane logowanie zdalne|
|`13`|CachedUnlock|Odblokowanie z użyciem cache|

## Typy szczególnie istotne dla SOC

```text
3  — dostęp sieciowy i lateral movement
5  — uruchomienie usługi
8  — potencjalnie ryzykowne uwierzytelnianie
9  — użycie alternatywnych poświadczeń
10 — sesja RDP
```

---

# Procesy i wykonanie kodu

## 4688 — utworzenie nowego procesu

```text
A new process has been created
```

To jedno z najważniejszych zdarzeń dla SOC.

Najważniejsze pola:

- `NewProcessName`,
    
- `NewProcessId`,
    
- `ParentProcessName`,
    
- `CreatorProcessId`,
    
- `CommandLine`,
    
- `SubjectUserName`,
    
- `TokenElevationType`,
    
- `MandatoryLabel`.
    

### Podejrzane procesy

```text
powershell.exe
pwsh.exe
cmd.exe
wscript.exe
cscript.exe
mshta.exe
rundll32.exe
regsvr32.exe
certutil.exe
bitsadmin.exe
wmic.exe
schtasks.exe
sc.exe
net.exe
net1.exe
nltest.exe
whoami.exe
```

### Podejrzane relacje parent-child

```text
WINWORD.EXE      → powershell.exe
EXCEL.EXE        → cmd.exe
OUTLOOK.EXE      → mshta.exe
w3wp.exe         → cmd.exe
services.exe     → nietypowy plik w katalogu użytkownika
explorer.exe     → plik z %TEMP%
```

### Ważna konfiguracja

Włącz rejestrowanie pełnej linii poleceń procesów:

```text
Include command line in process creation events
```

Bez tego zdarzenie `4688` ma znacznie mniejszą wartość analityczną.

---

## 4689 — zakończenie procesu

```text
A process has exited
```

Przydatne do:

- ustalania czasu życia procesu,
    
- korelacji z `4688`,
    
- wykrywania szybko kończących się skryptów,
    
- analizy timeline.
    

---

# Persystencja

## 4697 — instalacja usługi

```text
A service was installed in the system
```

Najważniejsze pola:

- `ServiceName`,
    
- `ServiceFileName`,
    
- `ServiceType`,
    
- `ServiceStartType`,
    
- `ServiceAccount`.
    

Podejrzane lokalizacje:

```text
C:\Users\
C:\ProgramData\
C:\Windows\Temp\
C:\Users\Public\
%AppData%
%Temp%
```

Zwróć uwagę na:

- losową nazwę usługi,
    
- uruchamianie PowerShella lub CMD,
    
- plik bez podpisu,
    
- ścieżkę zawierającą argumenty lub adres URL.
    

---

## Zadania harmonogramu

|Event ID|Znaczenie|
|--:|---|
|`4698`|Utworzono zadanie|
|`4699`|Usunięto zadanie|
|`4700`|Włączono zadanie|
|`4701`|Wyłączono zadanie|
|`4702`|Zmieniono zadanie|

Najważniejsze pola:

- `TaskName`,
    
- `TaskContent`,
    
- `Command`,
    
- `Arguments`,
    
- `UserId`,
    
- `Triggers`.
    

Podejrzane działania:

```text
powershell.exe -EncodedCommand ...
cmd.exe /c ...
mshta.exe http://...
rundll32.exe ...
plik z katalogu Temp lub AppData
```

> Samo usunięcie zadania `4699` nie oznacza persystencji. Potrzebne jest utworzenie lub zmiana zadania uruchamiającego podejrzany program.

---

## 4657 — zmiana wartości rejestru

```text
A registry value was modified
```

Szczególnie ważne lokalizacje:

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
HKLM\Software\Microsoft\Windows\CurrentVersion\Run
HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce
HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce
HKLM\SYSTEM\CurrentControlSet\Services
HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon
HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options
```

Sprawdź:

- nazwę wartości,
    
- poprzednią wartość,
    
- nową wartość,
    
- proces wykonujący zmianę,
    
- konto użytkownika.
    

---

# Konta i grupy

## Operacje na kontach

|Event ID|Znaczenie|Priorytet|
|--:|---|:-:|
|`4720`|Utworzono konto użytkownika|Wysoki|
|`4722`|Włączono konto|Średni/Wysoki|
|`4723`|Próba zmiany własnego hasła|Średni|
|`4724`|Próba resetu hasła innego konta|Wysoki|
|`4725`|Wyłączono konto|Średni|
|`4726`|Usunięto konto|Wysoki|
|`4738`|Zmieniono konto użytkownika|Wysoki|
|`4740`|Zablokowano konto|Średni/Wysoki|
|`4767`|Odblokowano konto|Średni|
|`4781`|Zmieniono nazwę konta|Wysoki|

## Co sprawdzić przy utworzeniu konta

Dla zdarzenia `4720` sprawdź:

- kto utworzył konto,
    
- gdzie konto zostało utworzone,
    
- nazwę konta,
    
- czas utworzenia,
    
- późniejsze dodanie do grup,
    
- pierwsze logowanie,
    
- działania wykonane przez konto.
    

---

## Zmiany członkostwa grup

### Grupy globalne

|Event ID|Znaczenie|
|--:|---|
|`4728`|Dodano członka|
|`4729`|Usunięto członka|
|`4737`|Zmieniono grupę|

### Grupy lokalne

|Event ID|Znaczenie|
|--:|---|
|`4732`|Dodano członka|
|`4733`|Usunięto członka|
|`4735`|Zmieniono grupę|

### Grupy uniwersalne

|Event ID|Znaczenie|
|--:|---|
|`4756`|Dodano członka|
|`4757`|Usunięto członka|
|`4755`|Zmieniono grupę|

Szczególnie monitoruj dodawanie użytkowników do:

```text
Administrators
Domain Admins
Enterprise Admins
Schema Admins
Account Operators
Backup Operators
Remote Desktop Users
Group Policy Creator Owners
DnsAdmins
```

---

## SID History

|Event ID|Znaczenie|
|--:|---|
|`4765`|Dodano SID History|
|`4766`|Nieudana próba dodania SID History|
|`4830`|Usunięto SID History|

Zmiana `SIDHistory` może zostać wykorzystana do ukrytej eskalacji uprawnień w Active Directory.

---

# Kerberos i NTLM

## 4768 — żądanie TGT

```text
A Kerberos authentication ticket (TGT) was requested
```

Analizuj:

- `TargetUserName`,
    
- `IpAddress`,
    
- `TicketEncryptionType`,
    
- `Status`,
    
- `PreAuthType`.
    

Podejrzane przypadki:

- konto żądające TGT z nowego hosta,
    
- użycie słabego szyfrowania,
    
- duża liczba żądań,
    
- brak preauthentication dla nietypowego konta.
    

---

## 4769 — żądanie biletu usługi

```text
A Kerberos service ticket was requested
```

Może pomóc wykrywać:

- Kerberoasting,
    
- lateral movement,
    
- nietypowe użycie kont serwisowych,
    
- dostęp do usług na wielu hostach.
    

Podejrzany wzorzec:

```text
Jedno konto
→ duża liczba różnych ServiceName/SPN
→ krótki czas
→ szyfrowanie RC4
```

---

## 4771 — nieudana preautoryzacja Kerberos

```text
Kerberos pre-authentication failed
```

Może wskazywać na:

- błędne hasło,
    
- password spraying,
    
- nieaktualne dane usługi,
    
- próbę logowania na zablokowane konto.
    

---

## 4776 — walidacja poświadczeń NTLM

```text
The domain controller attempted to validate the credentials for an account
```

Przydatne do analizy:

- NTLM authentication,
    
- logowań do starszych systemów,
    
- password spraying,
    
- ruchu pomiędzy stacjami i serwerami.
    

Monitoruj nietypowe użycie NTLM, szczególnie tam, gdzie powinien być stosowany Kerberos.

---

## Pozostałe zdarzenia Kerberos

|Event ID|Znaczenie|
|--:|---|
|`4770`|Odnowiono bilet usługi|
|`4772`|Nieudane żądanie TGT|
|`4773`|Nieudane żądanie biletu usługi|
|`4820`|TGT odrzucono przez ograniczenia dostępu|
|`4821`|Bilet usługi odrzucono przez ograniczenia dostępu|
|`4824`|Nieudana preautoryzacja DES/RC4 dla Protected Users|

---

# Rejestr, pliki i zasoby

## Dostęp do obiektów

|Event ID|Znaczenie|
|--:|---|
|`4656`|Zażądano uchwytu do obiektu|
|`4658`|Zamknięto uchwyt|
|`4659`|Zażądano uchwytu w celu usunięcia|
|`4660`|Usunięto obiekt|
|`4663`|Uzyskano dostęp do obiektu|
|`4670`|Zmieniono uprawnienia obiektu|

Obiektem może być:

- plik,
    
- katalog,
    
- klucz rejestru,
    
- proces,
    
- obiekt systemowy.
    

Zdarzenie `4663` jest przydatne tylko przy prawidłowo skonfigurowanym audycie SACL.

---

## Dostęp do udziałów sieciowych

### 5140 — dostęp do udziału

```text
A network share object was accessed
```

Pokazuje dostęp do udziału, np.:

```text
\\server\share
\\server\ADMIN$
\\server\C$
\\server\IPC$
```

### 5145 — sprawdzenie dostępu do obiektu w udziale

```text
A network share object was checked to see whether client can be granted desired access
```

Zawiera bardziej szczegółowe informacje:

- nazwę udziału,
    
- ścieżkę pliku,
    
- adres źródłowy,
    
- konto użytkownika,
    
- żądane uprawnienia.
    

Szczególnie monitoruj:

```text
ADMIN$
C$
IPC$
NETLOGON
SYSVOL
```

---

# Sieć i firewall

## Połączenia Windows Filtering Platform

|Event ID|Znaczenie|
|--:|---|
|`5154`|Zezwolono aplikacji nasłuchiwać na porcie|
|`5155`|Zablokowano nasłuchiwanie|
|`5156`|Zezwolono na połączenie|
|`5157`|Zablokowano połączenie|
|`5158`|Zezwolono na przypisanie portu|
|`5159`|Zablokowano przypisanie portu|

Najważniejsze pola:

- `Application`,
    
- `SourceAddress`,
    
- `SourcePort`,
    
- `DestAddress`,
    
- `DestPort`,
    
- `Protocol`,
    
- `Direction`.
    

### Przykładowa korelacja

```text
4688 — uruchomiono powershell.exe
5156 — powershell.exe połączył się z zewnętrznym IP
```

---

## Zmiany reguł firewalla

|Event ID|Znaczenie|
|--:|---|
|`4946`|Dodano regułę|
|`4947`|Zmieniono regułę|
|`4948`|Usunięto regułę|
|`4949`|Przywrócono ustawienia domyślne|
|`4950`|Zmieniono ustawienie firewalla|
|`4954`|Zmieniono politykę firewall przez GPO|
|`4956`|Zmieniono aktywny profil|
|`5050`|Próba programowego wyłączenia firewalla|

Szczególnie alarmujące:

- otwarcie portu RDP,
    
- reguła `Allow Any`,
    
- zezwolenie dla pliku w katalogu użytkownika,
    
- wyłączenie całego profilu,
    
- zmiana wykonana przez nietypowy proces.
    

---

# Active Directory

## Zmiany obiektów AD

|Event ID|Znaczenie|
|--:|---|
|`5136`|Zmieniono obiekt|
|`5137`|Utworzono obiekt|
|`5138`|Przywrócono usunięty obiekt|
|`5139`|Przeniesiono obiekt|
|`5141`|Usunięto obiekt|

Obiektem może być:

- użytkownik,
    
- grupa,
    
- komputer,
    
- GPO,
    
- OU,
    
- konto serwisowe,
    
- konfiguracja domeny.
    

### Szczególnie ważne zmiany

Monitoruj modyfikacje:

```text
member
memberOf
servicePrincipalName
userAccountControl
msDS-AllowedToDelegateTo
msDS-AllowedToActOnBehalfOfOtherIdentity
nTSecurityDescriptor
sIDHistory
gPLink
```

---

## Polityki i relacje zaufania

|Event ID|Znaczenie|
|--:|---|
|`4706`|Utworzono relację zaufania domen|
|`4707`|Usunięto relację zaufania|
|`4716`|Zmieniono informacje o zaufanej domenie|
|`4739`|Zmieniono politykę domeny|
|`4713`|Zmieniono politykę Kerberos|
|`6144`|Pomyślnie zastosowano politykę bezpieczeństwa GPO|
|`6145`|Błąd zastosowania polityki bezpieczeństwa GPO|

---

## Active Directory Certificate Services

Najważniejsze zdarzenia:

|Event ID|Znaczenie|
|--:|---|
|`4886`|Otrzymano żądanie certyfikatu|
|`4887`|Zatwierdzono żądanie i wydano certyfikat|
|`4888`|Odrzucono żądanie|
|`4890`|Zmieniono ustawienia Certificate Manager|
|`4891`|Zmieniono konfigurację CA|
|`4899`|Zmieniono szablon certyfikatu|
|`4900`|Zmieniono bezpieczeństwo szablonu|

W środowisku Active Directory zdarzenia te są istotne przy wykrywaniu ataków na AD CS.

---

# Integralność logów i systemu

## Dzienniki zdarzeń

|Event ID|Znaczenie|
|--:|---|
|`1100`|Usługa Event Log została zatrzymana|
|`1101`|Zdarzenia audytu zostały utracone|
|`1102`|Wyczyszczono dziennik audytu|
|`1104`|Dziennik Security jest pełny|
|`1105`|Wykonano automatyczny backup logu|
|`1108`|Usługa Event Log napotkała błąd|

### 1102 — wysoki priorytet

Wyczyszczenie dziennika Security może być:

- działaniem administratora,
    
- częścią procedury konserwacyjnej,
    
- próbą usunięcia śladów po ataku.
    

Sprawdź:

- konto czyszczące log,
    
- host,
    
- wcześniejsze procesy,
    
- wcześniejsze logowania,
    
- logi z EDR i SIEM,
    
- czy wyczyszczono także inne kanały.
    

---

## Polityka audytu

|Event ID|Znaczenie|
|--:|---|
|`4715`|Zmieniono SACL obiektu|
|`4719`|Zmieniono systemową politykę audytu|
|`4817`|Zmieniono ustawienia audytu obiektu|
|`4902`|Utworzono tabelę audytu per-user|
|`4907`|Zmieniono ustawienia audytu obiektu|
|`4912`|Zmieniono politykę audytu użytkownika|

Zmiana polityki audytu może oznaczać próbę ograniczenia widoczności SOC.

---

## Czas systemowy

### 4616 — zmieniono czas systemowy

Zmiana czasu może:

- zakłócić korelację logów,
    
- wpłynąć na Kerberos,
    
- utrudnić analizę timeline,
    
- świadczyć o próbie manipulacji dowodami.
    

Sprawdź:

- poprzedni czas,
    
- nowy czas,
    
- proces,
    
- konto,
    
- źródło synchronizacji NTP.
    

---

## Code Integrity

|Event ID|Znaczenie|
|--:|---|
|`5038`|Hash pliku wykonywalnego jest nieprawidłowy|
|`6281`|Hash strony obrazu jest nieprawidłowy|
|`6410`|Plik nie spełnia wymagań bezpieczeństwa procesu|

Mogą wskazywać na:

- zmodyfikowany plik,
    
- uszkodzony podpis,
    
- niezgodny sterownik,
    
- próbę załadowania nieautoryzowanego kodu.
    

---

# Korelacje zdarzeń

## Brute force zakończony sukcesem

```text
Wiele 4625
→ jedno konto lub wiele kont
→ jeden adres IP
→ następnie 4624
```

Dodatkowo sprawdź:

```text
4672 — uprawnienia administracyjne
4688 — uruchomione procesy
5156 — połączenia sieciowe
```

---

## Password spraying

```text
4625
→ wiele różnych kont
→ pojedyncze próby na każde konto
→ jeden adres IP
→ ten sam kod błędu
```

---

## Podejrzane logowanie RDP

```text
4624 LogonType 10
→ 4672
→ 4688
→ 4778/4779
```

Sprawdź źródłowy adres IP oraz procesy uruchomione w sesji.

---

## Utworzenie konta administratora

```text
4720 — utworzono konto
→ 4722 — włączono konto
→ 4732 lub 4728 — dodano do grupy uprzywilejowanej
→ 4624 — pierwsze logowanie
```

---

## Persystencja przez usługę

```text
4688 — sc.exe / PowerShell
→ 4697 — zainstalowano usługę
→ 4624 LogonType 5
→ 4688 — uruchomiono plik usługi
```

---

## Persystencja przez Scheduled Task

```text
4688 — schtasks.exe
→ 4698 lub 4702
→ 4624 LogonType 4
→ 4688 — uruchomiono polecenie zadania
```

---

## Podejrzany proces z komunikacją sieciową

```text
4688 — uruchomiono proces
→ 5156 — proces nawiązał połączenie
→ nietypowy adres IP lub port
```

---

## Dostęp do udziałów administracyjnych

```text
4624 LogonType 3
→ 5140 — dostęp do udziału
→ 5145 — dostęp do pliku
→ 4688 lub 4697 na hoście docelowym
```

Możliwe użycie:

- PsExec,
    
- SMB lateral movement,
    
- kopiowanie narzędzi,
    
- zdalna instalacja usługi.
    

---

## Próba usunięcia śladów

```text
Podejrzane 4624 / 4688 / 4698
→ 1102 — wyczyszczenie logu
```

`1102` po podejrzanej aktywności znacząco zwiększa priorytet incydentu.

---

# Pozostałe zdarzenia

Poniższe grupy zwykle mają niższy priorytet lub są istotne tylko w konkretnych środowiskach.

## 4608–4622 — start systemu i komponenty LSA

Obejmują:

- uruchamianie i zamykanie systemu,
    
- ładowanie pakietów uwierzytelniania,
    
- rejestrację procesów logowania,
    
- problemy z kolejką audytu,
    
- ładowanie pakietów bezpieczeństwa.
    

Warto analizować, gdy pojawia się nietypowy pakiet LSA lub problemy z audytem.

---

## 4634–4668 — sesje, IPsec i dostęp do obiektów

Obejmują:

- wylogowania,
    
- negocjacje IPsec,
    
- żądania uchwytów,
    
- operacje na obiektach,
    
- usunięcia plików,
    
- inicjalizację aplikacji.
    

Największą wartość mają przy szczegółowym audycie plików i rejestru.

---

## 4670–4696 — uprawnienia, procesy i DPAPI

Obejmują:

- zmianę ACL,
    
- operacje uprzywilejowane,
    
- zakończenie procesów,
    
- operacje na tokenach,
    
- backup i odzyskiwanie kluczy DPAPI.
    

Istotne podczas analizy privilege escalation i credential access.

---

## 4699–4718 — zadania, prawa użytkowników, domeny i IPsec

Obejmują:

- usuwanie i włączanie zadań,
    
- przydzielanie praw użytkowników,
    
- relacje zaufania,
    
- konfigurację IPsec,
    
- polityki odzyskiwania danych.
    

Monitoruj szczególnie zmiany praw użytkownika i zaufania domen.

---

## 4727–4764 — cykl życia grup

Obejmują:

- tworzenie grup,
    
- zmianę typu grup,
    
- dodawanie i usuwanie członków,
    
- usuwanie grup.
    

Najważniejsze są zmiany grup uprzywilejowanych.

---

## 4770–4799 — Kerberos, sesje i enumeracja kont

Obejmują:

- odnawianie biletów,
    
- błędy Kerberos,
    
- mapowanie kont,
    
- sesje RDP,
    
- zmianę nazwy konta,
    
- enumerację grup lokalnych,
    
- zapytania o puste hasło.
    

Enumeracja `4798` i `4799` może wystąpić podczas reconnaissance.

---

## 4800–4830 — blokada stacji i polityki dostępu

Obejmują:

- blokowanie i odblokowanie stacji,
    
- wygaszacz ekranu,
    
- błędy integralności RPC,
    
- ograniczenia Protected Users,
    
- odmowę RDP,
    
- Boot Configuration Data.
    

Istotne głównie podczas analizy sesji użytkownika i zabezpieczeń uwierzytelniania.

---

## 4864–4900 — infrastruktura certyfikatów

Obejmują:

- żądania i wydawanie certyfikatów,
    
- backup i odtwarzanie CA,
    
- import kluczy,
    
- zmiany konfiguracji CA,
    
- zmiany szablonów certyfikatów.
    

Ważne przede wszystkim w środowiskach z Active Directory Certificate Services.

---

## 4902–4913 — polityki audytu i dostępu

Obejmują:

- źródła zdarzeń,
    
- CrashOnAuditFail,
    
- specjalne grupy,
    
- per-user audit policy,
    
- Central Access Policy.
    

Nietypowe zmiany mogą wskazywać na próbę osłabienia monitoringu.

---

## 4928–4937 — replikacja Active Directory

Obejmują:

- rozpoczęcie i zakończenie replikacji,
    
- zmianę źródła replikacji,
    
- błędy replikacji,
    
- usuwanie lingering objects.
    

Istotne dla administratorów AD i podczas analizy replikacji domenowej.

---

## 4944–5051 — firewall, IPsec i integralność kodu

Obejmują:

- start polityki firewalla,
    
- zmiany reguł,
    
- blokowanie pakietów,
    
- problemy z IPsec,
    
- błędy Code Integrity,
    
- wirtualizację rejestru i plików.
    

Najważniejsze są zmiany firewalla oraz próby jego wyłączenia.

---

## 5056–5071 — operacje kryptograficzne

Obejmują:

- testy kryptograficzne,
    
- operacje na kluczach,
    
- operacje providerów,
    
- błędy dostępu do kluczy.
    

Zwykle mają zastosowanie diagnostyczne lub audytowe.

---

## 5120–5127 — OCSP Responder

Obejmują:

- uruchamianie usługi OCSP,
    
- zmiany konfiguracji,
    
- aktualizacje certyfikatu podpisującego,
    
- aktualizacje informacji o unieważnieniu.
    

Istotne w infrastrukturze PKI.

---

## 5136–5169 — Active Directory, SMB i Windows Filtering Platform

Obejmują:

- zmiany obiektów AD,
    
- dostęp do udziałów,
    
- blokowanie pakietów i połączeń,
    
- błędy SPN dla SMB.
    

To jedna z bardziej wartościowych grup dla SOC w środowisku domenowym.

---

## 5376–5452 — Credential Manager i Windows Filtering Platform

Obejmują:

- backup i odczyt poświadczeń,
    
- operacje Vault,
    
- zmiany filtrów WFP,
    
- zdarzenia IPsec.
    

Szczególnie istotne jest `5379`, jeśli pochodzi od nietypowego procesu.

---

## 5453–5485 — operacje IPsec

Obejmują:

- ładowanie polityk,
    
- błędy negocjacji,
    
- uruchamianie i zatrzymywanie IPsec,
    
- błędy interfejsów sieciowych.
    

Najczęściej istotne dla zespołów sieciowych.

---

## 5632–5890 — sieci, RPC i COM+

Obejmują:

- uwierzytelnianie do sieci przewodowej i Wi-Fi,
    
- wywołania RPC,
    
- modyfikacje katalogu COM+.
    

Nietypowe RPC może być istotne podczas lateral movement.

---

## 6144–6281 — GPO, NPS i Code Integrity

Obejmują:

- stosowanie polityki GPO,
    
- błędy GPO,
    
- decyzje Network Policy Server,
    
- blokady kont przez NPS,
    
- błędy integralności kodu.
    

Zdarzenia `6272` i `6273` są istotne dla VPN, Wi-Fi Enterprise i RADIUS.

---

## 6400–6424 — BranchCache, firewall i urządzenia

Obejmują:

- błędy BranchCache,
    
- przejęcie filtrowania przez Windows Firewall,
    
- nowe urządzenia,
    
- włączenie i wyłączenie urządzeń,
    
- blokady instalacji sprzętu.
    

Najważniejsze dla SOC:

```text
6416 — rozpoznano nowe urządzenie
6419 — zażądano wyłączenia urządzenia
6420 — urządzenie zostało wyłączone
6421 — zażądano włączenia urządzenia
6422 — urządzenie zostało włączone
6423 — instalacja urządzenia została zablokowana
```

---

## 8191

```text
Highest System-Defined Audit Message Value
```

Nie jest typowym zdarzeniem operacyjnym przeznaczonym do monitorowania przez SOC.

---

# Dodatkowe źródła logów

Windows Security Log powinien być uzupełniony innymi źródłami.

## PowerShell

Najważniejsze Event ID:

|Event ID|Znaczenie|
|--:|---|
|`4103`|Module Logging|
|`4104`|Script Block Logging|
|`400`|Uruchomienie PowerShell Engine|
|`403`|Zatrzymanie PowerShell Engine|

Szczególnie wartościowe jest `4104`, ponieważ może zawierać wykonywany skrypt.

---

## Sysmon

|Event ID|Znaczenie|
|--:|---|
|`1`|Utworzenie procesu|
|`3`|Połączenie sieciowe|
|`7`|Załadowanie obrazu/DLL|
|`8`|Utworzenie zdalnego wątku|
|`10`|Dostęp do procesu|
|`11`|Utworzenie pliku|
|`12–14`|Operacje na rejestrze|
|`15`|Alternate Data Stream|
|`17–18`|Named Pipes|
|`22`|Zapytanie DNS|
|`23`|Usunięcie pliku|
|`25`|Process Tampering|

---

## Microsoft Defender

|Event ID|Znaczenie|
|--:|---|
|`1116`|Wykryto zagrożenie|
|`1117`|Podjęto działanie wobec zagrożenia|
|`1118`|Działanie naprawcze nie powiodło się|
|`5001`|Wyłączono ochronę antywirusową|
|`5007`|Zmieniono konfigurację Defendera|

---

# Szybka lista

```text
1102 — wyczyszczenie logu Security
4616 — zmiana czasu systemowego
4624 — udane logowanie
4625 — nieudane logowanie
4648 — użycie jawnych poświadczeń
4657 — zmiana rejestru
4663 — dostęp do pliku lub obiektu
4672 — uprawnienia administracyjne
4688 — utworzenie procesu
4697 — instalacja usługi
4698 — utworzenie Scheduled Task
4702 — zmiana Scheduled Task
4719 — zmiana polityki audytu
4720 — utworzenie użytkownika
4724 — reset hasła
4728 — dodanie do grupy globalnej
4732 — dodanie do grupy lokalnej
4740 — blokada konta
4765 — dodanie SID History
4768 — żądanie Kerberos TGT
4769 — żądanie biletu usługi
4771 — błąd preauthentication Kerberos
4776 — walidacja NTLM
4946 — dodanie reguły firewalla
5050 — próba wyłączenia firewalla
5136 — zmiana obiektu AD
5140 — dostęp do udziału SMB
5145 — dostęp do pliku przez udział
5156 — dozwolone połączenie sieciowe
5157 — zablokowane połączenie
5379 — odczyt Credential Manager
6416 — podłączono nowe urządzenie
```

---

