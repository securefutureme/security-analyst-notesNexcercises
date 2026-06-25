Szybka ściąga dotycząca zabezpieczania stacji roboczych i serwerów Windows, ograniczania powierzchni ataku, ochrony poświadczeń oraz monitorowania zdarzeń bezpieczeństwa.

> TIP: Nie wdrażaj ustawień hardeningowych bez testów. Niektóre zabezpieczenia mogą powodować problemy ze starszym oprogramowaniem, sterownikami, uwierzytelnianiem lub zdalnym zarządzaniem.

---

## Spis treści

- [[#Szybka checklista]]
- [[#Przydatne polecenia]]
- [[#Szybka diagnostyka incydentu]]
- [[#Czego nie robić]]
- [[#1. Używaj wspieranego systemu]]
- [[#2. Aktualizuj system i aplikacje]]
- [[#3. Microsoft Defender Antivirus]]
- [[#4. Tamper Protection]]
- [[#5. Microsoft Defender Firewall]]
- [[#6. BitLocker]]
- [[#7. Konta i uwierzytelnianie]]
- [[#8. UAC i minimalne uprawnienia]]
- [[#9. Ochrona poświadczeń]]
- [[#10. Secure Boot i Memory Integrity]]
- [[#11. SmartScreen i ochrona aplikacji]]
- [[#12. Attack Surface Reduction]]
- [[#13. Windows Sandbox]]
- [[#14. Usługi, autostart i funkcje systemowe]]
- [[#15. RDP i dostęp zdalny]]
- [[#16. Protokoły i udziały sieciowe]]
- [[#17. Application Control]]
- [[#18. Logowanie i monitoring]]
- [[#19. Kopie zapasowe]]
- [[#20. Security Baselines]]

---

# Szybka checklista

-  System operacyjny powinien być nadal wspierany.
-  Windows Update działa i instaluje aktualizacje bezpieczeństwa.
-  Microsoft Defender Antivirus jest aktywny i aktualny.
-  Ochrona w czasie rzeczywistym jest włączona.
-  Tamper Protection jest aktywne.
-  Firewall działa dla profili Domain, Private i Public.
-  Dysk systemowy jest zaszyfrowany BitLockerem.
-  Klucz odzyskiwania BitLocker jest bezpiecznie zapisany.
-  Użytkownik pracuje na zwykłym koncie, a nie jako administrator.
-  UAC jest włączony.
-  Stosowane są Windows Hello, MFA lub klucze bezpieczeństwa.
-  Secure Boot i TPM są aktywne.
-  Memory Integrity jest włączone, jeżeli sprzęt i sterowniki są zgodne.
-  LSA Protection i Credential Guard są aktywne, jeśli są obsługiwane.
-  SmartScreen i ochrona przed phishingiem są włączone.
-  Nieużywane usługi, funkcje i konta zostały wyłączone.
-  RDP nie jest bezpośrednio dostępny z Internetu.
-  Dostępne są aktualne i przetestowane kopie zapasowe.
-  Logi bezpieczeństwa są zbierane i monitorowane.

---
# 1. Używaj wspieranego systemu

System bez aktualizacji bezpieczeństwa staje się coraz łatwiejszym celem.
## Zalecenia

- **używaj aktualnej wersji Windows 11,**
- sprawdzaj cykl wsparcia konkretnej wersji systemu,
- aktualizuj urządzenia do nowych wspieranych wydań,
- dla Windows Server sprawdzaj oddzielny cykl wsparcia,
- nie traktuj samego działania systemu jako dowodu, że jest bezpieczny.
## Windows 10

Standardowe wsparcie dla większości edycji Windows 10 zakończyło się:

```text
14 października 2025 r.
```

Dalsze używanie Windows 10 wymaga odpowiedniego programu ESU albo migracji do wspieranego systemu.
## Sprawdzenie wersji

```powershell
winver
```

```powershell
Get-ComputerInfo |
    Select-Object WindowsProductName, WindowsVersion, OsBuildNumber
```
# 2. Aktualizuj system i aplikacje

Aktualizacje eliminują znane podatności w:

- systemie operacyjnym,
- sterownikach,
- przeglądarkach,
- pakiecie Office,
- bibliotekach,
- aplikacjach firm trzecich.
## Sprawdzenie historii aktualizacji

```powershell
Get-HotFix |
    Sort-Object InstalledOn -Descending
```

Informacje o ostatnich aktualizacjach:

```powershell
Get-CimInstance Win32_QuickFixEngineering |
    Sort-Object InstalledOn -Descending
```
## Aktualizacje aplikacji przez WinGet

Lista dostępnych aktualizacji:

```powershell
winget upgrade
```

Aktualizacja konkretnej aplikacji:

```powershell
winget upgrade --id Mozilla.Firefox
```

Aktualizacja wszystkich obsługiwanych aplikacji:

```powershell
winget upgrade --all
```
## Środowisko firmowe

Aktualizacjami można zarządzać przez:

- Windows Update for Business,
- Microsoft Intune,
- Windows Autopatch,
- Configuration Manager,
- WSUS.

W środowisku produkcyjnym stosuj grupy testowe i pierścienie wdrożeniowe.
# 3. Microsoft Defender Antivirus

Microsoft Defender Antivirus zapewnia ochronę przed:

- malware,
- ransomware,
- trojanami,
- spyware,
- potencjalnie niechcianymi aplikacjami,
- złośliwymi skryptami.
## Sprawdzenie stanu

```powershell
Get-MpComputerStatus
```

Najważniejsze pola:

```text
AntivirusEnabled
RealTimeProtectionEnabled
BehaviorMonitorEnabled
IoavProtectionEnabled
AntispywareEnabled
TamperProtectionSource
AntivirusSignatureLastUpdated
```

Czytelniejszy wynik:

```powershell
Get-MpComputerStatus |
    Select-Object AntivirusEnabled,
                  RealTimeProtectionEnabled,
                  BehaviorMonitorEnabled,
                  IoavProtectionEnabled,
                  AntivirusSignatureLastUpdated
```
## Aktualizacja sygnatur

```powershell
Update-MpSignature
```
## Skan szybki

```powershell
Start-MpScan -ScanType QuickScan
```
## Skan pełny

```powershell
Start-MpScan -ScanType FullScan
```
## Historia wykryć

```powershell
Get-MpThreatDetection
```
## Zalecenia

Włącz:

- ochronę w czasie rzeczywistym,
- ochronę dostarczaną z chmury,
- automatyczne przesyłanie próbek,
- ochronę przed potencjalnie niechcianymi aplikacjami,
- Network Protection,
- Behavior Monitoring.

> Wykluczenia Defendera powinny być ograniczone do absolutnego minimum. Szerokie wykluczenie katalogu może umożliwić malware swobodne działanie.
# 4. Tamper Protection

Tamper Protection chroni ustawienia Microsoft Defender przed nieautoryzowaną modyfikacją.

Pomaga przeciwdziałać próbom:

- wyłączenia antywirusa,
- wyłączenia ochrony w czasie rzeczywistym,
- zmiany ustawień ochronnych,
- dodania nieautoryzowanych wykluczeń,
- modyfikacji ustawień Defendera przez rejestr.
## Lokalizacja

```text
Windows Security
→ Virus & threat protection
→ Manage settings
→ Tamper Protection
```
## Środowisko firmowe

Tamper Protection można centralnie zarządzać przez:

- Microsoft Intune,
- Microsoft Defender portal,
- Configuration Manager.

> Tamper Protection chroni Microsoft Defender. Nie zastępuje minimalnych uprawnień ani zabezpieczenia kont administratorów.
# 5. Microsoft Defender Firewall

Firewall powinien być aktywny dla wszystkich profili:

- Domain,
- Private,
- Public.

Domyślna polityka powinna blokować nieoczekiwany ruch przychodzący.
## Sprawdzenie stanu

```powershell
Get-NetFirewallProfile |
    Select-Object Name, Enabled, DefaultInboundAction, DefaultOutboundAction
```
## Włączenie wszystkich profili

```powershell
Set-NetFirewallProfile `
    -Profile Domain,Private,Public `
    -Enabled True
```
## Lista aktywnych reguł

```powershell
Get-NetFirewallRule -Enabled True |
    Select-Object DisplayName, Direction, Action, Profile
```
## Reguły zezwalające na ruch przychodzący

```powershell
Get-NetFirewallRule `
    -Direction Inbound `
    -Action Allow `
    -Enabled True
```
## Konsola zaawansowana

```powershell
wf.msc
```
## Zalecenia

- nie wyłączaj całego firewalla dla jednej aplikacji,
- twórz precyzyjne reguły dla programu, portu i adresów źródłowych,
- ograniczaj regułę do wymaganego profilu,
- usuwaj reguły pozostawione przez odinstalowane aplikacje,
- szczególnie kontroluj porty `22`, `135`, `139`, `445`, `3389`, `5985` i `5986`.

> Firewall ogranicza ruch, ale nie usuwa podatności w samej usłudze.
# 6. BitLocker

BitLocker szyfruje cały wolumin i chroni dane przed odczytem po:

- kradzieży laptopa,
- wyjęciu dysku,
- uruchomieniu innego systemu,
- utracie urządzenia,
- niewłaściwej utylizacji dysku.
## Sprawdzenie stanu

```powershell
Get-BitLockerVolume
```

Alternatywnie:

```cmd
manage-bde -status
```
## Najważniejsze zasady

- szyfruj dysk systemowy i nośniki z poufnymi danymi,
- używaj TPM,
- rozważ TPM wraz z PIN-em dla urządzeń wysokiego ryzyka,
- bezpiecznie zapisz klucz odzyskiwania,
- nie przechowuj jedynej kopii klucza na zaszyfrowanym urządzeniu,
- w firmie zapisuj recovery key w Entra ID, Active Directory lub systemie zarządzania.
## Klucz odzyskiwania

Klucz odzyskiwania może być potrzebny po:

- zmianie TPM,
- zmianie Secure Boot,
- aktualizacji firmware,
- zmianach konfiguracji rozruchowej,
- wymianie płyty głównej.
# 7. Konta i uwierzytelnianie

## Zasada podstawowa

Użytkownik powinien korzystać ze zwykłego konta i podawać dane administratora tylko podczas czynności administracyjnych.
## Zalecenia

- wyłącz nieużywane konta,

- zmień nazwę lub wyłącz nieużywane konto Administrator,
- nie używaj wspólnych kont administracyjnych,
- stosuj unikalne konta administratorów,
- chroń konta MFA,
- używaj długich haseł lub passphrases,
- blokuj popularne i ujawnione hasła,
- nie konfiguruj automatycznego logowania.
## Lista lokalnych użytkowników

```powershell
Get-LocalUser
```
## Członkowie lokalnej grupy Administratorzy

```powershell
Get-LocalGroupMember -Group "Administrators"
```

W polskiej wersji nazwa grupy może być zlokalizowana:

```powershell
Get-LocalGroup
```

## Wyłączenie nieużywanego konta

```powershell
Disable-LocalUser -Name "testuser"
```
## Windows Hello

Windows Hello umożliwia logowanie za pomocą:

- PIN-u przypisanego do urządzenia,
- odcisku palca,
- rozpoznawania twarzy,
- klucza bezpieczeństwa.

Windows Hello for Business wykorzystuje uwierzytelnianie oparte na kluczach i jest przeznaczone do centralnie zarządzanych środowisk firmowych.
# 8. UAC i minimalne uprawnienia

User Account Control ogranicza automatyczne wykonywanie operacji z uprawnieniami administratora.
## Sprawdzenie konfiguracji UAC

```powershell
Get-ItemProperty `
    "HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies\System" `
    -Name EnableLUA, ConsentPromptBehaviorAdmin, PromptOnSecureDesktop
```
## Zalecenia

- `EnableLUA` powinno być włączone,
- administrator powinien otrzymywać monit o podwyższenie uprawnień,
- monit powinien być wyświetlany na Secure Desktop,
- użytkownicy nie powinni stale pracować na kontach administracyjnych.

> UAC nie jest pełną granicą bezpieczeństwa. Jest warstwą utrudniającą automatyczne wykonywanie operacji uprzywilejowanych.
# 9. Ochrona poświadczeń

## LSA Protection

LSA Protection uruchamia proces LSASS jako chroniony proces i utrudnia:

- wstrzykiwanie nieautoryzowanego kodu,
- ładowanie niepodpisanych modułów,
- kradzież poświadczeń z pamięci LSASS.

Sprawdzenie procesu:

```powershell
Get-Process lsass
```
## Credential Guard

Credential Guard wykorzystuje Virtualization-Based Security do izolowania między innymi:

- hashy NTLM,
- biletów Kerberos TGT,
- poświadczeń domenowych.

Ogranicza skuteczność ataków:

```text
Pass-the-Hash
Pass-the-Ticket
Credential Dumping
```
## Sprawdzenie Device Guard i Credential Guard

```powershell
Get-CimInstance `
    -ClassName Win32_DeviceGuard `
    -Namespace root\Microsoft\Windows\DeviceGuard
```

Zwróć uwagę na:

```text
SecurityServicesConfigured
SecurityServicesRunning
VirtualizationBasedSecurityStatus
```

> Credential Guard może powodować problemy ze starszymi protokołami uwierzytelniania. Przetestuj zgodność przed wdrożeniem.
# 10. Secure Boot i Memory Integrity

## Secure Boot

Secure Boot pomaga zapobiegać uruchamianiu nieautoryzowanego kodu przed startem systemu.

Sprawdzenie:

```powershell
Confirm-SecureBootUEFI
```

Możliwe wyniki:

```text
True  — Secure Boot jest aktywny
False — Secure Boot jest wyłączony
```
## TPM

Sprawdzenie TPM:

```powershell
Get-Tpm
```

Najważniejsze pola:

```text
TpmPresent
TpmReady
TpmEnabled
TpmActivated
```
## Memory Integrity

Memory Integrity, znane również jako HVCI, wykorzystuje wirtualizację do ochrony integralności kodu działającego w jądrze.

Lokalizacja:

```text
Windows Security
→ Device security
→ Core isolation
→ Memory integrity
```

Przed włączeniem sprawdź zgodność sterowników.
# 11. SmartScreen i ochrona aplikacji

Microsoft Defender SmartScreen chroni przed:

- stronami phishingowymi,
- złośliwymi witrynami,
- podejrzanymi pobraniami,
- aplikacjami o niskiej reputacji,
- próbami socjotechniki.
## Lokalizacja

```text
Windows Security
→ App & browser control
→ Reputation-based protection
```
## Zalecane funkcje

- Check apps and files,
- SmartScreen for Microsoft Edge,
- phishing protection,
- Potentially unwanted app blocking,
- SmartScreen for Microsoft Store apps.

> Nie ignoruj automatycznie ostrzeżeń SmartScreen. Najpierw zweryfikuj podpis cyfrowy, hash, źródło pliku i reputację dostawcy.
# 12. Attack Surface Reduction

Reguły ASR ograniczają zachowania często wykorzystywane przez atakujących.

Przykładowe zabezpieczenia:

- blokowanie procesów potomnych aplikacji Office,
- blokowanie kodu wykonywalnego z poczty i webmaila,
- blokowanie nadużywania podatnych podpisanych sterowników,
- blokowanie skryptów uruchamiających pobrane pliki,
- blokowanie kradzieży poświadczeń z LSASS,
- blokowanie procesów uruchamianych przez aplikacje komunikacyjne.
## Sprawdzenie konfiguracji Defendera

```powershell
Get-MpPreference |
    Select-Object AttackSurfaceReductionRules_Ids,
                  AttackSurfaceReductionRules_Actions
```
## Tryby wdrożenia

```text
Disabled — reguła wyłączona
Audit    — rejestruje naruszenia, ale nie blokuje
Warn     — ostrzega użytkownika
Block    — blokuje działanie
```
## Zalecany proces wdrożenia

1. Włącz regułę w trybie Audit.
2. Zbieraj logi.  
3. Sprawdź wpływ na aplikacje.
4. Dodaj precyzyjne wyjątki, jeśli są konieczne.
5. Przełącz regułę w tryb Block.
6. Monitoruj zdarzenia i false positive.
# 13. Windows Sandbox

Windows Sandbox zapewnia jednorazowe, odizolowane środowisko Windows. Po zamknięciu jego zawartość jest usuwana.
## Zastosowanie

- testowanie nieznanej aplikacji,
- otwieranie dokumentu w środowisku tymczasowym,
- sprawzanie instalatora,
- podstawowe testy konfiguracji.
## Włączenie funkcji

```powershell
Enable-WindowsOptionalFeature `
    -Online `
    -FeatureName "Containers-DisposableClientVM" `
    -All
```

Sprawdzenie funkcji:

```powershell
Get-WindowsOptionalFeature `
    -Online `
    -FeatureName "Containers-DisposableClientVM"
```
## Ważne ograniczenia

Windows Sandbox nie jest pełnym laboratorium malware analysis.

Domyślnie może posiadać:

- dostęp do sieci,
- współdzielony schowek,
- integrację z hostem,
- możliwość kopiowania plików.

Do analizy prawdziwego malware lepiej użyć:

- dedykowanej maszyny wirtualnej,
- snapshotu,
- izolowanej sieci,
- FakeNet-NG lub INetSim,
- braku dostępu do systemów produkcyjnych,
- oddzielnych kont i danych testowych.

> Nie uruchamiaj aktywnego malware na komputerze, którego utrata lub kompromitacja byłaby problemem.
# 14. Usługi, autostart i funkcje systemowe

Każda niepotrzebna usługa zwiększa powierzchnię ataku.
## Uruchomione usługi

```powershell
Get-Service |
    Where-Object Status -eq "Running"
```

Usługi uruchamiane automatycznie:

```powershell
Get-CimInstance Win32_Service |
    Where-Object StartMode -eq "Auto" |
    Select-Object Name, DisplayName, State, StartName, PathName
```
## Autostart

```powershell
Get-CimInstance Win32_StartupCommand |
    Select-Object Name, Command, Location, User
```

## Zadania harmonogramu

```powershell
Get-ScheduledTask |
    Where-Object State -ne "Disabled"
```
## Autoruns

Sysinternals Autoruns umożliwia przegląd:

- Run i RunOnce,
- Scheduled Tasks,
- Services,
- Drivers,
- Explorer extensions,
- Winlogon,
- WMI,
- Office add-ins.

Szczególnie podejrzane są wpisy wskazujące na:

```text
%TEMP%
%AppData%
C:\Users\Public\
C:\ProgramData\
pliki bez podpisu
PowerShell lub cmd.exe
```
## Funkcje opcjonalne

Lista funkcji:

```powershell
Get-WindowsOptionalFeature -Online |
    Where-Object State -eq "Enabled"
```

Rozważ wyłączenie nieużywanych funkcji, np.:

- Telnet Client,
- TFTP Client,
- SMBv1,
- IIS,
- FTP Server,
- PowerShell 2.0,
- WSL, jeżeli nie jest potrzebny,
- Hyper-V, jeżeli nie jest wykorzystywany.

Nie wyłączaj funkcji bez sprawdzenia zależności.
# 15. RDP i dostęp zdalny

Remote Desktop Protocol jest częstym celem:

- brute force,
- password spraying,
- credential stuffing,
- ransomware,
- lateral movement.
## Zasady

- nie wystawiaj portu `3389` bezpośrednio do Internetu,
- wymagaj VPN lub Remote Desktop Gateway,
- stosuj MFA,
- włącz Network Level Authentication,
- ogranicz źródłowe adresy IP,
- ogranicz członkostwo w `Remote Desktop Users`,
- monitoruj logowania typu `10`,
- ustaw limit bezczynności sesji,
- wyłącz RDP, gdy nie jest potrzebny.
## Sprawdzenie stanu RDP

```powershell
Get-ItemProperty `
    "HKLM:\System\CurrentControlSet\Control\Terminal Server" `
    -Name fDenyTSConnections
```

Interpretacja:

```text
0 — RDP dozwolone
1 — RDP zablokowane
```
## Reguły firewall dla RDP

```powershell
Get-NetFirewallRule |
    Where-Object DisplayGroup -Match "Remote Desktop"
```
# 16. Protokoły i udziały sieciowe

## SMBv1

SMBv1 jest przestarzałym protokołem i powinien pozostać wyłączony, jeżeli nie istnieje udokumentowana konieczność jego używania.

Sprawdzenie:

```powershell
Get-WindowsOptionalFeature `
    -Online `
    -FeatureName SMB1Protocol
```
## Udziały sieciowe

```powershell
Get-SmbShare
```

Sesje SMB:

```powershell
Get-SmbSession
```

Otwarte pliki:

```powershell
Get-SmbOpenFile
```
## Zalecenia

- nie udostępniaj katalogów grupie `Everyone` bez potrzeby,
- ograniczaj dostęp za pomocą grup,
- stosuj zasadę minimalnych uprawnień,
- monitoruj dostępy do `ADMIN$`, `C$` i `IPC$`,
- ogranicz ruch SMB pomiędzy segmentami,
- blokuj port `445` na granicy sieci
## NTLM

Preferuj Kerberos w środowisku domenowym. Starsze mechanizmy LM i NTLMv1 powinny być wyłączone po przeprowadzeniu testów zgodności.

> Nie modyfikuj ustawień NTLM bez inwentaryzacji starszych urządzeń i aplikacji.
# 17. Application Control

Kontrola aplikacji ogranicza możliwość uruchamiania nieautoryzowanego kodu.
## AppLocker

AppLocker może tworzyć reguły dla:

- plików wykonywalnych,
- skryptów,
- instalatorów MSI,
- aplikacji pakietowych,
- bibliotek DLL.
## Windows Defender Application Control

WDAC zapewnia silniejszą kontrolę kodu i może zezwalać wyłącznie na:

- zaufanych wydawców,
- podpisane pliki,
- zatwierdzone aplikacje,
- określone lokalizacje lub hashe.
## Zalecany proces

1. Zbierz informacje o legalnych aplikacjach.
2. Utwórz politykę w trybie Audit.
3. Przeanalizuj zdarzenia.
4. Uzupełnij listę dozwolonych aplikacji.
5. Włącz egzekwowanie.
6. Przygotuj procedurę awaryjnego wycofania polityki.
# 18. Logowanie i monitoring

## Najważniejsze źródła

- Security,
- System,
- Application,
- Microsoft Defender,
- PowerShell Operational,
- Windows Firewall,
- Task Scheduler,
- Terminal Services,
- Sysmon, jeśli został wdrożony.
## Polityka audytu

```cmd
auditpol /get /category:*
```
## Ostatnie zdarzenia Security

```powershell
Get-WinEvent -LogName Security -MaxEvents 50
```
## Wybrane Event ID

```powershell
Get-WinEvent -FilterHashtable @{
    LogName = "Security"
    Id      = 4624,4625,4688,4697,4698,4720,4732,1102
}
```

Najważniejsze zdarzenia:

```text
1102 — wyczyszczenie dziennika audytu
4624 — udane logowanie
4625 — nieudane logowanie
4648 — użycie jawnych poświadczeń
4672 — przydzielenie specjalnych uprawnień
4688 — utworzenie procesu
4697 — instalacja usługi
4698 — utworzenie Scheduled Task
4702 — zmiana Scheduled Task
4720 — utworzenie użytkownika
4732 — dodanie do grupy lokalnej
4740 — blokada konta
5156 — zezwolenie na połączenie sieciowe
5157 — zablokowanie połączenia
```
## PowerShell Logging

W środowisku firmowym warto włączyć:

- Script Block Logging,
- Module Logging,
- Transcription,
- Protected Event Logging.

Najważniejszy Event ID:

```text
4104 — wykonany blok skryptu PowerShell
```

> Zbieranie logów powinno odbywać się centralnie, ponieważ atakujący z uprawnieniami administratora może próbować usunąć lokalne logi.
# 19. Kopie zapasowe

Backup chroni przed:

- ransomware,
- awarią dysku,
- przypadkowym usunięciem,
- błędną aktualizacją,
- uszkodzeniem systemu,
- sabotażem.
## Zasada 3-2-1

```text
3 kopie danych
2 różne typy nośników
1 kopia poza głównym środowiskiem
```
## Zalecenia

- przynajmniej jedna kopia powinna być offline lub immutable,
- konto backupowe nie powinno być zwykłym administratorem domeny,
- system backupowy powinien być oddzielony od środowiska produkcyjnego,
- monitoruj błędy wykonywania kopii,
- regularnie przeprowadzaj test odtworzenia,
- dokumentuj RPO i RTO.
## Punkty przywracania

Punkt przywracania nie zastępuje pełnej kopii zapasowej. Nie chroni skutecznie przed wszystkimi przypadkami:

- ransomware,
- uszkodzenia dysku,
- utraty urządzenia,
- skasowania całego woluminu.
# 20. Security Baselines

Security baseline to zestaw rekomendowanych ustawień bezpieczeństwa.

Może obejmować:

- Defender Antivirus,
- firewall,
- BitLocker,
- UAC,
- zasady kont,
- ochronę poświadczeń,
- protokoły sieciowe,
- logowanie,
- Edge,
- Microsoft 365 Apps.
## Narzędzia

- Microsoft Security Compliance Toolkit,
- Microsoft Intune Security Baselines,
- Group Policy,
- Microsoft Defender Vulnerability Management,
- CIS Benchmarks,
- DISA STIG — w odpowiednich środowiskach.
## Proces wdrożenia

1. Pobierz aktualną baseline.
2. Porównaj ją z aktualną konfiguracją.
3. Wdróż na małej grupie testowej.
4. Monitoruj błędy i zgodność.
5. Udokumentuj wyjątki.
6. Wdrażaj stopniowo na kolejne grupy.
7. Regularnie kontroluj drift konfiguracji.

> Baseline jest punktem początkowym, a nie konfiguracją odpowiednią dla każdego systemu bez zmian.
# Przydatne polecenia

## Informacje o systemie

```powershell
systeminfo
```

```powershell
Get-ComputerInfo
```
## Konta administratorów

```powershell
Get-LocalGroupMember "Administrators"
```
## Ostatnie logowania

```powershell
Get-WinEvent -FilterHashtable @{
    LogName = "Security"
    Id      = 4624,4625
} -MaxEvents 50
```
## Procesy z linią poleceń

```powershell
Get-CimInstance Win32_Process |
    Select-Object ProcessId, ParentProcessId, Name, CommandLine
```
## Połączenia sieciowe

```powershell
Get-NetTCPConnection |
    Sort-Object State, RemoteAddress
```

Połączenia ustanowione:

```powershell
Get-NetTCPConnection -State Established
```
## Porty nasłuchujące

```powershell
Get-NetTCPConnection -State Listen
```

```cmd
netstat -ano
```
## Proces odpowiedzialny za port

```powershell
Get-Process -Id <PID>
```
## Usługi

```powershell
Get-CimInstance Win32_Service |
    Select-Object Name, State, StartMode, StartName, PathName
```
## Zadania harmonogramu

```powershell
Get-ScheduledTask |
    Select-Object TaskName, TaskPath, State
```
## Podpis cyfrowy pliku

```powershell
Get-AuthenticodeSignature "C:\path\program.exe"
```
## Hash pliku

```powershell
Get-FileHash "C:\path\program.exe" -Algorithm SHA256
```
## Zastosowane polityki

```cmd
gpresult /h gpresult.html
```

```cmd
rsop.msc
```
## Stan Defendera

```powershell
Get-MpComputerStatus
```
## Stan BitLocker

```powershell
Get-BitLockerVolume
```
## Stan firewalla

```powershell
Get-NetFirewallProfile
```
# Szybka diagnostyka incydentu

## 1. Zapisz aktualny czas i dane hosta

```powershell
Get-Date
hostname
whoami /all
```
## 2. Sprawdź aktywne procesy

```powershell
Get-CimInstance Win32_Process |
    Select-Object ProcessId, ParentProcessId, Name, CommandLine
```
## 3. Sprawdź połączenia sieciowe

```powershell
Get-NetTCPConnection -State Established
```
## 4. Sprawdź nasłuchujące porty

```powershell
Get-NetTCPConnection -State Listen
```
## 5. Sprawdź autostart

```powershell
Get-CimInstance Win32_StartupCommand
```
## 6. Sprawdź zadania

```powershell
Get-ScheduledTask
```
## 7. Sprawdź usługi

```powershell
Get-CimInstance Win32_Service |
    Where-Object State -eq "Running"
```
## 8. Sprawdź konta

```powershell
Get-LocalUser
Get-LocalGroupMember "Administrators"
```
## 9. Sprawdź ostatnie zdarzenia bezpieczeństwa

```powershell
Get-WinEvent -FilterHashtable @{
    LogName   = "Security"
    StartTime = (Get-Date).AddHours(-2)
}
```
## 10. Zabezpiecz podejrzany plik

Przed usunięciem zapisz:

```powershell
Get-Item "C:\path\suspicious.exe" |
    Select-Object FullName, Length, CreationTime, LastWriteTime
```

```powershell
Get-FileHash "C:\path\suspicious.exe" -Algorithm SHA256
```

```powershell
Get-AuthenticodeSignature "C:\path\suspicious.exe"
```

Nie uruchamiaj podejrzanego pliku na systemie produkcyjnym.
# Czego nie robić

## Nie wyłączaj IPv6 bez konkretnej przyczyny

Wyłączenie IPv6 nie jest uniwersalnym zabezpieczeniem i może powodować problemy z:

- systemem Windows,
- Active Directory,
- aplikacjami,
- mechanizmami tunelowania,
- nowoczesnymi środowiskami chmurowymi.

Zamiast tego poprawnie konfiguruj firewall i monitoring IPv6.
## Nie używaj historycznego DisableAntiSpyware

Wpis:

```text
DisableAntiSpyware
```

jest historycznym mechanizmem i nie powinien być współcześnie traktowany jako prawidłowa metoda zarządzania Defenderem.

Używaj:

- Intune,
- Group Policy,
- Microsoft Defender portal,
- Configuration Manager,
- PowerShell cmdlets Defendera.
## Nie edytuj rejestru bez potrzeby

Bezpośrednia edycja rejestru:

- jest trudniejsza do audytu,
- może powodować błędy,
- może zostać nadpisana przez GPO,
- może nie być obsługiwana w nowych wersjach

Preferuj ustawienia systemowe, PowerShell, GPO lub Intune.
## Nie wyłączaj firewalla dla jednej aplikacji

Utwórz precyzyjną regułę zamiast wyłączać cały profil.
## Nie wyłączaj Defendera podczas zwykłego troubleshootingu

Najpierw sprawdź:

- historię ochrony,
- logi,
- dokładny alert,
- podpis aplikacji,
- możliwość utworzenia ograniczonego wyjątku.
## Nie wystawiaj usług administracyjnych do Internetu

Dotyczy szczególnie:

```text
RDP
WinRM
SMB
WMI
PowerShell Remoting
panele zarządzania
```

Preferuj VPN, MFA i ograniczenie adresów źródłowych.
## Nie zakładaj, że Sandbox jest nieprzenikalny

Windows Sandbox jest przydatnym narzędziem, ale analiza aktywnego malware powinna odbywać się w dedykowanym, izolowanym laboratorium.