# Git Cheat Sheet (Grundbefehle)

| Befehl                          | Zweck                                              |
| ------------------------------- | -------------------------------------------------- |
| `git init`                      | Neues Git‑Repository initialisieren                |
| `git status`                    | Arbeits‑ und Staging‑Status anzeigen               |
| `git add .` / `git add <datei>` | Änderungen zum Staging‑Bereich hinzufügen          |
| `git commit -m "Nachricht"`     | Gestagte Änderungen festschreiben                  |
| `git log --oneline --graph`     | Historie kompakt anzeigen                          |
| `git branch`                    | Lokale Branches auflisten                          |
| `git branch <name>`             | Neuen Branch anlegen                               |
| `git switch <name>`             | Zu bestehendem Branch wechseln                     |
| `git switch -c <name>`          | Neuen Branch anlegen **und** direkt wechseln       |
| `git merge <name>`              | Branch *<name>* in aktuellen Branch zusammenführen |
| `git push`                      | Lokale Commits zum Remote‑Repo übertragen          |
| `git pull`                      | Änderungen vom Remote‑Repo holen                   |

---

## Aufgaben

### 1 · Lokales Repository mit Branches

* Lege ein neues lokales Git‑Repository an.
* Erstelle drei einzelne Commits, jeweils mit einer neuen Datei.
* Erstelle zwei neue Branches `test1` und `test2`.
* Füge in jedem der beiden Branches jeweils zwei weitere Commits hinzu.

### 2 · Arbeiten mit GitHub

* Lege auf GitHub ein neues (leeres) Repository an.
* Klone das Repository lokal.
* Lege lokal zwei neue Branches an.
* Erstelle in jedem Branch einen Commit.
* Push alle Branches und Commits zurück zu GitHub.

### 3 · Lokales Repo nachträglich hochladen

* Initialisiere ein neues Git‑Repository in einem bestehenden Projektordner.
* Erstelle einige Testdateien und committe sie.
* Richte auf GitHub ein neues (leeres) Repository ein.
* Verbinde dein lokales Repository mit dem Remote‑Repository auf GitHub und lade den aktuellen Stand hoch.
