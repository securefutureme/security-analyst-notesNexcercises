
Szybka ściąga dotycząca podstawowego zabezpieczania systemów Linux, kontroli dostępu, SSH, zapory sieciowej, audytu, monitoringu oraz kopii zapasowych.

---

## Spis treści

- [[#Najważniejsze zasady]]
- [[#Hardening - Szybka checklista]]
- [[#Szybka diagnostyka incydentu]]
- [[#Silne uwierzytelnianie]]
- [[#Logowanie za pomocą kluczy SSH]]
- [[#Aktualizacje systemu]]
- [[#Usuwanie zbędnego oprogramowania]]
- [[#Ograniczenie dostępu do konta root]]
- [[#Kontrola portów i usług]]
- [[#Konfiguracja zapory sieciowej]]
- [[#SELinux i AppArmor]]
- [[#Audyt i monitoring]]
- [[#Kopie zapasowe]]
- [[#Bezpieczeństwo homelabu]]
- [[#Zarządzanie użytkownikami]]
- [[#Zarządzanie uprawnieniami]]
- [[#Procesy i połączenia sieciowe]]
- [[#Narzędzia bezpieczeństwa]]
- [[#Parametry bezpieczeństwa jądra]]

---
# Hardening - Szybka checklista

-  System oraz pakiety są aktualne.
-  Bezpośrednie logowanie użytkownika `root` przez SSH jest wyłączone.
-  SSH korzysta z kluczy zamiast samych haseł.
-  Konta administracyjne są chronione MFA, gdy jest to możliwe.
-  Uruchmione są tylko niezbędne usługi.
-  Otwarte są wyłącznie wymagane porty.
-  Zapora sieciowa działa zgodnie z zasadą domyślnej odmowy.
-  Usługi działają jako dedykowani użytkownicy bez uprawnień root.
-  SELinux lub AppArmor działa w trybie wymuszania.
-  Logi systemowe są regularnie analizowane.
-  Wykonywane są testowane kopie zapasowe.
-  Dostęp administracyjny nie jest bezpośrednio wystawiony do Internetu.

---

# Silne uwierzytelnianie

Bezpieczeństwo systemu zaczyna się od prawidłowego zarządzania kontami i danymi uwierzytelniającymi.

## Zalecenia

- używaj długich, unikalnych haseł,
- nie używaj tego samego hasła w wielu systemach,
- korzystaj z menedżera haseł,
- włącz uwierzytelnianie wieloskładnikowe,
- usuwaj lub blokuj nieużywane konta,
- ogranicz liczbę kont posiadających dostęp administracyjny,
- stosuj blokadę konta lub opóźnienia po wielu błędnych logowaniach.

Długość hasła jest zwykle ważniejsza niż samo dodawanie znaków specjalnych.

Przykład bezpieczniejszego podejścia:

```text
kilka-losowych-slow-polaczonych-w-dlugie-haslo
```
## Zmiana hasła

```bash
passwd
```

Zmiana hasła innego użytkownika:

```bash
sudo passwd user1
```

## Sprawdzenie polityki wygaśnięcia hasła

```bash
sudo chage -l user1
```

Ustawienie maksymalnego wieku hasła na 90 dni:

```bash
sudo chage -M 90 user1
```

> Okresowa zmiana haseł nie powinna zastępować stosowania unikalnych haseł, MFA oraz reagowania na rzeczywiste oznaki kompromitacji.

---
# Logowanie za pomocą kluczy SSH

Klucze SSH są bezpieczniejszą metodą uwierzytelniania niż samo hasło i znacząco ograniczają skuteczność ataków brute force.
## Generowanie klucza

Zalecany algorytm:

```bash
ssh-keygen -t ed25519 -a 100
```

Alternatywnie RSA:

```bash
ssh-keygen -t rsa -b 4096
```

## Kopiowanie klucza publicznego na serwer

```bash
ssh-copy-id user@server
```
## Połączenie z serwerem

```bash
ssh user@server
```

Z użyciem konkretnego klucza:

```bash
ssh -i ~/.ssh/id_ed25519 user@server
```

## Uprawnienia plików SSH

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```
## Podstawowy hardening serwera SSH

Plik konfiguracyjny:

```text
/etc/ssh/sshd_config
```

Przykładowe ustawienia:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
PermitEmptyPasswords no
MaxAuthTries 3
X11Forwarding no
AllowUsers admin analyst
```

Sprawdzenie składni konfiguracji:

```bash
sudo sshd -t
```

Ponowne załadowanie usługi:

```bash
sudo systemctl reload ssh
```

lub:

```bash
sudo systemctl reload sshd
```

> Przed wyłączeniem logowania hasłem upewnij się, że logowanie za pomocą klucza działa w osobnej sesji terminala.

# Aktualizacje systemu

Aktualizacje usuwają znane podatności w jądrze, bibliotekach, usługach oraz aplikacjach.
## Debian i Ubuntu

Aktualizacja listy pakietów:

```bash
sudo apt update
```

Instalacja aktualizacji:

```bash
sudo apt upgrade
```

Pełna aktualizacja zależności:

```bash
sudo apt full-upgrade
```

Usunięcie niepotrzebnych zależności:

```bash
sudo apt autoremove
```

## Fedora, RHEL i dystrybucje pochodne

```bash
sudo dnf upgrade
```

Lista dostępnych aktualizacji bezpieczeństwa:

```bash
sudo dnf updateinfo list security
```

Instalacja aktualizacji bezpieczeństwa:

```bash
sudo dnf upgrade --security
```

## Sprawdzenie wersji systemu i jądra

```bash
cat /etc/os-release
uname -a
```

## Automatyczne aktualizacje

W systemach Debian/Ubuntu można użyć:

```bash
sudo apt install unattended-upgrades
```

Konfiguracja:

```bash
sudo dpkg-reconfigure unattended-upgrades
```

> Automatyczne aktualizacje powinny być monitorowane. W systemach produkcyjnych aktualizacje należy wcześniej testować i posiadać procedurę wycofania zmian.

---

# Usuwanie zbędnego oprogramowania

Każdy dodatkowy pakiet, demon lub zewnętrzne repozytorium zwiększa powierzchnię ataku.
## Lista zainstalowanych pakietów

Debian/Ubuntu:

```bash
dpkg -l
```

RHEL/Fedora:

```bash
rpm -qa
```
## Lista uruchomionych usług

```bash
systemctl --type=service --state=running
```

Lista włączonych usług:

```bash
systemctl list-unit-files --type=service --state=enabled
```
## Zatrzymanie i wyłączenie usługi

```bash
sudo systemctl disable --now nazwa-uslugi
```
## Usuięcie pakietu

Debian/Ubuntu:

```bash
sudo apt remove nazwa-pakietu
```

Usunięcie wraz z konfiguracją:

```bash
sudo apt purge nazwa-pakietu
```

Fedora/RHEL:

```bash
sudo dnf remove nazwa-pakietu
```

## Zasada minimalizacji

System powinien zawierać tylko:

- wymagane pakiety,
- wymagane usługi,
- wymagane konta,
- wymagane porty,
- wymagane repozytoria.

---
# Ograniczenie dostępu do konta root

Konto `root` posiada pełną kontrolę nad systemem. Codzienna praca bezpośrednio jako `root` zwiększa ryzyko przypadkowego uszkodzenia systemu oraz utrudnia audyt działań.
## Zalecane podejście

1. Utwórz zwykłego użytkownika.
2. Nadaj mu wymagane uprawnienia `sudo`.
3. Wyłącz bezpośrednie logowanie `root` przez SSH.
4. Używaj `sudo` tylko do konkretnych operacji administracyjnych.

## Utworzenie użytkownika

```bash
sudo useradd -m -s /bin/bash adminuser
sudo passwd adminuser
```

W Debianie/Ubuntu można użyć:

```bash
sudo adduser adminuser
```
## Dodanie użytkownika do grupy administracyjnej

Debian/Ubuntu:

```bash
sudo usermod -aG sudo adminuser
```

RHEL/Fedora:

```bash
sudo usermod -aG wheel adminuser
```
## Bezpieczna edycja sudoers

```bash
sudo visudo
```

Przykład ograniczenia użytkownika do konkretnego polecenia:

```text
analyst ALL=(root) /usr/bin/systemctl restart nginx
```

## Usługi nie powinny działać jako root

Usługa sieciowa powinna działać jako:

- dedykowany użytkownik systemowy,
- bez interaktywnej powłoki,
- z minimalnym dostępem do plików,
- z ograniczonymi capabilities,
- z profilem SELinux lub AppArmor.

Sprawdzenie użytkownika procesu:

```bash
ps -eo user,pid,comm,args
```

# Kontrola portów i usług

Otwarte porty mogą ujawniać usługi dostępne lokalnie lub zdalnie.
## Sprawdzenie nasłuchujących portów

Zalecane narzędzie:

```bash
sudo ss -tulpn
```

Znaczenie opcji:

- `-t` — TCP,
- `-u` — UDP,
- `-l` — porty nasłuchujące,
- `-p` — proces,
- `-n` — adresy i porty w formie numerycznej.

Tylko TCP:

```bash
sudo ss -ltnp
```

Tylko UDP:

```bash
sudo ss -lunp
```
## Alternatywa: netstat

```bash
sudo netstat -tulpn
```

> `netstat` jest narzędziem starszym. W większości współczesnych systemów zalecane jest `ss`.

## Proces korzystający z portu

```bash
sudo lsof -i :8080
```

lub:

```bash
sudo fuser -v 8080/tcp
```

## Skan lokalnego hosta

```bash
nmap -sV 127.0.0.1
```

Skan z innej maszyny w autoryzowanym środowisku:

```bash
nmap -sV 192.168.1.10
```

## Pytania kontrolne

Dla każdego otwartego portu ustal:

1. Jaki proces nasłuchuje?
2. Czy usługa jest potrzebna?
3. Czy port musi być dostępny zdalnie?
4. Czy dostęp można ograniczyć do konkretnej sieci?
5. Czy usługa wymaga uwierzytelnienia?
6. Czy transmisja jest szyfrowana?

---
# Konfiguracja zapory sieciowej

Zapora sieciowa ogranicza ruch przychodzący, wychodzący lub przekazywany pomiędzy interfejsami.

> Firewall jest jedną z warstw ochrony. Nie naprawia podatnej aplikacji i nie zastępuje aktualizacji, uwierzytelniania ani segmentacji sieci.

## UFW

Sprawdzenie stanu:

```bash
sudo ufw status verbose
```

Domyślne zasady:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Zezwolenie na SSH:

```bash
sudo ufw allow OpenSSH
```

Zezwolenie na port:

```bash
sudo ufw allow 443/tcp
```

Ograniczenie SSH do konkretnej sieci:

```bash
sudo ufw allow from 192.168.1.0/24 to any port 22 proto tcp
```

Włączenie zapory:

```bash
sudo ufw enable
```

Usunięcie reguły:

```bash
sudo ufw delete allow 443/tcp
```

## firewalld

Sprawdzenie stanu:

```bash
sudo firewall-cmd --state
```

Aktywne strefy:

```bash
sudo firewall-cmd --get-active-zones
```

Lista reguł:

```bash
sudo firewall-cmd --list-all
```

Dodanie usługi HTTPS:

```bash
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
```

Dodanie portu:

```bash
sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload
```

## nftables

Wyświetlenie aktualnych reguł:

```bash
sudo nft list ruleset
```

`nftables` jest współczesnym mechanizmem filtrowania pakietów w jądrze Linux i zastępuje wiele zastosowań starszego `iptables`.

---

# SELinux i AppArmor

SELinux i AppArmor implementują **Mandatory Access Control**. Ograniczają działania procesu nawet wtedy, gdy tradycyjne uprawnienia plików pozwalałyby na większy dostęp.
## SELinux

Najczęściej spotykany w:

- RHEL,
- Fedora,
- Rocky Linux,
- AlmaLinux,
- CentOS Stream.

Sprawdzenie stanu:

```bash
sestatus
```

lub:

```bash
getenforce
```

Możliwe tryby:

```text
Enforcing   — polityki są wymuszane
Permissive  — naruszenia są logowane, ale nieblokowane
Disabled    — SELinux jest wyłączony
```

Tymczasowa zmiana trybu:

```bash
sudo setenforce 0
sudo setenforce 1
```

Lista kontekstów:

```bash
ls -Z
```

Przywrócenie prawidłowego kontekstu:

```bash
sudo restorecon -Rv /var/www/html
```

Sprawdzenie wartości boolean:

```bash
getsebool httpd_can_network_connect
```

Zmiana trwała:

```bash
sudo setsebool -P httpd_can_network_connect on
```

## AppArmor

Najczęściej spotykany w:

- Ubuntu,
- Debianie,
- SUSE.

Sprawdzenie stanu:

```bash
sudo aa-status
```

Przeładowanie profilu:

```bash
sudo apparmor_parser -r /etc/apparmor.d/nazwa-profilu
```

Tryb wymuszania:

```bash
sudo aa-enforce /etc/apparmor.d/nazwa-profilu
```

Tryb nauki:

```bash
sudo aa-complain /etc/apparmor.d/nazwa-profilu
```

> Nie wyłączaj SELinux lub AppArmor wyłącznie po to, aby aplikacja zaczęła działać. Najpierw przeanalizuj logi i dostosuj politykę.

# Audyt i monitoring

Regularny audyt pozwala wykrywać błędy konfiguracji, podejrzane działania oraz nieautoryzowane zmiany.
## Logi systemowe

Bieżące logi:

```bash
journalctl
```

Logi od ostatniego uruchomienia:

```bash
journalctl -b
```

Logi konkretnej usługi:

```bash
journalctl -u ssh
```

lub:

```bash
journalctl -u sshd
```

Logi z ostatniej godziny:

```bash
journalctl --since "1 hour ago"
```

Śledzenie logów na żywo:

```bash
journalctl -f
```

## Próby logowania

Udane logowania:

```bash
last
```

Nieudane logowania:

```bash
sudo lastb
```

Aktualnie zalogowani użytkownicy:

```bash
who
```

Więcej informacji o aktywnych sesjach:

```bash
w
```
## auditd

Sprawdzenie usługi:

```bash
systemctl status auditd
```

Lista reguł:

```bash
sudo auditctl -l
```

Monitorowanie pliku:

```bash
sudo auditctl -w /etc/passwd -p wa -k passwd_changes
```

Wyszukanie zdarzeń:

```bash
sudo ausearch -k passwd_changes
```

Raport uwierzytelniania:

```bash
sudo aureport -au
```
## Lynis

Instalacja:

```bash
sudo apt install lynis
```

Uruchomienie audytu:

```bash
sudo lynis audit system
```

Lynis może wskazać:

- słabe ustawienia SSH,
- brakujące aktualizacje,
- niewłaściwe uprawnienia,
- brakujące mechanizmy ochronne,
- błędy konfiguracji usług.
## Kontrola integralności

### AIDE

Inicjalizacja bazy:

```bash
sudo aideinit
```

Sprawdzenie zmian:

```bash
sudo aide --check
```
### Tripwire

Narzędzie do wykrywania zmian w krytycznych plikach systemowych.

> Kontrola integralności jest skuteczna tylko wtedy, gdy baza referencyjna została utworzona na zaufanym systemie i jest bezpiecznie przechowywana.

# Kopie zapasowe

Backup jest kluczowym elementem ochrony przed:

- awarią,
- błędem administratora,
- usunięciem danych,
- ransomware,
- uszkodzeniem systemu plików,
- nieudaną aktualizacją.
## Zasada 3-2-1

- posiadaj co najmniej **3 kopie danych**,
- przechowuj je na **2 różnych typach nośników**,
- co najmniej **1 kopię przechowuj poza głównym środowiskiem**.
## Rsync

Kopia katalogu:

```bash
rsync -avh /dane/ /backup/dane/
```

Kopia przez SSH:

```bash
rsync -avh -e ssh /dane/ user@backup-server:/backup/dane/
```

Usuwanie z backupu plików, których nie ma już w źródle:

```bash
rsync -avh --delete /dane/ /backup/dane/
```

> Opcja `--delete` może usunąć dane z katalogu docelowego. Przed użyciem sprawdź wynik za pomocą `--dry-run`.

Test:

```bash
rsync -avh --delete --dry-run /dane/ /backup/dane/
```
## Archiwum tar

```bash
tar -czf backup-etc.tar.gz /etc
```
## Szyfrowanie kopii

```bash
gpg --symmetric backup-etc.tar.gz
```
## Najważniejszy test

Backup nie jest potwierdzony, dopóki nie wykonano testowego przywrócenia danych.

Sprawdzaj:

- czy kopia zawiera aktualne pliki,
- czy dane nie są uszkodzone,
- czy klucze szyfrujące są dostępne,
- ile trwa odtworzenie systemu,
- czy procedura przywracania jest udokumentowana.
# Bezpieczeństwo homelabu

W homelabie często jedna osoba wykonuje większość działań administracyjnych. Nie oznacza to jednak, że wszystkie usługi powinny działać jako `root`.
## Najważniejsze zasady

### 1.Nie wystawiaj usług bez potrzeby

Najlepszym sposobem ochrony portu jest niewystawianie go do publicznego Internetu.

Preferowana kolejność dostępu:

1. VPN,
2. prywatna sieć lub VLAN,
3. reverse proxy z silnym uwierzytelnianiem,
4. bezpośrednie wystawienie portu — tylko gdy jest konieczne.

Przykładowe rozwiązania VPN:

- WireGuard,
- Tailscale,
- Headscale.

### 2.Porty administracyjne

Porty zapewniające dostęp administracyjny, np.:

- SSH,
- Cockpit,
- panel hypervisora,
- panel routera,
- panel zarządzania kontenerami,

nie powinny być bezpośrednio dostępne z publicznego Internetu.
### 3. Kontenery

Kontener ogranicza aplikację, ale sam w sobie nie gwarantuje pełnej izolacji.

Dobre praktyki:

- uruchamiaj proces jako użytkownik bez uprawnień root,
- używaj obrazu minimalnego,
- nie używaj trybu `--privileged`,
- nie montuj niepotrzebnie `/var/run/docker.sock`,
- ograniczaj capabilities,
- ustawiaj system plików jako read-only, jeśli jest to możliwe,
- aktualizuj obrazy,
- skanuj zależności i obrazy.

Przykład:

```bash
docker run \
  --read-only \
  --cap-drop=ALL \
  --security-opt=no-new-privileges \
  --user 1000:1000 \
  image-name
```
### 4. Ochrona warstwowa

Bezpieczeństwo powinno obejmować wiele niezależnych warstw:

```text
VPN
→ firewall
→ uwierzytelnianie
→ minimalne uprawnienia
→ aktualizacje
→ SELinux/AppArmor
→ monitoring
→ backup
```

---
# Zarządzanie użytkownikami

|Polecenie|Zastosowanie|Przykład|
|---|---|---|
|`passwd`|Zmiana hasła|`sudo passwd user1`|
|`chpasswd`|Zbiorcza zmiana haseł|`sudo chpasswd < users.txt`|
|`chage`|Polityka wygaśnięcia hasła|`sudo chage -M 90 user1`|
|`useradd`|Utworzenie użytkownika|`sudo useradd -m user2`|
|`usermod`|Modyfikacja użytkownika|`sudo usermod -aG sudo user2`|
|`userdel`|Usunięcie użytkownika|`sudo userdel -r user2`|
|`groupadd`|Utworzenie grupy|`sudo groupadd analysts`|
|`groupmod`|Modyfikacja grupy|`sudo groupmod -n soc analysts`|
|`groupdel`|Usunięcie grupy|`sudo groupdel analysts`|
|`id`|Informacje o użytkowniku|`id user1`|
|`groups`|Grupy użytkownika|`groups user1`|
|`getent`|Odczyt baz użytkowników i grup|`getent passwd user1`|
## Blokada konta

```bash
sudo usermod -L user1
```

Odblokowanie:

```bash
sudo usermod -U user1
```

Wygaśnięcie konta:

```bash
sudo chage -E 0 user1
```

# Zarządzanie uprawnieniami

|Polecenie|Zastosowanie|Przykład|
|---|---|---|
|`chmod`|Zmiana uprawnień|`chmod 640 file.txt`|
|`chown`|Zmiana właściciela|`sudo chown user1 file.txt`|
|`chgrp`|Zmiana grupy|`sudo chgrp analysts file.txt`|
|`umask`|Domyślne uprawnienia nowych plików|`umask 077`|
|`getfacl`|Wyświetlenie ACL|`getfacl file.txt`|
|`setfacl`|Modyfikacja ACL|`setfacl -m u:user1:r file.txt`|
|`lsattr`|Atrybuty pliku|`lsattr file.txt`|
|`chattr`|Modyfikacja atrybutów|`sudo chattr +i file.txt`|
## Przykładowe uprawnienia

```bash
chmod 600 private.key
```

Tylko właściciel może czytać i modyfikować plik.

```bash
chmod 640 config.conf
```

- właściciel: odczyt i zapis,
- grupa: odczyt,
- pozostali: brak dostępu.

```bash
chmod 750 script.sh
```

- właściciel: pełne uprawnienia,
- grupa: odczyt i wykonanie,
- pozostali: brak dostępu.

## Znaczenie wartości

|Wartość|Uprawnienie|
|--:|---|
|`4`|odczyt|
|`2`|zapis|
|`1`|wykonanie|
Przykład:

```text
7 = 4 + 2 + 1 = rwx
6 = 4 + 2     = rw-
5 = 4 + 1     = r-x
4 = 4         = r--
```
## Pliki z bitem SUID lub SGID

Wyszukiwanie plików SUID:

```bash
sudo find / -type f -perm -4000 2>/dev/null
```

Wyszukiwanie plików SGID:

```bash
sudo find / -type f -perm -2000 2>/dev/null
```

Nietypowy plik SUID może stanowić ścieżkę eskalacji uprawnień.
# Procesy i połączenia sieciowe

|Polecenie|Zastosowanie|Przykład|
|---|---|---|
|`ps`|Lista procesów|`ps aux`|
|`top`|Monitoring procesów|`top`|
|`htop`|Interaktywny monitoring|`htop`|
|`pstree`|Drzewo procesów|`pstree -ap`|
|`pgrep`|Wyszukiwanie procesu|`pgrep -af nginx`|
|`lsof`|Otwarte pliki i sockety|`sudo lsof -i`|
|`ss`|Analiza socketów|`sudo ss -tulpn`|
|`fuser`|Proces używający pliku lub portu|`sudo fuser -v 443/tcp`|
|`kill`|Wysłanie sygnału do procesu|`kill PID`|
|`systemctl`|Zarządzanie usługami|`systemctl status ssh`|
## Podejrzany proces

```bash
ps aux --sort=-%cpu | head
```

```bash
ps aux --sort=-%mem | head
```

Pełna linia poleceń:

```bash
ps -eo pid,ppid,user,lstart,cmd
```

Pliki otwarte przez proces:

```bash
sudo lsof -p PID
```

Ścieżka pliku wykonywalnego:

```bash
readlink -f /proc/PID/exe
```

Argumenty procesu:

```bash
tr '\0' ' ' < /proc/PID/cmdline
```

Połączenia konkretnego procesu:

```bash
sudo lsof -Pan -p PID -i
```
# Narzędzia bezpieczeństwa

## Narzędzia sieciowe

|Narzędzie|Zastosowanie|
|---|---|
|`ssh`|Szyfrowany dostęp zdalny|
|`scp`|Kopiowanie plików przez SSH|
|`sftp`|Interaktywny transfer plików przez SSH|
|`ss`|Analiza socketów|
|`nmap`|Skanowanie portów i usług|
|`tcpdump`|Przechwytywanie pakietów|
|`Wireshark`|Graficzna analiza ruchu|
|`curl`|Wysyłanie żądań HTTP i innych protokołów|
|`wget`|Pobieranie plików|
|`dig`|Diagnostyka DNS|
|`traceroute`|Analiza trasy pakietów|
Przechwytywanie ruchu:

```bash
sudo tcpdump -i any -nn
```

Ruch DNS:

```bash
sudo tcpdump -i any -nn port 53
```

Zapis do pliku PCAP:

```bash
sudo tcpdump -i any -nn -w capture.pcap
```
## Zapora i ochrona dostępu

|Narzędzie|Zastosowanie|
|---|---|
|`ufw`|Prosta konfiguracja firewalla|
|`firewalld`|Firewall oparty na strefach|
|`nftables`|Współczesny firewall Linux|
|`iptables`|Starszy interfejs filtrowania pakietów|
|`fail2ban`|Blokowanie źródeł wielu nieudanych prób logowania|

Status Fail2Ban:

```bash
sudo fail2ban-client status
```

Status konkretnego jaila:

```bash
sudo fail2ban-client status sshd
```
## Audyt i kontrola integralności

|Narzędzie|Zastosowanie|
|---|---|
|`auditd`|Audyt wywołań systemowych i zdarzeń|
|`Lynis`|Audyt konfiguracji i hardening|
|`AIDE`|Kontrola integralności plików|
|`Tripwire`|Wykrywanie zmian w plikach|
|`Logwatch`|Raportowanie zdarzeń z logów|
|`OpenSCAP`|Audyt zgodności i hardening|
## Wykrywanie rootkitów

|Narzędzie|Zastosowanie|
|---|---|
|`chkrootkit`|Wyszukiwanie oznak popularnych rootkitów|
|`rkhunter`|Kontrola rootkitów, backdoorów i anomalii|
Uruchomienie:

```bash
sudo chkrootkit
```

```bash
sudo rkhunter --check
```

> Wynik tych narzędzi nie jest jednoznacznym potwierdzeniem infekcji. Mogą generować false positive i powinny być traktowane jako element szerszej analizy.
## Kryptografia

|Narzędzie|Zastosowanie|
|---|---|
|`gpg`|Szyfrowanie i podpisywanie plików|
|`openssl`|Certyfikaty, klucze i operacje kryptograficzne|
|`sha256sum`|Obliczanie hashy SHA-256|
|`md5sum`|Obliczanie MD5 — niezalecane do bezpieczeństwa kryptograficznego|
Hash pliku:

```bash
sha256sum file.iso
```

Generowanie losowych danych:

```bash
openssl rand -base64 32
```

Sprawdzenie certyfikatu serwera:

```bash
openssl s_client -connect example.com:443 -servername example.com
```

# Parametry bezpieczeństwa jądra

Wyświetlenie parametru:

```bash
sysctl net.ipv4.tcp_syncookies
```

Tymczasowa zmiana:

```bash
sudo sysctl -w net.ipv4.tcp_syncookies=1
```

Trwała konfiguracja powinna znaleźć się w pliku:

```text
/etc/sysctl.conf
```

lub:

```text
/etc/sysctl.d/99-security.conf
```

Przykład:

```text
net.ipv4.tcp_syncookies = 1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.default.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.default.send_redirects = 0
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1
```

Wczytanie konfiguracji:

```bash
sudo sysctl --system
```

> Parametry jądra należy dostosować do funkcji hosta. Inne ustawienia będą odpowiednie dla serwera, routera, kontenera i stacji roboczej.
# Szybka diagnostyka incydentu

## 1. Sprawdź użytkowników i logowania

```bash
who
w
last
sudo lastb
```

## 2. Sprawdź procesy

```bash
ps auxf
pstree -ap
```

## 3. Sprawdź połączenia

```bash
sudo ss -tulpn
sudo ss -tpn
```

## 4. Sprawdź usługi

```bash
systemctl --type=service --state=running
systemctl --failed
```

## 5. Sprawdź ostatnie logi

```bash
journalctl --since "2 hours ago"
```

## 6. Sprawdź zadania cykliczne

```bash
crontab -l
sudo ls -la /etc/cron*
sudo systemctl list-timers --all
```

## 7. Sprawdź autostart

```bash
systemctl list-unit-files --state=enabled
ls -la ~/.config/autostart/
```

## 8. Sprawdź ostatnio zmienione pliki

```bash
sudo find /etc -type f -mtime -1 -ls
```

```bash
sudo find /tmp /var/tmp /dev/shm -type f -ls
```

## 9. Sprawdź konta uprzywilejowane

```bash
getent group sudo
getent group wheel
awk -F: '$3 == 0 {print $1}' /etc/passwd
```

Standardowo tylko użytkownik `root` powinien posiadać UID `0`.

## 10. Zabezpiecz dowody

Przed usuwaniem podejrzanych plików:

```bash
sha256sum suspicious_file
stat suspicious_file
file suspicious_file
```

Kopię podejrzanego pliku należy przechowywać w bezpiecznej, odizolowanej lokalizacji.
# Najważniejsze zasady

1. **Minimalne uprawnienia** — użytkownik i usługa powinny mieć tylko niezbędny dostęp.
2. **Minimalna powierzchnia ataku** — wyłącz zbędne porty, usługi i pakiety.
3. **Defense in depth** — nie polegaj na jednym mechanizmie ochronnym.
4. **Regularne aktualizacje** — eliminuj znane podatności.
5. **Silne uwierzytelnianie** — korzystaj z kluczy SSH i MFA.
6. **Monitoring i logowanie** — wykrycie incydentu jest równie ważne jak prewencja.
7. **Testowane backupy** — kopia bez testu odtworzenia nie daje pewności odzyskania danych.
8. **Bezpieczne ustawienia domyślne** — domyślna odmowa dostępu jest bezpieczniejsza niż domyślne zezwolenie.
9. **Segmentacja sieci** — systemy administracyjne i publiczne usługi powinny być rozdzielone.
10. **Dokumentacja** — każda istotna zmiana konfiguracji powinna być możliwa do odtworzenia i zweryfikowania.
