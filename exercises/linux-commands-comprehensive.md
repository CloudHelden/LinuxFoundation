# Umfassende Linux-Befehle Übung

## Übersicht
Diese Übung deckt alle wichtigen Linux-Befehle ab, die im Linux Foundation Kurs behandelt werden. Die Übung ist in thematische Bereiche unterteilt und baut aufeinander auf.

## Vorbereitung
- Stellen Sie sicher, dass Sie Zugriff auf ein Ubuntu Linux System haben (VM oder WSL)
- Erstellen Sie ein Arbeitsverzeichnis: `mkdir ~/linux-übung && cd ~/linux-übung`

## Teil 1: Dateisystem Navigation

### Übung 1.1: Grundlegende Navigation
```bash
# 1. Wo befinden Sie sich gerade?
pwd

# 2. Listen Sie alle Dateien im aktuellen Verzeichnis auf
ls
ls -la
ls -lh

# 3. Navigieren Sie zum Home-Verzeichnis
cd ~
cd $HOME
cd

# 4. Navigieren Sie zum Root-Verzeichnis und erkunden Sie die Struktur
cd /
ls
cd /etc
pwd
cd /var/log
pwd

# 5. Verwenden Sie relative und absolute Pfade
cd ../..
cd ./etc
cd /home/$USER
```

### Übung 1.2: Verzeichnisstruktur erkunden
```bash
# 1. Zeigen Sie die Verzeichnisstruktur an
tree /etc -L 2
tree ~ -L 3

# 2. Finden Sie Ihr aktuelles Verzeichnis in der Hierarchie
pwd
cd ..
pwd
cd -  # Zurück zum vorherigen Verzeichnis
```

## Teil 2: Datei- und Verzeichnisverwaltung

### Übung 2.1: Erstellen und Löschen
```bash
# 1. Erstellen Sie eine Verzeichnisstruktur
mkdir -p projekt/src/main
mkdir -p projekt/docs/{user,admin}
mkdir -p projekt/tests/{unit,integration}

# 2. Erstellen Sie Dateien
touch projekt/README.md
touch projekt/src/main/{app.py,config.py,utils.py}
echo "# Mein Projekt" > projekt/README.md

# 3. Verzeichnisbaum anzeigen
tree projekt

# 4. Dateien und Verzeichnisse löschen
rm projekt/src/main/utils.py
rmdir projekt/tests/integration
rm -r projekt/tests  # Vorsicht: Löscht rekursiv!
```

### Übung 2.2: Kopieren und Verschieben
```bash
# 1. Dateien kopieren
cp projekt/README.md projekt/README.backup
cp -r projekt projekt_backup

# 2. Dateien verschieben/umbenennen
mv projekt/README.backup projekt/docs/README.old
mv projekt/src projekt/source

# 3. Mehrere Dateien gleichzeitig
cp projekt/source/main/*.py projekt/docs/

# 4. Mit Wildcards arbeiten
cp *.md backup/
mv *.backup /tmp/
```

## Teil 3: Dateiinhalte bearbeiten

### Übung 3.1: Dateien anzeigen
```bash
# 1. Verschiedene Methoden zum Anzeigen
cat /etc/passwd
less /etc/passwd  # Navigation mit Space, b, q
more /etc/passwd

# 2. Nur Teile anzeigen
head -n 5 /etc/passwd
tail -n 10 /etc/passwd
tail -f /var/log/syslog  # Live-Monitoring

# 3. Zeilennummern anzeigen
cat -n /etc/passwd
nl /etc/passwd
```

### Übung 3.2: Textbearbeitung
```bash
# 1. Mit nano arbeiten
nano testfile.txt
# Strg+O zum Speichern, Strg+X zum Beenden

# 2. Mit vi/vim arbeiten (Grundlagen)
vi testfile.txt
# i für Insert-Modus
# ESC zum Verlassen des Insert-Modus
# :wq zum Speichern und Beenden
# :q! zum Beenden ohne Speichern

# 3. Einfache Bearbeitungen mit echo
echo "Neue Zeile" >> testfile.txt
echo "Überschreiben" > testfile.txt
```

## Teil 4: Suchen und Finden

### Übung 4.1: Dateien finden
```bash
# 1. Nach Namen suchen
find ~ -name "*.txt"
find /etc -name "*.conf" 2>/dev/null
find . -iname "*readme*"  # Case-insensitive

# 2. Nach Typ suchen
find ~ -type f -name "*.sh"  # Nur Dateien
find ~ -type d -name "config" # Nur Verzeichnisse

# 3. Nach Größe suchen
find ~ -size +1M  # Größer als 1MB
find ~ -size -100k # Kleiner als 100KB

# 4. Nach Zeit suchen
find ~ -mtime -7  # Geändert in den letzten 7 Tagen
find ~ -mmin -60  # Geändert in den letzten 60 Minuten
```

### Übung 4.2: In Dateien suchen
```bash
# 1. Mit grep suchen
grep "root" /etc/passwd
grep -i "error" /var/log/syslog  # Case-insensitive
grep -r "TODO" ~/projekt/        # Rekursiv
grep -n "function" *.py          # Mit Zeilennummern

# 2. Erweiterte grep-Optionen
grep -v "^#" /etc/passwd  # Zeilen ohne # am Anfang
grep -c "error" logfile   # Nur Anzahl
grep -A 2 -B 2 "error" logfile  # Kontext anzeigen

# 3. Mit anderen Tools
which python3
whereis python3
locate "*.conf"  # Benötigt updatedb
```

## Teil 5: Prozessverwaltung

### Übung 5.1: Prozesse anzeigen
```bash
# 1. Laufende Prozesse anzeigen
ps
ps aux
ps -ef
pstree

# 2. Top und htop verwenden
top  # q zum Beenden
htop # Falls installiert

# 3. Spezifische Prozesse finden
ps aux | grep firefox
pgrep firefox
pidof firefox
```

### Übung 5.2: Prozesse verwalten
```bash
# 1. Prozesse im Hintergrund
sleep 100 &
jobs
fg %1
bg %1

# 2. Prozesse beenden
kill <PID>
kill -9 <PID>  # Erzwingen
killall firefox
pkill -f "python.*test"

# 3. Prozess-Prioritäten
nice -n 10 cp großedatei.iso /backup/
renice -n 5 -p <PID>
```

## Teil 6: Berechtigungen und Benutzer

### Übung 6.1: Dateiberechtigungen
```bash
# 1. Berechtigungen anzeigen
ls -l
stat datei.txt

# 2. Berechtigungen ändern
chmod 755 script.sh
chmod u+x script.sh
chmod go-w datei.txt
chmod -R 644 ~/dokumente/

# 3. Besitzer ändern
sudo chown $USER:$USER datei.txt
sudo chown -R www-data:www-data /var/www/

# 4. Spezielle Berechtigungen
chmod +t /tmp/shared/  # Sticky bit
chmod u+s executable   # SUID
```

### Übung 6.2: Benutzerverwaltung
```bash
# 1. Benutzerinformationen
whoami
id
groups
who
w

# 2. Zu anderem Benutzer wechseln
su - username
sudo -u username command

# 3. Benutzer verwalten (mit sudo)
sudo useradd -m -s /bin/bash testuser
sudo passwd testuser
sudo usermod -aG sudo testuser
sudo deluser testuser
```

## Teil 7: Netzwerk und System

### Übung 7.1: Netzwerkbefehle
```bash
# 1. Netzwerkkonfiguration anzeigen
ip addr show
ip a
ifconfig  # Falls vorhanden
hostname
hostname -I

# 2. Netzwerkverbindungen testen
ping -c 4 google.com
ping6 -c 4 google.com
traceroute google.com
nslookup google.com
dig google.com

# 3. Ports und Verbindungen
netstat -tlnp
ss -tlnp
lsof -i :80
```

### Übung 7.2: Systeminformationen
```bash
# 1. Systeminfos abrufen
uname -a
lsb_release -a
cat /etc/os-release
uptime
free -h
df -h
du -sh ~

# 2. Hardware-Informationen
lscpu
lsmem
lsblk
lsusb
lspci

# 3. Kernel und Module
lsmod
modinfo <modulname>
dmesg | less
journalctl -xe
```

## Teil 8: Paketverwaltung (Ubuntu/Debian)

### Übung 8.1: APT verwenden
```bash
# 1. Paketlisten aktualisieren
sudo apt update

# 2. Pakete suchen und Info anzeigen
apt search nginx
apt show nginx
apt list --installed

# 3. Pakete installieren und entfernen
sudo apt install htop
sudo apt remove htop
sudo apt purge htop
sudo apt autoremove

# 4. System aktualisieren
sudo apt upgrade
sudo apt full-upgrade
```

### Übung 8.2: Andere Paketmanager
```bash
# 1. Snap-Pakete
snap list
snap find firefox
sudo snap install firefox
sudo snap remove firefox

# 2. Mit dpkg arbeiten
dpkg -l
dpkg -L paketname
sudo dpkg -i paket.deb
```

## Teil 9: Textverarbeitung und Filter

### Übung 9.1: Pipes und Redirection
```bash
# 1. Ausgabe umleiten
ls -la > dateilieste.txt
echo "Anhängen" >> dateiliste.txt
find / -name "*.conf" 2> fehler.log
command 2>&1 > alles.log

# 2. Pipes verwenden
ps aux | grep python
ls -la | grep "^d" | wc -l
cat /etc/passwd | cut -d: -f1 | sort
```

### Übung 9.2: Textverarbeitungs-Tools
```bash
# 1. Mit cut arbeiten
cut -d: -f1,3 /etc/passwd
cut -c1-10 datei.txt

# 2. Mit sort und uniq
sort datei.txt
sort -n zahlen.txt
sort -r datei.txt | uniq

# 3. Mit awk arbeiten
awk '{print $1}' datei.txt
awk -F: '{print $1, $3}' /etc/passwd
ps aux | awk '{sum+=$3} END {print sum}'

# 4. Mit sed arbeiten
sed 's/alt/neu/g' datei.txt
sed -i 's/alt/neu/g' datei.txt
sed -n '5,10p' datei.txt
```

## Teil 10: Archivierung und Kompression

### Übung 10.1: Archive erstellen
```bash
# 1. Mit tar arbeiten
tar -cvf archiv.tar verzeichnis/
tar -czvf archiv.tar.gz verzeichnis/
tar -cjvf archiv.tar.bz2 verzeichnis/

# 2. Archive entpacken
tar -xvf archiv.tar
tar -xzvf archiv.tar.gz -C /zielverzeichnis/
tar -tf archiv.tar  # Inhalt anzeigen

# 3. Mit zip arbeiten
zip -r archiv.zip verzeichnis/
unzip archiv.zip
unzip -l archiv.zip  # Inhalt anzeigen
```

## Abschlussübung: Skript erstellen

Erstellen Sie ein Bash-Skript, das mehrere der gelernten Befehle kombiniert:

```bash
#!/bin/bash
# backup.sh - Einfaches Backup-Skript

# Variablen
BACKUP_DIR="/home/$USER/backups"
SOURCE_DIR="/home/$USER/dokumente"
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_FILE="backup_$DATE.tar.gz"

# Backup-Verzeichnis erstellen
mkdir -p $BACKUP_DIR

# Backup erstellen
echo "Erstelle Backup von $SOURCE_DIR..."
tar -czf $BACKUP_DIR/$BACKUP_FILE $SOURCE_DIR 2>/dev/null

# Alte Backups löschen (älter als 7 Tage)
find $BACKUP_DIR -name "backup_*.tar.gz" -mtime +7 -delete

# Status ausgeben
if [ $? -eq 0 ]; then
    echo "Backup erfolgreich erstellt: $BACKUP_FILE"
    ls -lh $BACKUP_DIR/$BACKUP_FILE
else
    echo "Fehler beim Erstellen des Backups!"
    exit 1
fi
```

## Tipps und Best Practices

1. **Manual Pages nutzen**: `man befehl` für Dokumentation
2. **Tab-Completion**: Tab-Taste für Autovervollständigung
3. **History nutzen**: `history`, Pfeiltasten, Strg+R
4. **Aliase erstellen**: `alias ll='ls -la'`
5. **Vorsicht mit rm**: Immer zweimal prüfen!
6. **sudo verstehen**: Nur wenn nötig verwenden
7. **Pipes kombinieren**: Mächtige Werkzeugketten erstellen

## Weiterführende Übungen

1. Erstellen Sie ein Monitoring-Skript für Systemressourcen
2. Automatisieren Sie tägliche Aufgaben mit cron
3. Schreiben Sie ein Log-Analyse-Skript
4. Erstellen Sie eine Benutzer-Management-Lösung
5. Entwickeln Sie ein Netzwerk-Diagnose-Tool