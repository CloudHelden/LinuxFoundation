# Linux Essentials – 10 Prüfungsfragen und Übungen

Willkommen zu den ersten 10 Prüfungsfragen aus dem Bereich Linux Essentials!

Die meisten Fragen kannst du direkt im Ubuntu Server (z.B. per Multipass) praktisch testen. Dort findest du zu jeder Frage eine Aufgabenstellung, Tipps und – falls sinnvoll – eine praktische Anleitung. Fragen, die sich nicht sinnvoll am Server üben lassen (z.B. zur Auswahl einer Distribution), findest du mit Multiple-Choice.

Klicke auf "Hilfe" oder "Lösung", um Hinweise oder die Musterlösung einzublenden.

---

## Frage 1

**Aufgabenstellung:**
Was sind die Unterschiede zwischen Festplattenlaufwerken (HDD) und Solid State Disks (SSD)?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Mit `lsblk -d -o name,rota` kannst du feststellen, ob ein Laufwerk rotierend ist (1 = HDD, 0 = SSD).
* HDDs haben mechanische Bauteile, SSDs nicht.
* SSDs sind schneller, teurer und robuster gegen Erschütterungen.

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

* Nutze auf deinem Server `lsblk -d -o name,rota` oder `cat /sys/block/sda/queue/rotational`.
* Werte aus:

  * **1** = HDD (mechanisch, rotierend)
  * **0** = SSD (elektronisch, keine beweglichen Teile)
* Hintergrund: SSDs arbeiten schneller, leiser und sind weniger störanfällig, aber meist teurer pro GB.

**Antwort für die Prüfung:**
Festplattenlaufwerke (HDD) haben einen Motor und bewegliche Teile, SSDs nicht.
SSDs bieten einen schnelleren Zugriff auf gespeicherte Daten als Festplattenlaufwerke.

</details>

---

## Frage 2

**Aufgabenstellung:**
Mehrere Teammitglieder haben bereits Erfahrung mit Red Hat Enterprise Linux. Für ein kleines Hobbyprojekt möchte das Team einen Linux-Server aufsetzen, ohne für ein Abonnement zu bezahlen. Welche der folgenden Linux-Distributionen ermöglicht es den Teammitgliedern, ihr Wissen aus Red Hat Enterprise Linux am besten zu nutzen?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Es wird eine Distribution gesucht, die kostenlos ist und auf Red Hat basiert.
* Solche Distributionen sind oft zu Red Hat kompatibel („binary compatible“).

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Ubuntu
B) Debian
C) CentOS
D) Arch Linux

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Die richtige Antwort ist CentOS, weil diese Distribution zu Red Hat Enterprise Linux kompatibel ist, aber kostenlos genutzt werden kann.

**Antwort für die Prüfung:**
CentOS

</details>

---

## Frage 3

**Aufgabenstellung:**
Reverse DNS weist IP-Adressen Hostnamen zu. Wie wird der Name der IP-Adresse 198.51.100.165 auf einem DNS-Server gespeichert?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Reverse DNS bedeutet, einer IP-Adresse einen Namen zuzuweisen.
* Das geschieht über einen PTR-Record. Die IP wird dabei umgedreht und mit in-addr.arpa ergänzt.

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Die Adresse wird als PTR-Record für 165.100.51.198.in-addr.arpa gespeichert.

**Antwort für die Prüfung:**
In dem PTR-Record für 165.100.51.198.in-addr.arpa.

</details>

---

## Frage 4

**Aufgabenstellung:**
Welche der folgenden Bus-Typen kann Festplattenlaufwerke mit dem Motherboard verbinden?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Typische Bus-Typen für Festplatten sind SATA, SCSI, IDE.
* Überlege, welcher heute noch Standard ist.

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) PCIe
B) USB
C) SATA
D) HDMI

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Richtig ist SATA. SATA ist der aktuelle Standard-Bus für Festplatten und SSDs im PC-Bereich.

**Antwort für die Prüfung:**
Der SATA-Bus

</details>

---

## Frage 5

**Aufgabenstellung:**
Mit welchem der folgenden Befehle kann ein DNS-Name in eine IP-Adresse aufgelöst werden?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Es gibt Befehle wie `host`, `dig` oder `nslookup` für DNS-Abfragen.
* Teste zum Beispiel:

  ```bash
  host google.de
  ```

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Der Befehl `host` löst einen Namen auf eine IP-Adresse auf.

**Antwort für die Prüfung:**
host

</details>

---

## Frage 6

**Aufgabenstellung:**
Welche Informationen können mit dem Befehl `top` angezeigt werden?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* `top` ist ein Befehl zur Überwachung von Prozessen und Systemressourcen auf einem Linux-System.
* Schau dir die Spalten und Übersichten in der Ausgabe von `top` an.

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Laufende Prozesse und deren Ressourcenverbrauch
B) Auflistung installierter Softwarepakete
C) Liste aller User im System
D) Inhalt des Verzeichnisses /etc

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Die richtige Antwort ist: Laufende Prozesse und deren Ressourcenverbrauch.

**Antwort für die Prüfung:**
Laufende Prozesse und deren Ressourcenverbrauch.

</details>

---

## Frage 7

**Aufgabenstellung:**
Welche der folgenden Ausgaben stammt vom Befehl `free`?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Starte auf deinem Server `free -h`, um die typische Speicherübersicht zu sehen.
* Die Ausgabe zeigt RAM- und Swap-Belegung an.

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Auflistung von Prozessen und deren PID
B) Speicherstatistik: total, used, free, shared, buff/cache, available
C) Liste von Dateinamen
D) Informationen zu Netzwerkinterfaces

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Richtig ist die Speicherstatistik wie:

```
total        used        free      shared  buff/cache   available
Mem:            15Gi       2.3Gi         9Gi       910Mi       3.0Gi        11Gi
Swap:          2.0Gi          0B       2.0Gi
```

**Antwort für die Prüfung:**
Speicherstatistik: total, used, free, shared, buff/cache, available

</details>

---

## Frage 8

**Aufgabenstellung:**
Was trifft auf den Befehl `dmesg` zu?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* `dmesg` zeigt Kernel-Meldungen und Boot-Logs an.
* Probiere `dmesg | head` aus, um die ersten Zeilen zu sehen.

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

`dmesg` zeigt den Inhalt des Kernel-Ringpuffers an. Je nach Systemaktivität sind alte Einträge ggf. schon überschrieben.

**Antwort für die Prüfung:**
Es zeigt den Inhalt des Kernel-Ringpuffers an. Manche ältere Infos können durch neuere überschrieben werden.

</details>

---

## Frage 9

**Aufgabenstellung:**
Welche der folgenden Ausgaben könnte vom Befehl `last` stammen?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Starte `last` auf deinem System, um Anmeldeprotokolle zu sehen.
* Typische Ausgabe zeigt Benutzer, Terminal, Login- und Logout-Zeit.

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) root tty2 Wed May 17 21:11 - 21:11 (00:00)
B) PID Benutzer CPU Speicher
C) Hostname IP-Adresse
D) Dateiliste

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Beispiel-Ausgabe: `root tty2 Wed May 17 21:11 - 21:11 (00:00)` stammt von `last` und zeigt eine Anmeldung an.

**Antwort für die Prüfung:**
root tty2 Wed May 17 21:11 - 21:11 (00:00)

</details>

---

## Frage 10

**Aufgabenstellung:**
Was trifft auf den Besitzer einer Datei zu?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Mit `ls -l dateiname` kannst du dir den Besitzer einer Datei anschauen.
* Jede Datei gehört einem Benutzer und einer Gruppe.

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Eine Datei kann mehreren Benutzern gleichzeitig gehören.
B) Eine Datei hat genau einen Benutzer und eine Gruppe als Eigentümer.
C) Dateien haben keinen Besitzer.
D) Jede Datei gehört nur zu einem Verzeichnis.

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Die richtige Antwort ist: Eine Datei hat genau einen Benutzer und eine Gruppe als Eigentümer.

**Antwort für die Prüfung:**
Jede Datei gehört genau einem Benutzer und einer Gruppe.

</details>

---

## Frage 11

**Aufgabenstellung:**
Wie lauten die Zugriffsrechte einer regulären Datei, wenn die Berechtigungen mit dem Befehl `chmod 654 file.txt` gesetzt wurden?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Die Zahl steht für die Rechte: 6 = rw-, 5 = r-x, 4 = r--
* Reihenfolge: Benutzer, Gruppe, Andere.
* Nutze `ls -l file.txt` nach dem Setzen.

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Die Rechte sind: `-rw-r-xr--`

**Antwort für die Prüfung:**
-rw-r-xr--

</details>

---

## Frage 12

**Aufgabenstellung:**
Welche der folgenden Befehle können zum Archivieren und gleichzeitigen Komprimieren mit tar genutzt werden? (Mehrfachauswahl möglich – **zwei** Antworten richtig)

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Die Option `-z` steht für gzip-Kompression, `-j` für bzip2-Kompression.
* Beispiel: `tar -czf archiv.tar.gz ordner/` oder `tar -cjf archiv.tar.bz2 ordner/`

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) -z
B) -g
C) -z2
D) -bz
E) -j

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Richtig sind: -z und -j

**Antwort für die Prüfung:**
-z; -j

</details>

---

## Frage 13

**Aufgabenstellung:**
Wie lauten die Zugriffsrechte für das Verzeichnis `/tmp/`?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Nutze `ls -ld /tmp/` auf deinem System.
* Suche nach einem „t" am Ende der Rechte.

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Die Rechte sind: **rwxrwxrwt**

Das **"t"** am Ende ist das sogenannte Sticky-Bit. Es sorgt dafür, dass nur der Eigentümer einer Datei (oder root) diese im Verzeichnis löschen/umbenennen darf – auch wenn andere im Verzeichnis Schreibrechte haben. Das schützt die Dateien aller User in gemeinsam genutzten Verzeichnissen wie `/tmp/`.

**Antwort für die Prüfung:**
rwxrwxrwt

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Die Rechte sind: rwxrwxrwt

**Antwort für die Prüfung:**
rwxrwxrwt

</details>

---

## Frage 14

**Aufgabenstellung:**
Welche Informationen werden in der Datei `/etc/passwd` gespeichert?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Schau dir den Aufbau der Datei `/etc/passwd` an (z.B. mit `cat /etc/passwd | head -3`).
* Typische Infos sind Benutzername, UID, GID, Shell etc.

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Der Benutzername
B) Die UID (User ID)
C) Die Standard-Shell des Benutzers
D) Das Passwort im Klartext
E) Die Gruppe des Benutzers

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Gespeichert werden Benutzername, UID, Standard-Shell und weitere Informationen, aber **kein** Klartext-Passwort.

**Antwort für die Prüfung:**
Der Benutzername; Die UID (User ID); Die Standard-Shell des Benutzers

</details>

---

## Frage 15

**Aufgabenstellung:**
Mit welchem Befehl kann ein neuer Benutzer „tux“ angelegt werden, inklusive Erstellung des Home-Verzeichnisses mit Standard-Konfigurationsdateien?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>

* Prüfe mit `man useradd`, welche Optionen die Home-Verzeichnisse direkt anlegen.
* Typisch: Option `-m` bei useradd.

</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>

Mit `useradd -m tux` wird ein neuer Benutzer angelegt und das Home-Verzeichnis erstellt.

**Antwort für die Prüfung:**
useradd -m tux

</details>

---

## Frage 16

**Aufgabenstellung:**
Welcher der folgenden Befehle erstellt ein Archiv `work.tar` aus dem Inhalt des Verzeichnisses `./work/`?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) tar -cf work.tar ./work/
B) tar -xvf work.tar ./work/
C) tar -z work.tar ./work/
D) tar --list work.tar

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Schau dir `man tar` an.  
- Überlege, wie man mit tar ein Archiv erstellt.  
- Tipp: `-c` für create, `-f` für Dateiname.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist:  
tar -cf work.tar ./work/

**Antwort für die Prüfung:**
tar -cf work.tar ./work/

</details>

---

## Frage 17

**Aufgabenstellung:**
Das aktuelle Verzeichnis enthält folgende Datei:
`-rwxr-xr-x 1 root root 859688 Feb 7 08:15 test.sh`
Wie kann dieses Skript ausgeführt werden (das Skript ist gültig)?

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) bash test.sh
B) ./test.sh
C) sh < test.sh
D) source test.sh

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Die Datei ist ausführbar (`x`).  
- Du kannst Skripte direkt oder mit einem Interpreter starten.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig sind:  
A) bash test.sh  
B) ./test.sh

**Antwort für die Prüfung:**
bash test.sh; ./test.sh

</details>

---

## Frage 18

**Aufgabenstellung:**
Welche Taste kann gedrückt werden, um das Programm `less` zu beenden?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) e
B) q
C) z
D) x

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Starte z. B. `less /etc/passwd` und probiere verschiedene Tasten aus.  
- Achte auf die Hinweise am unteren Rand von less.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist:  
q

**Antwort für die Prüfung:**
q

</details>

---

## Frage 19

**Aufgabenstellung:**
Welches Schlüsselwort wird in einem Shell-Skript verwendet, um eine Schleife zu beginnen? (Bitte **nur ein** Stichwort!)

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Erstelle ein Testskript mit einer Schleife.  
- Bekannte Schleifen in Bash: for, while, until
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Das Schlüsselwort ist:  
for

**Antwort für die Prüfung:**
for

</details>

---

## Frage 20

**Aufgabenstellung:**
Mit welchem der folgenden Befehle kann nach der Datei `foo.txt` im Verzeichnis `/home` gesucht werden?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) find /home -name foo.txt
B) search /home foo.txt
C) grep foo.txt /home
D) locate /home/foo.txt

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Schau dir den Befehl `find` an.  
- Tipp: Die Option `-name` sucht nach Dateinamen.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist:  
find /home -name foo.txt

**Antwort für die Prüfung:**
find /home -name foo.txt

</details>

---

## Frage 21

**Aufgabenstellung:**
Ein Verzeichnis enthält die Dateien: a.txt und b.txt. Was gibt folgendes Shell-Skript aus?

```bash
for file in *.txt; do echo $file; done
```

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, was der Platzhalter *.txt macht.
- Das Skript geht alle passenden Dateien durch und gibt den Namen aus.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Das Skript gibt Folgendes aus:
a.txt
b.txt

**Antwort für die Prüfung:**
a.txt b.txt

</details>

---

## Frage 22

**Aufgabenstellung:**
Du erhältst beim Ausführen von `./test.sh` folgende Fehlermeldung:

```
bash: ./test.sh: Permission denied
```

Die Datei sieht so aus: `-rw-r--r-- 1 root exec 24551 Apr 2 12:36 test.sh`. Was muss getan werden, damit das Skript ausführbar ist?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Die Datei nach /usr/bin verschieben
B) Den Besitzer auf root setzen
C) Das Ausführungsbit setzen
D) Die Datei mit bash starten

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe die Dateirechte (`ls -l`).
- Zum Ausführen braucht die Datei ein x (execute) in den Rechten.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die Datei braucht das Ausführungsbit (x) gesetzt.

**Antwort für die Prüfung:**
Das Ausführungsbit sollte im Dateirecht gesetzt werden.

</details>

---

## Frage 23

**Aufgabenstellung:**
Mit welchem Befehl kann die Ausgabe von `export-logs` sortiert werden?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) export-logs | sort
B) export-logs sort
C) sort export-logs
D) sort < export-logs

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, wie du die Ausgabe eines Befehls in einen anderen schickst (Pipe).
- Schau dir die Syntax von sort an.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist:
export-logs | sort

**Antwort für die Prüfung:**
export-logs | sort

</details>

---

## Frage 24

**Aufgabenstellung:**
Was ist eine Linux-Distribution?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Ein einzelner Kernel
B) Ein Paket aus Kernel, Systemtools und Software
C) Nur ein Desktop-Umgebung
D) Ein Windows-Ersatz

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Lies die Definition einer Distribution z.B. in Wikipedia nach.
- Überlege, was alles zu Ubuntu, Fedora etc. gehört.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist: Ein Paket aus Kernel, Systemtools und Software.

**Antwort für die Prüfung:**
Ein Bündel aus Kernel, Systemwerkzeugen und weiterer Software.

</details>

---

## Frage 25

**Aufgabenstellung:**
Wo befindet sich bei einem Raspberry Pi das Betriebssystem?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Auf einer eingebauten SSD
B) Im Netzwerk
C) Auf einer entnehmbaren SD-Karte
D) Im RAM

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, wie du ein System auf dem Raspberry Pi installierst.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Das Betriebssystem liegt auf einer entnehmbaren SD-Karte.

**Antwort für die Prüfung:**
Auf einer entnehmbaren SD-Karte, die in den Raspberry Pi gesteckt wird.

</details>

---

## Frage 26

**Aufgabenstellung:**
Welches Programm ist ein grafischer Editor für Vektorgrafiken?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) GIMP
B) Inkscape
C) Audacity
D) LibreOffice Writer

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Suche nach Open-Source-Vektor-Editoren.
- Welches Programm ist auf SVG spezialisiert?
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist: Inkscape.

**Antwort für die Prüfung:**
Inkscape

</details>

---

## Frage 27

**Aufgabenstellung:**
Welches Paketmanagement-Tool wird bei Red Hat-basierten Systemen eingesetzt?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) apt
B) yum
C) rpm
D) dpkg

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Suche nach Paketverwaltung für CentOS und RHEL.
- rpm und yum werden beide genutzt, rpm ist das Standard-Tool.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist: rpm

**Antwort für die Prüfung:**
rpm

</details>

---

## Frage 28

**Aufgabenstellung:**
Welches Zeichen im Shell-Prompt weist darauf hin, dass die Shell mit Root-Rechten läuft?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) \$
B) #
C) %
D) @

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Melde dich als root und als normaler User an, beachte das Prompt-Zeichen.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Das Zeichen ist: #

**Antwort für die Prüfung:**

#

</details>

---

## Frage 29

**Aufgabenstellung:**
Welche Dienste werden typischerweise von Public-Cloud-Anbietern angeboten? (Mehrfachauswahl möglich – **drei** Antworten richtig)

**Multiple Choice (Es sind **drei** Antworten richtig):**
A) Infrastructure as a Service (IaaS)
B) Platform as a Service (PaaS)
C) Netzwerk als Dienst (NaaS)
D) Software as a Service (SaaS)
E) Office as a Service (OaaS)

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Informiere dich über typische Abkürzungen im Cloud-Bereich.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig sind: IaaS, PaaS, SaaS

**Antwort für die Prüfung:**
Infrastructure as a Service (IaaS); Platform as a Service (PaaS); Software as a Service (SaaS)

</details>

---

## Frage 30

**Aufgabenstellung:**
Was regelt eine Free Software-Lizenz?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Die Bedingungen für das Verändern und Weitergeben der Software
B) Die Hardwarevoraussetzungen
C) Die garantierte Verfügbarkeit
D) Die Installation

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Recherchiere, was Open-Source-Lizenzen bedeuten.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die Lizenz regelt, wie die Software genutzt, verändert und weitergegeben werden darf.

**Antwort für die Prüfung:**
Bedingungen für das Verändern und Weitergeben der Software.

</details>

---

## Frage 31

**Aufgabenstellung:**
Der Befehl `rm Downloads` führt zu folgender Fehlermeldung:

```
rm: cannot remove 'Downloads/': Is a directory
```

Welche der folgenden Befehle kannst du stattdessen nutzen, um das Verzeichnis zu entfernen (angenommen, es ist leer)?

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) rm -r Downloads
B) rmdir Downloads
C) del Downloads
D) rm Downloads /

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Der Standard-rm-Befehl funktioniert bei Verzeichnissen nicht ohne Option.  
- rmdir löscht nur leere Verzeichnisse.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig sind: rm -r Downloads und rmdir Downloads

**Antwort für die Prüfung:**
rm -r Downloads; rmdir Downloads

</details>

---

## Frage 32

**Aufgabenstellung:**
Was ist bei einem rekursiven Verzeichnislisting der Unterschied zur normalen Anzeige?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Es werden alle Dateien angezeigt, aber keine Verzeichnisse
B) Es werden auch Inhalte von Unterverzeichnissen angezeigt
C) Es wird nur das aktuelle Verzeichnis angezeigt
D) Es werden nur leere Verzeichnisse angezeigt

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, was die Option -R bei ls macht.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Bei einem rekursiven Listing werden auch die Inhalte von Unterverzeichnissen angezeigt.

**Antwort für die Prüfung:**
Es werden auch Inhalte von Unterverzeichnissen angezeigt.

</details>

---

## Frage 33

**Aufgabenstellung:**
Wie kannst du Informationen zur richtigen Verwendung des Befehls `ls` erhalten?

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) man ls
B) info ls
C) ls --docs
D) usage ls

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, wie du unter Linux Hilfe zu Befehlen bekommst (Manpages etc.).
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig sind: man ls und info ls

**Antwort für die Prüfung:**
man ls; info ls

</details>

---

## Frage 34

**Aufgabenstellung:**
In welchem Verzeichnis befinden sich typischerweise Informationen, Dokumentation und Beispiel-Konfigurationsdateien installierter Softwarepakete?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) /etc
B) /usr/share/doc/
C) /home
D) /var/log

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, wo Dokumentation von installierten Programmen zu finden ist (z.B. über apt).
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist: /usr/share/doc/

**Antwort für die Prüfung:**
/usr/share/doc/

</details>

---

## Frage 35

**Aufgabenstellung:**
Ein Benutzer befindet sich im Verzeichnis `/home/user/Downloads/` und führt folgenden Befehl aus:
`ls ../Documents/`
Welcher Verzeichnisinhalt wird angezeigt (sofern vorhanden)?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) /home/user/Downloads/Documents/
B) /home/user/Documents/
C) /home/Documents/
D) /Documents/

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, wie relative Pfade mit `..` funktionieren.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Der Inhalt von /home/user/Documents/ wird angezeigt.

**Antwort für die Prüfung:**
/home/user/Documents/

</details>

---

## Frage 36

**Aufgabenstellung:**
Wie kannst du das Verzeichnis `/new/dir/` zur PATH-Umgebungsvariablen hinzufügen?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) PATH=\$PATH:/new/dir
B) export PATH=/new/dir:\$PATH
C) set PATH=/new/dir:\$PATH
D) PATH = \$PATH:/new/dir

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Die richtige Lösung funktioniert sofort im aktuellen Terminal.
- Achte auf das `export` und die richtige Reihenfolge.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist: export PATH=/new/dir:$PATH

**Antwort für die Prüfung:**
export PATH=/new/dir:\$PATH

</details>

---

## Frage 37

**Aufgabenstellung:**
Ein Verzeichnis enthält die drei Dateien: texts 1.txt, texts 2.txt, texts 3.csv. Mit welchem Befehl kopierst du die beiden Dateien, die auf .txt enden, ins Verzeichnis `/tmp/`?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) cp *.txt /tmp/
B) cp *.csv /tmp/
C) cp texts* /tmp/
D) cp /tmp/*.txt .

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, wie Wildcards funktionieren und prüfe die Endung.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: cp *.txt /tmp/

**Antwort für die Prüfung:**
cp \*.txt /tmp/

</details>

---

## Frage 38

**Aufgabenstellung:**
Mit welchem Zeichen kannst du einen langen Befehl in der Shell umbrechen?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A)&#x20;
B) /
C) |
D) \_

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Schreibe einen langen Befehl und teste die verschiedenen Zeichen.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Das richtige Zeichen ist: \

**Antwort für die Prüfung:**  \\

</details>

---

## Frage 39

**Aufgabenstellung:**
Welcher der folgenden DNS-Record-Typen enthält eine IP-Adresse? (Es sind **zwei** Antworten richtig)

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) A
B) AAAA
C) MX
D) TXT

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe die Bedeutung von DNS-Typen A, AAAA, MX, TXT.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
A und AAAA halten IP-Adressen (A für IPv4, AAAA für IPv6).

**Antwort für die Prüfung:**
A; AAAA

</details>

---

## Frage 40

**Aufgabenstellung:**
Welcher der folgenden Werte könnte eine Prozess-ID (PID) unter Linux sein?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) 0
B) 21398
C) -1
D) 65536

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, wie PIDs aufgebaut sind und ob sie negativ/0 sein können.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Eine typische PID ist: 21398

**Antwort für die Prüfung:**
21398

</details>

---
