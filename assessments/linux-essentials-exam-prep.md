# Linux Essentials Prüfungsvorbereitung (010-160)

## Prüfungsübersicht

**Prüfungscode:** 010-160  
**Dauer:** 60 Minuten  
**Fragen:** 40 Multiple-Choice  
**Bestehensgrenze:** 500 von 800 Punkten  
**Sprachen:** Deutsch, Englisch und weitere  
**Zertifizierung:** Lebenslang gültig (kein Ablaufdatum)

## Gewichtung der Prüfungsthemen

| Topic | Gewichtung | Beschreibung |
|-------|------------|--------------|
| 1. The Linux Community and a Career in Open Source | 7% | Linux-Evolution, Distributionen, Open Source |
| 2. Finding Your Way on a Linux System | 8% | Command Line Basics, Hilfe |
| 3. The Power of the Command Line | 40% | Dateiverwaltung, Verzeichnisse, Archive |
| 4. The Linux Operating System | 20% | Hardware, Prozesse, Netzwerk |
| 5. Security and File Permissions | 25% | Benutzer, Gruppen, Berechtigungen |

---

## Topic 1: The Linux Community and a Career in Open Source (7%)

### 1.1 Linux Evolution and Popular Operating Systems

**Schlüsselkonzepte:**
- Geschichte von Linux (Linus Torvalds, 1991)
- Kernel vs. Distribution
- Major Distributionen und ihre Derivate

**Wichtige Distributionen:**
```
Debian-Familie:
├── Debian
├── Ubuntu
│   ├── Kubuntu (KDE)
│   ├── Xubuntu (XFCE)
│   └── Linux Mint
└── Raspbian (Raspberry Pi)

Red Hat-Familie:
├── Red Hat Enterprise Linux (RHEL)
├── Fedora
├── CentOS/Rocky Linux
└── openSUSE

Andere:
├── Arch Linux
├── Gentoo
└── Slackware
```

**Prüfungsfragen-Beispiel:**
```
Welche Distribution ist NICHT von Debian abgeleitet?
a) Ubuntu
b) Linux Mint
c) Fedora ✓
d) Raspbian
```

### 1.2 Major Open Source Applications

**Wichtige Open Source Software:**
- **Office:** LibreOffice, OpenOffice
- **Browser:** Firefox, Chromium
- **Email:** Thunderbird, Evolution
- **Graphics:** GIMP, Inkscape, Blender
- **Multimedia:** VLC, Audacity
- **Development:** GCC, Git, Apache, MySQL/MariaDB

**Merkhilfe:** LAMP-Stack
- **L**inux
- **A**pache (Webserver)
- **M**ySQL/MariaDB (Datenbank)  
- **P**HP/Python/Perl (Programmierung)

### 1.3 Open Source Software and Licensing

**Lizenztypen:**

| Lizenz | Copyleft | Kommerzielle Nutzung | Beispiel Software |
|--------|----------|---------------------|-------------------|
| GPL | Stark | Ja* | Linux Kernel, GCC |
| LGPL | Schwach | Ja | glibc, GTK+ |
| BSD | Nein | Ja | FreeBSD, OpenBSD |
| MIT | Nein | Ja | X11, Node.js |
| Apache | Nein | Ja | Apache HTTP Server |

*Bei GPL: Änderungen müssen auch GPL sein

**Prüfungstipp:** GPL = "viral license" - Änderungen müssen auch Open Source sein

### 1.4 ICT Skills and Working in Linux

**Karrierewege:**
- System Administrator
- DevOps Engineer
- Cloud Engineer
- Security Specialist
- Software Developer

**Wichtige Skills:**
- Command Line Interface (CLI)
- Shell Scripting
- Netzwerk-Grundlagen
- Virtualisierung
- Container (Docker)
- Cloud (AWS, Azure, GCP)

---

## Topic 2: Finding Your Way on a Linux System (8%)

### 2.1 Command Line Basics

**Shell-Typen:**
```bash
# Verfügbare Shells anzeigen
cat /etc/shells

# Aktuelle Shell
echo $SHELL
echo $0

# Shell wechseln
bash
sh
zsh
```

**Wichtige Variablen:**
```bash
echo $PATH      # Ausführbare Programme
echo $HOME      # Home-Verzeichnis
echo $USER      # Benutzername
echo $PWD       # Aktuelles Verzeichnis
echo $OLDPWD    # Vorheriges Verzeichnis
```

### 2.2 Using the Command Line to Get Help

**Hilfe-Befehle:**
```bash
# Manual Pages
man ls
man -k network    # Suche nach Keyword
man 5 passwd      # Section 5 (Dateiformat)

# Sections:
# 1 - Befehle
# 2 - Systemaufrufe
# 3 - Bibliotheksfunktionen
# 4 - Gerätedateien
# 5 - Dateiformate
# 6 - Spiele
# 7 - Verschiedenes
# 8 - Systemverwaltung

# Andere Hilfe
ls --help
help cd          # Für built-in Befehle
info coreutils   # Detaillierte Info
which ls         # Pfad zum Befehl
type cd          # Typ des Befehls
whereis ls       # Alle Pfade
```

### 2.3 Using Directories and Listing Files

**Verzeichnisstruktur (FHS):**
```
/
├── bin     # Essenzielle Befehle
├── boot    # Boot-Dateien
├── dev     # Gerätedateien
├── etc     # Konfiguration
├── home    # Benutzer-Homes
├── lib     # Bibliotheken
├── media   # Wechselmedien
├── mnt     # Temporäre Mounts
├── opt     # Optionale Software
├── proc    # Prozess-Info
├── root    # Root-Home
├── sbin    # System-Befehle
├── srv     # Service-Daten
├── sys     # Kernel-Schnittstelle
├── tmp     # Temporäre Dateien
├── usr     # Benutzer-Programme
└── var     # Variable Daten
```

**Navigation:**
```bash
pwd              # Print Working Directory
cd /etc          # Absoluter Pfad
cd ../..         # Zwei Ebenen hoch
cd -             # Vorheriges Verzeichnis
cd ~             # Home
cd ~user         # Home von 'user'
```

**Listing:**
```bash
ls              # Einfache Liste
ls -l           # Long format
ls -la          # Mit versteckten
ls -lh          # Human readable
ls -lt          # Nach Zeit sortiert
ls -lS          # Nach Größe sortiert
ls -R           # Rekursiv
```

### 2.4 Creating, Moving and Deleting Files

**Dateiverwaltung:**
```bash
# Erstellen
touch file.txt
mkdir directory
mkdir -p dir1/dir2/dir3    # Parent-Verzeichnisse

# Kopieren
cp source dest
cp -r dir1 dir2            # Rekursiv
cp -i file1 file2          # Interaktiv
cp -p file1 file2          # Preserve attributes

# Verschieben/Umbenennen
mv old new
mv file.txt /tmp/
mv -i source dest          # Interaktiv

# Löschen
rm file.txt
rm -r directory            # Rekursiv
rm -rf directory           # Force + Rekursiv
rmdir empty_dir            # Nur leere Verzeichnisse
```

**Wildcards (Globbing):**
```bash
*       # Beliebig viele Zeichen
?       # Genau ein Zeichen
[abc]   # Ein Zeichen aus der Liste
[a-z]   # Bereich
[!abc]  # Nicht in der Liste

# Beispiele
ls *.txt
ls file?.dat
ls [A-Z]*
ls *.[ch]    # .c oder .h Dateien
```

---

## Topic 3: The Power of the Command Line (40%)

### 3.1 Archiving Files on the Command Line

**tar (Tape Archive):**
```bash
# Erstellen
tar -cvf archiv.tar verzeichnis/     # Create, Verbose, File
tar -czvf archiv.tar.gz verzeichnis/ # Mit gzip
tar -cjvf archiv.tar.bz2 verzeichnis/ # Mit bzip2
tar -cJvf archiv.tar.xz verzeichnis/ # Mit xz

# Entpacken
tar -xvf archiv.tar                  # eXtract
tar -xzvf archiv.tar.gz
tar -xjvf archiv.tar.bz2
tar -xJvf archiv.tar.xz

# Anzeigen
tar -tvf archiv.tar                  # lisT

# Wichtige Optionen
-C /ziel    # Change directory
--exclude   # Dateien ausschließen
```

**Kompression:**
```bash
# gzip (schnell, weniger Kompression)
gzip file.txt         # Erstellt file.txt.gz
gunzip file.txt.gz    # Entpackt
zcat file.txt.gz      # Anzeigen ohne entpacken

# bzip2 (langsamer, bessere Kompression)
bzip2 file.txt        # Erstellt file.txt.bz2
bunzip2 file.txt.bz2  # Entpackt
bzcat file.txt.bz2    # Anzeigen

# xz (sehr gute Kompression)
xz file.txt           # Erstellt file.txt.xz
unxz file.txt.xz      # Entpackt
xzcat file.txt.xz     # Anzeigen

# zip (Windows-kompatibel)
zip archiv.zip file1 file2
zip -r archiv.zip verzeichnis/
unzip archiv.zip
unzip -l archiv.zip   # Liste anzeigen
```

### 3.2 Searching and Extracting Data from Files

**grep (Global Regular Expression Print):**
```bash
grep "muster" datei.txt
grep -i "muster" datei.txt    # Case-insensitive
grep -v "muster" datei.txt    # Invert (ohne Muster)
grep -n "muster" datei.txt    # Mit Zeilennummern
grep -c "muster" datei.txt    # Count
grep -r "muster" verzeichnis/ # Rekursiv
grep -E "regex" datei.txt     # Extended regex
grep "^Start" datei.txt       # Zeilen die mit Start beginnen
grep "Ende$" datei.txt        # Zeilen die mit Ende enden
```

**Regular Expressions Basics:**
```
^    # Zeilenanfang
$    # Zeilenende
.    # Ein beliebiges Zeichen
*    # 0 oder mehr vom vorherigen
+    # 1 oder mehr (Extended)
?    # 0 oder 1 (Extended)
[]   # Zeichenklasse
|    # Oder (Extended)
```

**Textverarbeitung:**
```bash
# cat - Concatenate
cat file.txt
cat file1 file2 > combined.txt
cat -n file.txt    # Mit Zeilennummern

# head/tail
head file.txt      # Erste 10 Zeilen
head -n 20 file.txt
tail file.txt      # Letzte 10 Zeilen
tail -n 20 file.txt
tail -f logfile    # Follow (live)

# cut - Spalten extrahieren
cut -d: -f1 /etc/passwd      # Delimiter :, Field 1
cut -d: -f1,3 /etc/passwd    # Fields 1 und 3
cut -c1-10 file.txt          # Characters 1-10

# sort
sort file.txt
sort -n numbers.txt          # Numerisch
sort -r file.txt            # Reverse
sort -u file.txt            # Unique

# uniq - Duplikate entfernen
sort file.txt | uniq
sort file.txt | uniq -c     # Mit Anzahl
sort file.txt | uniq -d     # Nur Duplikate

# wc - Word Count
wc file.txt         # Lines, Words, Bytes
wc -l file.txt      # Nur Lines
wc -w file.txt      # Nur Words
wc -c file.txt      # Nur Bytes/Characters
```

### 3.3 Turning Commands into a Script

**Shebang und Ausführung:**
```bash
#!/bin/bash
# Mein erstes Script

echo "Hallo Welt!"
```

**Script ausführbar machen:**
```bash
chmod +x script.sh
./script.sh
```

**Variablen:**
```bash
#!/bin/bash
NAME="Linux"
echo "Hallo $NAME"
echo "Hallo ${NAME}!"

# Spezielle Variablen
echo $0    # Script-Name
echo $1    # Erstes Argument
echo $#    # Anzahl Argumente
echo $@    # Alle Argumente
echo $?    # Exit-Status letzter Befehl
echo $$    # Prozess-ID
```

**Kontrollstrukturen:**
```bash
# if-Bedingung
if [ -f datei.txt ]; then
    echo "Datei existiert"
fi

# for-Schleife
for i in 1 2 3; do
    echo "Nummer: $i"
done

# while-Schleife
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    count=$((count + 1))
done
```

**Test-Operatoren:**
```bash
-f file     # File exists
-d dir      # Directory exists
-r file     # Readable
-w file     # Writable
-x file     # Executable
-s file     # Size > 0
-z string   # String ist leer
-n string   # String ist nicht leer
```

---

## Topic 4: The Linux Operating System (20%)

### 4.1 Choosing an Operating System

**Desktop-Umgebungen:**
- **GNOME:** Modern, ressourcenintensiv (Ubuntu default)
- **KDE Plasma:** Feature-reich, anpassbar
- **XFCE:** Leichtgewichtig, stabil
- **LXDE/LXQt:** Sehr leicht
- **Cinnamon:** Traditionell (Linux Mint)
- **MATE:** GNOME 2 Fork

**Auswahlkriterien:**
- Hardware-Ressourcen
- Stabilität vs. aktuelle Software
- Support-Zeitraum
- Community vs. Enterprise
- Package Management (apt, yum, pacman)

### 4.2 Understanding Computer Hardware

**Hardware-Informationen:**
```bash
# CPU
lscpu
cat /proc/cpuinfo
nproc    # Anzahl Prozessoren

# Memory
free -h
cat /proc/meminfo

# Disk
lsblk
fdisk -l
df -h     # Disk free
du -sh *  # Disk usage

# PCI Devices
lspci
lspci -v

# USB
lsusb
lsusb -v

# Kernel Module
lsmod
modinfo module_name

# Hardware Summary
sudo lshw -short
sudo dmidecode
```

**Wichtige Verzeichnisse:**
- `/proc` - Prozess- und Kernel-Info
- `/sys` - Sysfs (Kernel-Schnittstellen)
- `/dev` - Device-Dateien

### 4.3 Where Data is Stored

**Dateisystem-Hierarchie:**
```bash
# Programme
/bin, /sbin       # System-essentiell
/usr/bin, /usr/sbin  # Normale Programme
/usr/local/bin    # Lokale Programme

# Konfiguration
/etc              # System-Config
~/.config         # User-Config

# Daten
/var/log          # Log-Dateien
/var/spool        # Warteschlangen
/tmp              # Temporär (beim Boot gelöscht)
/var/tmp          # Temporär (persistent)

# Libraries
/lib, /lib64      # System
/usr/lib          # Programme
```

**Prozess-Informationen:**
```bash
ps              # Eigene Prozesse
ps aux          # Alle Prozesse
ps -ef          # Full format
pstree          # Baum-Ansicht

top             # Live-Monitor
htop            # Besserer Monitor

kill PID        # SIGTERM (15)
kill -9 PID     # SIGKILL
killall name    # Nach Name
pkill pattern   # Nach Muster
```

### 4.4 Your Computer on the Network

**Netzwerk-Befehle:**
```bash
# IP-Konfiguration
ip addr show
ip a            # Kurzform
ifconfig        # Veraltet

# Hostname
hostname
hostname -f     # FQDN
hostnamectl

# DNS
cat /etc/resolv.conf
nslookup google.com
dig google.com
host google.com

# Verbindungen testen
ping -c 4 google.com
ping6 google.com
traceroute google.com

# Ports
netstat -tlnp   # TCP listening
ss -tlnp        # Moderner
nmap localhost  # Port-Scan

# Netzwerk-Config
cat /etc/hosts
cat /etc/hostname
cat /etc/network/interfaces    # Debian
cat /etc/sysconfig/network-scripts/  # RedHat
```

---

## Topic 5: Security and File Permissions (25%)

### 5.1 Basic Security and Identifying User Types

**Benutzertypen:**
- **root** - UID 0, vollständige Kontrolle
- **System-Benutzer** - UID 1-999, für Services
- **Normale Benutzer** - UID 1000+

**Benutzer-Befehle:**
```bash
# Identität
whoami
id
groups

# Benutzer wechseln
su - username    # Login shell
su username      # Nur wechseln
sudo command     # Als root ausführen

# Benutzer-Info
w                # Wer ist eingeloggt
who
last             # Login-Historie
finger username  # User-Info (falls installiert)
```

**Wichtige Dateien:**
```bash
/etc/passwd     # Benutzer-Datenbank
/etc/shadow     # Verschlüsselte Passwörter
/etc/group      # Gruppen
/etc/sudoers    # sudo-Berechtigungen
```

### 5.2 Creating Users and Groups

**Benutzerverwaltung:**
```bash
# Benutzer erstellen
sudo useradd username
sudo useradd -m -s /bin/bash username  # Mit Home und Shell
sudo adduser username   # Debian: Interaktiv

# Passwort setzen
sudo passwd username

# Benutzer ändern
sudo usermod -aG gruppe username  # Zu Gruppe hinzufügen
sudo usermod -s /bin/zsh username # Shell ändern
sudo usermod -L username          # Lock
sudo usermod -U username          # Unlock

# Benutzer löschen
sudo userdel username
sudo userdel -r username  # Mit Home-Verzeichnis

# Gruppen
sudo groupadd gruppe
sudo groupdel gruppe
sudo gpasswd -a user gruppe  # User zu Gruppe
sudo gpasswd -d user gruppe  # User aus Gruppe
```

### 5.3 Managing File Permissions and Ownership

**Berechtigungen verstehen:**
```
-rwxr-xr-- 1 user group 1234 Jan 1 12:00 file.txt
│└┬┘└┬┘└┬┘
│ │  │  └── Other (4+0+0 = 4)
│ │  └───── Group (4+1+0 = 5)  
│ └──────── User  (4+2+1 = 7)
└────────── Type (- = File, d = Directory, l = Link)

r = read    = 4
w = write   = 2
x = execute = 1
```

**chmod - Berechtigungen ändern:**
```bash
# Numerisch
chmod 755 file.sh    # rwxr-xr-x
chmod 644 file.txt   # rw-r--r--
chmod 600 private    # rw-------

# Symbolisch
chmod u+x file.sh    # User + execute
chmod g-w file.txt   # Group - write
chmod o=r file.txt   # Other = read only
chmod a+r file.txt   # All + read
chmod +x script.sh   # Alle + execute

# Rekursiv
chmod -R 755 verzeichnis/
```

**chown - Besitzer ändern:**
```bash
sudo chown user file.txt
sudo chown user:group file.txt
sudo chown :group file.txt      # Nur Gruppe
sudo chown -R user:group verz/  # Rekursiv
```

### 5.4 Special Directories and Files

**Spezielle Berechtigungen:**
```bash
# SUID (4) - Als Besitzer ausführen
chmod u+s executable
chmod 4755 executable
# Beispiel: /usr/bin/passwd

# SGID (2) - Als Gruppe ausführen / Vererbung
chmod g+s directory
chmod 2755 directory

# Sticky Bit (1) - Nur Besitzer kann löschen
chmod +t directory
chmod 1777 /tmp
```

**Links:**
```bash
# Hard Link (gleiche Inode)
ln file.txt hardlink.txt

# Symbolic Link (Verweis)
ln -s /pfad/zu/original symlink
ln -s ../file.txt link.txt  # Relativ
```

---

## Praktische Übungen

### Übung 1: Dateisystem-Navigation
```bash
# 1. Navigiere zu /usr/share/doc
cd /usr/share/doc

# 2. Liste alle Verzeichnisse die mit 'lib' beginnen
ls -d lib*

# 3. Finde die größte Datei
ls -lS | head -5

# 4. Gehe zurück zum Home-Verzeichnis
cd ~
```

### Übung 2: Textverarbeitung
```bash
# 1. Erstelle eine Datei mit Zahlen
seq 1 100 > numbers.txt

# 2. Zeige nur gerade Zahlen
grep "0$\|2$\|4$\|6$\|8$" numbers.txt

# 3. Zähle die Zeilen
wc -l numbers.txt

# 4. Sortiere rückwärts
sort -nr numbers.txt > reversed.txt
```

### Übung 3: Archivierung
```bash
# 1. Erstelle Test-Struktur
mkdir -p backup/{docs,images,config}
touch backup/docs/file{1..5}.txt

# 2. Archiviere mit Kompression
tar -czvf backup.tar.gz backup/

# 3. Liste Inhalt
tar -tzf backup.tar.gz

# 4. Extrahiere in neues Verzeichnis
mkdir restore
tar -xzvf backup.tar.gz -C restore/
```

### Übung 4: Berechtigungen
```bash
# 1. Erstelle Script
echo '#!/bin/bash' > script.sh
echo 'echo "Hallo von $USER"' >> script.sh

# 2. Mache ausführbar nur für Besitzer
chmod 700 script.sh

# 3. Erstelle Gruppe und teile
sudo groupadd developers
sudo usermod -aG developers $USER
sudo chown $USER:developers script.sh
chmod 750 script.sh
```

---

## Prüfungstipps

### Zeitmanagement
- 60 Minuten für 40 Fragen = 1,5 Minuten pro Frage
- Schwierige Fragen markieren und später bearbeiten
- Letzte 5 Minuten für Review nutzen

### Häufige Fallen
1. **Pfade:** Relative vs. Absolute unterscheiden
2. **Permissions:** Numerisch und symbolisch kennen
3. **Wildcards:** `*` vs `?` vs `[...]`
4. **Pipes:** Reihenfolge beachten
5. **Case-Sensitivity:** Linux unterscheidet Groß/Klein

### Lernstrategie
1. **Hands-On:** Alle Befehle selbst ausprobieren
2. **Man Pages:** `man` Befehl regelmäßig nutzen
3. **Notizen:** Eigene Befehlsreferenz erstellen
4. **Übung:** Täglich 30 Minuten CLI nutzen
5. **Mock Exams:** Online-Übungsprüfungen

### Wichtigste Befehle für die Prüfung
```bash
# Must-Know Befehle
ls, cd, pwd, mkdir, rm, cp, mv
cat, less, head, tail, grep, sort
tar, gzip, bzip2
chmod, chown, useradd, passwd
ps, kill, df, free, ping
man, which, type, help
```

### Merkhilfen
- **Permissions:** 4(r) + 2(w) + 1(x) = 7(rwx)
- **tar:** **C**reate, e**X**tract, **T**est, **F**ile
- **ps aux:** **A**ll **U**ser e**X**tended
- **grep:** **G**lobal **R**egular **E**xpression **P**rint

---

## Zusätzliche Ressourcen

### Online-Übungen
- [Linux Journey](https://linuxjourney.com/)
- [Linux Survival](https://linuxsurvival.com/)
- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)

### Dokumentation
- [Man Pages Online](https://man7.org/linux/man-pages/)
- [GNU Coreutils](https://www.gnu.org/software/coreutils/manual/)
- [TLDP Guides](https://tldp.org/guides.html)

### Prüfungssimulation
- Erstellen Sie eigene Flashcards
- Üben Sie mit Zeitlimit
- Erklären Sie Konzepte anderen
- Dokumentieren Sie Ihre Fehler

## Checkliste vor der Prüfung

- [ ] Alle Topics durchgearbeitet
- [ ] Praktische Übungen absolviert
- [ ] Mock Exam bestanden
- [ ] Befehlsreferenz erstellt
- [ ] Schwache Themen wiederholt
- [ ] Prüfungsanmeldung bestätigt
- [ ] Ausreichend Schlaf vor Prüfung

Viel Erfolg bei Ihrer Linux Essentials Prüfung!