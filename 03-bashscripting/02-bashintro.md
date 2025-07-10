# Interaktive Bash-Skripte

Bash-Skripte können interaktiv gestaltet werden, indem sie Eingaben vom Nutzer abfragen, verarbeiten und darauf reagieren. Hier lernst du:

* Nutzer-Eingaben mit `read`
* Pausen mit `sleep`
* Fortgeschrittene `read`-Optionen (silent, timeout, Standardwerte)
* Einfache Quiz-Anwendung mit Timer

---

## 1. User Input mit `read`

**Syntax:**

```bash
read VARIABLE_NAME
```

Liess eine Eingabe ein und speichere sie in `VARIABLE_NAME`.

---

## 2. Übungen zu User Input

### Übung 2.1: Name abfragen

```bash
#!/bin/bash

echo "Wie heißt du?"
sleep 1
read name
echo "Hallo, $name!"
```

#### Transfer-Aufgabe 2.1

Lasse das Skript den Wohnort des Nutzers abfragen und ihn mitecho begrüßen, z.B. „Willkommen aus Berlin, \$wohnort!“.

---

### Übung 2.2: Mac-Passwort abfragen

```bash
#!/bin/bash

echo "Wie ist dein Mac-Passwort?"
sleep 1
read pw
echo "Dein Passwort lautet: $pw"
```

#### Transfer-Aufgabe 2.2

Frage ein anderes geheimes Wort ab (z. B. Lieblingsfarbe) verdeckt ab und bestätige die Eingabe.

---

### Übung 2.3: Zwei Zahlen addieren

```bash
#!/bin/bash

echo "Gib Zahl A ein:"
sleep 1
read A
echo "Gib Zahl B ein:"
sleep 1
read B
SUM=$((A + B))
echo "Die Summe von $A und $B ist: $SUM"
```

#### Transfer-Aufgabe 2.3

Erweitere das Skript, sodass es drei Zahlen liest und deren Produkt berechnet und ausgibt.

---

## 3. Erweiterte Optionen für `read`

### 3.1 Verdeckte Eingabe

```bash
read -sp "Passwort: " pw
echo
echo "Eingabe gespeichert."
```

* `-s`: Silent-Modus, unterdrückt Anzeige der Eingabe (z.B. für Passwörter)
* `-p`: Zeigt den Prompt-Text an

#### Transfer-Aufgabe 3.1

Frage verdeckt nach einem Passwort und bestätige die Eingabe mit einer echo-Anweisung.

---

### 3.2 Timeout

```bash
read -t 5 -p "Eingabe in 5 Sekunden: " val
echo
echo "Du hast eingegeben: $val"
```

* `-t 5`: Zeitlimit von 5 Sekunden
* `-p`: Prompt vor Einlesen

#### Transfer-Aufgabe 3.2

Setze einen Timeout von 3 Sekunden und frage nach einer Bestätigung (ja/nein). Gib anschließend die Antwort aus.

---

### 3.3 Standardwerte

```bash
read -p "Name (Standard: Gast): " name
name=${name:-Gast}
echo "Hallo, $name!"
```

* `name=${name:-Gast}`: Setzt `name` auf `Gast`, falls leer oder nicht gesetzt

#### Transfer-Aufgabe 3.3

Frage den Lieblingsfußballverein ab mit Standardwert "Bayern" und gib den gewählten Verein aus.

---

## 5. Lösungen

<details>
<summary>Übung 2.1 Lösung</summary>

```bash
#!/bin/bash

echo "Wie heißt du?"
sleep 1
read name
echo "Hallo, $name!"
```

</details>

<details>
<summary>Übung 2.2 Lösung</summary>

```bash
#!/bin/bash

echo "Wie ist dein Mac-Passwort?"
sleep 1
read pw
echo "Dein Passwort lautet: $pw"
```

</details>

<details>
<summary>Übung 2.3 Lösung</summary>

```bash
#!/bin/bash

echo "Gib Zahl A ein:"
sleep 1
read A
echo "Gib Zahl B ein:"
sleep 1
read B
SUM=$((A + B))
echo "Die Summe von $A und $B ist: $SUM"
```

</details>

<details>
<summary>Transfer 2.1 Lösung</summary>

```bash
# Transfer 2.1: Wohnort abfragen
echo "Wo wohnst du?"
sleep 1
read wohnort
echo "Willkommen aus $wohnort!"
```

</details>

<details>
<summary>Transfer 2.2 Lösung</summary>

```bash
# Transfer 2.2: Lieblingsfarbe verdeckt abfragen
read -sp "Deine Lieblingsfarbe: " colour
echo
echo "Du hast eine Farbe eingegeben."
```

</details>

<details>
<summary>Transfer 2.3 Lösung</summary>

```bash
# Transfer 2.3: Produkt von drei Zahlen berechnen
echo "Gib Zahl 1 ein:"
sleep 1
read X
echo "Gib Zahl 2 ein:"
sleep 1
read Y
echo "Gib Zahl 3 ein:"
sleep 1
read Z
PROD=$((X * Y * Z))
echo "Das Produkt ist: $PROD"
```

</details>

<details>
<summary>Transfer 3.1 Lösung</summary>

```bash
# Transfer 3.1: Passwort verdeckt abfragen
read -sp "Passwort: " pw
echo
echo "Eingabe gespeichert."
```

</details>

<details>
<summary>Transfer 3.2 Lösung</summary>

```bash
# Transfer 3.2: Timeout 3s Bestätigung abfragen
read -t 3 -p "Bestätigen? (ja/nein): " ans
echo "Du hast gewählt: $ans"
```

</details>

<details>
<summary>Transfer 3.3 Lösung</summary>

```bash
# Transfer 3.3: Lieblingsfußballverein mit Standard Bayern
read -p "Lieblingsfußballverein (Standard: Bayern): " club
club=${club:-Bayern}
echo "Dein Verein: $club"
```

</details>
