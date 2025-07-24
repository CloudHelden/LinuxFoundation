# Markdown Cheat Sheet

## Geschichte von Markdown

Markdown wurde 2004 von **John Gruber** in Zusammenarbeit mit **Aaron Swartz** entwickelt. Das Ziel war es, eine einfache Markup-Sprache zu schaffen, die sowohl für Menschen lesbar als auch in HTML konvertierbar ist. Der Name "Markdown" ist ein Wortspiel auf "Markup" und deutet darauf hin, dass es eine vereinfachte Alternative zu komplexeren Markup-Sprachen wie HTML darstellt.

Markdown wurde schnell populär, besonders in der Entwicklergemeinschaft, und wird heute auf Plattformen wie GitHub, Reddit, Stack Overflow und vielen anderen verwendet.

---

## Grundlegende Syntax

### Überschriften

```markdown
# H1 - Hauptüberschrift
## H2 - Unterüberschrift
### H3 - Unterunterüberschrift
#### H4
##### H5
###### H6
```

### Textformatierung

```markdown
**Fetter Text** oder __fetter Text__
*Kursiver Text* oder _kursiver Text_
***Fett und kursiv***
~~Durchgestrichener Text~~
`Inline-Code`
```

**Beispiel:**
- **Fetter Text**
- *Kursiver Text*
- ***Fett und kursiv***
- ~~Durchgestrichener Text~~
- `Inline-Code`

### Listen

#### Ungeordnete Listen
```markdown
- Element 1
- Element 2
  - Unterelement 2.1
  - Unterelement 2.2
- Element 3

* Alternative Syntax
+ Weitere Alternative
```

#### Geordnete Listen
```markdown
1. Erstes Element
2. Zweites Element
   1. Unterelement 2.1
   2. Unterelement 2.2
3. Drittes Element
```

### Links und Bilder

#### Links
```markdown
[Linktext](https://beispiel.de)
[Linktext mit Titel](https://beispiel.de "Titel beim Hover")
<https://automatischer-link.de>
```

#### Bilder
```markdown
![Alt-Text](bild.jpg)
![Alt-Text](bild.jpg "Bildtitel")
```

### Code-Blöcke

#### Inline-Code
```markdown
Verwende `console.log()` für die Ausgabe.
```

#### Code-Blöcke
````markdown
```javascript
function helloWorld() {
    console.log("Hallo Welt!");
}
```
````

#### Code-Block ohne Syntax-Highlighting
```markdown
    Eingerückter Code-Block
    (4 Leerzeichen oder 1 Tab)
```

### Zitate

```markdown
> Dies ist ein Zitat.
> Es kann mehrzeilig sein.
>
> > Verschachtelte Zitate sind auch möglich.
```

**Ergebnis:**
> Dies ist ein Zitat.
> Es kann mehrzeilig sein.

### Horizontale Linien

```markdown
---
***
___
```

---

### Tabellen

```markdown
| Spalte 1 | Spalte 2 | Spalte 3 |
|----------|----------|----------|
| Zeile 1  | Daten    | Mehr     |
| Zeile 2  | Weitere  | Daten    |

| Links    | Zentriert | Rechts |
|:---------|:---------:|-------:|
| Text     | Text      | Text   |
```

**Ergebnis:**
| Spalte 1 | Spalte 2 | Spalte 3 |
|----------|----------|----------|
| Zeile 1  | Daten    | Mehr     |
| Zeile 2  | Weitere  | Daten    |

### Escape-Zeichen

```markdown
\* Literales Sternchen statt kursiv
\# Literale Raute statt Überschrift
\\ Literaler Backslash
```

### Zeilenwechsel

```markdown
Zwei Leerzeichen am Ende einer Zeile  
erzeugen einen Zeilenwechsel.

Eine Leerzeile erzeugt einen neuen Absatz.
```

---

## Erweiterte Syntax (GitHub Flavored Markdown)

### Aufgabenlisten
```markdown
- [x] Erledigte Aufgabe
- [ ] Offene Aufgabe
- [ ] Weitere offene Aufgabe
```

**Ergebnis:**
- [x] Erledigte Aufgabe
- [ ] Offene Aufgabe

### Syntax-Highlighting für Code
````markdown
```python
def hello_world():
    print("Hallo Welt!")
```
````

### Tabellen mit Ausrichtung
```markdown
| Links    | Zentriert | Rechts |
|:---------|:---------:|-------:|
| Text     | Text      | Text   |
```

### Fußnoten
```markdown
Hier ist eine Fußnote[^1].

[^1]: Dies ist die Fußnote.
```

---

## Nützliche Tipps

1. **Vorschau verwenden**: Die meisten Editoren bieten eine Live-Vorschau
2. **Konsistent bleiben**: Wähle einen Stil und bleibe dabei (z.B. `*` vs `_` für kursiv)
3. **Leerzeilen verwenden**: Sie verbessern die Lesbarkeit des Markdown-Codes
4. **Tools nutzen**: Editoren wie Typora, Mark Text oder VS Code mit Markdown-Erweiterungen

---

## Häufige Anwendungen

- **Dokumentation**: README-Dateien, Wikis
- **Blogs**: Viele Static Site Generators nutzen Markdown
- **Notizen**: Obsidian, Notion, Roam Research
- **Plattformen**: GitHub, GitLab, Stack Overflow, Reddit
- **E-Books**: Konvertierung zu verschiedenen Formaten

---

*Erstellt mit Markdown - einfach, lesbar und vielseitig!*