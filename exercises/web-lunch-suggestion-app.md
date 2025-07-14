# Übung: Mittagessen-Vorschlag-Website

## Lernziele
Nach Abschluss dieser Übung können die Teilnehmer:
- Eine einfache interaktive Webanwendung mit HTML, CSS und JavaScript erstellen
- Arrays und Zufallsfunktionen in JavaScript verwenden
- Event-Handler implementieren
- DOM-Manipulation durchführen
- Eine benutzerfreundliche Oberfläche gestalten

## Übungsbeschreibung
Erstellen Sie eine Website, die zufällige Vorschläge für das Mittagessen macht. Die Anwendung soll verschiedene Gerichte vorschlagen und optional nach Kategorien filtern können.

## Aufgabe 1: HTML-Struktur (30 Minuten)

Erstellen Sie eine Datei `lunch-suggestion.html` mit folgender Grundstruktur:

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mittagessen-Vorschläge</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h1>Was gibt's heute zu Mittag?</h1>
        
        <div class="suggestion-box">
            <p id="suggestion">Klicken Sie auf den Button für einen Vorschlag!</p>
        </div>
        
        <button id="suggest-btn">Neuer Vorschlag</button>
        
        <div class="filter-section">
            <h3>Filter:</h3>
            <label>
                <input type="checkbox" id="vegetarian" value="vegetarian">
                Vegetarisch
            </label>
            <label>
                <input type="checkbox" id="quick" value="quick">
                Schnell (< 30 Min)
            </label>
            <label>
                <input type="checkbox" id="healthy" value="healthy">
                Gesund
            </label>
        </div>
    </div>
    
    <script src="script.js"></script>
</body>
</html>
```

## Aufgabe 2: CSS-Styling (30 Minuten)

Erstellen Sie eine Datei `style.css`:

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}

.container {
    background-color: white;
    padding: 2rem;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0,0,0,0.1);
    text-align: center;
    max-width: 500px;
    width: 90%;
}

h1 {
    color: #333;
    margin-bottom: 2rem;
}

.suggestion-box {
    background-color: #f8f8f8;
    padding: 2rem;
    border-radius: 8px;
    margin-bottom: 1.5rem;
    min-height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
}

#suggestion {
    font-size: 1.2rem;
    color: #555;
}

#suggest-btn {
    background-color: #4CAF50;
    color: white;
    border: none;
    padding: 12px 30px;
    font-size: 1rem;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
}

#suggest-btn:hover {
    background-color: #45a049;
}

.filter-section {
    margin-top: 2rem;
    text-align: left;
}

.filter-section h3 {
    margin-bottom: 1rem;
    color: #666;
}

.filter-section label {
    display: block;
    margin-bottom: 0.5rem;
    cursor: pointer;
}

.filter-section input[type="checkbox"] {
    margin-right: 0.5rem;
}
```

## Aufgabe 3: JavaScript-Funktionalität (45 Minuten)

Erstellen Sie eine Datei `script.js`:

```javascript
// Mittagessen-Daten mit Kategorien
const lunchOptions = [
    { name: "Pizza Margherita", vegetarian: true, quick: true, healthy: false },
    { name: "Caesar Salat", vegetarian: false, quick: true, healthy: true },
    { name: "Spaghetti Bolognese", vegetarian: false, quick: false, healthy: false },
    { name: "Gemüse-Curry", vegetarian: true, quick: false, healthy: true },
    { name: "Döner Kebab", vegetarian: false, quick: true, healthy: false },
    { name: "Buddha Bowl", vegetarian: true, quick: true, healthy: true },
    { name: "Hamburger mit Pommes", vegetarian: false, quick: true, healthy: false },
    { name: "Quinoa-Salat", vegetarian: true, quick: true, healthy: true },
    { name: "Ramen-Suppe", vegetarian: false, quick: false, healthy: true },
    { name: "Falafel-Wrap", vegetarian: true, quick: true, healthy: true },
    { name: "Lachs mit Reis", vegetarian: false, quick: false, healthy: true },
    { name: "Veggie-Burger", vegetarian: true, quick: true, healthy: false },
    { name: "Pad Thai", vegetarian: false, quick: false, healthy: false },
    { name: "Caprese-Sandwich", vegetarian: true, quick: true, healthy: true },
    { name: "Hähnchen-Wrap", vegetarian: false, quick: true, healthy: true }
];

// DOM-Elemente
const suggestionElement = document.getElementById('suggestion');
const suggestButton = document.getElementById('suggest-btn');
const vegetarianCheckbox = document.getElementById('vegetarian');
const quickCheckbox = document.getElementById('quick');
const healthyCheckbox = document.getElementById('healthy');

// Funktion zum Filtern der Optionen
function getFilteredOptions() {
    return lunchOptions.filter(option => {
        if (vegetarianCheckbox.checked && !option.vegetarian) return false;
        if (quickCheckbox.checked && !option.quick) return false;
        if (healthyCheckbox.checked && !option.healthy) return false;
        return true;
    });
}

// Funktion zum Generieren eines zufälligen Vorschlags
function generateSuggestion() {
    const filteredOptions = getFilteredOptions();
    
    if (filteredOptions.length === 0) {
        suggestionElement.textContent = "Keine Optionen mit diesen Filtern verfügbar!";
        return;
    }
    
    const randomIndex = Math.floor(Math.random() * filteredOptions.length);
    const suggestion = filteredOptions[randomIndex];
    
    suggestionElement.textContent = suggestion.name;
    
    // Animation hinzufügen
    suggestionElement.style.opacity = '0';
    setTimeout(() => {
        suggestionElement.style.transition = 'opacity 0.5s';
        suggestionElement.style.opacity = '1';
    }, 100);
}

// Event-Listener
suggestButton.addEventListener('click', generateSuggestion);

// Optional: Bei Filter-Änderung neuen Vorschlag generieren
[vegetarianCheckbox, quickCheckbox, healthyCheckbox].forEach(checkbox => {
    checkbox.addEventListener('change', () => {
        if (suggestionElement.textContent !== "Klicken Sie auf den Button für einen Vorschlag!") {
            generateSuggestion();
        }
    });
});
```

## Aufgabe 4: Erweiterte Features (30 Minuten)

### 4.1 Verlauf hinzufügen
Fügen Sie eine Liste der letzten 5 Vorschläge hinzu:

```javascript
// Verlauf-Array
let history = [];
const maxHistory = 5;

// In der generateSuggestion() Funktion ergänzen:
function generateSuggestion() {
    // ... existierender Code ...
    
    // Zum Verlauf hinzufügen
    if (suggestion) {
        history.unshift(suggestion.name);
        if (history.length > maxHistory) {
            history.pop();
        }
        updateHistoryDisplay();
    }
}

function updateHistoryDisplay() {
    const historyElement = document.getElementById('history-list');
    historyElement.innerHTML = history.map(item => `<li>${item}</li>`).join('');
}
```

### 4.2 Favoriten-System
Implementieren Sie die Möglichkeit, Gerichte als Favoriten zu markieren:

```javascript
// LocalStorage für Favoriten nutzen
let favorites = JSON.parse(localStorage.getItem('lunchFavorites')) || [];

function toggleFavorite(dishName) {
    const index = favorites.indexOf(dishName);
    if (index > -1) {
        favorites.splice(index, 1);
    } else {
        favorites.push(dishName);
    }
    localStorage.setItem('lunchFavorites', JSON.stringify(favorites));
    updateFavoriteDisplay();
}
```

## Aufgabe 5: Responsive Design (15 Minuten)

Ergänzen Sie die CSS-Datei um Media Queries:

```css
@media (max-width: 600px) {
    .container {
        padding: 1rem;
    }
    
    h1 {
        font-size: 1.5rem;
    }
    
    #suggestion {
        font-size: 1rem;
    }
    
    #suggest-btn {
        width: 100%;
    }
}
```

## Bonus-Aufgaben

### Bonus 1: Kategorien hinzufügen
- Fügen Sie weitere Kategorien hinzu (z.B. "Budget-freundlich", "Glutenfrei")
- Implementieren Sie eine Preisanzeige

### Bonus 2: Animationen
- Fügen Sie einen Lade-Spinner während der Vorschlagsgenerierung hinzu
- Implementieren Sie eine "Slot-Machine"-Animation beim Generieren

### Bonus 3: API-Integration
- Nutzen Sie eine echte Rezept-API (z.B. Spoonacular API)
- Zeigen Sie Bilder der Gerichte an

### Bonus 4: Weitere Features
- Implementieren Sie eine "Teilen"-Funktion für Social Media
- Fügen Sie eine Bewertungsfunktion hinzu
- Erstellen Sie einen "Wochenplan"-Generator

## Abgabekriterien

1. Die Website zeigt zufällige Mittagessen-Vorschläge an
2. Filter funktionieren korrekt
3. Das Design ist ansprechend und responsiv
4. Der Code ist sauber strukturiert und kommentiert
5. Mindestens eine Bonus-Aufgabe wurde implementiert

## Hilfreiche Ressourcen

- [MDN Web Docs - JavaScript Arrays](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [MDN Web Docs - Math.random()](https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Math/random)
- [MDN Web Docs - Event Handling](https://developer.mozilla.org/de/docs/Web/API/EventTarget/addEventListener)
- [CSS Tricks - Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)