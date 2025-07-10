# Bedingte Anweisungen in Bash: `if` / `elif` / `else`

Bash-Skripte können Entscheidungen treffen und ihren Ablauf je nach Eingabe oder Zustand ändern. Dafür nutzt man die \`\`**-Struktur** mit optionalen `elif`- und `else`-Zweigen.

---

## 1. Aufbau einer `if`-Struktur

```bash
if [ BEDINGUNG ]; then       # Test-Konstruktion: wenn BEDINGUNG wahr ist
  # Anweisungen, die ausgeführt werden
elif [ ANDERE_BEDINGUNG ]; then  # weitere Bedingung
  # alternative Anweisungen
else                        # wenn keine Bedingung erfüllt ist
  # Fallback-Anweisungen
fi                          # Ende der if-Struktur
```

---

## 2. Beispiele&#x20;

### 2.1 Weggabelung

\*Mit diesem Beispiel lernst du, wie man eine einfache Weggabelung mit `if` / `elif` / `else`*setzt.*

```bash
#!/bin/bash

echo "Du stehst vor einer Kreuzung."
echo "Gehst du links oder rechts?"
read richtung

if [ "$richtung" = "links" ]; then
  echo "Du biegst nach links ab."
elif [ "$richtung" = "rechts" ]; then
  echo "Du biegst nach rechts ab."
else
  echo "Ungültige Richtung!"
fi
```

**Übung 2.1**: Erweitere das Skript um die Option **"geradeaus"** und gib dann **"Du gehst weiter geradeaus."** aus.

---

### 2.2 Frühstückswahl

*Mit diesem Beispiel übst du, wie man Benutzereingaben ausliest und mehrere Alternativen mit `if` / `elif` / `else` abprüft.*

```bash
#!/bin/bash

echo "Möchtest du heute Brötchen oder Brot?"
read wunsch

if [ "$wunsch" = "Brötchen" ]; then
  echo "Gute Wahl!"
elif [ "$wunsch" = "Brot" ]; then
  echo "Brot ist herzhaft!"
else
  echo "Dann eben Müsli."
fi
```

**Übung 2.2**: Füge die Option **"Croissant"** hinzu und gib bei Eingabe **"Luxus-Frühstück!"** aus.


---

### 2.4 Dateiprüfung

*Hier lernst du, wie man mit `if` prüft, ob eine Datei existiert oder nicht.*
-e prüft ob eine Datei existiert im if Statement.

```bash
#!/bin/bash

# Prüfe, ob '1.txt' existiert mit -e
if [ -e "1.txt" ]; then
  echo "Datei 1.txt existiert."
else
  echo "Datei 1.txt existiert nicht."
fi
```

**Übung 2.4**: Erweitere das Skript so, dass es die Datei **`1.txt`** anlegt, falls sie nicht existiert, und danach eine Bestätigung ausgibt.

---

## 3. Hausaufgabe: Helden-Abenteuer

Mit verschachtelten `if`-Anweisungen kannst du mehrere Entscheidungen hintereinander abbilden und so komplexere Abläufe gestalten.
Probiere das folgende Beispiel aus und finde alle möglichen Pfade durch unterschiedliche Eingaben.

### Verschachtelte Weggabelung (Nested `if`)

```bash
#!/bin/bash

echo "Du stehst vor einer Kreuzung: links oder rechts?"
read richtung

if [ "$richtung" = "links" ]; then
  echo "Erneute Kreuzung: geradeaus oder zurück?"
  read weg2
  if [ "$weg2" = "geradeaus" ]; then
    echo "Du findest den Ausgang."
  else
    echo "Du gehst zurück zum Start."
  fi
elif [ "$richtung" = "rechts" ]; then
  echo "Du siehst einen Tunnel: hinein oder umkehren?"
  read weg2
  if [ "$weg2" = "hinein" ]; then
    echo "Du findest einen Schatz."
  else
    echo "Du kehrst um und gehst zurück."
  fi
else
  echo "Ungültige Eingabe!"
fi
```

---

Schreibe ein kleines Text-Abenteuer!

Wähle ein eigenes Thema (z. B. Fußballstadion (Schlängel dich durch die Menge um dir eine Bratwurst zu holen), Pokémon-Labyrinth) und kommentiere wichtige Schritte. Nutze alle Befehle und Tool wie read -p und sleep und die wir vorher gelernt haben. Stelle morgen im Unterricht dein eigens kleines Abenteuer vor.  

Viel Spaß beim Coden deines Abenteuers! :)
