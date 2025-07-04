# Praktische Übung: Nginx Virtual Hosts - Mehrere Websites verwalten

## 🎯 Übungsziel
**Dauer**: 90 Minuten  
**Schwierigkeit**: Aufbauend auf Grundlagen  
**Voraussetzungen**: Abgeschlossene nginx-webserver-setup Übung  

**Lernziele:**
- Virtual Hosts (Server Blocks) verstehen und einrichten
- Mehrere Websites auf einem Server hosten
- DNS-Grundlagen in der Praxis anwenden
- Sicherheitstrennung zwischen Sites verstehen
- Strukturiertes Arbeiten mit nginx-Konfigurationen

---

## 📋 Voraussetzungen Check

### Bestehende Umgebung verifizieren
```bash
# Nginx läuft?
sudo systemctl status nginx

# Standard-Seite erreichbar?
curl -I localhost

# Verfügbarer Speicher?
df -h /var/www

# Aktuelle nginx-Konfiguration
ls -la /etc/nginx/sites-*
```

**✅ Bereit wenn:**
- [ ] Nginx läuft und Standard-Seite erreichbar
- [ ] Mindestens 1GB freier Speicher
- [ ] Root/sudo Zugriff vorhanden

---

## 🏢 Szenario: Kleine Firma - Drei Websites

**Die Aufgabe:**  
Eine kleine Firma namens "learnlinux GmbH" benötigt drei Websites:
1. **Hauptseite** (www.learnlinux.local) - Öffentliche Firmenpräsenz
2. **Kundencenter** (portal.learnlinux.local) - Login-geschützter Bereich
3. **Entwickler-Docs** (docs.learnlinux.local) - Interne Dokumentation

---

## 🛠️ Teil 1: Vorbereitung und Struktur (20 Min.)

### Aufgabe 1.1: Verzeichnisstruktur erstellen
```bash
# Basis-Struktur für alle Sites
sudo mkdir -p /var/www/{learnlinux,portal,docs}/html

# Berechtigungen setzen
sudo chown -R $USER:$USER /var/www/{learnlinux,portal,docs}
sudo chmod -R 755 /var/www

# Struktur verifizieren
tree /var/www/ -d -L 2
# Falls tree nicht installiert: sudo apt install tree
```

### Aufgabe 1.2: Test-Inhalte erstellen
```bash
# Hauptseite
cat > /var/www/learnlinux/html/index.html << 'EOF'
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>learnlinux GmbH - Willkommen</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            max-width: 1200px; 
            margin: 0 auto; 
            padding: 20px;
            background: #f5f5f5;
        }
        header { 
            background: #2c3e50; 
            color: white; 
            padding: 2rem; 
            border-radius: 10px;
            text-align: center;
        }
        .content { 
            background: white; 
            padding: 2rem; 
            margin-top: 2rem;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        .links { 
            margin-top: 2rem; 
            padding: 1rem;
            background: #ecf0f1;
            border-radius: 5px;
        }
        a { color: #3498db; text-decoration: none; }
        a:hover { text-decoration: underline; }
    </style>
</head>
<body>
    <header>
        <h1>🚀 learnlinux GmbH</h1>
        <p>Innovative Lösungen für Ihr Business</p>
    </header>
    
    <div class="content">
        <h2>Willkommen auf unserer Hauptseite</h2>
        <p>Dies ist die öffentliche Website der learnlinux GmbH.</p>
        
        <h3>Unsere Services:</h3>
        <ul>
            <li>Cloud-Lösungen</li>
            <li>Webentwicklung</li>
            <li>IT-Beratung</li>
        </ul>
        
        <div class="links">
            <h3>Weitere Bereiche:</h3>
            <ul>
                <li><a href="http://portal.learnlinux.local">Kundencenter</a> (Login erforderlich)</li>
                <li><a href="http://docs.learnlinux.local">Entwickler-Dokumentation</a> (Intern)</li>
            </ul>
        </div>
    </div>
    
    <footer style="text-align: center; margin-top: 2rem; color: #666;">
        <p>Server: nginx | Host: www.learnlinux.local | © 2024 learnlinux GmbH</p>
    </footer>
</body>
</html>
EOF

# Kundencenter
cat > /var/www/portal/html/index.html << 'EOF'
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>learnlinux - Kundencenter</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            max-width: 800px; 
            margin: 0 auto; 
            padding: 20px;
            background: #e8f4f8;
        }
        .login-box { 
            background: white; 
            padding: 3rem; 
            border-radius: 10px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.1);
            text-align: center;
        }
        .secure { 
            color: #27ae60; 
            font-weight: bold;
        }
        button { 
            background: #3498db; 
            color: white; 
            padding: 10px 30px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover { background: #2980b9; }
    </style>
</head>
<body>
    <div class="login-box">
        <h1>🔐 learnlinux Kundencenter</h1>
        <p class="secure">Sicherer Bereich - Authentifizierung erforderlich</p>
        
        <h3>Willkommen im Kundencenter!</h3>
        <p>Hier finden Sie:</p>
        <ul style="text-align: left; display: inline-block;">
            <li>Ihre Rechnungen</li>
            <li>Support-Tickets</li>
            <li>Projekt-Updates</li>
            <li>Downloads</li>
        </ul>
        
        <p><button onclick="alert('Login-Funktion wird in Lektion 7 implementiert!')">Zum Login</button></p>
        
        <hr style="margin: 2rem 0;">
        <p style="color: #666;">Host: portal.learnlinux.local</p>
    </div>
</body>
</html>
EOF

# Entwickler-Dokumentation
cat > /var/www/docs/html/index.html << 'EOF'
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>learnlinux - Developer Docs</title>
    <style>
        body { 
            font-family: 'Courier New', monospace; 
            max-width: 1000px; 
            margin: 0 auto; 
            padding: 20px;
            background: #1e1e1e;
            color: #d4d4d4;
        }
        .header { 
            background: #2d2d30; 
            padding: 1rem; 
            border-left: 4px solid #007acc;
        }
        code { 
            background: #2d2d30; 
            padding: 2px 5px; 
            border-radius: 3px;
        }
        pre { 
            background: #2d2d30; 
            padding: 1rem; 
            overflow-x: auto;
            border-radius: 5px;
        }
        a { color: #569cd6; }
        .warning { 
            background: #5a1e1e; 
            border-left: 4px solid #f44336;
            padding: 1rem;
            margin: 1rem 0;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>📚 learnlinux Developer Documentation</h1>
        <p>Internal Use Only - Nur für Entwickler</p>
    </div>
    
    <div class="warning">
        ⚠️ <strong>WARNUNG:</strong> Diese Dokumentation enthält sensible Informationen.
        Zugriff nur aus dem internen Netzwerk gestattet!
    </div>
    
    <h2>Quick Links</h2>
    <ul>
        <li><a href="#api">API Dokumentation</a></li>
        <li><a href="#deploy">Deployment Guide</a></li>
        <li><a href="#security">Security Guidelines</a></li>
    </ul>
    
    <h2>Server Info</h2>
    <pre>
Host: docs.learnlinux.local
Server: nginx
Environment: Development
Last Updated: $(date)
    </pre>
    
    <h2>Beispiel API Endpoint</h2>
    <pre>
GET /api/v1/status
Authorization: Bearer YOUR_TOKEN_HERE

Response:
{
    "status": "operational",
    "version": "1.0.0",
    "uptime": "99.9%"
}
    </pre>
    
    <footer style="margin-top: 3rem; padding-top: 1rem; border-top: 1px solid #444;">
        <p>learnlinux Internal Documentation - Confidential</p>
    </footer>
</body>
</html>
EOF
```

### Aufgabe 1.3: Berechtigungen finalisieren
```bash
# Nginx-Benutzer als Eigentümer
sudo chown -R www-data:www-data /var/www/{learnlinux,portal,docs}

# Verzeichnisse 755, Dateien 644
sudo find /var/www -type d -exec chmod 755 {} \;
sudo find /var/www -type f -exec chmod 644 {} \;

# Verifizieren
ls -la /var/www/
```

---

## 🌐 Teil 2: Virtual Hosts konfigurieren (30 Min.)

### Aufgabe 2.1: Erste Site - Hauptseite
```bash
# Neue Server Block Konfiguration erstellen
sudo nano /etc/nginx/sites-available/learnlinux
```

**Inhalt für learnlinux:**
```nginx
server {
    listen 80;
    listen [::]:80;
    
    # Server Namen definieren
    server_name www.learnlinux.local learnlinux.local;
    
    # Document Root
    root /var/www/learnlinux/html;
    index index.html index.htm;
    
    # Logging
    access_log /var/log/nginx/learnlinux_access.log;
    error_log /var/log/nginx/learnlinux_error.log;
    
    # Location Block
    location / {
        try_files $uri $uri/ =404;
    }
    
    # Sicherheits-Header
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    
    # Statische Dateien cachen
    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }
}
```

### Aufgabe 2.2: Zweite Site - Kundencenter
```bash
sudo nano /etc/nginx/sites-available/portal
```

**Inhalt für portal:**
```nginx
server {
    listen 80;
    listen [::]:80;
    
    server_name portal.learnlinux.local;
    
    root /var/www/portal/html;
    index index.html index.htm;
    
    # Separate Logs für Portal
    access_log /var/log/nginx/portal_access.log;
    error_log /var/log/nginx/portal_error.log;
    
    location / {
        try_files $uri $uri/ =404;
    }
    
    # Vorbereitung für späteren Passwortschutz
    # auth_basic "Kundencenter - Bitte anmelden";
    # auth_basic_user_file /etc/nginx/.htpasswd_portal;
    
    # Security Headers
    add_header X-Frame-Options "DENY" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header Strict-Transport-Security "max-age=31536000" always;
}
```

### Aufgabe 2.3: Dritte Site - Developer Docs
```bash
sudo nano /etc/nginx/sites-available/docs
```

**Inhalt für docs:**
```nginx
server {
    listen 80;
    listen [::]:80;
    
    server_name docs.learnlinux.local;
    
    root /var/www/docs/html;
    index index.html index.htm;
    
    # Separate Logs
    access_log /var/log/nginx/docs_access.log;
    error_log /var/log/nginx/docs_error.log;
    
    # Zugriffsbeschränkung (nur lokales Netzwerk)
    location / {
        # Nur localhost und privates Netzwerk erlauben
        allow 127.0.0.1;
        allow ::1;
        allow 10.0.0.0/8;
        allow 172.16.0.0/12;
        allow 192.168.0.0/16;
        deny all;
        
        try_files $uri $uri/ =404;
    }
    
    # Keine Indizierung durch Suchmaschinen
    location = /robots.txt {
        add_header Content-Type text/plain;
        return 200 "User-agent: *\nDisallow: /\n";
    }
}
```

---

## 🔗 Teil 3: Sites aktivieren und DNS (20 Min.)

### Aufgabe 3.1: Virtual Hosts aktivieren
```bash
# Symbolische Links erstellen
sudo ln -s /etc/nginx/sites-available/learnlinux /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/portal /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/docs /etc/nginx/sites-enabled/

# Default-Site deaktivieren (optional)
sudo rm /etc/nginx/sites-enabled/default

# Konfiguration testen
sudo nginx -t

# Nginx neu laden
sudo systemctl reload nginx
```

### Aufgabe 3.2: Lokale DNS-Einträge (/etc/hosts)
```bash
# Hosts-Datei bearbeiten
sudo nano /etc/hosts
```

**Folgende Zeilen hinzufügen:**
```
# learnlinux Virtual Hosts
127.0.0.1    learnlinux.local www.learnlinux.local
127.0.0.1    portal.learnlinux.local
127.0.0.1    docs.learnlinux.local
```

### Aufgabe 3.3: Sites testen
```bash
# Test mit curl
curl -H "Host: www.learnlinux.local" http://localhost
curl -H "Host: portal.learnlinux.local" http://localhost
curl -H "Host: docs.learnlinux.local" http://localhost

# Oder direkt mit den Hostnamen
curl http://www.learnlinux.local
curl http://portal.learnlinux.local
curl http://docs.learnlinux.local

# Headers prüfen
curl -I http://www.learnlinux.local
```

---

## 🔍 Teil 4: Monitoring und Troubleshooting (20 Min.)

### Aufgabe 4.1: Log-Analyse
```bash
# Logs in Echtzeit beobachten
sudo tail -f /var/log/nginx/learnlinux_access.log

# In anderem Terminal: Sites aufrufen
for site in www.learnlinux.local portal.learnlinux.local docs.learnlinux.local; do
    echo "Testing $site..."
    curl -s $site > /dev/null
done

# Fehler-Logs prüfen
sudo tail /var/log/nginx/*_error.log
```

### Aufgabe 4.2: Performance-Test
```bash
# Apache Bench installieren (falls nicht vorhanden)
sudo apt install apache2-utils -y

# Einfacher Load-Test
ab -n 100 -c 10 http://www.learnlinux.local/
ab -n 100 -c 10 http://portal.learnlinux.local/
ab -n 100 -c 10 http://docs.learnlinux.local/

# Ergebnisse interpretieren
# - Requests per second
# - Time per request
# - Transfer rate
```

### Aufgabe 4.3: Troubleshooting-Übung
```bash
# Problem 1: Site nicht erreichbar
# Simulieren: Tippfehler in server_name
sudo nano /etc/nginx/sites-available/learnlinux
# Ändern Sie server_name zu "ww.learnlinux.local" (fehlendes w)

sudo nginx -t
sudo systemctl reload nginx

# Debuggen
curl http://www.learnlinux.local
# Sollte 404 oder default page zeigen

# Lösung: server_name korrigieren
```

---

## 🛡️ Teil 5: Sicherheit und Best Practices (20 Min.)

### Aufgabe 5.1: Basis-Authentifizierung für Portal
```bash
# htpasswd installieren
sudo apt install apache2-utils -y

# Passwort-Datei erstellen
sudo htpasswd -c /etc/nginx/.htpasswd_portal kunde1
# Passwort eingeben

# Weiteren Benutzer hinzufügen
sudo htpasswd /etc/nginx/.htpasswd_portal kunde2

# Portal-Konfiguration aktivieren
sudo nano /etc/nginx/sites-available/portal
# Kommentare bei auth_basic Zeilen entfernen

# Nginx neu laden
sudo systemctl reload nginx

# Testen
curl http://portal.learnlinux.local
# Sollte 401 Unauthorized zeigen

curl -u kunde1:PASSWORT http://portal.learnlinux.local
# Sollte Seite anzeigen
```

### Aufgabe 5.2: SSL-Vorbereitung (Self-Signed für Test)
```bash
# SSL-Zertifikat für Tests erstellen
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/learnlinux.key \
    -out /etc/ssl/certs/learnlinux.crt \
    -subj "/C=DE/ST=Berlin/L=Berlin/O=learnlinux/CN=*.learnlinux.local"

# HTTPS-Version der Hauptseite
sudo nano /etc/nginx/sites-available/learnlinux-ssl
```

**Inhalt für learnlinux-ssl:**
```nginx
server {
    listen 443 ssl;
    listen [::]:443 ssl;
    
    server_name www.learnlinux.local learnlinux.local;
    
    ssl_certificate /etc/ssl/certs/learnlinux.crt;
    ssl_certificate_key /etc/ssl/private/learnlinux.key;
    
    # Moderne SSL-Einstellungen
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
    
    root /var/www/learnlinux/html;
    index index.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
}

# HTTP zu HTTPS Weiterleitung
server {
    listen 80;
    server_name www.learnlinux.local learnlinux.local;
    return 301 https://$server_name$request_uri;
}
```

### Aufgabe 5.3: Sicherheits-Check
```bash
# Nginx-Version verstecken
sudo nano /etc/nginx/nginx.conf
# In http block hinzufügen:
# server_tokens off;

# Überprüfen
curl -I http://www.learnlinux.local
# Server header sollte nur "nginx" zeigen, keine Version

# Berechtigungen final prüfen
sudo find /var/www -type d -exec chmod 755 {} \;
sudo find /var/www -type f -exec chmod 644 {} \;
sudo chown -R www-data:www-data /var/www
```

---

## 📊 Abschluss-Projekt: Status-Dashboard

### Bonus-Aufgabe: Monitoring-Seite erstellen
```bash
# Status-Seite mit Server-Infos
sudo nano /var/www/learnlinux/html/status.html
```

**Inhalt für status.html:**
```html
<!DOCTYPE html>
<html>
<head>
    <title>learnlinux - Server Status</title>
    <meta http-equiv="refresh" content="30">
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        .status-grid { 
            display: grid; 
            grid-template-columns: repeat(3, 1fr); 
            gap: 20px; 
            margin-top: 20px;
        }
        .site-card { 
            border: 2px solid #ddd; 
            padding: 20px; 
            border-radius: 8px;
            text-align: center;
        }
        .online { border-color: #4CAF50; background: #f1f8f4; }
        .auth { border-color: #ff9800; background: #fff3e0; }
        .restricted { border-color: #f44336; background: #ffebee; }
        h1 { color: #333; }
        .timestamp { color: #666; font-size: 0.9em; }
    </style>
</head>
<body>
    <h1>🚦 learnlinux Server Status Dashboard</h1>
    <p class="timestamp">Letzte Aktualisierung: <span id="time"></span></p>
    
    <div class="status-grid">
        <div class="site-card online">
            <h2>Hauptseite</h2>
            <p>✅ Online</p>
            <p><a href="http://www.learnlinux.local">www.learnlinux.local</a></p>
            <p>Öffentlich zugänglich</p>
        </div>
        
        <div class="site-card auth">
            <h2>Kundencenter</h2>
            <p>🔐 Authentifizierung</p>
            <p><a href="http://portal.learnlinux.local">portal.learnlinux.local</a></p>
            <p>Login erforderlich</p>
        </div>
        
        <div class="site-card restricted">
            <h2>Developer Docs</h2>
            <p>🚫 Eingeschränkt</p>
            <p><a href="http://docs.learnlinux.local">docs.learnlinux.local</a></p>
            <p>Nur internes Netzwerk</p>
        </div>
    </div>
    
    <h3>Server-Informationen:</h3>
    <ul>
        <li>Webserver: nginx</li>
        <li>Betriebssystem: Ubuntu</li>
        <li>Virtual Hosts: 3 aktiv</li>
        <li>SSL: Teilweise aktiviert</li>
    </ul>
    
    <script>
        document.getElementById('time').textContent = new Date().toLocaleString('de-DE');
    </script>
</body>
</html>
```

---

## ✅ Abschluss-Checkliste

### Erfolgs-Kriterien:
- [ ] Drei Virtual Hosts erfolgreich konfiguriert
- [ ] Alle Sites über ihre Domains erreichbar
- [ ] Separate Log-Dateien für jede Site
- [ ] Basis-Authentifizierung für Portal funktioniert
- [ ] IP-Beschränkung für Docs funktioniert
- [ ] Sicherheits-Header implementiert
- [ ] Performance-Test durchgeführt

### Verständnis-Check:
- [ ] Unterschied zwischen sites-available und sites-enabled verstanden
- [ ] server_name Direktive und ihre Funktion klar
- [ ] Log-Rotation Konzept verstanden
- [ ] DNS-Auflösung im Browser nachvollzogen

### Aufräumen:
```bash
# Logs archivieren
sudo tar -czf ~/nginx-lab-logs.tar.gz /var/log/nginx/*learnlinux* /var/log/nginx/*portal* /var/log/nginx/*docs*

# Bei Bedarf: Sites deaktivieren
# sudo rm /etc/nginx/sites-enabled/{learnlinux,portal,docs}
# sudo systemctl reload nginx
```

---

## 💡 Erweiterte Herausforderungen

### Challenge 1: Load Balancing vorbereiten
- Erstellen Sie zwei Versionen der Hauptseite
- Konfigurieren Sie nginx als Load Balancer
- Testen Sie Round-Robin Verteilung

### Challenge 2: Caching implementieren
- Aktivieren Sie Browser-Caching für statische Dateien
- Implementieren Sie nginx Proxy-Cache
- Messen Sie Performance-Verbesserungen

### Challenge 3: Monitoring erweitern
- Installieren Sie GoAccess für Echtzeit-Analyse
- Erstellen Sie ein Bash-Script für tägliche Reports
- Automatisieren Sie Log-Rotation

---

## 🎯 Reflexion und nächste Schritte

### Was Sie gelernt haben:
1. **Virtual Hosts** - Mehrere Websites auf einem Server
2. **DNS-Integration** - Lokale Namensauflösung
3. **Sicherheitstrennung** - Verschiedene Zugriffsebenen
4. **Log-Management** - Separate Logs pro Site
5. **Performance-Testing** - Grundlegende Lasttests

### Nächste Themen:
- Reverse Proxy Konfiguration
- SSL/TLS mit Let's Encrypt
- Container-basierte Deployments
- CI/CD Integration
- Advanced Security (ModSecurity, fail2ban)

---

**🎉 Gratulation!** Sie haben erfolgreich eine Multi-Site nginx-Umgebung aufgebaut und verwaltet!