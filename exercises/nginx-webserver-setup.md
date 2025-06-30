# Praktische Übung: Nginx Webserver auf AWS

## 🎯 Übungsziel
**Dauer**: 90 Minuten  
**Schwierigkeit**: Anwendung der Grundlagen  
**Voraussetzungen**: Grundlegende Linux-Befehle, AWS-Account  

**Lernziele:**
- Ersten eigenen Webserver auf AWS einrichten
- Paketmanagement in der Praxis anwenden
- Services verwalten mit systemctl
- Dateiberechtigungen praktisch nutzen
- Troubleshooting in echter Umgebung

---

## 🚀 Vorbereitung: AWS Instance starten

### Schritt 1: EC2 Instance erstellen
```bash
# AWS Console: https://console.aws.amazon.com/ec2/
# 1. "Launch Instance" klicken
# 2. Ubuntu Server 22.04 LTS auswählen
# 3. Instance Type: t2.micro (Free Tier)
# 4. Key Pair: Erstellen oder vorhandenes verwenden
# 5. Security Group: SSH (22) und HTTP (80) erlauben
# 6. Storage: 8GB Standard (reicht für Übung)
```

### Schritt 2: SSH-Verbindung herstellen
```bash
# Ihre .pem Datei herunterladen und sicher speichern
chmod 400 ~/Downloads/mein-key.pem

# Mit Instance verbinden (IP-Adresse aus AWS Console)
ssh -i ~/Downloads/mein-key.pem ubuntu@[IHRE-PUBLIC-IP]

# Beispiel:
ssh -i ~/Downloads/linux101-key.pem ubuntu@3.250.123.45
```

### ✅ Checkpoint 1
- [ ] Erfolgreich mit AWS Instance verbunden
- [ ] Prompt zeigt: `ubuntu@ip-xxx-xxx-xxx-xxx:~$`
- [ ] Kommando `whoami` gibt "ubuntu" zurück

---

## 📦 Teil 1: System vorbereiten (20 Min.)

### Aufgabe 1.1: System-Informationen sammeln
```bash
# Wo sind wir?
pwd
hostname

# Was haben wir für ein System?
lsb_release -a
uname -a

# Wie viel Speicher?
free -h
df -h

# Welche Netzwerk-Konfiguration?
ip addr show
```

**📝 Notieren Sie sich:**
- Ubuntu-Version: _______________
- Verfügbarer RAM: _______________
- Öffentliche IP: _______________

### Aufgabe 1.2: System aktualisieren
```bash
# Paketlisten aktualisieren
sudo apt update

# Ausgabe verstehen:
# "Hit" = keine Änderung
# "Get" = neue Pakete verfügbar
# "Ign" = Repository ignoriert

# Wie viele Updates verfügbar?
apt list --upgradable | wc -l

# System upgraden
sudo apt upgrade -y
```

**🤔 Reflexionsfrage:** Warum führen wir `apt update` vor `apt upgrade` aus?

<details>
<summary>💡 Antwort</summary>

`apt update` lädt die neuesten Paketlisten herunter, aber installiert nichts. `apt upgrade` installiert dann die Updates basierend auf diesen Listen. Ohne `update` würde `upgrade` veraltete Informationen verwenden.

</details>

---

## 🌐 Teil 2: Nginx installieren (25 Min.)

### Aufgabe 2.1: Nginx-Paket installieren
```bash
# Prüfen ob nginx bereits installiert
which nginx
systemctl status nginx

# Nginx installieren
sudo apt install nginx -y

# Installation verifizieren
nginx -v
which nginx

# Status des Service prüfen
sudo systemctl status nginx
```

**Erwartete Ausgabe:**
```
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since...
```

### Aufgabe 2.2: Nginx-Konfiguration verstehen
```bash
# Wo sind die wichtigen Dateien?
ls -la /etc/nginx/

# Hauptkonfiguration anschauen
sudo cat /etc/nginx/nginx.conf | head -20

# Default Website-Konfiguration
sudo cat /etc/nginx/sites-available/default

# Wo liegen die Webseiten-Dateien?
ls -la /var/www/html/
```

### Aufgabe 2.3: Ersten Test durchführen
```bash
# Lokaler Test
curl localhost

# Was sollten Sie sehen?
# <!DOCTYPE html>
# <html>
# <head>
# <title>Welcome to nginx!</title>

# Von außen testen (andere Methode)
curl http://[IHRE-PUBLIC-IP]
```

**🎉 Erfolg:** Wenn Sie HTML-Code sehen, läuft Ihr Webserver!

**📱 Browser-Test:** Öffnen Sie http://[IHRE-PUBLIC-IP] im Browser

---

## ✏️ Teil 3: Eigene Webseite erstellen (30 Min.)

### Aufgabe 3.1: Eigene HTML-Seite erstellen
```bash
# Backup der Original-Seite
sudo cp /var/www/html/index.nginx-debian.html /var/www/html/index.nginx-debian.html.backup

# Neue Index-Seite erstellen
sudo nano /var/www/html/index.html
```

**Inhalt für index.html:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mein Linux 101 Webserver</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; background: #f4f4f4; }
        .container { background: white; padding: 30px; border-radius: 10px; }
        h1 { color: #333; }
        .info { background: #e9f7ff; padding: 15px; border-left: 4px solid #007acc; }
        .success { color: #28a745; font-weight: bold; }
    </style>
</head>
<body>
    <div class="container">
        <h1>🎉 Erfolg! Mein erster Linux Webserver</h1>
        
        <div class="info">
            <h3>Server-Informationen:</h3>
            <p><strong>Betriebssystem:</strong> Ubuntu 22.04 LTS</p>
            <p><strong>Webserver:</strong> Nginx</p>
            <p><strong>Standort:</strong> AWS EC2</p>
            <p><strong>Erstellt von:</strong> [IHR NAME]</p>
            <p><strong>Datum:</strong> [HEUTIGES DATUM]</p>
        </div>

        <h3>🔧 Was ich gelernt habe:</h3>
        <ul>
            <li>EC2 Instance starten und SSH-Verbindung</li>
            <li>apt Paketmanager verwenden</li>
            <li>systemctl Services verwalten</li>
            <li>Dateien mit nano bearbeiten</li>
            <li>Berechtigungen verstehen</li>
        </ul>

        <p class="success">✅ Linux 101 - Mission erfolgreich!</p>
    </div>
</body>
</html>
```

### Aufgabe 3.2: Webseite testen
```bash
# Lokaler Test
curl localhost | head -10

# Browser-Test durchführen
# Öffnen Sie: http://[IHRE-PUBLIC-IP]
```

### Aufgabe 3.3: Weitere Seiten hinzufügen
```bash
# Info-Seite erstellen
sudo nano /var/www/html/info.html
```

**Inhalt für info.html:**
```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Server Information</title>
</head>
<body>
    <h1>Server-Details</h1>
    <pre>
# Diese Informationen mit Linux-Befehlen gesammelt:
Hostname: $(hostname)
Uptime: $(uptime)
Disk Usage: $(df -h /)
Memory: $(free -h)
    </pre>
    <p><a href="/">← Zurück zur Hauptseite</a></p>
</body>
</html>
```

---

## 🔧 Teil 4: Service-Management (15 Min.)

### Aufgabe 4.1: Nginx steuern
```bash
# Service stoppen
sudo systemctl stop nginx

# Status prüfen
sudo systemctl status nginx

# Website testen (sollte nicht erreichbar sein)
curl localhost

# Service wieder starten
sudo systemctl start nginx

# Status prüfen
sudo systemctl status nginx

# Service neu laden (ohne Unterbrechung)
sudo systemctl reload nginx

# Service neu starten
sudo systemctl restart nginx
```

### Aufgabe 4.2: Autostart konfigurieren
```bash
# Prüfen ob nginx automatisch startet
sudo systemctl is-enabled nginx

# Autostart aktivieren (falls nicht schon aktiv)
sudo systemctl enable nginx

# Autostart deaktivieren (nur zum Testen)
sudo systemctl disable nginx

# Wieder aktivieren
sudo systemctl enable nginx
```

### Aufgabe 4.3: Logs untersuchen
```bash
# Nginx Access Logs anschauen
sudo tail -f /var/log/nginx/access.log

# In anderem Terminal: Website aufrufen
curl localhost

# Error Logs prüfen
sudo tail /var/log/nginx/error.log

# Systemd Logs für nginx
sudo journalctl -u nginx -n 20
```

---

## 🛡️ Teil 5: Sicherheit und Berechtigungen

### Aufgabe 5.1: Berechtigungen verstehen
```bash
# Wem gehören die Web-Dateien?
ls -la /var/www/html/

# Nginx-Benutzer prüfen
ps aux | grep nginx

# Nginx läuft als welcher Benutzer?
# Master Process: root
# Worker Processes: www-data
```

### Aufgabe 5.2: Berechtigungen anpassen
```bash
# Sichere Berechtigungen setzen
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/

# Prüfen
ls -la /var/www/html/
```

### Aufgabe 5.3: Firewall-Status prüfen
```bash
# UFW Status
sudo ufw status

# Falls aktiv: HTTP erlauben
sudo ufw allow 'Nginx Full'
sudo ufw status verbose
```

---

## 🔍 Troubleshooting-Szenarien

### Szenario 1: Nginx startet nicht
```bash
# Problem simulieren
sudo systemctl stop nginx
sudo nano /etc/nginx/nginx.conf
# Fügen Sie eine ungültige Zeile hinzu: "invalid syntax;"

# Versuchen zu starten
sudo systemctl start nginx

# Fehler diagnostizieren
sudo systemctl status nginx
sudo nginx -t
sudo journalctl -u nginx -n 10

# Problem beheben
sudo nano /etc/nginx/nginx.conf
# Ungültige Zeile entfernen
sudo systemctl start nginx
```

### Szenario 2: Website nicht erreichbar
```bash
# Mögliche Ursachen prüfen:

# 1. Service läuft?
sudo systemctl status nginx

# 2. Port 80 gebunden?
sudo ss -tlnp | grep :80

# 3. Firewall blockiert?
sudo ufw status

# 4. AWS Security Group?
# In AWS Console prüfen: Port 80 erlaubt?
```

---

## 📋 Abschluss-Checkliste

### Erfolgs-Verifizierung:
- [ ] Nginx erfolgreich installiert
- [ ] Eigene HTML-Seite erstellt und erreichbar
- [ ] Service-Befehle verstanden (start/stop/restart/reload)
- [ ] Logs gelesen und interpretiert
- [ ] Grundlegende Troubleshooting durchgeführt
- [ ] Berechtigungen verstanden

### Aufräumen (Optional):
```bash
# Instance beenden um Kosten zu sparen
# AWS Console → EC2 → Instance auswählen → Actions → Instance State → Terminate

# Oder stoppen für später:
# AWS Console → EC2 → Instance auswählen → Actions → Instance State → Stop
```

---

## 🎯 Reflexions-Fragen

1. **Was war anders als erwartet?**
   _________________________________

2. **Welcher Befehl war am nützlichsten?**
   _________________________________

3. **Was würden Sie als nächstes erkunden?**
   _________________________________

4. **Welche Herausforderung war am schwierigsten?**
   _________________________________

---

## 🚀 Bonus-Herausforderungen

### Level 1: SSL/HTTPS aktivieren
```bash
# Let's Encrypt installieren
sudo apt install certbot python3-certbot-nginx

# Domain benötigt (für echtes SSL)
# Für Übung: Self-signed certificate
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/nginx-selfsigned.key \
    -out /etc/ssl/certs/nginx-selfsigned.crt
```

### Level 2: Virtual Hosts einrichten
```bash
# Zweite Website erstellen
sudo mkdir /var/www/test
sudo nano /var/www/test/index.html

# Neue Site-Konfiguration
sudo nano /etc/nginx/sites-available/test

# Site aktivieren
sudo ln -s /etc/nginx/sites-available/test /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### Level 3: Monitoring einrichten
```bash
# Nginx Status Page aktivieren
sudo nano /etc/nginx/sites-available/default
# Fügen Sie location /nginx_status hinzu

# Monitoring mit curl
curl localhost/nginx_status
```

---

## 📚 Weiterführende Ressourcen

- [Nginx Beginner's Guide](https://nginx.org/en/docs/beginners_guide.html)
- [AWS EC2 User Guide](https://docs.aws.amazon.com/ec2/index.html)
- [Ubuntu Server Guide](https://ubuntu.com/server/docs)

---

**🎉 Herzlichen Glückwunsch!** Sie haben erfolgreich Ihren ersten Webserver auf AWS eingerichtet und dabei viele Linux-Grundlagen praktisch angewendet!