# Mermaid-Diagramm-Leitfaden für Linux 101

## Überblick
Dieser Leitfaden hilft Dozenten und Studenten, visuelle Diagramme mit Mermaid-Syntax zu erstellen. Alle Diagramme werden automatisch in GitHub, GitLab und vielen Markdown-Viewern gerendert.

## Kurzreferenz

### 1. Prozessfluss-Diagramme

```mermaid
graph LR
    A[Benutzereingabe] --> B{Gültig?}
    B -->|Ja| C[Verarbeiten]
    B -->|Nein| D[Fehler]
    C --> E[Ausgabe]
    D --> A
```

**Verwenden für**: Befehlsabläufe, Entscheidungsbäume, Fehlerbehebungsanleitungen

### 2. System-Architektur

```mermaid
graph TB
    subgraph "Anwendungsschicht"
        A1[Webserver]
        A2[App-Server]
        A3[Cache]
    end
    
    subgraph "Datenschicht"
        D1[(Datenbank)]
        D2[Dateispeicher]
    end
    
    A1 --> A2
    A2 --> A3
    A2 --> D1
    A3 --> D1
    A1 --> D2
```

**Verwenden für**: Systemkomponenten, Netzwerktopologie, Service-Beziehungen

### 3. Sequenz-Diagramme

```mermaid
sequenceDiagram
    participant U as Benutzer
    participant S as Shell
    participant K as Kernel
    participant H as Hardware
    
    U->>S: Befehl eingeben
    S->>K: System-Call
    K->>H: Hardware-Anfrage
    H-->>K: Antwort
    K-->>S: Ergebnis
    S-->>U: Ausgabe
```

**Verwenden für**: System-Calls, Netzwerkprotokolle, Prozesskommunikation

### 4. Zustandsdiagramme

```mermaid
stateDiagram-v2
    [*] --> Laufend
    Laufend --> Schlafend: wait()
    Laufend --> Gestoppt: SIGSTOP
    Schlafend --> Laufend: aufwachen
    Gestoppt --> Laufend: SIGCONT
    Laufend --> Zombie: exit()
    Zombie --> [*]: parent wait()
```

**Verwenden für**: Prozesszustände, Service-Lebenszyklus, Dateizustände

### 5. Git-Workflows

```mermaid
gitGraph
    commit
    branch feature
    checkout feature
    commit
    commit
    checkout main
    merge feature
    commit
```

**Verwenden für**: Versionskontrolle, Branching-Strategien, Deployment-Abläufe

### 6. Entitäts-Beziehungen

```mermaid
erDiagram
    BENUTZER ||--o{ PROZESS : besitzt
    PROZESS ||--o{ DATEI : greift_zu
    BENUTZER ||--o{ GRUPPE : gehört_zu
    GRUPPE ||--o{ DATEI : besitzt
    
    BENUTZER {
        int uid
        string benutzername
        string home_verz
    }
    PROZESS {
        int pid
        int uid
        string befehl
    }
    DATEI {
        string pfad
        int berechtigungen
        int uid
        int gid
    }
    GRUPPE {
        int gid
        string gruppenname
    }
```

**Verwenden für**: Berechtigungsmodelle, Datenbank-Schemas, Systembeziehungen

### 7. Gantt-Diagramme (für Kursplanung)

```mermaid
gantt
    title Linux 101 Kurs-Zeitplan
    dateFormat  YYYY-MM-DD
    section Monat 1
    Grundlagen      :2024-01-01, 14d
    Dateisystem     :14d
    section Monat 2  
    Administration  :28d
    section Monat 3
    Automatisierung :21d
    Abschlussprojekt:7d
```

**Verwenden für**: Kurs-Zeitplan, Projektplanung, Labor-Termine

### 8. Kreisdiagramme (für Ressourcennutzung)

```mermaid
pie title Speichernutzung
    "System" : 15
    "Anwendungen" : 25
    "Benutzerdaten" : 45
    "Freier Speicher" : 15
```

**Verwenden für**: Ressourcenverteilung, Zeitaufteilung, Umfrageergebnisse

## Best Practices

### 1. Einfach halten
```mermaid
graph LR
    A[Eingabe] --> B[Verarbeitung] --> C[Ausgabe]
```

### 2. Klare Bezeichnungen verwenden
```mermaid
graph TD
    A[Benutzer führt aus: ls -la] --> B{Dateien vorhanden?}
    B -->|Ja| C[Dateiliste anzeigen]
    B -->|Nein| D[Leeres Verzeichnis zeigen]
```

### 3. Farbkodierung zur Betonung
```mermaid
graph TD
    A[Normaler Prozess] --> B[Warnprozess]
    B --> C[Kritischer Prozess]
    
    style B fill:#ff9,stroke:#333,stroke-width:2px
    style C fill:#f99,stroke:#333,stroke-width:4px
```

### 4. Verwandte Elemente gruppieren
```mermaid
graph TB
    subgraph "Benutzerbefehle"
        A[ls]
        B[cd]
        C[pwd]
    end
    
    subgraph "Admin-Befehle"
        D[sudo]
        E[chmod]
        F[chown]
    end
    
    A --> G[Dateisystem]
    D --> G
```

## Häufige Diagramme für Linux-Unterricht

### Berechtigungsfluss
```mermaid
graph TD
    A[Benutzer fordert Dateizugriff an] --> B{Benutzer besitzt Datei?}
    B -->|Ja| C{Benutzerberechtigungen prüfen}
    B -->|Nein| D{Benutzer in Dateigruppe?}
    D -->|Ja| E{Gruppenberechtigungen prüfen}
    D -->|Nein| F{Andere-Berechtigungen prüfen}
    
    C -->|Lesen| G[Lesen erlauben]
    C -->|Schreiben| H[Schreiben erlauben]
    C -->|Ausführen| I[Ausführen erlauben]
    C -->|Keine| J[Zugriff verweigern]
    
    E -->|Hat Berechtigung| K[Aktion erlauben]
    E -->|Keine Berechtigung| J
    
    F -->|Hat Berechtigung| K
    F -->|Keine Berechtigung| J
```

### Boot-Prozess
```mermaid
graph TD
    A[BIOS/UEFI] --> B[Bootloader GRUB]
    B --> C[Kernel wird geladen]
    C --> D[initramfs]
    D --> E[Init-System systemd]
    E --> F[System-Services]
    F --> G[Login-Prompt]
    G --> H[Benutzer-Session]
```

### Netzwerk-Paketfluss
```mermaid
sequenceDiagram
    participant App as Anwendung
    participant Socket
    participant TCP/IP
    participant NIC as Netzwerkkarte
    participant Network as Netzwerk
    
    App->>Socket: send() Daten
    Socket->>TCP/IP: Paket erstellen
    TCP/IP->>NIC: Übertragen
    NIC->>Network: Physische Übertragung
    Network-->>NIC: Antwort
    NIC-->>TCP/IP: Paket empfangen
    TCP/IP-->>Socket: Daten verarbeiten
    Socket-->>App: recv() Daten
```

## Integrations-Tipps

### 1. In Markdown-Dateien
Diagramm-Code in dreifache Backticks mit `mermaid` Identifier setzen:
````markdown
```mermaid
graph LR
    A --> B
```
````

### 2. Für Präsentationen
- Als SVG/PNG für Folien exportieren
- Live-Rendering-Tools verwenden
- Diagramme auf einzelne Folien beschränken

### 3. Studenten-Übungen
Lassen Sie Studenten Diagramme erstellen für:
- Ihr Verständnis von Konzepten
- Fehlerbehebungs-Workflows  
- System-Designs
- Befehls-Beziehungen

## Tools und Ressourcen

### Rendering-Tools
- **GitHub/GitLab**: Native Unterstützung
- **VS Code**: Mermaid-Extension
- **Online**: https://mermaid.live/
- **CLI**: `mmdc` (mermaid CLI)

### Lernressourcen
- [Offizielle Dokumentation](https://mermaid-js.github.io/mermaid/)
- [Live-Editor](https://mermaid.live/edit)
- [Beispiel-Galerie](https://mermaid-js.github.io/mermaid/#/examples)

## Übung: Eigenes erstellen

Versuchen Sie ein Diagramm zu erstellen für:
1. Wie `sudo` funktioniert
2. Dateiberechtigungs-Prüfungsfluss
3. Ihren täglichen Linux-Workflow
4. Netzwerk-Fehlerbehebungsschritte

Denken Sie daran: Diagramme sollten klären, nicht verkomplizieren!