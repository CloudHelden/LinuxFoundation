# MkDocs auf GitHub Pages deployen

Diese Anleitung zeigt, wie du dein MkDocs-Projekt auf GitHub Pages veröffentlichst.

---

## Schritt 1: Git Repository initialisieren

Gehe in deinen MkDocs-Projektordner:
```bash
cd mein-projekt
```

Git Repository initialisieren:
```bash
git init
```

Erste Dateien hinzufügen:
```bash
git add .
git commit -m "Initial commit"
```

---

## Schritt 2: GitHub Repository erstellen

1. Gehe zu [GitHub](https://github.com)
2. Klicke auf **"New repository"** (grüner Button)
3. Repository-Name eingeben (z.B. `mein-mkdocs-projekt`)
4. **Wichtig**: Repository als **Public** erstellen (für kostenlose GitHub Pages)
5. **NICHT** "Initialize with README" ankreuzen
6. Klicke **"Create repository"**

---

## Schritt 3: Lokales Repository mit GitHub verbinden

GitHub zeigt dir nach der Erstellung Befehle an. Nutze diese:

```bash
git remote add origin https://github.com/DEIN-USERNAME/mein-mkdocs-projekt.git
git branch -M main
git push -u origin main
```

**Ersetze `DEIN-USERNAME` und `mein-mkdocs-projekt` mit deinen Werten!**

---

## Schritt 4: Manuelles Deployment

```bash
# Testen ob gh-deploy bereits verfügbar ist
mkdocs gh-deploy

# Falls der Befehl nicht gefunden wird:
pipx inject mkdocs-material ghp-import

# Oder mit Force-Installation:
pipx install 'mkdocs[gh-deploy]' --force
```

Das erstellt automatisch einen `gh-pages` Branch und deployed deine Website.

---

## Schritt 5: GitHub Pages aktivieren

1. Gehe zu deinem GitHub Repository
2. Klicke auf **"Settings"** (oben rechts)
3. Scrolle runter zu **"Pages"** (linke Seitenleiste)
4. Bei **"Source"** wähle: **"Deploy from a branch"**
5. Bei **"Branch"** wähle: **"gh-pages"** und **"/ (root)"**
6. Klicke **"Save"**

## Schritt 6: Website aufrufen

```
https://DEIN-USERNAME.github.io/REPOSITORY-NAME/
```

Nach dem Deployment (kann 2-3 Minuten dauern) ist deine Website erreichbar unter:

```
https://DEIN-USERNAME.github.io/REPOSITORY-NAME/
```

Beispiel: `https://maxmustermann.github.io/mein-mkdocs-projekt/`

---

## Projektstruktur für GitHub

Deine finale Projektstruktur sollte so aussehen:

```
mein-projekt/
├── docs/
│   ├── index.md
│   └── about.md
├── mkdocs.yml
├── .gitignore
└── README.md               # Optional
```

### .gitignore erstellen

Erstelle eine `.gitignore` Datei:
```bash
echo "site/" > .gitignore
```

Das verhindert, dass der `site/` Ordner (Build-Output) ins Repository kommt.

---

## Troubleshooting

### Problem: "Repository not found"
**Lösung**: Prüfe Repository-Name und GitHub-Username in der Remote-URL

### Problem: GitHub Pages zeigt 404
**Lösung**: 
1. Prüfe ob Repository **public** ist
2. Warte 2-3 Minuten nach dem Deployment
3. Prüfe GitHub Actions Logs bei Fehlern

### Problem: CSS/Theme wird nicht geladen
**Lösung**: Füge in `mkdocs.yml` hinzu:
```yaml
site_url: https://DEIN-USERNAME.github.io/REPOSITORY-NAME/
```

### Problem: GitHub Actions schlägt fehl
**Lösung**: 
1. Falls du doch GitHub Actions nutzen möchtest, siehe Online-Tutorials
2. Für manuelles Deployment: `mkdocs gh-deploy` verwenden

---

## Workflow für Updates

Nach Änderungen an deiner Dokumentation:

```bash
# Änderungen committen
git add .
git commit -m "Update documentation"

# Zu GitHub pushen
git push

# Website manuell deployen
mkdocs gh-deploy
```

---

## Tipps

1. **Custom Domain**: Du kannst eine eigene Domain in den GitHub Pages Settings konfigurieren
2. **Private Repositories**: GitHub Pages für private Repos benötigt GitHub Pro
3. **Build-Zeit**: Komplexe Sites können 2-3 Minuten zum Build brauchen
4. **Caching**: Der GitHub Actions Workflow nutzt Caching für schnellere Builds

---

*Deine MkDocs-Website ist jetzt live auf GitHub Pages! 🚀*