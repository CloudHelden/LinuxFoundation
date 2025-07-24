# MkDocs Installation und Erste Schritte

## Installation

### Schritt 1: pipx installieren
```bash
brew install pipx
```

### Schritt 2: MkDocs mit Material Theme installieren
```bash
pipx install mkdocs-material --include-deps
```
*Dies installiert MkDocs automatisch mit dem beliebten Material Theme*

### Schritt 2.1: Deutsche Sprache vorbereiten (optional)
```bash
pipx install 'mkdocs[i18n]'
```

**Falls eine Warnung über Symlinks erscheint, ist das normal - funktioniert trotzdem!**

*Die deutsche Sprache wird später in der mkdocs.yml konfiguriert.*

### Schritt 3: PATH konfigurieren
```bash
pipx ensurepath
```

### Schritt 4: Terminal neu starten
- **Terminal komplett schließen**
- **Neues Terminal-Fenster öffnen**

Nach dem Neustart sollte `mkdocs` verfügbar sein!

---

## Erste Schritte mit MkDocs

### Neues Projekt erstellen
```bash
mkdocs new mein-projekt
cd mein-projekt
```

### Projektstruktur
```
mein-projekt/
    mkdocs.yml    # Konfigurationsdatei
    docs/
        index.md  # Homepage
```

### Entwicklungsserver starten
```bash
mkdocs serve
```

Die Dokumentation ist dann unter `http://127.0.0.1:8000` erreichbar.

### Erste Seite bearbeiten
Öffne `docs/index.md` und bearbeite den Inhalt:

```markdown
# Willkommen zu meiner Dokumentation

Das ist meine erste MkDocs-Seite!

## Über dieses Projekt

Hier beschreibe ich mein Projekt...
```

### Grundkonfiguration mit deutschem Theme
Öffne `mkdocs.yml` und ersetze den Inhalt mit:

```yaml
site_name: Mein Projekt
theme:
  name: material
  language: de
nav:
  - Home: index.md
```

*Dies aktiviert das Material Theme mit deutscher Sprache (falls du Schritt 2.1 gemacht hast).*

### Neue Seiten hinzufügen
1. Erstelle eine neue Markdown-Datei in `docs/`:
   ```bash
   touch docs/about.md
   ```

2. Füge sie zur Navigation in `mkdocs.yml` hinzu:
   ```yaml
   site_name: Mein Projekt
   theme:
     name: material
     language: de
   nav:
     - Home: index.md
     - Über uns: about.md
   ```

### Website bauen
```bash
mkdocs build
```

Die fertige Website wird im `site/` Ordner erstellt.

---

## Wichtige MkDocs-Befehle

| Befehl | Beschreibung |
|--------|--------------|
| `mkdocs new [dir-name]` | Neues Projekt erstellen |
| `mkdocs serve` | Entwicklungsserver starten |
| `mkdocs build` | Statische Website bauen |
| `mkdocs -h` | Hilfe anzeigen |

---

## Konfiguration (mkdocs.yml)

Grundlegende Konfiguration:

```yaml
site_name: Mein Projekt
site_description: Eine tolle Dokumentation
site_author: Dein Name

nav:
  - Home: index.md
  - Über uns: about.md
  - Kontakt: contact.md

theme:
  name: material  # Erfordert: pipx install mkdocs-material

markdown_extensions:
  - toc:
      permalink: true
  - codehilite
```

---

## Sprache auf Deutsch umstellen

### Internationale Unterstützung installieren
```bash
pipx install 'mkdocs[i18n]'
```

## Beliebte Themes

### Material Theme installieren

**Wichtig**: Installiere mkdocs-material anstatt mkdocs für das beste Ergebnis:

```bash
# Falls mkdocs bereits installiert ist, erst entfernen:
pipx uninstall mkdocs

# Dann mkdocs-material mit allen Abhängigkeiten installieren:
pipx install mkdocs-material --include-deps

# PATH neu laden
pipx ensurepath
```

**Terminal neu starten** nach der Installation!

Dann in `mkdocs.yml`:
```yaml
site_name: Mein Projekt
theme:
  name: material
  palette:
    primary: blue
    accent: light blue
```

---

## Tipps

1. **Live-Reload**: Der `mkdocs serve` Befehl lädt Änderungen automatisch neu
2. **Markdown-Syntax**: Nutze Standard-Markdown für den Inhalt
3. **Bilder**: Lege Bilder in `docs/images/` und verlinke sie mit `![Alt](images/bild.png)`
4. **Links**: Interne Links funktionieren mit `[Text](andere-seite.md)`

---

## Fehlerbehebung

**Problem**: `mkdocs: command not found`
**Lösung**: 
1. `pipx ensurepath` ausführen
2. Terminal neu starten
3. Falls immer noch nicht funktioniert: `export PATH="$PATH:~/.local/bin"`

**Problem**: `ERROR - Config value 'theme': Unrecognised theme name: 'material'`
**Lösung**: 
1. `pipx uninstall mkdocs` (falls vorhanden)
2. `pipx install mkdocs-material --include-deps`
3. `pipx ensurepath`
4. Terminal neu starten

---

*Viel Erfolg mit deiner MkDocs-Dokumentation!*