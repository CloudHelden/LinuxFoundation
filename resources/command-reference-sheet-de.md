# Linux Befehls-Referenz

## 🎯 Kurzreferenz-Format
Jeder Befehl zeigt: `befehl [optionen] <erforderlich> [optional]`

---

## 📁 Navigationsbefehle

### pwd - Print Working Directory
```bash
pwd                     # Aktuelles Verzeichnis anzeigen
```
**Merkhilfe**: "Wo bin ich?"

### cd - Change Directory
```bash
cd                      # Nach Hause gehen
cd ~                    # Nach Hause gehen (explizit)
cd /pfad/zum/verz      # Zu spezifischem Pfad gehen
cd ..                   # Eine Ebene nach oben
cd ../..               # Zwei Ebenen nach oben
cd -                    # Zum vorherigen Verzeichnis gehen
```
**Merkhilfe**: "cd" = "change directory" (Verzeichnis wechseln)

### ls - List
```bash
ls                      # Dateien auflisten
ls -l                   # Langes Format (Details)
ls -a                   # Alle Dateien (inkl. versteckte)
ls -la                  # Optionen kombinieren
ls -lh                  # Menschenlesbare Größen
ls -lt                  # Nach Zeit sortieren
ls /pfad/zum/verz      # Spezifisches Verzeichnis auflisten
```
**Merkhilfe**: "ls" = "list" (auflisten)

---

## 📝 Dateioperationen

### touch - Datei erstellen/aktualisieren
```bash
touch dateiname         # Leere Datei erstellen
touch datei1 datei2    # Mehrere Dateien erstellen
```
**Merkhilfe**: "Berühren zum Erstellen"

### cp - Copy
```bash
cp quelle ziel         # Datei kopieren
cp -r quelle ziel      # Verzeichnis kopieren (rekursiv)
cp -i quelle ziel      # Interaktiv (vor Überschreiben fragen)
```
**Merkhilfe**: "cp" = "copy" (kopieren)

### mv - Move/Rename
```bash
mv alterName neuerName # Datei umbenennen
mv datei /pfad/zu/     # Datei verschieben
mv -i quelle ziel      # Interaktiver Modus
```
**Merkhilfe**: "mv" = "move" (verschieben)

### rm - Remove
```bash
rm dateiname           # Datei löschen
rm -i dateiname        # Vor Löschen bestätigen
rm -r verzeichnis      # Verzeichnis löschen
rm -rf verzeichnis     # Zwangsweise löschen (GEFÄHRLICH!)
```
**Merkhilfe**: "rm" = "remove" (entfernen - KEIN RÜCKGÄNGIG!)

### mkdir - Make Directory
```bash
mkdir verzeichnisname  # Verzeichnis erstellen
mkdir -p pfad/zu/verz  # Übergeordnete Verzeichnisse auch erstellen
```
**Merkhilfe**: "mkdir" = "make directory" (Verzeichnis erstellen)

---

## 👀 Dateien anzeigen

### cat - Concatenate/Display
```bash
cat dateiname          # Ganze Datei anzeigen
cat datei1 datei2     # Mehrere Dateien anzeigen
```
**Merkhilfe**: "Cat zeigt alles"

### less - Durch Datei blättern
```bash
less dateiname         # Mit Seitenwechsel anzeigen
# In less:
# Leertaste = nächste Seite
# b = vorherige Seite
# / = suchen
# q = beenden
```
**Merkhilfe**: "Less ist mehr (kontrolliert)"

### head - Anfang zeigen
```bash
head dateiname         # Erste 10 Zeilen
head -n 20 dateiname  # Erste 20 Zeilen
```
**Merkhilfe**: "Head = Kopf/Anfang"

### tail - Ende zeigen
```bash
tail dateiname         # Letzte 10 Zeilen
tail -n 20 dateiname  # Letzte 20 Zeilen
tail -f dateiname     # Datei verfolgen/beobachten
```
**Merkhilfe**: "Tail = Schwanz/Ende"

---

## 🔍 Suchen

### grep - In Dateien suchen
```bash
grep "text" dateiname  # Text in Datei finden
grep -i "text" datei  # Groß-/Kleinschreibung ignorieren
grep -n "text" datei  # Zeilennummern anzeigen
grep -r "text" verz/  # In Verzeichnis suchen
```
**Merkhilfe**: "Grep greift Muster"

### find - Dateien finden
```bash
find . -name "*.txt"   # Nach Name finden
find / -type f         # Nur Dateien finden
find / -type d         # Nur Verzeichnisse finden
find . -size +1M       # Dateien größer als 1MB finden
```
**Merkhilfe**: "Find findet Dateien"

---

## ℹ️ Hilfe bekommen

### man - Manual-Seiten
```bash
man befehl             # Handbuch für Befehl anzeigen
man -k stichwort      # Handbücher durchsuchen
```
**Navigation**: Leertaste=vorwärts, b=zurück, q=beenden

### help - Eingebaute Hilfe
```bash
befehl --help          # Schnelle Hilfe
help befehl           # Für Shell-Builtins
```

### which - Befehlsort finden
```bash
which befehl           # Pfad zum Befehl anzeigen
```

### type - Befehlstyp anzeigen
```bash
type befehl            # Zeigen was Befehl ist
```

---

## 🚀 Produktivitäts-Shortcuts

### History
```bash
history                # Befehlsverlauf anzeigen
!!                    # Letzten Befehl ausführen
!n                    # Befehl Nummer n ausführen
!text                 # Letzten Befehl mit 'text' ausführen
```

### Tab-Vervollständigung
```bash
bef[TAB]              # Befehl vervollständigen
/ho[TAB]/us[TAB]     # Pfad vervollständigen
```

### Wildcards
```bash
*                     # Beliebige Zeichen
?                     # Einzelnes Zeichen
[abc]                 # a, b oder c
[0-9]                 # Beliebige Ziffer
```

---

## ⚡ Wesentliche Kombinationen

### Pipes und Umleitung
```bash
befehl1 | befehl2     # Ausgabe an nächsten Befehl weiterleiten
befehl > datei        # Ausgabe in Datei umleiten
befehl >> datei       # Ausgabe an Datei anhängen
befehl < datei        # Eingabe aus Datei lesen
befehl 2> error.log   # Fehler umleiten
```

### Häufige Kombinationen
```bash
ls -la | grep ".txt"   # Nur txt-Dateien auflisten
ps aux | grep prozess  # Laufenden Prozess finden
history | grep cd      # cd-Befehle finden
cat datei | less       # Durch Datei blättern
```

---

## 🔧 System-Informationen

### System-Info
```bash
uname -a               # System-Informationen
hostname              # Hostname anzeigen
whoami                # Aktueller Benutzername
id                    # Benutzer- und Gruppen-IDs
date                  # Aktuelles Datum/Zeit
uptime                # System-Betriebszeit
```

### Speicher und Memory
```bash
df -h                 # Freier Speicherplatz
du -h                 # Speicherverbrauch
free -h               # Speicher-Nutzung
```

### Prozess-Befehle
```bash
ps                    # Ihre Prozesse
ps aux                # Alle Prozesse
top                   # Interaktiver Prozess-Viewer
kill PID              # Prozess stoppen
```

---

## 💡 Profi-Tipps für Anfänger

### Sicherheit zuerst
1. **Immer `ls` vor `rm` verwenden**
2. **`-i` Flag für interaktive Bestätigung verwenden**
3. **Backups vor großen Änderungen erstellen**
4. **Fehlermeldungen sorgfältig lesen**

### Lernpfad
1. **Zuerst Navigation meistern** (cd, ls, pwd)
2. **Dann Dateioperationen** (cp, mv, rm)
3. **Dann Anzeigen** (cat, less, head, tail)
4. **Schließlich Suchen** (grep, find)

### Gedächtnisstützen
- **pwd** = "print working directory" = "wo?"
- **cd** = "change directory" = "gehe zu"
- **ls** = "list" = "zeig mir"
- **cp** = "copy" = "duplizieren"
- **mv** = "move" = "verschieben/umbenennen"
- **rm** = "remove" = "für immer löschen!"

### Übungsbefehle
```bash
# Sicherer Übungsbereich
mkdir ~/playground
cd ~/playground
# Hier üben!
```

---

## 📋 Befehls-Checkliste

### Woche 1 Wesentliches
- [ ] pwd - Wissen wo Sie sind
- [ ] ls - Sehen was da ist
- [ ] cd - Sich bewegen
- [ ] mkdir - Verzeichnisse erstellen
- [ ] touch - Dateien erstellen
- [ ] cp - Zeug kopieren
- [ ] mv - Zeug verschieben/umbenennen
- [ ] rm - Löschen (vorsichtig!)
- [ ] cat - Dateien anzeigen
- [ ] man - Hilfe bekommen

### Woche 2 Ziele
- [ ] grep - In Dateien suchen
- [ ] find - Dateien finden
- [ ] less - Große Dateien anzeigen
- [ ] head/tail - Teile anzeigen
- [ ] | - Pipes verwenden
- [ ] > - Ausgabe umleiten

---

**Drucken Sie dieses Blatt aus und behalten Sie es während der Übungen griffbereit!**