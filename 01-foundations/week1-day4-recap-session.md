# Woche 1, Tag 4 — Wiederholung & Gruppenarbeit

## 🎯 Tagesziel
**Dauer**: 3 Stunden  
**Format**: Interaktive Wiederholung mit Gruppenübungen  
**Ziel**: Festigung der Grundlagen aus den ersten drei Tagen durch praktische Anwendung

---

## 📋 Tagesablauf

### Teil 1: Warm-up Quiz (30 Min.)
- Individuelle Selbsteinschätzung
- Gemeinsame Besprechung

### Teil 2: Gruppen-Challenges (90 Min.)
- 3 praktische Szenarien in Kleingruppen
- Präsentation der Lösungen

### Teil 3: Knowledge Café (45 Min.)
- Rotierendes Gruppengespräch
- Erfahrungsaustausch

### Teil 4: Abschluss & Ausblick (15 Min.)
- Zusammenfassung
- Vorbereitung auf Woche 2

---

## 🧠 Teil 1: Warm-up Quiz (30 Min.)

### Selbsttest: Was habe ich gelernt?

**Anleitung**: Beantwortet die Fragen zuerst individuell (10 Min.), dann besprecht sie in der Gruppe (20 Min.).

#### A. Command Line Basics (Tag 1)

1. **Was macht der Befehl `pwd`?**
   - [ ] Ändert das Passwort
   - [ ] Zeigt das aktuelle Verzeichnis
   - [ ] Listet Dateien auf
   - [ ] Erstellt ein Verzeichnis

2. **Wie navigiert man zum Home-Verzeichnis? (Mehrere richtig)**
   - [ ] `cd ~`
   - [ ] `cd /home/$USER`
   - [ ] `cd`
   - [ ] `cd home`

3. **Was zeigt `ls -la`?**
   - [ ] Nur Verzeichnisse
   - [ ] Alle Dateien inkl. versteckte mit Details
   - [ ] Nur große Dateien
   - [ ] Systemlogs

4. **Vervollständige den Befehl zum Erstellen verschachtelter Verzeichnisse:**
   ```bash
   mkdir _____ projekt/src/main
   ```

#### B. Linux Architektur (Tag 2)

5. **Ordne die Schichten richtig zu (von unten nach oben):**
   - [ ] Anwendungen
   - [ ] Kernel
   - [ ] Hardware
   - [ ] Shell/GUI

6. **Was ist KEIN Init-System?**
   - [ ] systemd
   - [ ] SysV init
   - [ ] nginx
   - [ ] Upstart

7. **Welcher Befehl zeigt laufende Prozesse?**
   - [ ] `ps aux`
   - [ ] `ls -l`
   - [ ] `pwd`
   - [ ] `cd /proc`

8. **Was bedeutet "Everything is a file" in Linux?**
   _________________________________

#### C. Benutzer & Gruppen (Tag 3)

9. **Welche UID hat der root-Benutzer?**
   - [ ] 1
   - [ ] 0
   - [ ] 1000
   - [ ] 100

10. **Mit welchem Befehl fügt man einen Benutzer einer Gruppe hinzu?**
    ```bash
    sudo _______ -aG developers alice
    ```

11. **Was bewirkt das Set-GID-Bit auf einem Verzeichnis?**
    - [ ] Nur root kann zugreifen
    - [ ] Neue Dateien erben die Gruppe des Verzeichnisses
    - [ ] Dateien werden automatisch ausführbar
    - [ ] Das Verzeichnis wird gelöscht

12. **Wo werden Benutzerinformationen gespeichert?**
    - [ ] /etc/passwd
    - [ ] /home/users
    - [ ] /var/users
    - [ ] /usr/passwd

### 📊 Auswertung
- **10-12 richtig**: Exzellent! Du bist bereit für Woche 2
- **7-9 richtig**: Gut! Ein paar Konzepte nochmal wiederholen
- **4-6 richtig**: Grundlagen sitzen, aber mehr Übung nötig
- **0-3 richtig**: Keine Sorge! Nutze die Gruppenübungen zum Lernen

---

## 👥 Teil 2: Gruppen-Challenges (90 Min.)

### Gruppeneinteilung
Bildet 3er-Gruppen. Jede Gruppe bearbeitet alle drei Challenges nacheinander (je 25 Min. + 5 Min. Präsentation).

### Challenge 1: "Der neue Praktikant" (30 Min.)

**Szenario**: Max startet als Praktikant in eurer Firma. Er braucht:
- Ein Benutzerkonto
- Zugriff auf das Praktikanten-Verzeichnis
- Eingeschränkte Rechte (kein sudo)
- Ein gemeinsames Projekt-Verzeichnis mit anderen Praktikanten

**Aufgaben**:
1. Plant die notwendigen Schritte
2. Erstellt die Befehle (ohne sie auszuführen)
3. Erklärt eure Sicherheitsüberlegungen

**Dokumentiert**:
```bash
# Eure Befehle hier:
# 1. Gruppe erstellen
# 2. Benutzer anlegen
# 3. Verzeichnisse einrichten
# 4. Berechtigungen setzen
```

**Bonus**: Wie stellt ihr sicher, dass Max nach 3 Monaten automatisch deaktiviert wird?

### Challenge 2: "Das Mysterium der vollen Festplatte" (30 Min.)

**Szenario**: Der Server meldet "No space left on device", aber `df -h` zeigt noch 30% frei.

**Eure Mission**:
1. Listet mögliche Ursachen auf
2. Welche Befehle würdet ihr zur Diagnose nutzen?
3. Erstellt einen Troubleshooting-Leitfaden

**Hilfreiche Befehle** (erforscht ihre Bedeutung):
- `df -h` vs `df -i`
- `du -sh /*`
- `lsof | grep deleted`
- `find / -size +100M`

**Diskutiert**: Was könnte die Diskrepanz erklären?

### Challenge 3: "Die Prozess-Lawine" (30 Min.)

**Szenario**: Ein Skript hat versehentlich hunderte Prozesse gestartet. Das System reagiert träge.

**Aufgaben**:
1. Wie findet ihr die problematischen Prozesse?
2. Wie stoppt ihr sie sicher?
3. Wie verhindert ihr das in Zukunft?

**Erstellt eine Checkliste**:
```markdown
## Notfall-Prozedur bei Prozess-Überflutung
1. [ ] System-Last prüfen mit: _____
2. [ ] Prozesse identifizieren mit: _____
3. [ ] Prozesse beenden mit: _____
4. [ ] Präventionsmaßnahmen: _____
```

### Präsentationen
Jede Gruppe stellt EINE ihrer Lösungen vor (5 Min.). Andere Gruppen geben Feedback.

---

## ☕ Teil 3: Knowledge Café (45 Min.)

### Ablauf
Drei "Tische" mit je einem Thema. Gruppen rotieren alle 15 Minuten.

### Tisch 1: "CLI Tricks & Tipps"
**Moderationsfragen**:
- Welche Tastenkombination hat euch am meisten geholfen?
- Welchen Befehl findet ihr am nützlichsten?
- Was war eure größte "Aha"-Erkenntnis?

**Sammelt auf Flipchart**:
```
Top 5 CLI-Tricks unserer Gruppe:
1. ________________
2. ________________
3. ________________
4. ________________
5. ________________
```

### Tisch 2: "Linux vs. Windows"
**Diskussionsthemen**:
- Größte Unterschiede in der Philosophie?
- Was vermisst ihr von Windows?
- Was gefällt euch besser an Linux?

**Erstellt eine Vergleichstabelle**:
| Aspekt | Linux | Windows |
|--------|-------|---------|
| Dateisystem | | |
| Benutzerkonzept | | |
| Software-Installation | | |
| Sicherheit | | |

### Tisch 3: "Real-World Szenarien"
**Brainstorming**:
- In welchen Jobs braucht man diese Skills?
- Welche Probleme könntet ihr jetzt schon lösen?
- Was wollt ihr als nächstes lernen?

**Mindmap erstellen**:
```
Linux-Skills im Job
├── DevOps
│   └── ...
├── Support
│   └── ...
└── Administration
    └── ...
```

---

## 🎮 Bonus: Speed Challenge (falls Zeit bleibt)

### "Command Line Staffellauf"
Teams treten gegeneinander an. Jeder muss eine Aufgabe lösen, dann wechseln.

**Aufgaben**:
1. Navigiere zu /var/log
2. Finde alle .log Dateien
3. Zeige die letzten 5 Zeilen von syslog
4. Erstelle Verzeichnis ~/sprint/fertig
5. Finde deine User-ID heraus

**Regeln**:
- Keine Maus erlaubt
- Tab-Completion erwünscht
- Erster fertig gewinnt!

---

## 📝 Teil 4: Abschluss & Ausblick (15 Min.)

### Reflexion (5 Min.)
Jeder teilt mit:
- Eine Sache, die jetzt klar ist
- Eine Sache, die noch unklar ist
- Ein Ziel für nächste Woche

### Hausaufgabe für Woche 2
1. **Übt die CLI täglich** (15 Min.):
   - Navigiert nur mit Terminal
   - Erstellt eine Verzeichnisstruktur für ein Projekt
   - Experimentiert mit neuen Befehlen

2. **Mini-Projekt** (optional):
   - Erstellt einen Benutzer für ein Familienmitglied
   - Richtet getrennte Verzeichnisse ein
   - Dokumentiert eure Schritte

3. **Vorbereitung**:
   - Lest über Dateiberechtigungen (rwx)
   - Schaut euch `chmod` und `chown` an

### Ausblick Woche 2
**Montag**: Dateiberechtigungen Deep Dive
- Oktal-Notation
- Spezielle Bits (SUID, SGID, Sticky)
- Praktische Übungen

**Mittwoch**: Prozessmanagement
- Prozess-Lebenszyklus
- Signale
- Systemd Services

**Freitag**: Shell Scripting Basics
- Erste Skripte
- Variablen und Schleifen
- Automatisierung

---

## 🏆 Zertifikat: Woche 1 Abgeschlossen!

```
┌─────────────────────────────────────┐
│                                     │
│     🐧 LINUX BASICS CHAMPION 🐧      │
│                                     │
│    Hat erfolgreich abgeschlossen:   │
│         • CLI Navigation            │
│         • System-Architektur        │
│         • Benutzer & Gruppen        │
│                                     │
│     Name: ___________________      │
│     Datum: __________________      │
│                                     │
└─────────────────────────────────────┘
```

### Erfolgs-Checkliste
- [ ] Kann sicher im Terminal navigieren
- [ ] Versteht Linux-Architektur-Grundlagen
- [ ] Kann Benutzer und Gruppen verwalten
- [ ] Hat an allen Gruppenübungen teilgenommen
- [ ] Ist bereit für Woche 2!

---

## 📚 Zusatzmaterial für Interessierte

### Weiterführende Übungen
1. **Terminal-Kunst**: Erstellt ASCII-Art mit echo und Dateien
2. **Benutzer-Simulation**: Spielt verschiedene Rollen (Admin, User, Service)
3. **Mini-Forensik**: Findet heraus, wer zuletzt angemeldet war

### Empfohlene Ressourcen
- `man intro` - Einführung in die Manual-Pages
- LinuxCommand.org - Für CLI-Vertiefung
- Ubuntu Community Help - Für praktische Anleitungen

### Fun Facts zum Angeben
- Linux läuft auf 100% der Top 500 Supercomputer
- Der Linux-Kernel hat über 28 Millionen Zeilen Code
- Linus Torvalds wollte ursprünglich sein OS "Freax" nennen

---

**🎉 Gratulation!** Ihr habt die erste Woche erfolgreich gemeistert! Nutzt das Wochenende zum Üben und Experimentieren. Denkt daran: Der beste Weg Linux zu lernen ist, es täglich zu benutzen!

**Motto für's Wochenende**: "In Linux gibt es keine Fehler, nur Lernmöglichkeiten!" 🚀