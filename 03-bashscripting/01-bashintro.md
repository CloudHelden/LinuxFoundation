# Bash-Scripting Tutorial

Dieses Tutorial führt Schritt für Schritt in einfache Bash-Skripte unter Linux ein. Am Ende kannst du eigene Skripte schreiben, ausführbar machen und einfache Automatisierungen durchführen.

---

## 1. Was ist Bash?

* **Bash** (Bourne Again Shell) ist die Standard-Shell (Kommandozeile) unter vielen Linux-Distributionen.
* Du gibst Befehle direkt in die Bash ein oder schreibst sie in Dateien (Skripte), die du später ausführst.

---

## 2. Skripte ausführbar machen

1. Erstelle eine Datei mit der Endung `.sh`, z. B. `skript.sh`.

2. Schreibe oben als erste Zeile den Shebang, damit das System weiß, welche Shell genutzt werden soll:

   ```bash
   #!/bin/bash
   ```

3. Mache die Datei ausführbar:

   ```bash
   chmod +x skript.sh
   ```

4. Führe das Skript aus:

   ```bash
   ./skript.sh
   ```

---

## 3. Grundlagen: Variablen, Rechnen & Dateiumleitung

### 3.1 Variablen

* Eine Variable speichert einen Wert unter einem Namen. Beispiel:

  ```bash
  NAME="Anna"
  ```
* Auf den Inhalt greifst du mit `$` zu:

  ```bash
  echo "$NAME"
  ```
* Keine Leerzeichen um `=`: `X=10`, nicht `X = 10`.

### 3.2 Rechnen

* Mit `(( ... ))` oder `$(( ... ))` kannst du Arithmetik durchführen:

  ```bash
  A=4
  B=7
  SUM=$((A + B))
  echo "$SUM"
  ```

### 3.3 Dateiumleitung

* `>` überschreibt eine Datei:

  ```bash
  echo "Hallo" > datei.txt
  ```
* `>>` hängt an eine Datei an:

  ```bash
  echo "Welt" >> datei.txt
  ```

---

## 4. Übungen

### 4.1 Echo-Befehle

1. **Übung 1.1**: Gib mit `echo` die Nachricht `„Willkommen im Bash-Tutorial“` aus.
2. **Übung 1.2**: Gib mit `echo` deinen Lieblingsspruch aus, z. B. „Carpe diem“.
3. **Übung 1.3**: Gib mit `echo` das Ergebnis der Rechnung `10 - 4` aus.

### 4.2 Variablen & Rechnen

4. **Übung 2.1**: Lege eine Variable `P=20` an und gib sie aus.
5. **Übung 2.2**: Lege zwei Variablen `C=6` und `D=3` an, berechne `C * D` und gib das Ergebnis aus.

### 4.3 Dateiumleitung

6. **Übung 3.1**: Erstelle mit `echo` eine Datei `status.log` und schreibe die Zeile `„Script gestartet“` hinein.
7. **Übung 3.2**: Hänge mit `echo` die Zeile `„Script beendet“` an dieselbe Datei an.

---
## 6. Lösungen

<details>
<summary>4.1 Echo-Befehle</summary>

```bash
#!/bin/bash
# Übung 1.1
echo "Willkommen im Bash-Tutorial"

# Übung 1.2
echo "Carpe diem"

# Übung 1.3
echo $((10 - 4))
```

</details>

<details>
<summary>4.2 Variablen & Rechnen</summary>

```bash
#!/bin/bash
# Übung 2.1
P=20
echo "$P"

# Übung 2.2
C=6
D=3
ERG=$((C * D))
echo "$ERG"
```

</details>

<details>
<summary>4.3 Dateiumleitung</summary>

```bash
#!/bin/bash
# Übung 3.1
echo "Script gestartet" > status.log

# Übung 3.2
echo "Script beendet" >> status.log
```

</details>
