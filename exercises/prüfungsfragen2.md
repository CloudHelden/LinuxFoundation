# Linux Essentials – Fragen 41 bis 80

Hier findest du zwanzig weitere typische Prüfungsfragen aus dem Bereich Linux Essentials – Multiple Choice sofort sichtbar, Hilfen und Lösungen zum Einklappen.

---

## Frage 41

**Aufgabenstellung:**
Welches Protokoll wird für die automatische IP-Adressvergabe in Netzwerken verwendet?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) DHCP
B) DNS
C) FTP
D) NFS

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, welches Protokoll PCs ihre IP-Adresse im LAN zuweist.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist: DHCP

**Antwort für die Prüfung:**
DHCP

</details>

---

## Frage 42

**Aufgabenstellung:**
Welches der folgenden Geräte bezeichnet eine Festplattenpartition?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) /dev/sda2
B) /mnt/usb
C) /dev/ttyS0
D) /proc/cpuinfo

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, wie Festplattenpartitionen in Linux bezeichnet werden.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: /dev/sda2

**Antwort für die Prüfung:**
/dev/sda2

</details>

---

## Frage 43

**Aufgabenstellung:**
Was trifft auf Linux Hardware-Treiber zu?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Treiber müssen immer extern installiert werden
B) Treiber sind nie Teil des Kernels
C) Treiber werden entweder als Kernel-Module geladen oder sind in den Kernel kompiliert
D) Treiber sind immer Open Source

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, wie Linux Treiber verwaltet (Kernel, Module).
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist: Treiber werden entweder als Kernel-Module geladen oder sind in den Kernel kompiliert.

**Antwort für die Prüfung:**
Treiber sind entweder in den Kernel kompiliert oder werden als Kernel-Modul geladen.

</details>

---

## Frage 44

**Aufgabenstellung:**
Was befindet sich im Verzeichnis `/proc/`?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Benutzerprofile
B) Ein Verzeichnis je laufendem Prozess
C) Backups
D) Systemprotokolle

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, was du mit `ls /proc/` siehst.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Im Verzeichnis /proc/ gibt es ein Verzeichnis pro laufendem Prozess.

**Antwort für die Prüfung:**
Ein Verzeichnis je laufendem Prozess.

</details>

---

## Frage 45

**Aufgabenstellung:**
Ein Server soll für mehrere Jahre Dienste bereitstellen und regelmäßig Sicherheitsupdates erhalten. Welche der folgenden Linux-Distributionen eignen sich hierfür? (Es sind **zwei** Antworten richtig)

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) Ubuntu Linux LTS
B) Gentoo
C) Red Hat Enterprise Linux
D) Arch Linux

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- LTS steht für „Long Term Support“.
- Red Hat ist für Stabilität und Langzeit-Support bekannt.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig sind: Ubuntu Linux LTS und Red Hat Enterprise Linux

**Antwort für die Prüfung:**
Ubuntu Linux LTS; Red Hat Enterprise Linux

</details>

---

## Frage 46

**Aufgabenstellung:**
Welches Verzeichnis muss mit Lese- und Schreibrechten gemountet sein, falls es auf einem eigenen Dateisystem liegt?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) /var
B) /usr
C) /etc
D) /bin

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, wo temporäre und sich ändernde Daten liegen.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: /var

**Antwort für die Prüfung:**
/var

</details>

---

## Frage 47

**Aufgabenstellung:**
Mit welchem Befehl wird die Eigentümerschaft einer Datei auf den Benutzer tux geändert?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) chgrp tux doku.odt
B) chown tux doku.odt
C) usermod tux doku.odt
D) setuser tux doku.odt

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe die Syntax der verschiedenen Kommandos zum Ändern von Besitzern.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: chown tux doku.odt

**Antwort für die Prüfung:**
chown tux doku.odt

</details>

---

## Frage 48

**Aufgabenstellung:**
Was passiert mit einer Datei außerhalb des Home-Verzeichnisses, wenn das Benutzerkonto gelöscht wird?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Die Datei wird ebenfalls gelöscht
B) Die Datei wird verschlüsselt
C) Die Datei bleibt bestehen, als Eigentümer steht die ehemalige UID
D) Die Datei wird dem Administrator übertragen

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, was mit verwaisten Dateien im System geschieht.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die Datei bleibt bestehen, als Eigentümer steht die ehemalige UID.

**Antwort für die Prüfung:**
Die UID des ehemaligen Besitzers wird als Eigentümer angezeigt, Rechte bleiben erhalten.

</details>

---

## Frage 49

**Aufgabenstellung:**
Was ist die Funktion des Verzeichnisses `/etc/skel`?

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) Es enthält Standard-Konfigurationsdateien für neue Benutzer
B) Es speichert Backup-Dateien aller User
C) Dateien werden bei der Benutzererstellung ins Home kopiert
D) Es enthält die Root-Passwörter im Klartext

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Schau nach, was /etc/skel bei „useradd“ macht.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
A und C sind richtig: /etc/skel enthält die Vorlagen für neue Home-Verzeichnisse, diese werden beim Anlegen eines Benutzers kopiert.

**Antwort für die Prüfung:**
Es enthält Standard-Konfigurationsdateien; Sie werden bei Benutzererstellung ins Home kopiert.

</details>

---

## Frage 50

**Aufgabenstellung:**
Was ist über symbolische Links im Linux-Dateisystem korrekt?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Ein symbolischer Link kann auf eine Datei auf einem anderen Dateisystem zeigen
B) Ein symbolischer Link kann nur auf lokale Dateien zeigen
C) Symbolische Links sind fest mit einer Inode verbunden
D) Symbolische Links erhöhen die Dateigröße massiv

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, was ein „symlink“ ist und ob er auf alles zeigen kann.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: Ein symbolischer Link kann auf eine Datei auf einem anderen Dateisystem zeigen.

**Antwort für die Prüfung:**
Ein symbolischer Link kann auf eine Datei auf einem anderen Dateisystem zeigen.

</details>

---

## Frage 51

**Aufgabenstellung:**
Welche Dateien liefern die Informationen für folgenden Output?

```
uid=1000 (bob) gid=1000 (bob) groups=1000 (bob), 10 (wheel), 150 (wireshark), 989 (docker), 1001 (libvirt)
```

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) /etc/passwd
B) /etc/shadow
C) /etc/group
D) /etc/hostname

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, wo Unix User-IDs und Gruppen gespeichert werden.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die Informationen kommen aus: /etc/passwd und /etc/group

**Antwort für die Prüfung:**
/etc/passwd; /etc/group

</details>

---

## Frage 52

**Aufgabenstellung:**
Was kann mit dem Befehl `passwd` gemacht werden? (Es sind **zwei** Antworten richtig)

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) Passwort eines Users ändern
B) Account eines Users sperren
C) Einen neuen User anlegen
D) Die Gruppenmitgliedschaft ändern

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, welche passwd-Optionen es gibt.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Mit passwd kann das Passwort geändert und ein User gesperrt werden.

**Antwort für die Prüfung:**
Passwort ändern; Account sperren

</details>

---

## Frage 53

**Aufgabenstellung:**
Was macht der Befehl `su`?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Erstellt ein neues User-Konto
B) Wechselt die Shell oder führt einen Befehl als anderer User aus
C) Setzt ein neues Passwort
D) Startet ein Backup

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Probiere `su` in einer Testumgebung.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Mit su kann ein Befehl oder eine Shell als anderer User ausgeführt werden.

**Antwort für die Prüfung:**
Wechselt die Shell oder führt einen Befehl als anderer User aus

</details>

---

## Frage 54

**Aufgabenstellung:**
Wie lautet der Parameter von `ls`, um eine rekursive Auflistung zu erhalten? (Bitte nur die Option, ohne Werte!)

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die Option lautet: -R

**Antwort für die Prüfung:**
-R

</details>

---

## Frage 55

**Aufgabenstellung:**
Wie kannst du dir in der Regel eine Kurzübersicht (Hilfe) zu einem Linux-Befehl anzeigen lassen?

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) Befehl -h
B) Befehl --help
C) Befehl -?
D) Befehl /help

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Probiere verschiedene Hilfsoptionen aus, z.B. `ls -h` oder `ls --help`.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
-h und --help liefern meistens eine Hilfeübersicht

**Antwort für die Prüfung:**
-h; --help

</details>

---

## Frage 56

**Aufgabenstellung:**
Welcher Befehl zeigt den absoluten Pfad des aktuellen Arbeitsverzeichnisses an?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) cd
B) ls
C) pwd
D) echo \$PATH

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, was pwd macht.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Der Befehl ist: pwd

**Antwort für die Prüfung:**
pwd

</details>

---

## Frage 57

**Aufgabenstellung:**
Wie kann der Inhalt der Datei `Texts 2.txt` angezeigt werden? (Es sind **zwei** Antworten richtig)

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) cat 'Texts 2.txt'
B) cat Texts\ 2.txt
C) cat Texts\_2.txt
D) cat < Texts 2.txt

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, wie man mit Leerzeichen in Dateinamen umgeht.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig sind: cat 'Texts 2.txt' und cat Texts\ 2.txt

**Antwort für die Prüfung:**
cat 'Texts 2.txt'; cat Texts\ 2.txt

</details>

---

## Frage 58

**Aufgabenstellung:**
Welcher Befehl zeigt nur Dateinamen, aber keine weiteren Infos an?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) ls -a
B) ls -l
C) cat -n
D) head -n 1

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, was die verschiedenen ls-Optionen machen.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die richtige Antwort ist: ls -a

**Antwort für die Prüfung:**
ls -a

</details>

---

## Frage 59

**Aufgabenstellung:**
Wofür dient die PATH-Umgebungsvariable?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Sie enthält den Verlauf aller ausgeführten Befehle
B) Sie erlaubt die Ausführung von Kommandos ohne Pfadangabe
C) Sie speichert das aktuelle Arbeitsverzeichnis
D) Sie hält die letzten zehn Befehle bereit

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Probiere: echo $PATH; führe ein Kommando aus, das nicht im Standardpfad liegt.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Sie erlaubt die Ausführung von Kommandos ohne Pfadangabe.

**Antwort für die Prüfung:**
Sie erlaubt die Ausführung von Kommandos ohne Pfadangabe.

</details>

---

## Frage 60

**Aufgabenstellung:**
Wie weist man die Variable USERNAME den Wert bob zu?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) USERNAME=bob
B) set USERNAME=bob
C) USERNAME==bob
D) export=USERNAME\:bob

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Probiere in der Shell verschiedene Zuweisungen aus.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: USERNAME=bob

**Antwort für die Prüfung:**
USERNAME=bob

</details>

---

## Frage 61

**Aufgabenstellung:**
Wie heißt das Kommando zur Anzeige von Handbuchseiten (Manual Pages)?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) help
B) manual
C) man
D) info

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Probiere verschiedene Befehle aus: help, man, info usw.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Der Befehl ist: man

**Antwort für die Prüfung:**
man

</details>

---

## Frage 62

**Aufgabenstellung:**
Wie kopiert man alle Inhalte von /etc/ samt Unterverzeichnissen nach /root/?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) cp -r /etc/\* /root
B) cp /etc/ /root
C) copy -r /etc/ /root/
D) mv /etc /root/

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe den Unterschied zwischen cp und cp -r.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: cp -r /etc/* /root

**Antwort für die Prüfung:**
cp -r /etc/\* /root

</details>

---

## Frage 63

**Aufgabenstellung:**
Wie kann man die Zeilen einer Datei alphabetisch sortieren lassen?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) sort datei.txt
B) order datei.txt
C) cat datei.txt | sort -r
D) echo sort datei.txt

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Probiere verschiedene Kommandos zum Sortieren aus.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
sort datei.txt sortiert die Zeilen alphabetisch.

**Antwort für die Prüfung:**
sort datei.txt

</details>

---

## Frage 64

**Aufgabenstellung:**
Welches Beispiel zeigt den allgemeinen Aufbau einer for-Schleife im Shell-Skript?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) for file in *.txt; do echo \$i; done
B) for do echo \$file; done
C) foreach file (*.txt) { echo \$file }
D) loop i = 1 to 10

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Vergleiche typische Shell-Syntax in Bash.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: for file in *.txt; do echo $i; done

**Antwort für die Prüfung:**
for file in \*.txt; do echo \$i; done

</details>

---

## Frage 65

**Aufgabenstellung:**
Welcher Operator im regulären Ausdruck steht dafür, dass das vorherige Zeichen null- oder einmal vorkommen darf?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) \*
B) +
C) ?
D) |

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Probiere einfache Regex-Beispiele aus: z.B. "a?b", "ab?c".
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Das Fragezeichen ?

**Antwort für die Prüfung:**
?

</details>

---

## Frage 66

**Aufgabenstellung:**
Wie macht man die Variable MYVAR so verfügbar, dass script.sh ihren Wert anzeigen kann?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) export MYVAR=value
B) set MYVAR=value
C) assign MYVAR=value
D) expose MYVAR=value

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, wie Umgebungsvariablen "vererbt" werden.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: export MYVAR=value

**Antwort für die Prüfung:**
export MYVAR=value

</details>

---

## Frage 67

**Aufgabenstellung:**
Welchen Rückgabewert hat ein Shell-Skript nach erfolgreicher Ausführung?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) 1
B) 0
C) 255
D) -1

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überprüfe den Wert mit "echo $?" nach erfolgreichen Kommandos.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: 0

**Antwort für die Prüfung:**
0

</details>

---

## Frage 68

**Aufgabenstellung:**
Wie erzeugt man das ZIP-Archiv poems.zip mit allen .txt-Dateien im aktuellen Verzeichnis?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) zip poems.zip \*.txt
B) zip \*.txt poems.zip
C) zip -cfz poems.zip \*.txt
D) zcat \*.txt poems.zip

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, wie zip-Befehle funktionieren (zip --help).
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: zip poems.zip *.txt

**Antwort für die Prüfung:**
zip poems.zip \*.txt

</details>

---

## Frage 69

**Aufgabenstellung:**
Was trifft auf ein typisches Shell-Skript zu? (Es sind **zwei** Antworten richtig)

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) Es hat das Ausführungsrecht (x)
B) Es startet mit der Zeichenfolge #!
C) Es beginnt mit <html>
D) Es benötigt kein Ausführungsrecht

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Schaue dir den Aufbau von Shell-Skripten an, z.B. mit "cat script.sh"
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig sind: Es hat das Ausführungsrecht und startet mit #!

**Antwort für die Prüfung:**
Es hat das Ausführungsrecht (x); Es startet mit #!

</details>

---

## Frage 70

**Aufgabenstellung:**
Wie extrahierst du den Inhalt von file1.tar.gz?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) tar -czf file1.tar.gz
B) ztar file1.tar.gz
C) tar -xzf file1.tar.gz
D) tar --extract file1.tar.gz

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Probiere die verschiedenen tar-Optionen (tar --help).
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: tar -xzf file1.tar.gz

**Antwort für die Prüfung:**
tar -xzf file1.tar.gz

</details>

---

## Frage 71

**Aufgabenstellung:**
Wie findet man alle Zeilen in der Datei operating-systems.txt, die den Begriff linux (unabhängig von Groß-/Kleinschreibung) enthalten?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) grep linux operating-systems.txt
B) grep -i linux operating-systems.txt
C) grep -c linux operating-systems.txt
D) find linux operating-systems.txt

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Schau dir die grep-Optionen für "case insensitive" an.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: grep -i linux operating-systems.txt

**Antwort für die Prüfung:**
grep -i linux operating-systems.txt

</details>

---

## Frage 72

**Aufgabenstellung:**
Was ist bei Passwörtern auf einem Linux-System korrekt?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Passwörter werden im Klartext gespeichert
B) Passwörter werden nur als Hash gespeichert
C) Passwörter werden nie gespeichert
D) Passwörter stehen in /etc/group

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, wie Passwörter in /etc/shadow aussehen.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: Passwörter werden nur als Hash gespeichert

**Antwort für die Prüfung:**
Passwörter werden nur als Hash gespeichert.

</details>

---

## Frage 73

**Aufgabenstellung:**
Welche der folgenden Programme sind Webserver? (Es sind **zwei** Antworten richtig)

**Multiple Choice (Es sind **zwei** Antworten richtig):**
A) Apache
B) NGINX
C) Postfix
D) Samba

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Informiere dich über bekannte Open-Source-Webserver.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig sind: Apache und NGINX

**Antwort für die Prüfung:**
Apache; NGINX

</details>

---

## Frage 74

**Aufgabenstellung:**
Welche der folgenden Linux-Distributionen stammt von Red Hat Enterprise Linux ab?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) CentOS
B) Ubuntu
C) Debian
D) openSUSE

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Recherchiere, welche Distribution „binary compatible“ zu RHEL ist.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: CentOS

**Antwort für die Prüfung:**
CentOS

</details>

---

## Frage 75

**Aufgabenstellung:**
Was trifft auf freie Software zu?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Sie darf nur von Unternehmen verwendet werden
B) Sie darf von jedem geändert werden
C) Sie darf nicht verteilt werden
D) Sie muss kostenpflichtig sein

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe die Definition von „Free Software“ z.B. bei der FSF.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Sie darf von jedem geändert werden.

**Antwort für die Prüfung:**
Sie darf von jedem geändert werden.

</details>

---

## Frage 76

**Aufgabenstellung:**
Wie wird eine neue Linux-Instanz bei einem IaaS-Cloudanbieter bereitgestellt?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Der User installiert alles selbst von Grund auf
B) Der Anbieter stellt Images der beliebtesten Distributionen bereit
C) Alles wird ausschließlich per Container gemacht
D) Man braucht zwingend Windows-Lizenzen

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe die typische Bereitstellung bei AWS, Azure, Hetzner etc.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Der Anbieter stellt Images bereit.

**Antwort für die Prüfung:**
Der Anbieter stellt Images beliebter Linux-Distributionen bereit.

</details>

---

## Frage 77

**Aufgabenstellung:**
Was unterscheidet ein privates Browserfenster von einem normalen Fenster? (Es sind **drei** Antworten richtig)

**Multiple Choice (Es sind **drei** Antworten richtig):**
A) Es werden keine Cookies gespeichert
B) Keine Einträge im Browserverlauf
C) Es werden keine regulären Cookies gesendet
D) Passwörter werden nie gespeichert

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Vergleiche Incognito/Privatmodus in verschiedenen Browsern.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig sind: A, B und C

**Antwort für die Prüfung:**
Keine Cookies werden dauerhaft gespeichert; Kein Browserverlauf; Keine regulären Cookies werden gesendet.

</details>

---

## Frage 78

**Aufgabenstellung:**
Was ist die bevorzugte Quelle für die Installation neuer Anwendungen in einem Linux-Betriebssystem?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Die offizielle Webseite des Herstellers
B) Die Paketquelle (Repository) der Distribution
C) Github
D) Ein fremder USB-Stick

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Überlege, wie Updates und Sicherheit am besten gewährleistet sind.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Richtig ist: Die Paketquelle der Distribution

**Antwort für die Prüfung:**
Die Paketquelle (Repository) der Distribution

</details>

---

## Frage 79

**Aufgabenstellung:**
Was ist bei der Speicherung von Passwörtern in Linux besonders zu beachten?

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Recherchiere, wie /etc/shadow funktioniert.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Passwörter werden in gehashter Form gespeichert, niemals im Klartext.

**Antwort für die Prüfung:**
Passwörter werden nur als Hash gespeichert.

</details>

---

## Frage 80

**Aufgabenstellung:**
Was ist das Ziel einer Free-Software-Lizenz?

**Multiple Choice (Es ist **eine** Antwort richtig):**
A) Die Nutzung und Weitergabe zu erlauben, auch verändert
B) Die Nutzung strikt zu verbieten
C) Nur Firmen dürfen das Programm nutzen
D) Der Quelltext darf nicht verändert werden

**Hilfe:**

<details>
<summary>Klicken, um Hilfe anzuzeigen</summary>
- Prüfe, was unter GPL und anderen Lizenzen erlaubt ist.
</details>

**Lösung:**

<details>
<summary>Klicken, um die Lösung zu sehen</summary>
Die Nutzung, Veränderung und Weitergabe sind bei Free Software explizit erlaubt.

**Antwort für die Prüfung:**
Die Nutzung und Weitergabe ist auch verändert erlaubt.

</details>
