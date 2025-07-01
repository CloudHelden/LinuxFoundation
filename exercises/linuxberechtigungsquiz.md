# Berechtigungsquiz auf Ubuntu

Dieses Dokument beschreibt, wie du ein interaktives Berechtigungsquiz auf deinem Ubuntu-System einrichtest und durchführst. Du legst zunächst 30 Dateien/Verzeichnisse mit unterschiedlichen Berechtigungen an, richtest das Quiz-CLI-Tool ein und beantwortest dann nacheinander alle Fragen.

---

## 1. Fragen anlegen

Erstelle ein Bash-Script namens `setup_quiz.sh`, das 30 Items (`frage1` bis `frage30`) mit variierenden Berechtigungen anlegt:

```bash
#!/usr/bin/env bash
# setup_quiz.sh
# Erstellt 30 Fragen-Items (abwechselnd Dateien und Verzeichnisse)
# mit jeweils unterschiedlichen Berechtigungen und Namen frage1…frage30.

set -e  # Stoppe bei Fehler

# Array mit 30 Oktal-Berechtigungen
perms=(
  644 600 755 700 750 740 666 664 660 644
  600 544 550 555 500 755 711 733 700 744
  640 620 750 730 700 770 777 711 721 641
)

for i in "${!perms[@]}"; do
  qnum=$((i + 1))
  name="frage${qnum}"
  perm="${perms[i]}"

  # Abwechselnd Datei (ungerade) und Verzeichnis (gerade)
  if (( qnum % 2 == 1 )); then
    touch "$name"
  else
    mkdir "$name"
  fi

  chmod "$perm" "$name"
  echo "Erstellt: $name  → Berechtigungen: $perm"
done

echo "Setup abgeschlossen: 30 Items angelegt."
```

1. Speichere das Skript als `setup_quiz.sh` im gewünschten Verzeichnis.
2. Mache es ausführbar:

   ```bash
   chmod +x setup_quiz.sh
   ```
3. Führe das Skript aus:

   ```bash
   ./setup_quiz.sh
   ```

Alle 30 Fragen-Items (`frage1` bis `frage30`) wurden nun in deinem aktuellen Verzeichnis angelegt.

---

## 2. Quiz-CLI einrichten

Lege das Python-CLI-Tool **bquiz** an, das dich interaktiv durch jede Frage führt.
@andy Danke dir für den Hinweis

1. Erstelle eine Datei namens `bquiz` mit folgendem Inhalt:

   ```python
   #!/usr/bin/env python3
   # bquiz

   import os
   import stat
   import subprocess
   import sys

   def get_mode(path):
       """Gibt die Datei-Modus-Zeichenkette zurück, z.B. '-rwxr-x--x'."""
       st = os.lstat(path)
       return stat.filemode(st.st_mode), st.st_mode

   def choose_perm_semantic(who):
       options = [
           ("---", "1) keine Rechte"),
           ("r--", "2) nur Lesen"),
           ("rw-", "3) Lesen & Schreiben"),
           ("r-x", "4) Lesen & Ausführen"),
           ("rwx", "5) Lesen, Schreiben & Ausführen"),
           ("rwx", "5) Lesen, Schreiben & Ausführen"),
           ("--x", "6) nur Ausführen"),
           ("-w-", "7) nur Schreiben"),
           ("-wx", "8) Schreiben & Ausführen"),
       ]
       print(f"{who}:")
       for _, label in options:
           print(f"   {label}")
       sel = input("→ Nummer eingeben [1–8]: ").strip()
       mapping = {str(i+1): code for i, (code, _) in enumerate(options)}
       if sel in mapping:
           return mapping[sel]
       else:
           print("Ungültige Eingabe, bitte 1–8 wählen.\n")
           return choose_perm_semantic(who)

   def quiz(path):
       print(f"\n=== Quiz für: {path} ===\n")
       try:
           out = subprocess.check_output(["ls", "-la", path], text=True)
           print(out.rstrip(), "\n")
       except subprocess.CalledProcessError as e:
           print(f"Fehler beim Aufruf von ls: {e}", file=sys.stderr)
           return

       mode_str, mode_raw = get_mode(path)
       score = 0

       # 1) Dateityp
       print("1) Dateityp:")
       print("   ‘-’ = Datei")
       print("   ‘d’ = Verzeichnis")
       ans = input("→ Bitte ‘-’ oder ‘d’ eingeben: ").strip()
       if ans == mode_str[0]:
           print("✅ Richtig!\n")
           score += 1
       else:
           print(f"❌ Falsch! Richtige Antwort wäre: {mode_str[0]}\n")

       # 2–4) Besitzer, Gruppe, Andere
       parts = [
           ("2) Besitzer", mode_str[1:4]),
           ("3) Gruppe",   mode_str[4:7]),
           ("4) Andere",   mode_str[7:10]),
       ]
       for titel, richtig in parts:
           print(f"{titel}:")
           antwort = choose_perm_semantic(titel.split()[1])
           if antwort == richtig:
               print("✅ Richtig!\n")
               score += 1
           else:
               print(f"❌ Falsch! Richtige Antwort wäre: {richtig}\n")

       # 5) chmod-Oktalzahl mit Referenz
       octal = format(mode_raw & 0o777, '03o')
       chmod_str = '0' + octal
       print(f"5) {mode_str}  Gebe die chmod-Oktalzahl an (mit führender 0), z.B. 0644")
       ans5 = input("→ ").strip()
       if ans5 == chmod_str:
           print("✅ Richtig!\n")
           score += 1
       else:
           print(f"❌ Falsch! Richtige Antwort wäre: {chmod_str}\n")

       print(f"Ergebnis: {score} von 5 richtig.\n")

   def main():
       if len(sys.argv) < 2:
           print(f"Usage: bquiz <Datei-oder-Verzeichnis> [...", file=sys.stderr)
           sys.exit(1)

       for path in sys.argv[1:]:
           if not os.path.exists(path):
               print(f"Pfad nicht gefunden: {path}", file=sys.stderr)
               continue
           quiz(path)

   if __name__ == "__main__":
       main()
   ```

2. Mache das Skript ausführbar und verschiebe es in dein `$PATH`:

   ```bash
   chmod +x bquiz
   sudo mv bquiz /usr/local/bin/
   ```

---

## 3. Quiz starten

Führe das Quiz für alle 30 Fragen-Items nacheinander aus.

```bash
bquiz frage1 frage2 frage3 ... frage30
```

Das Tool zeigt dir für jede Frage:

1. Dateityp (Datei oder Verzeichnis)
2. Berechtigungen des Besitzers
3. Berechtigungen der Gruppe
4. Berechtigungen für „Andere“
5. Die chmod-Oktalzahl (mit führender Null)

Am Ende jeder Runde erhältst du eine Auswertung deiner Antworten.

Viel Erfolg beim Üben deines Linux-Dateisystem-Wissens!
