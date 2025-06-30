# Woche 1: Navigation-Grundlagen Übungen

## Übungsset-Übersicht
**Zeit**: 60 Minuten  
**Schwierigkeit**: Duale Spur  
**Voraussetzungen**: Tag 1-2 Lektionen abgeschlossen

---

## 🟢 Spur A: Grundlagen-Übungen

### Übung A1: Verzeichnis-Explorer (20 Min.)
**Ziel**: Grundlegende Navigationsbefehle meistern

#### Teil 1: Wo bin ich?
```bash
# 1. Ihren aktuellen Standort prüfen
pwd

# 2. Was sehen Sie in der Ausgabe?
# Schreiben Sie Ihre Antwort: ________________

# 3. Zu Ihrem Home-Verzeichnis gehen (3 verschiedene Wege)
cd
cd ~
cd $HOME

# 4. Überprüfen, dass Sie zu Hause sind
pwd
```

#### Teil 2: Sich bewegen
```bash
# 1. Zum Root-Verzeichnis gehen
cd /

# 2. Auflisten was da ist
ls

# 3. Zum /etc Verzeichnis gehen
cd etc

# 4. Zum vorherigen Verzeichnis zurück
cd -

# 5. Eine Ebene nach oben gehen
cd ..
```

#### Teil 3: Ihren Arbeitsbereich erstellen
```bash
# 1. Nach Hause gehen
cd

# 2. Eine Verzeichnisstruktur erstellen:
mkdir linux101
cd linux101
mkdir exercises
mkdir projects
mkdir notes

# 3. Ihre Struktur überprüfen
ls
tree  # Falls tree installiert ist
```

**Erfolgs-Checkliste:**
- [ ] Kann pwd ohne nachzudenken verwenden
- [ ] Verstehe Unterschied zwischen / und ~
- [ ] Kann in Verzeichnissen hoch und runter navigieren
- [ ] Organisierten Arbeitsbereich erstellt

### Übung A2: Dateien auflisten (20 Min.)
**Ziel**: ls-Optionen verstehen

#### Geführte Entdeckung:
```bash
# 1. Grundlegende Auflistung
cd /etc
ls

# 2. Detaillierte Auflistung
ls -l
# Frage: Was bedeuten die Spalten?

# 3. Versteckte Dateien zeigen
cd ~
ls -a
# Frage: Welche Dateien beginnen mit Punkt?

# 4. Menschenlesbare Größen
ls -lh
# Frage: Was hat sich geändert?

# 5. Nach Zeit sortieren
ls -lt
# Frage: Welche Datei ist die neueste?
```

#### Praxis-Aufgaben:
1. Die größte Datei in /var/log finden
2. Nur Verzeichnisse in /etc auflisten
3. Versteckte Dateien in Ihrem Home zeigen
4. Dateien in /bin zählen

**Hinweise-Box:**
```
Denken Sie daran:
- Versteckte Dateien beginnen mit .
- ls -la kombiniert Optionen
- Verwenden Sie man ls für Hilfe
```

### Übung A3: Hilfe bekommen (20 Min.)
**Ziel**: Lernen, Informationen zu finden

#### Hilfe-Methoden:
```bash
# Methode 1: Manual-Seiten
man ls
# Navigation: Leertaste=nächste, q=beenden

# Methode 2: Hilfe-Flag
ls --help

# Methode 3: Befehls-Info
info ls

# Methode 4: Which und Type
which ls
type ls
```

#### Schnitzeljagd:
Mit Hilfe herausfinden:
1. Wie man Dateien in umgekehrter Reihenfolge auflistet
2. Wie man Dateigrößen in Bytes zeigt
3. Was ls -R macht
4. Wie man nur Verzeichnisse auflistet

**Antwort-Vorlage:**
```
1. Umgekehrte Reihenfolge: ls _____
2. Größe in Bytes: ls _____
3. ls -R macht: ___________
4. Nur Verzeichnisse: _____
```

---

## 🔵 Spur B: Beschleunigte Übungen

### Übung B1: Fortgeschrittene Navigation (20 Min.)
**Ziel**: Effiziente Dateisystem-Navigation

#### Geschwindigkeits-Herausforderung:
```bash
# Setup (zuerst ausführen):
mkdir -p ~/maze/{level1/{room1,room2},level2/{room3,room4}}
touch ~/maze/level1/room1/{key1,door1}
touch ~/maze/level2/room3/{treasure,trap}

# Jetzt navigieren und Aufgaben erledigen:
# 1. Alle Dateien mit 'key' finden (ein Befehl)
# 2. Nur Verzeichnisse auflisten (keine Dateien)
# 3. Vollständigen Pfad aller 'treasure' Dateien zeigen
# 4. Gesamtanzahl der Dateien im Labyrinth zählen
```

#### Power-Navigation:
```bash
# Diese fortgeschrittenen Techniken verwenden:
# 1. Zum vorherigen Verzeichnis springen
cd -

# 2. CDPATH verwenden
export CDPATH=.:~:/etc:/var
cd log  # Geht zu /var/log

# 3. Schnelle Substitution
cd /var/log
cd log tmp  # Wechselt zu /var/tmp

# 4. Verzeichnisse stapeln
pushd /etc
pushd /var
popd
```

### Übung B2: Befehls-Kombinationen (20 Min.)
**Ziel**: Befehle effektiv verketten

#### Pipeline-Praxis:
```bash
# 1. 10 größte Dateien in /usr finden
ls -la /usr/bin | sort -k5 -n -r | head -10

# 2. Eindeutige Dateierweiterungen in /etc zählen
ls /etc | grep '\.' | sed 's/.*\.//' | sort | uniq -c

# 3. Kürzlich geänderte Configs finden
find /etc -name "*.conf" -mtime -7 2>/dev/null

# 4. Verzeichnis-Bericht erstellen
echo "=== System-Verzeichnisse ===" > ~/report.txt
ls -ld /etc /var /usr >> ~/report.txt
```

#### Herausforderungs-Aufgaben:
1. One-Liner schreiben, um alle PDF-Dateien im Home zu finden
2. Top 5 speicherverbrauchende Verzeichnisse auflisten
3. Alle in der letzten Stunde geänderten Dateien finden
4. Verzeichnisbaum-Visualisierung erstellen

### Übung B3: Effizienz-Tools (20 Min.)
**Ziel**: Schneller arbeiten mit Shortcuts

#### Ihre Umgebung einrichten:
```bash
# 1. Nützliche Aliase erstellen
echo "alias ll='ls -la'" >> ~/.bashrc
echo "alias ..='cd ..'" >> ~/.bashrc
echo "alias ...='cd ../..'" >> ~/.bashrc
source ~/.bashrc

# 2. History-Shortcuts
history | tail -20
!ls  # Letzten ls-Befehl ausführen
!!   # Letzten Befehl ausführen
!$   # Letztes Argument verwenden

# 3. Tab-Vervollständigung meistern
cd /u[TAB]/lo[TAB]/sh[TAB]

# 4. Glob-Muster
ls *.conf
ls [a-c]*
ls {*.txt,*.log}
```

#### Produktivitäts-Herausforderung:
Erstellen Sie einen Befehl, der:
1. Alle Log-Dateien findet
2. Nur heutige Dateien zeigt
3. Größe und Pfad anzeigt
4. Ergebnis im Bericht speichert

**Bonus**: Machen Sie es zu einem Alias!

---

## 📊 Bewertungs-Rubrik

### Spur A Erfolgskriterien:
- 3 Übungen komplett: **Bestanden**
- Hilfe effektiv verwenden: **+Bonus**
- Keine Syntax-Fehler: **Gut**
- Erklärt was Befehle machen: **Ausgezeichnet**

### Spur B Erfolgskriterien:
- Kern + 2 Herausforderungen komplett: **Bestanden**
- Effiziente Lösungen: **Gut**
- Kreative Ansätze: **Ausgezeichnet**
- Hilft Spur A Student: **+Bonus**

## 🤝 Pair-Programming Option

### Gemischte Paare (A+B):
- B-Student führt ohne zu übernehmen
- A-Student tippt alle Befehle
- Beide erklären was passiert
- Rollen alle 10 Minuten wechseln

### Gleiche Spur Paare:
- Abwechselnd "Fahrer" und "Navigator" sein
- Diskutieren vor dem Tippen
- Sich gegenseitig herausfordern
- Entdeckungen teilen

## 📝 Reflexions-Fragen

### Für alle:
1. Was war der nützlichste Befehl, den Sie gelernt haben?
2. Was hat Sie am meisten verwirrt?
3. Wie werden Sie sich diese Befehle merken?
4. Was möchten Sie mehr erkunden?

### Spur A Zusätzlich:
- Welche Hilfe-Methode bevorzugen Sie?
- Zeichnen Sie Ihre mentale Karte des Dateisystems

### Spur B Zusätzlich:
- Welcher Effizienz-Tipp spart die meiste Zeit?
- Entwerfen Sie eine komplexe Pipeline für eine echte Aufgabe

---

## 🏠 Hausaufgaben

### Spur A:
1. Navigation täglich 15 Min. üben
2. Jeden Tag ein neues Verzeichnis erkunden
3. Täglich `man` für einen neuen Befehl verwenden

### Spur B:
1. 5 nützliche Aliase erstellen
2. Skript schreiben um Downloads zu organisieren
3. `find` Befehl tiefgehend erkunden

## 💡 Tipps für den Erfolg

### Universelle Tipps:
- **Täglich üben**: Sogar 10 Minuten helfen
- **Fehler machen**: Sie sind Lernmöglichkeiten
- **Fragen stellen**: Keine Frage ist dumm
- **Notizen machen**: In Ihren eigenen Worten

### Spur-spezifisch:
- **Spur A**: Fokus auf Genauigkeit vor Geschwindigkeit
- **Spur B**: Sich selbst mit Einschränkungen herausfordern

---

**Denken Sie daran**: Das Ziel ist nicht, zuerst fertig zu werden, sondern tief zu verstehen!