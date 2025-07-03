Woche 1, Tag 3 — Benutzer‑ & Gruppen‑Grundlagen (Linux Essentials 1.6)
Ziel: Verstehe die Konzepte hinter Benutzerkonten, UIDs/GIDs & Zugriffskontroll‑Dateien, bevor wir mit praktischer Verwaltung fortfahren.

## 0 · Lernziele

* **Benutzer‑ & Kontotypen** (root, regulär, System‑ & Service‑Accounts) unterscheiden
* **UID/GID‑Räume** & ihr Zweck erklären
* **Wichtige Zugriffskontrolldateien** in `/etc` aufzählen & beschreiben
* **CLI‑Tools** einsetzen, um Informationen über Benutzer & Anmeldungen abzurufen

---

## 1 · Einführung in Zugriffskontrollen (5 min)

Linux erbt die Unix-Access-Control von 1970 — immer noch schlank & effektiv. Moderne Desktop-Umgebungen setzen vieles automatisch, doch das Fundament bleibt unverändert:

```mermaid
graph TD
  OS[Linux‑Kernel] -->|fragt| AC[Unix ACL]
  AC --> UID[UID]
  AC --> GID[GID]
  AC --> PERM[rwx]
  PERM --> DECISION{Zugriff erlaubt?}
```

---

## 2 · Kontotypen & UID‑Bereiche (20 min)

| Kontotyp         | UID‑Range (üblich) | Home    | Shell              | Beispiel          |
| ---------------- | ------------------ | ------- | ------------------ | ----------------- |
| **root**         | 0                  | `/root` | `/bin/bash`        | root              |
| **System (alt)** | 1–99 (oder <100)   | —       | `/sbin/nologin`    | daemon, bin       |
| **System (neu)** | 100–499            | —       | `/sbin/nologin`    | systemd‑network   |
| **Service**      | 500–999 oder >1000 | var.    | `/sbin/nologin`    | postgres (Fedora) |
| **Benutzer**     | ≥ 1000             | `/home` | `/bin/bash` (std.) | emma              |


## 2.1 · Set-GID-Bit auf Verzeichnisse (5 min)

| Aktion                         | Befehl                          | Wirkung                                                                                 |
|--------------------------------|---------------------------------|-----------------------------------------------------------------------------------------|
| Set-GID auf Verzeichnis setzen | `sudo chmod g+s <Verzeichnis>` | Neu angelegte Dateien erben die GID des Verzeichnisses und erhalten so gruppenweite Rechte |

> **Hinweis:** In der `ls -l`-Ausgabe erscheint dann ein kleines `s` im Gruppen-bit, z. B. `drwxr-s r-x`.

**Primäre & sekundäre Gruppen**

* Primäre GID bestimmt Datei‑Besitz bei Anlage
* Sekundäre Gruppen bündeln zusätzliche Rechte

---

## 3 · Schlüssel‑Dateien in `/etc` (15 min)

| Datei          | Inhalt (gekürzt)                      | Wer darf lesen? |
| -------------- | ------------------------------------- | --------------- |
| `/etc/passwd`  | UID, GID, Home, Shell, kein Hash      | alle            |
| `/etc/shadow`  | Passwort‑Hashes, Ablaufdaten          | root, authd     |
| `/etc/group`   | Gruppenname ↔ GID, Mitglieder         | alle            |
| `/etc/gshadow` | Gruppen‑Hashes, Admin‑Listen          | root            |
| `/etc/sudoers` | sudo‑Regeln (via `visudo` bearbeiten) | root            |

```mermaid
erDiagram
  passwd ||--|| shadow : "USERNAME key"
  group  ||--|| gshadow : "GROUPNAME key"
```

---

## 4 · CLI‑Infos abrufen (10 min)

| Zweck            | Befehl           | Sample‑Output (gekürzt)     |
| ---------------- | ---------------- | --------------------------- |
| Eigene IDs sehen | `id`             | `uid=1000(emma) gid=1000 …` |
| Andere anzeigen  | `id bob`         | —                           |
| Aktive Logins    | `who` / `w`      | TTY, Idle, Cmd              |
| Login‑Historie   | `last` / `lastb` | erfolgreich / fehlgeschl.   |

Tipp: Nutze `last -F | head` für die letzten 10 Events mit Zeitstempel.

---

## 5 · Mini‑Übung (2 min)

> *Keine Änderungen am System! Nur lesen & beobachten.*

1. Zeige alle Konten mit UID < 100 an:

   ```bash
   awk -F: '$3<100 {print $1,$3}' /etc/passwd
   ```

2. Notiere die GIDs der Gruppen, in denen du Mitglied bist:

   ```bash
   id -Gn
   id -G
   ```

---

## 6 · Reflexions‑Fragen (5 min)

* Warum ist `/etc/passwd` für alle lesbar, `/etc/shadow` aber nicht?
* Welche Risiken birgt ein Service‑Account mit gültiger Bash‑Shell?

---

# Übungsaufgaben: User-Management

## 1. User anlegen & prüfen

**Aufgabe:** Lege den Nutzer **bernd** an, inklusive Home-Verzeichnis und Bash-Shell.
**Prüfen:** Ermittele anschließend mit den passenden Befehlen, welche UID, GID und Gruppen **bernd** zugewiesen sind.

## 2. Passwort setzen & testen

**Aufgabe:** Vergib für **bernd** ein Passwort und wechsle in seinen Benutzerkontext.
**Test:** Erstelle in seinem Home-Verzeichnis eine Datei `~/.login_test` und wechsle zurück zum Admin.

## 3. Datei-Eigentümer prüfen

**Aufgabe:** Lege als Admin eine Bashdatei mit echo "hello world" unter `/home` an und weise sie **bernd** als Eigentümer zu. Setze gezielt (chmod) die Gruppen- und Benutzerrechte so das Bernd die Datei nicht ausführen kann.
**Test:** Melde dich als **bernd** an und prüfe Lese- und Schreib und Ausführrechte der Datei.

## 4. Gruppe anlegen & User hinzufügen

**Aufgabe:** Erstelle die Gruppe **projekt** und füge **bernd** als Sekundärmitglied hinzu.
**Prüfen:** Überprüfe anschließend, dass **bernd** wirklich Teil der Gruppe **projekt** ist.

## 5. Aufräumen: User & Gruppe löschen

**Aufgabe:** Entferne **bernd** aus der Gruppe **projekt**, lösche den Benutzer **bernd** mitsamt seinem Home-Verzeichnis und entferne abschließend die Gruppe **projekt**.


# Übungsaufgaben: Gruppen-Management

## 1. Gruppe anlegen & Eigenschaften prüfen

**Aufgabe:** Erstelle die Gruppe **marketing**.
**Prüfen:** Welche GID und Einträge existieren für **marketing**? Nutze die passenden Befehle, um das zu ermitteln.

## 2. Benutzer zur Gruppe hinzufügen & entfernen

**Aufgabe:** Füge den bestehenden Benutzer **bernd** zur Gruppe **marketing** hinzu und entferne ihn anschließend wieder.
**Prüfen:** Wie überprüfst du, dass **bernd** zur Gruppe gehört bzw. nicht mehr dazugehört?

## 3. Primäre Gruppe ändern

**Aufgabe:** Lege die Gruppe **support** an und setze sie als primäre Gruppe von **bernd**.
**Prüfen:** Wie kannst du via `id` oder anderen Befehlen bestätigen, dass die GID jetzt zu **support** gehört?

## 4. Set-GID auf Verzeichnis anwenden

**Aufgabe:** Erstelle ein Verzeichnis `/srv/team_docs` und aktiviere das Set-GID-Bit (chmod g+s ).
**Prüfen:** Wie kannst du zeigen, dass neu erstellte Dateien im Verzeichnis die Gruppen-ID von `/srv/team_docs` geerbt haben?

## 5. Gruppe umbennen & löschen

**Aufgabe:** Benenne die Gruppe **support** in **helpdesk** um, lege einen Dummy-Benutzer **tester** an, füge ihn zu **helpdesk** hinzu und überprüfe die Umbenennung.
**Aufräumen:** Lösche abschließend sowohl die Gruppe **helpdesk** als auch den Dummy-Benutzer.

> **Hinweis:** Nutzt für alle Befehle `sudo` und kontrolliert jeden Schritt mit `getent`, `id`, `groups` oder `ls -l`. Viel Erfolg!

## 9 · Schatten im Tänzelnden Pony (40 min)
![Frodo](frodo.png)

Tipp: versuchts mal ohne ChatGPT und nur mit Google

> **Filmszene:** Regen peitscht gegen die Schindeln, als Frodo und seine Gefährten das lichtdurchflutete Schankzimmer des **Tänzelnden Pony** betreten. Butterblume wischt sich die Hände an der Schürze ab und ruft: »Hobbits!«, woraufhin neugierige Köpfe hochfahren. In einer dunklen Ecke aber glimmt bereits das rote Auge des Feindes …

### Setup – das Wirtshaus füllt sich

* **Zwei Gestalten**: Lege frische Konten für **Frodo** und **Sauron** an.
* **Die Runde der Zecher**: Schaffe die Gruppe **wirtshaus** und lege Samwise, Merry, Pippin und ein paar unbekannte Halblinge samt Sauron dort an.
* **Der Eine Ring**: Erstelle im Heimverzeichnis Frodos eine Datei namens `ring`, die nur ihm gehört. Und schreibe den Text **„One Ring to rule them all“** hinein.

> *Gandalf hatte gewarnt:* »Hüte dich vor neugierigen Blicken – sogar Bier kann die Zunge lösen.«

---

### 1 · Frodo betritt das Wirtshaus

Füge Frodo der fröhlichen Truppe in **wirtshaus** hinzu und vergewissere dich – etwa mit einem Blick in die Gruppendatei –, dass er nun am Schank­tisch sitzt.

### 2 · Der erste Griff nach dem Ring

Im Gewirr der Musik rutscht Frodo der Ring an den Finger. 

* Schaffe eine neue Geheimbund‑Gruppe **ring**. 
* Übertrage die *Besitzrechte* der Datei `ring` auf diese Bruderschaft und erlaube ausschließlich ihren Mitgliedern das Lesen. 
* Nimm Frodo in die Gruppe auf – er verschwindet für die Gäste förmlich aus dem Blickfeld.

> *Frodo hört ein Flüstern:* »Ein Ring, sie zu knechten …«

### 3 · Das Auge entdeckt ihn

Der Schatten in der Ecke richtet sich auf – Sauron verspürt die Präsenz des Rings.
\* Füge **Sauron** derselben Gruppe **ring** hinzu, damit auch er den verführerischen Glanz erblickt. \* Prüfe aus Saurons Perspektive mit cat, dass die verborgene Datei Ring nun lesbar ist.

### 4 · Der Schreck und die Entsagung

Frodo schreckt auf, zieht den Ring hastig ab. Entziehe der Datei `ring` die Gruppenzugehörigkeit zu **ring** oder ersetze sie durch Frodos Privatgruppe. 
 Entferne Sauron wieder aus der Geheimgilde. 

### 5 · Schweigen des Feindes

Ein letzter Test aus Saurons Sicht sollte nun ins Leere laufen – kein *`cat`* enthüllt mehr das Geheimnis. Das Auge schließt sich, und das Wirtshaus kehrt zum Klang der Fiedel zurück.

> **Ergebnis:** Wie im Film erweckt Frodo mit einem unbeabsichtigten Schritt die Aufmerksamkeit des Feindes – doch rechtzeitig gelingt es ihm, den Blick Saurons wieder zu trüben.
