# Zip zip zip
**Unterschied zwischen Archivieren und Komprimieren**

Komprimierung wird eingesetzt, um den Platzbedarf für einen bestimmten Datensatz zu reduzieren. Üblicherweise dient Komprimierung der Einsparung von Speicherplatz für eine Datei oder der Menge der über eine Netzwerkverbindung gesendeten Daten. Kompression funktioniert durch das Ersetzen sich wiederholender Muster durch Daten. Kompression gibt es in zwei Varianten: **verlustfrei** (lossless) und **verlustbehaftet** (lossy).

Archivierung hingegen fasst mehrere Dateien und Verzeichnisse in einer einzigen Datei zusammen, ohne deren Inhalt selbst zu verändern. So lassen sich Backups, Source‑Code‑Pakete oder Langzeitarchive übersichtlich verwalten.

Linux-Systeme verfügen über mehrere Komprimierungs- und Archivierungswerkzeuge. In dieser
Lektion wurden die gängigsten behandelt. Das meistgenutzte Archivierungswerkzeug ist **tar**..
Wenn eine Interaktion mit Windows-Systemen erforderlich ist, können **zip** und **unzip** ZIP-
Dateien erstellen und extrahieren.

Der Befehl **tar** hat einige Optionen, die man sich merken sollte:

* `x` steht für **Extrahieren**
* `c` steht für **Erstellen**
* `t` steht für **Anzeigen der Inhalte**
* `u` steht für **Hinzufügen oder Ersetzen von Dateien**
* `v` listet die Dateien auf, die von tar beim Erstellen oder Entpacken eines Archivs verarbeitet werden

Das Repository der typischen Linux-Distribution verfügt über viele Komprimierungswerkzeuge,
darunter **gzip**, **bzip2** und **xz**. Komprimierungsalgorithmen unterstützen oft verschiedene
Ebenen, mit denen Sie Geschwindigkeit oder Dateigröße optimieren können. Dateien lassen sich mit
**gunzip**, **bunzip2** und **unxz** dekomprimieren.

Komprimierungswerkzeuge umfassen häufig Programme, die sich wie gängige Textdateiwerkzeuge verhalten,
mit dem Unterschied, dass sie mit komprimierten Dateien arbeiten. Einige von ihnen sind **zcat**, **bzcat**
und **xzcat**. Sie werden oft zusammen mit Programmen wie **grep**, **more**, **less**, **diff** und **cmp** ausgeliefert.

**Hinweis:**
Alle aufgeführten Befehle sind in einer Standard-Ubuntu-Installation verfügbar, mit Ausnahme von **zip** und **unzip**, die bei Bedarf nachinstalliert werden können:

```bash
sudo apt update && sudo apt install zip unzip
```

**Befehle, die in den Übungen verwendet werden:**

| Befehl  | Beschreibung                                               | Ubuntu-Paket     |
| ------- | ---------------------------------------------------------- | ---------------- |
| bunzip2 | Dekomprimiert eine mit bzip2 komprimierte Datei.           | bzip2            |
| bzcat   | Gibt den Inhalt einer mit bzip komprimierten Datei aus.    | bzip2            |
| bzip2   | Komprimiert Dateien mit dem bzip2-Algorithmus und -Format. | bzip2            |
| gunzip  | Dekomprimiert eine mit gzip komprimierte Datei.            | gzip             |
| gzip    | Komprimiert Dateien mit dem gzip-Algorithmus und -Format.  | gzip             |
| tar     | Erstellt, aktualisiert, listet und extrahiert tar-Archive. | tar              |
| unxz    | Dekomprimiert eine mit xz komprimierte Datei.              | xz-utils         |
| unzip   | Dekomprimiert und extrahiert Inhalte aus einer ZIP-Datei.  | unzip (optional) |
| xz      | Komprimiert Dateien mit dem xz-Algorithmus und -Format.    | xz-utils         |
| zcat    | Gibt den Inhalt einer mit gzip komprimierten Datei aus.    | gzip             |
| zip     | Erzeugt und komprimiert ZIP-Archive.                       | zip (optional)   |

---

# Vorbereitung

```bash
cd ~
mkdir -p linux_exercises/compression
cd linux_exercises/compression
# Erstelle eine große Testdatei
cat /etc/hosts /etc/passwd /etc/group > bigfile
# Erstelle kleine Textdateien
echo "Hallo Welt" > hello.txt
echo "Foo Bar"   > foo.txt
# Erstelle ein Unterverzeichnis mit weiteren Dateien
mkdir texts
echo "Zeile1" > texts/a.txt
echo "Zeile2" > texts/b.txt
```

* Wechsel ins Home-Verzeichnis
* Erzeuge Übungs- und Testdateien

---

In dieser Übung nutzen wir **gzip**, um eine große Datei zu komprimieren und anschließend wieder zu dekomprimieren. Wir beobachten die Platzersparnis und testen verschiedene Kompressionsstufen.

# Übung 1: gzip

1. **Komprimieren**

   ```bash
   gzip bigfile
   ```

   * Ersetzt `bigfile` durch `bigfile.gz` mit Standard-Kompressionslevel (6).

2. **Ergebnis prüfen**

   ```bash
   ls -lh bigfile.gz
   ```

   * Zeigt Dateigröße in menschenlesbarer Form.

3. **Dekomprimieren**

   ```bash
   gunzip bigfile.gz
   ```

   * Entpackt und entfernt die `.gz`-Datei.

4. **Kompressionsstufen testen**

   ```bash
   cp bigfile bigfile-gz1
   cp bigfile bigfile-gz9
   gzip -1 bigfile-gz1
   gzip -9 bigfile-gz9
   ls -lh bigfile-gz*.gz
   ```

   * `-1` schnelle, geringe Kompression; `-9` langsame, hohe Kompression.

---

In dieser Übung nutzen wir **bzip2**, um eine Datei mit einem anderen Algorithmus zu komprimieren und anschließend wieder zu dekomprimieren. Wir vergleichen Kompressionsrate und Geschwindigkeit.

# Übung 2: bzip2

1. **Komprimieren**

   ```bash
   bzip2 bigfile
   ```

   * Erstellt `bigfile.bz2` (bessere Kompression als gzip, aber langsamer).

2. **Ergebnis prüfen**

   ```bash
   ls -lh bigfile.bz2
   ```

3. **Dekomprimieren**

   ```bash
   bunzip2 bigfile.bz2
   ```

   * Entpackt und entfernt die `.bz2`-Datei.

---

In dieser Übung verwenden wir **xz**, um die Datei mit dem effizientesten, aber langsamsten Algorithmus zu komprimieren und zu dekomprimieren, und vergleichen die Ergebnisse.

# Übung 3: xz

1. **Komprimieren**

   ```bash
   xz bigfile
   ```

   * Erstellt `bigfile.xz` (beste Kompression, aber am langsamsten).

2. **Ergebnis prüfen**

   ```bash
   ls -lh bigfile.xz
   ```

3. **Dekomprimieren**

   ```bash
   unxz bigfile.xz
   ```

   * Entpackt und entfernt die `.xz`-Datei.

---

In dieser Übung erstellen wir mit **tar** ein unkomprimiertes Archiv aus mehreren Quelldateien und listen anschließend den Inhalt des Archivs auf.

# Übung 4: tar-Archiv erstellen

1. **Arbeitsverzeichnis prüfen**

   ```bash
   cd ~/linux_exercises/compression
   ```

   * Stelle sicher, dass du im Verzeichnis mit deinen Quelldateien bist.

2. **Archiv erstellen**

   ```bash
   tar cf test_plain.tar bigfile hello.txt foo.txt texts
   ```

   * `c` (create), `f` (file) → erstellt `test_plain.tar` im aktuellen Verzeichnis.

3. **Inhalt anzeigen**

   ```bash
   tar -tf test_plain.tar
   ```

   * `t` (list) zeigt alle Dateien im Archiv ohne Extrahieren.
   * Beispielausgabe:

     ```text
     bigfile
     hello.txt
     foo.txt
     texts/
     texts/a.txt
     texts/b.txt
     ```

---

---

In dieser Übung kombinieren wir **tar** und **gzip** in einem Schritt, um ein komprimiertes Archiv zu erstellen. Anschließend prüfen wir den Inhalt und extrahieren eine einzelne Datei.

# Übung 5: tar + gzip on the fly

1. **Kombinieren + Komprimieren**

   ```bash
   tar -czf ../archive/test_gzip.tar.gz bigfile hello.txt foo.txt texts
   ```

   * `z` fügt gzip-Kompression hinzu.

2. **Prüfen**

   ```bash
   ls -lh ../archive/test_gzip.tar.gz
   tar -tzf ../archive/test_gzip.tar.gz
   ```

   * `-tzf` listet Dateien in der gzip-komprimierten TAR.

3. **Einzelne Datei extrahieren**

   ```bash
   mkdir ../archive/extract_partial
   cd ../archive/extract_partial
   tar -xzf ../test_gzip.tar.gz foo.txt
   ls
   ```

   * `x` (extract), `z` (gzip), `f` (file) → nur `foo.txt` entpacken.

---

In dieser Übung vergleichen wir die **bzip2**- und **xz**-Kompression in Kombination mit **tar**, indem wir zwei verschiedene komprimierte Tar-Archive erstellen und deren Größen vergleichen.

# Übung 6: tar + bzip2 und tar + xz

1. **bzip2-Kompression**

   ```bash
   tar -cjf ../archive/test_bzip2.tar.bz2 bigfile
   ls -lh ../archive/test_bzip2.tar.bz2
   ```

   * `j` für bzip2.

2. **xz-Kompression**

   ```bash
   tar -cJf ../archive/test_xz.tar.xz bigfile
   ls -lh ../archive/test_xz.tar.xz
   ```

   * `J` für xz.

---

In dieser Übung erstellen wir mit **zip** ein Windows-kompatibles Archiv und entpacken es mit **unzip**, um die Interoperabilität zwischen Systemen zu testen.

# Übung 7: ZIP-Dateien (Windows-kompatibel)

1. **Arbeitsverzeichnis**

   ```bash
   mkdir ~/linux_exercises/zip && cd ~/linux_exercises/zip
   mkdir dir && touch dir/{file1,file2}
   ```

2. **ZIP erstellen**

   ```bash
   zip -r myarchive.zip dir
   ```

   * `-r` (recursive): Verzeichnis und Inhalte packen.

3. **Inhalt anzeigen**

   ```bash
   unzip -l myarchive.zip
   ```

   * `-l` listet ZIP-Inhalt.

4. **Entpacken**

   ```bash
   rm -rf dir
   unzip myarchive.zip
   ls dir
   ```

   * Entfernen, um zu prüfen, dass `unzip` Verzeichnis wiederherstellt.

---

---

# Geführte Übungen

1. **Tool erkennen nach Dateinamenerweiterung**
   Welches der folgenden Tools wurde entsprechend der jeweiligen Erweiterung zur Erstellung dieser Dateien verwendet?

   | Dateiname        | Tool |
   | ---------------- | ---- |
   | `archive.tar`    |      |
   | `archive.tgz`    |      |
   | `archive.tar.xz` |      |

2. **Archiv vs. Komprimiert**
   Welche dieser Dateien sind entsprechend der jeweiligen Erweiterung Archive und welche sind komprimiert?

   | Dateiname      | Archiv | Komprimiert |
   | -------------- | ------ | ----------- |
   | `file.tar`     |        |             |
   | `file.tar.bz2` |        |             |
   | `file.zip`     |        |             |
   | `file.xz`      |        |             |

3. **Datei zu gzip-komprimiertem tar hinzufügen**
   Wie würden Sie eine Datei zu einer mit gzip komprimierten tar-Datei hinzufügen?

   ```bash
   # Befehl hier eintragen
   ```

4. **Kompressionsstufen in zip**
   Unterstützt zip verschiedene Kompressionsstufen? Wenn ja, wie geben Sie die Stufe an?

   ```bash
   # Beispielbefehl hier eintragen
   ```

Viel Erfolg beim Üben! Wenn du Fragen hast, melde dich gerne.

---

# Klausurfragen

### Frage 13

**Welche der folgenden Tar‑Optionen übernimmt Kompression? (Wähle zwei.)**

* `-z`
* `-g`
* `-z2`
* `-bz`
* `-j`

**Lösung:** `-z` und `-j`
**Erklärung:**

* Die Option `-z` weist `tar` an, das integrierte **gzip**-Programm zu verwenden und die Daten on‑the‑fly zu komprimieren.
* Die Option `-j` nutzt stattdessen **bzip2** für die Kompression.
  Beide Optionen legen den Archivstrom durch ihren Algorithmus, während `tar` selbst nur das Archivformat verwaltet.

---

### Frage 70

**Welcher der folgenden Befehle erstellt das ZIP‑Archiv ****`poems.zip`**** mit allen Dateien im aktuellen Verzeichnis, deren Namen auf ****`.txt`**** enden?**

* `zip *.txt > poems.zip`
* `zcat *.txt poems.zip`
* `zip poems.zip *.txt`
* `zip cfz poems.zip *.txt`
* `cat *.txt | zip poems.zip`

**Lösung:** `zip poems.zip *.txt`
**Erklärung:**

* `zip` erwartet zunächst den Namen des zu erstellenden Archivs und dann die Dateien, die hineingepackt werden sollen.
* Die Syntax `zip poems.zip *.txt` sagt also: Erzeuge `poems.zip` und füge alle `.txt`-Dateien im aktuellen Verzeichnis hinzu.
* Varianten wie `zip cfz` tauchen nur bei `tar` auf, nicht bei `zip`.

---

### Frage 72

**Welcher der folgenden Befehle extrahiert den Inhalt des komprimierten Archivs ****`file1.tar.gz`****?**

* `tar -czf file1.tar.gz`
* `ztar file1.tar.gz`
* `tar -xzf file1.tar.gz`
* `tar --extract file1.tar.gz`
* `detar file1.tar.gz`

**Lösung:** `tar -xzf file1.tar.gz`
**Erklärung:**

* `-x` (extract) weist `tar` an, Dateien aus einem Archiv zu entpacken,
* `-z` sagt, dass es sich um ein **gzip**-komprimiertes Archiv handelt und `tar` den Datenstrom zuerst durch `gunzip` leiten soll.
* `-f` spezifiziert die Archivdatei.
  Zusammen entpackt `tar -xzf file1.tar.gz` also korrekt ein gzip-komprimiertes Tar-Archiv.
