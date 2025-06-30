# Interaktives Labor: Linux-Berechtigungen

## 🎯 Labor-Übersicht
**Dauer**: 90 Minuten  
**Typ**: Praktische Übung  
**Schwierigkeitsgrad**: Progressiv (Einfach → Schwer)  
**Ziel**: Linux-Berechtigungen durch praktische Szenarien meistern

---

## 🏗️ Labor-Setup-Skript

Führen Sie dies zuerst aus, um Ihre Laborumgebung zu erstellen:

```bash
#!/bin/bash
# Speichern als: setup-permissions-lab.sh
# Ausführen mit: bash setup-permissions-lab.sh

echo "🔧 Einrichten der Berechtigungs-Laborumgebung..."

# Labor-Verzeichnis erstellen
mkdir -p ~/permissions-lab/{company,projects,shared,personal}
cd ~/permissions-lab

# Benutzersimulation erstellen (verschiedene Gruppen verwenden)
echo "📁 Verzeichnisstruktur erstellen..."

# Firmenverzeichnisse
mkdir -p company/{hr,finance,it,public}
mkdir -p projects/{alpha,beta,gamma}
mkdir -p shared/{documents,tools,reports}

# Beispieldateien erstellen
echo "📄 Beispieldateien erstellen..."
echo "Mitarbeiterhandbuch" > company/public/handbook.txt
echo "Gehaltsdaten - VERTRAULICH" > company/hr/salaries.txt
echo "Budget 2024 - EINGESCHRÄNKT" > company/finance/budget.txt
echo "Server-Passwörter - NUR IT" > company/it/passwords.txt

echo "Projekt Alpha Spezifikationen" > projects/alpha/specs.txt
echo "Projekt Beta Code" > projects/beta/code.sh
echo "Projekt Gamma Daten" > projects/gamma/data.csv

echo "Besprechungsnotizen" > shared/documents/notes.txt
echo "#!/bin/bash\necho 'Backup-Tool'" > shared/tools/backup.sh
echo "Q4 Bericht" > shared/reports/q4-report.txt

# Test-Skript erstellen
cat > shared/tools/system-info.sh << 'EOF'
#!/bin/bash
echo "=== System-Informations-Tool ==="
echo "Benutzer: $(whoami)"
echo "Gruppen: $(groups)"
echo "Datum: $(date)"
echo "Betriebszeit: $(uptime -p)"
EOF

echo "✅ Laborumgebung erstellt in ~/permissions-lab/"
echo "📋 Bereit für die Übungen!"
```

---

## 📚 Teil 1: Berechtigungen verstehen (30 Min.)

### Übung 1.1: Berechtigungs-Grundlagen

```bash
cd ~/permissions-lab

# Berechtigungen untersuchen
ls -la company/public/
```

#### 🤔 Fragen:
1. Was bedeutet `-rw-rw-r--`?
2. Wer kann handbook.txt lesen?
3. Wer kann sie ändern?

<details>
<summary>📖 Kurzreferenz</summary>

```
Berechtigungsformat: -rwxrwxrwx
                     │├─┼─┼─┤
                     ││ │ │ └── Andere (alle anderen)
                     ││ │ └──── Gruppe
                     ││ └────── Benutzer (Besitzer)
                     │└──────── Dateityp (- = Datei, d = Verzeichnis)
                     │
Berechtigungen: r = lesen (4), w = schreiben (2), x = ausführen (1)
```

</details>

### Übung 1.2: Numerische Notation

Berechnen Sie die Berechtigungen für diese Szenarien:

```bash
# Welcher numerische Wert ergibt:
# Besitzer: lesen, schreiben, ausführen
# Gruppe: lesen, ausführen
# Andere: nur lesen

# Probieren Sie es aus:
touch test-file.txt
chmod ??? test-file.txt  # Ersetzen Sie ??? mit Ihrer Antwort
ls -l test-file.txt
```

<details>
<summary>💡 Antwort</summary>

```bash
chmod 754 test-file.txt
# 7 = rwx (4+2+1) für Besitzer
# 5 = r-x (4+0+1) für Gruppe  
# 4 = r-- (4+0+0) für Andere
```

</details>

### Übung 1.3: Das Berechtigungsspiel

```bash
# Erstellen Sie eine Datei mit bestimmten Berechtigungen
touch game.txt
chmod 640 game.txt

# Erreichen Sie diese Berechtigungen mit symbolischer Notation:
# -rw-r----- 
chmod u=??,g=?,o=? game.txt  # Füllen Sie die Lücken aus
```

---

## 🔐 Teil 2: Praktische Szenarien (30 Min.)

### Szenario 2.1: Die Passwortdatei sichern

```bash
# Die IT-Passwortdatei ist derzeit für alle lesbar!
ls -l company/it/passwords.txt

# Ihre Aufgabe: Machen Sie sie nur für den Besitzer lesbar
# Versuchen Sie es zuerst selbst!
```

<details>
<summary>🔑 Lösung</summary>

```bash
chmod 600 company/it/passwords.txt
# ODER
chmod u=rw,g=,o= company/it/passwords.txt

# Überprüfen:
ls -l company/it/passwords.txt
# Sollte zeigen: -rw-------
```

</details>

### Szenario 2.2: Gemeinsame Projektzusammenarbeit

```bash
# Das Projekt-Alpha-Team muss zusammenarbeiten
# Anforderungen:
# - Teammitglieder können specs.txt lesen und schreiben
# - Andere können nur lesen
# - Erstellen Sie ein gemeinsames Verzeichnis, in dem das Team Dateien hinzufügen kann

# Beginnen Sie hier:
cd projects/alpha
```

<details>
<summary>🔑 Lösung</summary>

```bash
# Dateiberechtigungen setzen
chmod 664 specs.txt

# Für echte Zusammenarbeit (wenn Sie Gruppen hätten):
# chmod 664 specs.txt
# chgrp project-alpha specs.txt

# Gemeinsamen Arbeitsbereich erstellen
mkdir shared-workspace
chmod 775 shared-workspace
# Dies ermöglicht Gruppenmitgliedern, Dateien zu erstellen
```

</details>

### Szenario 2.3: Das ausführbare Skript

```bash
cd ~/permissions-lab/shared/tools

# Machen Sie das Backup-Skript nur für Besitzer und Gruppe ausführbar
ls -l backup.sh

# Test vorher:
./backup.sh  # Sollte fehlschlagen

# Berechtigungen korrigieren:
# Ihre Lösung hier...

# Test nachher:
./backup.sh  # Sollte funktionieren
```

<details>
<summary>🔑 Lösung</summary>

```bash
chmod 750 backup.sh
# ODER
chmod u=rwx,g=rx,o= backup.sh

# Überprüfen, ob es funktioniert:
./backup.sh
```

</details>

---

## 🎮 Teil 3: Interaktive Herausforderungen (30 Min.)

### Herausforderung 3.1: Berechtigungs-Rätsel

```bash
# Führen Sie dieses Setup aus:
mkdir -p puzzle/{box1,box2,box3}
echo "Schatz!" > puzzle/box2/gold.txt
chmod 711 puzzle
chmod 700 puzzle/box1
chmod 711 puzzle/box2  
chmod 755 puzzle/box3
chmod 644 puzzle/box2/gold.txt

# Herausforderung: Ohne root oder sudo zu sein:
# 1. Können Sie den Inhalt von puzzle/ auflisten?
# 2. Können Sie gold.txt lesen?
# 3. Können Sie ls in box2 ausführen?
# 4. Warum erzeugen diese Berechtigungen dieses Verhalten?
```

<details>
<summary>🧩 Lösung & Erklärung</summary>

```bash
# 1. puzzle/ auflisten
ls puzzle/  # Funktioniert! Verzeichnis hat Ausführen (1) = kann durchquert werden

# 2. gold.txt lesen
cat puzzle/box2/gold.txt  # Funktioniert! Sie können hindurchgehen

# 3. box2 auflisten
ls puzzle/box2/  # Schlägt fehl! Keine Leseberechtigung für Verzeichnis

# Erklärung:
# - Ausführen bei Verzeichnis = kann hindurchgehen
# - Lesen bei Verzeichnis = kann Inhalt auflisten
# - Verzeichnis 711 = kann zugreifen, wenn Sie den Dateinamen kennen!
```

</details>

### Herausforderung 3.2: Der eingeschränkte Bericht

```bash
# Setup
echo "Vertraulicher Bericht v2" > shared/reports/confidential.txt
chmod 640 shared/reports/confidential.txt

# Herausforderung: Setzen Sie Berechtigungen so, dass:
# 1. Sie lesen/schreiben können
# 2. Ihre Gruppe nur lesen kann  
# 3. Andere überhaupt nicht zugreifen können
# 4. Aber erstellen Sie eine "öffentliche Zusammenfassung", die jeder lesen kann
```

<details>
<summary>🔐 Lösung</summary>

```bash
# Bereits korrekt für confidential.txt (640)

# Öffentliche Zusammenfassung erstellen
echo "Berichtszusammenfassung: Alles gut" > shared/reports/summary.txt
chmod 644 shared/reports/summary.txt

# Überprüfen
ls -la shared/reports/
```

</details>

### Herausforderung 3.3: Das Ausführungs-Mysterium

```bash
# Erstellen Sie dieses Testszenario:
cd ~/permissions-lab
cat > test-exec.sh << 'EOF'
#!/bin/bash
echo "Skript ausgeführt von: $(whoami)"
echo "Aktuelle Berechtigungen: $(ls -l $0)"
EOF

# Ungewöhnliche Berechtigungen setzen:
chmod 111 test-exec.sh

# Fragen:
# 1. Können Sie das Skript lesen?
# 2. Können Sie es ausführen?
# 3. Können Sie es bearbeiten?
```

<details>
<summary>🎭 Antwort</summary>

```bash
# 1. Lesen?
cat test-exec.sh  # NEIN! Keine Leseberechtigung

# 2. Ausführen?
./test-exec.sh  # JA! Ausführungsberechtigung vorhanden

# 3. Bearbeiten?
echo "neue Zeile" >> test-exec.sh  # NEIN! Keine Schreibberechtigung

# Dies zeigt, dass die Ausführungsberechtigung unabhängig funktioniert!
```

</details>

---

## 🏆 Teil 4: Fortgeschrittenes interaktives Labor (30 Min.)

### Labor 4.1: Eine sichere Verzeichnisstruktur erstellen

```bash
# Ihre Mission: Erstellen Sie ein Mini-Firmenverzeichnissystem
# Anforderungen:
# - Öffentlicher Ordner: Alle können lesen, nur Sie können schreiben
# - Privater Ordner: Nur Sie können zugreifen
# - Team-Ordner: Sie und Gruppe können lesen/schreiben, andere nichts
# - Archiv-Ordner: Schreibgeschützt für alle

# Beginnen Sie mit dem Aufbau:
mkdir -p mycompany/{public,private,team,archive}
```

<details>
<summary>📋 Vollständige Lösung</summary>

```bash
# Öffentlicher Ordner
chmod 755 mycompany/public

# Privater Ordner  
chmod 700 mycompany/private

# Team-Ordner
chmod 770 mycompany/team

# Archiv-Ordner
chmod 755 mycompany/archive
# Dateien darin schreibgeschützt machen:
touch mycompany/archive/old-data.txt
chmod 444 mycompany/archive/old-data.txt

# Alles überprüfen:
ls -la mycompany/
```

</details>

### Labor 4.2: Der Berechtigungs-Simulator

```bash
# Diese Übung simuliert Mehrbenutzer-Berechtigungen
# Da wir keine echten Benutzer erstellen können, spielen wir Rollen

# Simulation einrichten:
mkdir -p simulation/{alice,bob,shared}
echo "Alices Tagebuch" > simulation/alice/diary.txt
echo "Bobs Code" > simulation/bob/code.py
echo "Gemeinsame Notizen" > simulation/shared/notes.txt

# Berechtigungen setzen als ob:
# - alice/ privat für Alice ist
# - bob/ privat für Bob ist  
# - shared/ kollaborativ ist

chmod 700 simulation/alice
chmod 700 simulation/bob
chmod 775 simulation/shared
chmod 664 simulation/shared/notes.txt

# Testszenarien:
# 1. Wenn Sie Bob wären, könnten Sie Alices Tagebuch lesen?
# 2. Wenn Sie Alice wären, könnten Sie gemeinsame Notizen bearbeiten?
# 3. Welche Berechtigungen würden Bob erlauben, seinen Code mit Alice zu teilen?
```

### Labor 4.3: Reale Skript-Berechtigungen

```bash
# Erstellen Sie ein produktionsähnliches Skript-Setup
mkdir -p scripts/{development,production,archive}

# Entwicklungsskript (Entwickler können ändern)
cat > scripts/development/deploy-test.sh << 'EOF'
#!/bin/bash
echo "Bereitstellung in TEST-Umgebung..."
echo "Version: Entwicklung"
EOF

# Produktionsskript (nur lesen/ausführen)
cat > scripts/production/deploy-prod.sh << 'EOF'
#!/bin/bash
echo "Bereitstellung in PRODUKTIONS-Umgebung..."
echo "Version: Stabil"
echo "⚠️  VORSICHT: Produktionsbereitstellung!"
EOF

# Angemessene Berechtigungen setzen:
# Entwicklung: rwxrwx---
# Produktion: r-xr-x---
# Ihre Befehle hier...
```

<details>
<summary>🚀 Lösung</summary>

```bash
# Entwicklungsskripte
chmod 770 scripts/development/deploy-test.sh

# Produktionsskripte (kein Schreiben zur Unfallvermeidung)
chmod 550 scripts/production/deploy-prod.sh

# Testen
./scripts/development/deploy-test.sh
./scripts/production/deploy-prod.sh

# Versuchen Sie, Produktion zu ändern (sollte für Gruppe fehlschlagen)
echo "schlechte Änderung" >> scripts/production/deploy-prod.sh
```

</details>

---

## 🎯 Finale Herausforderung: Der Berechtigungs-Escape-Room

```bash
# Escape Room einrichten
mkdir -p escape-room/{door1,door2,door3,exit}
echo "🔑 Schlüssel zu Tür 2" > escape-room/door1/key1.txt
echo "🔑 Schlüssel zu Tür 3" > escape-room/door2/key2.txt
echo "🔑 Schlüssel zum Ausgang" > escape-room/door3/key3.txt
echo "🎉 Glückwunsch! Du bist entkommen!" > escape-room/exit/freedom.txt

# Rätsel-Berechtigungen setzen
chmod 111 escape-room
chmod 755 escape-room/door1
chmod 600 escape-room/door1/key1.txt
chmod 111 escape-room/door2
chmod 644 escape-room/door2/key2.txt
chmod 100 escape-room/door3
chmod 444 escape-room/door3/key3.txt
chmod 500 escape-room/exit
chmod 400 escape-room/exit/freedom.txt

# Ihre Mission:
# Navigieren Sie durch alle Türen und lesen Sie die freedom.txt-Datei
# Dokumentieren Sie, welche Befehle funktionieren und warum!
```

<details>
<summary>🏃 Fluchtweg</summary>

```bash
# Kann escape-room/ nicht auflisten (kein Lesen), aber cd (Ausführen)
cd escape-room

# Tür 1: Kann ls und eintreten
ls door1/  # Funktioniert (755)
cat door1/key1.txt  # Schlägt fehl (600 - nur Besitzer)

# Tür 2: Kann eintreten, aber nicht ls
cd door2  # Funktioniert (Ausführen)
ls  # Schlägt fehl (kein Lesen)
cat key2.txt  # Funktioniert, wenn Sie den Dateinamen kennen! (644)

# Tür 3: Kann nur eintreten
cd ../door3  # Funktioniert (nur Ausführen)
cat key3.txt  # Funktioniert (444 - jeder kann lesen)

# Ausgang: 
cd ../exit  # Funktioniert (Ausführen)
cat freedom.txt  # Funktioniert (400 - Besitzer lesen)

# Die Lektion: Ausführungsberechtigung lässt Sie durchqueren!
```

</details>

---

## 📝 Labor-Zusammenfassung & Best Practices

### Wichtigste Erkenntnisse:
1. **Lesen** = Inhalt sehen (Dateien) oder auflisten (Verzeichnisse)
2. **Schreiben** = Inhalt ändern oder Dateien hinzufügen/entfernen
3. **Ausführen** = ausführen (Dateien) oder durchqueren (Verzeichnisse)

### Berechtigungs-Kurzanleitung:
```bash
# Häufige Berechtigungsmuster:
644 - Standard-Datei (rw-r--r--)
755 - Ausführbar/Verzeichnis (rwxr-xr-x)
600 - Private Datei (rw-------)
700 - Privates Verzeichnis (rwx------)
666 - Warnung! Zu offen (rw-rw-rw-)
777 - Gefahr! Niemals verwenden (rwxrwxrwx)
```

### Praxis-Tipps:
1. **Standard-umask**: Mit `umask` Befehl prüfen
2. **Spezielle Bits**: Lernen Sie setuid, setgid, sticky bit
3. **ACLs**: Für komplexe Berechtigungen `getfacl`/`setfacl` verwenden
4. **Sicherheit**: Prinzip der geringsten Privilegien immer!

---

## 🏁 Abschluss-Checkliste

Verfolgen Sie Ihren Fortschritt:
- [ ] Teil 1 abgeschlossen: Berechtigungen verstehen
- [ ] Teil 2 abgeschlossen: Praktische Szenarien  
- [ ] Teil 3 abgeschlossen: Interaktive Herausforderungen
- [ ] Teil 4 abgeschlossen: Fortgeschrittenes Labor
- [ ] Aus dem Berechtigungs-Escape-Room entkommen
- [ ] Kann rwx für Dateien vs. Verzeichnisse erklären
- [ ] Vertraut mit numerischer und symbolischer Notation

**Glückwunsch! Sie haben Linux-Berechtigungen gemeistert! 🎉**