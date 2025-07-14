# AWS EC2 User Data Automatisierung - Übung

## Lernziele
- User Data Scripts für EC2-Instanzen erstellen
- Automatische Software-Installation beim Boot
- Verifizierung und Logging implementieren
- Fehlerbehandlung in User Data Scripts
- Cloud-Init vs. Shell Scripts verstehen

## Voraussetzungen
- AWS Account mit EC2-Zugriff
- Grundlegende Linux-Kenntnisse
- Verständnis von Bash-Scripting

## Teil 1: Basis User Data Script

### Übung 1.1: Einfaches Installation Script

Erstellen Sie ein User Data Script, das beim Boot grundlegende Tools installiert:

```bash
#!/bin/bash
# Basis User Data Script für Ubuntu/Debian

# Logging einrichten
exec > >(tee /var/log/user-data.log)
exec 2>&1
echo "User Data Script gestartet: $(date)"

# System aktualisieren
apt-get update -y
apt-get upgrade -y

# Grundlegende Tools installieren
apt-get install -y \
    curl \
    wget \
    git \
    htop \
    tree \
    unzip \
    jq

# Verifizierung
echo "=== Installierte Pakete prüfen ==="
for package in curl wget git htop tree unzip jq; do
    if dpkg -l | grep -q "^ii  $package"; then
        echo "✓ $package erfolgreich installiert"
    else
        echo "✗ $package Installation fehlgeschlagen"
    fi
done

echo "User Data Script beendet: $(date)"
```

### Übung 1.2: Web Server Setup

User Data Script für einen NGINX Web Server:

```bash
#!/bin/bash
set -e  # Bei Fehler abbrechen

# Logging
LOG_FILE="/var/log/userdata-webserver.log"
exec > >(tee -a $LOG_FILE)
exec 2>&1

echo "========================================="
echo "Web Server Setup gestartet: $(date)"
echo "========================================="

# Variablen
DOMAIN="example.com"
WEB_ROOT="/var/www/html"

# System Update
echo "System wird aktualisiert..."
apt-get update -y
apt-get upgrade -y

# NGINX installieren
echo "NGINX wird installiert..."
apt-get install -y nginx

# Firewall konfigurieren
echo "Firewall wird konfiguriert..."
ufw --force enable
ufw allow ssh
ufw allow 'Nginx Full'

# Custom Index Page erstellen
cat > $WEB_ROOT/index.html << 'EOF'
<!DOCTYPE html>
<html>
<head>
    <title>EC2 Web Server</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 50px; }
        .info { background-color: #e7f3fe; padding: 20px; border-radius: 5px; }
    </style>
</head>
<body>
    <h1>EC2 Web Server läuft!</h1>
    <div class="info">
        <p><strong>Instance ID:</strong> <span id="instance-id">Lädt...</span></p>
        <p><strong>Availability Zone:</strong> <span id="az">Lädt...</span></p>
        <p><strong>Public IP:</strong> <span id="public-ip">Lädt...</span></p>
        <p><strong>Setup Zeit:</strong> SETUP_TIME</p>
    </div>
    <script>
        // EC2 Metadaten abrufen
        fetch('http://169.254.169.254/latest/meta-data/instance-id')
            .then(r => r.text())
            .then(data => document.getElementById('instance-id').textContent = data);
        
        fetch('http://169.254.169.254/latest/meta-data/placement/availability-zone')
            .then(r => r.text())
            .then(data => document.getElementById('az').textContent = data);
            
        fetch('http://169.254.169.254/latest/meta-data/public-ipv4')
            .then(r => r.text())
            .then(data => document.getElementById('public-ip').textContent = data);
    </script>
</body>
</html>
EOF

# Setup-Zeit einfügen
sed -i "s/SETUP_TIME/$(date)/" $WEB_ROOT/index.html

# NGINX neustarten
systemctl restart nginx
systemctl enable nginx

# Verifizierung
echo "=== Service Status prüfen ==="
if systemctl is-active --quiet nginx; then
    echo "✓ NGINX läuft"
else
    echo "✗ NGINX läuft nicht"
    exit 1
fi

# Test der Webseite
if curl -s http://localhost | grep -q "EC2 Web Server"; then
    echo "✓ Webseite erreichbar"
else
    echo "✗ Webseite nicht erreichbar"
fi

echo "Web Server Setup abgeschlossen: $(date)"
```

## Teil 2: Erweiterte Installationen

### Übung 2.1: Docker Installation mit Verifizierung

```bash
#!/bin/bash
# Docker Installation mit umfassender Verifizierung

# Fehlerbehandlung
set -euo pipefail
trap 'echo "Fehler in Zeile $LINENO"' ERR

# Logging Setup
LOG_DIR="/var/log/ec2-userdata"
mkdir -p $LOG_DIR
LOG_FILE="$LOG_DIR/docker-setup-$(date +%Y%m%d-%H%M%S).log"
exec > >(tee -a $LOG_FILE)
exec 2>&1

echo "================================================"
echo "Docker Installation gestartet: $(date)"
echo "Instance: $(ec2-metadata --instance-id | cut -d' ' -f2)"
echo "================================================"

# Funktion für Statusmeldungen
log_status() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1"
}

# Funktion für Verifizierung
verify_installation() {
    local package=$1
    local command=$2
    
    log_status "Prüfe $package..."
    
    if command -v $command &> /dev/null; then
        version=$($command --version 2>/dev/null || echo "Version nicht verfügbar")
        log_status "✓ $package installiert: $version"
        return 0
    else
        log_status "✗ $package nicht gefunden"
        return 1
    fi
}

# System vorbereiten
log_status "System wird vorbereitet..."
apt-get update -y
apt-get install -y \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Docker GPG Key hinzufügen
log_status "Docker Repository wird eingerichtet..."
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Docker Repository hinzufügen
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null

# Docker installieren
log_status "Docker wird installiert..."
apt-get update -y
apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin

# Docker Service starten
log_status "Docker Service wird gestartet..."
systemctl start docker
systemctl enable docker

# Docker Gruppe einrichten
usermod -aG docker ubuntu 2>/dev/null || true

# Verifizierung
log_status "=== Installation wird verifiziert ==="

# Docker verifizieren
verify_installation "Docker" "docker"

# Docker Compose verifizieren
verify_installation "Docker Compose" "docker-compose"

# Docker Service Status
if systemctl is-active --quiet docker; then
    log_status "✓ Docker Service läuft"
    
    # Docker Info
    docker info --format "Docker Version: {{.ServerVersion}}"
    docker info --format "Storage Driver: {{.Driver}}"
    
    # Test Container starten
    log_status "Teste Docker mit Hello World Container..."
    if docker run --rm hello-world &> /dev/null; then
        log_status "✓ Docker Container Test erfolgreich"
    else
        log_status "✗ Docker Container Test fehlgeschlagen"
    fi
else
    log_status "✗ Docker Service läuft nicht"
    exit 1
fi

# Erstelle Docker Status Script
cat > /usr/local/bin/check-docker << 'EOF'
#!/bin/bash
echo "=== Docker Status ==="
echo "Service: $(systemctl is-active docker)"
echo "Version: $(docker --version)"
echo "Containers: $(docker ps -q | wc -l) running"
echo "Images: $(docker images -q | wc -l) total"
EOF

chmod +x /usr/local/bin/check-docker

log_status "Docker Installation abgeschlossen!"
log_status "Log-Datei: $LOG_FILE"
```

### Übung 2.2: Monitoring Stack (Prometheus + Grafana)

```bash
#!/bin/bash
# Monitoring Stack Installation

# Konfiguration
PROMETHEUS_VERSION="2.45.0"
GRAFANA_VERSION="10.0.0"
NODE_EXPORTER_VERSION="1.6.0"

# Logging
LOG_FILE="/var/log/monitoring-setup.log"
exec > >(tee -a $LOG_FILE)
exec 2>&1

echo "Monitoring Stack Installation: $(date)"

# Benutzer erstellen
useradd --no-create-home --shell /bin/false prometheus
useradd --no-create-home --shell /bin/false node_exporter

# Verzeichnisse erstellen
mkdir -p /etc/prometheus /var/lib/prometheus
mkdir -p /var/lib/grafana

# Prometheus installieren
cd /tmp
wget -q https://github.com/prometheus/prometheus/releases/download/v${PROMETHEUS_VERSION}/prometheus-${PROMETHEUS_VERSION}.linux-amd64.tar.gz
tar xzf prometheus-${PROMETHEUS_VERSION}.linux-amd64.tar.gz
cp prometheus-${PROMETHEUS_VERSION}.linux-amd64/{prometheus,promtool} /usr/local/bin/
cp -r prometheus-${PROMETHEUS_VERSION}.linux-amd64/{consoles,console_libraries} /etc/prometheus/
chown -R prometheus:prometheus /etc/prometheus /var/lib/prometheus

# Prometheus Konfiguration
cat > /etc/prometheus/prometheus.yml << 'EOF'
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
  
  - job_name: 'node'
    static_configs:
      - targets: ['localhost:9100']
EOF

# Prometheus Service
cat > /etc/systemd/system/prometheus.service << 'EOF'
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
EOF

# Node Exporter installieren
wget -q https://github.com/prometheus/node_exporter/releases/download/v${NODE_EXPORTER_VERSION}/node_exporter-${NODE_EXPORTER_VERSION}.linux-amd64.tar.gz
tar xzf node_exporter-${NODE_EXPORTER_VERSION}.linux-amd64.tar.gz
cp node_exporter-${NODE_EXPORTER_VERSION}.linux-amd64/node_exporter /usr/local/bin/
chown node_exporter:node_exporter /usr/local/bin/node_exporter

# Node Exporter Service
cat > /etc/systemd/system/node_exporter.service << 'EOF'
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
EOF

# Grafana installieren
apt-get install -y software-properties-common
add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
wget -q -O - https://packages.grafana.com/gpg.key | apt-key add -
apt-get update -y
apt-get install -y grafana

# Services starten
systemctl daemon-reload
systemctl start prometheus node_exporter grafana-server
systemctl enable prometheus node_exporter grafana-server

# Verifizierung
echo "=== Service Verifizierung ==="
services=("prometheus" "node_exporter" "grafana-server")
for service in "${services[@]}"; do
    if systemctl is-active --quiet $service; then
        echo "✓ $service läuft"
    else
        echo "✗ $service läuft nicht"
    fi
done

# Port Verifizierung
echo "=== Port Verifizierung ==="
ports=("9090:Prometheus" "9100:Node-Exporter" "3000:Grafana")
for port_info in "${ports[@]}"; do
    port="${port_info%%:*}"
    name="${port_info#*:}"
    if ss -tlnp | grep -q ":$port "; then
        echo "✓ $name läuft auf Port $port"
    else
        echo "✗ $name nicht erreichbar auf Port $port"
    fi
done

# Erstelle Status Script
cat > /usr/local/bin/check-monitoring << 'EOF'
#!/bin/bash
echo "=== Monitoring Stack Status ==="
echo "Prometheus: http://$(curl -s http://169.254.169.254/latest/meta-data/public-ipv4):9090"
echo "Grafana: http://$(curl -s http://169.254.169.254/latest/meta-data/public-ipv4):3000"
echo ""
curl -s localhost:9090/-/healthy && echo " - Prometheus ist healthy"
curl -s localhost:9100/metrics | head -5 && echo " - Node Exporter liefert Metriken"
EOF

chmod +x /usr/local/bin/check-monitoring

echo "Monitoring Stack Installation abgeschlossen!"
```

## Teil 3: Cloud-Init Integration

### Übung 3.1: Cloud-Init mit mehreren Formaten

```yaml
#cloud-config
# Cloud-Init Konfiguration für umfassende System-Setup

# Pakete aktualisieren
package_update: true
package_upgrade: true

# Zu installierende Pakete
packages:
  - nginx
  - postgresql
  - redis-server
  - python3-pip
  - nodejs
  - npm
  - git
  - curl
  - htop

# Benutzer erstellen
users:
  - name: appuser
    groups: [sudo, docker]
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh_authorized_keys:
      - ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC... your-key-here

# Dateien erstellen
write_files:
  - path: /etc/motd
    content: |
      ################################################
      #  Willkommen auf dem Application Server       #
      #  Umgebung: Production                        #
      #  Setup: $(date)                              #
      ################################################
    
  - path: /home/ubuntu/app-setup.sh
    permissions: '0755'
    content: |
      #!/bin/bash
      echo "Application Setup wird ausgeführt..."
      
      # Node.js App Setup
      cd /home/ubuntu
      git clone https://github.com/example/sample-app.git
      cd sample-app
      npm install
      
      # PM2 installieren
      npm install -g pm2
      
      # App starten
      pm2 start app.js --name "sample-app"
      pm2 save
      pm2 startup systemd -u ubuntu --hp /home/ubuntu
      
  - path: /usr/local/bin/health-check
    permissions: '0755'
    content: |
      #!/bin/bash
      echo "=== System Health Check ==="
      echo "Datum: $(date)"
      echo ""
      echo "CPU Auslastung:"
      top -bn1 | grep "Cpu(s)" | awk '{print "  "$2" %"}'
      echo ""
      echo "Speicher:"
      free -h | grep "^Mem:" | awk '{print "  Total: "$2", Used: "$3", Free: "$4}'
      echo ""
      echo "Festplatte:"
      df -h / | tail -1 | awk '{print "  Total: "$2", Used: "$3", Free: "$4", Usage: "$5}'
      echo ""
      echo "Laufende Services:"
      for service in nginx postgresql redis; do
        if systemctl is-active --quiet $service; then
          echo "  ✓ $service"
        else
          echo "  ✗ $service"
        fi
      done

# Befehle ausführen
runcmd:
  # System konfigurieren
  - echo "127.0.0.1 app.local" >> /etc/hosts
  
  # PostgreSQL konfigurieren
  - sudo -u postgres createuser appuser
  - sudo -u postgres createdb appdb -O appuser
  
  # Redis konfigurieren
  - sed -i 's/^# requirepass/requirepass mysecretpassword/' /etc/redis/redis.conf
  - systemctl restart redis-server
  
  # Application Setup ausführen
  - su - ubuntu -c '/home/ubuntu/app-setup.sh'
  
  # Firewall konfigurieren
  - ufw allow 22/tcp
  - ufw allow 80/tcp
  - ufw allow 443/tcp
  - ufw --force enable
  
  # Logging einrichten
  - |
    cat > /etc/rsyslog.d/30-userdata.conf << EOF
    :programname, isequal, "cloud-init" /var/log/cloud-init-output.log
    & stop
    EOF
  - systemctl restart rsyslog
  
  # Abschlussprüfung
  - /usr/local/bin/health-check > /var/log/initial-health-check.log

# Services verwalten
manage_etc_hosts: true

# Finale Nachricht
final_message: "System bereit nach $UPTIME Sekunden"
```

### Übung 3.2: Kombiniertes Shell und Cloud-Init Script

```bash
#!/bin/bash
# Multipart User Data - Shell Script Teil

# Dieser Teil wird als Shell Script ausgeführt
LOG_FILE="/var/log/custom-setup.log"
exec > >(tee -a $LOG_FILE)
exec 2>&1

echo "Custom Setup Script gestartet: $(date)"

# Funktion für farbige Ausgaben
print_status() {
    case $1 in
        "success") echo -e "\033[32m✓ $2\033[0m" ;;
        "error") echo -e "\033[31m✗ $2\033[0m" ;;
        "info") echo -e "\033[34mℹ $2\033[0m" ;;
    esac
}

# EC2 Metadaten abrufen
INSTANCE_ID=$(ec2-metadata --instance-id | cut -d " " -f 2)
AZ=$(ec2-metadata --availability-zone | cut -d " " -f 2)
REGION=$(echo $AZ | sed 's/[a-z]$//')

print_info "Instance: $INSTANCE_ID in $AZ"

# Tags abrufen und als Umgebungsvariablen setzen
aws ec2 describe-tags --region $REGION \
    --filters "Name=resource-id,Values=$INSTANCE_ID" \
    --query 'Tags[*].[Key,Value]' --output text | \
while read key value; do
    export "TAG_${key}=${value}"
    echo "export TAG_${key}='${value}'" >> /etc/environment
done

# Anwendungsspezifisches Setup basierend auf Tags
if [ ! -z "$TAG_Environment" ]; then
    case "$TAG_Environment" in
        "production")
            print_info "Production Setup wird ausgeführt..."
            # Production-spezifische Konfiguration
            ;;
        "staging")
            print_info "Staging Setup wird ausgeführt..."
            # Staging-spezifische Konfiguration
            ;;
        "development")
            print_info "Development Setup wird ausgeführt..."
            # Development-spezifische Konfiguration
            ;;
    esac
fi

# CloudWatch Agent installieren
print_info "CloudWatch Agent wird installiert..."
wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb
dpkg -i amazon-cloudwatch-agent.deb
rm amazon-cloudwatch-agent.deb

# CloudWatch Agent Konfiguration
cat > /opt/aws/amazon-cloudwatch-agent/etc/config.json << 'EOF'
{
  "metrics": {
    "namespace": "EC2/CustomMetrics",
    "metrics_collected": {
      "cpu": {
        "measurement": [
          "cpu_usage_idle",
          "cpu_usage_iowait"
        ],
        "metrics_collection_interval": 60
      },
      "disk": {
        "measurement": [
          "used_percent"
        ],
        "metrics_collection_interval": 60,
        "resources": [
          "*"
        ]
      },
      "mem": {
        "measurement": [
          "mem_used_percent"
        ],
        "metrics_collection_interval": 60
      }
    }
  },
  "logs": {
    "logs_collected": {
      "files": {
        "collect_list": [
          {
            "file_path": "/var/log/user-data.log",
            "log_group_name": "/aws/ec2/userdata",
            "log_stream_name": "{instance_id}"
          },
          {
            "file_path": "/var/log/nginx/access.log",
            "log_group_name": "/aws/ec2/nginx",
            "log_stream_name": "{instance_id}-access"
          }
        ]
      }
    }
  }
}
EOF

# CloudWatch Agent starten
/opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl \
    -a fetch-config \
    -m ec2 \
    -s \
    -c file:/opt/aws/amazon-cloudwatch-agent/etc/config.json

print_status "success" "CloudWatch Agent konfiguriert und gestartet"

# Erstelle umfassendes Verifizierungs-Script
cat > /usr/local/bin/verify-setup << 'EOF'
#!/bin/bash

echo "================================"
echo "Setup Verifizierung"
echo "================================"
echo ""

# Farben
GREEN='\033[0;32m'
RED='\033[0;31m'
NC='\033[0m'

# Funktion für Service-Check
check_service() {
    if systemctl is-active --quiet $1; then
        echo -e "${GREEN}✓${NC} $1 läuft"
        return 0
    else
        echo -e "${RED}✗${NC} $1 läuft nicht"
        return 1
    fi
}

# Funktion für Port-Check
check_port() {
    if nc -z localhost $1 2>/dev/null; then
        echo -e "${GREEN}✓${NC} Port $1 ist offen ($2)"
        return 0
    else
        echo -e "${RED}✗${NC} Port $1 ist geschlossen ($2)"
        return 1
    fi
}

# Funktion für Datei-Check
check_file() {
    if [ -f "$1" ]; then
        echo -e "${GREEN}✓${NC} Datei existiert: $1"
        return 0
    else
        echo -e "${RED}✗${NC} Datei fehlt: $1"
        return 1
    fi
}

# Services prüfen
echo "Services:"
services=("nginx" "postgresql" "redis-server" "amazon-cloudwatch-agent")
for service in "${services[@]}"; do
    check_service $service
done
echo ""

# Ports prüfen
echo "Ports:"
check_port 80 "HTTP"
check_port 443 "HTTPS"
check_port 5432 "PostgreSQL"
check_port 6379 "Redis"
echo ""

# Wichtige Dateien prüfen
echo "Konfigurationsdateien:"
check_file "/etc/nginx/nginx.conf"
check_file "/etc/postgresql/*/main/postgresql.conf"
check_file "/etc/redis/redis.conf"
echo ""

# System-Ressourcen
echo "System-Ressourcen:"
echo "CPU Cores: $(nproc)"
echo "RAM: $(free -h | grep "^Mem:" | awk '{print $2}')"
echo "Disk: $(df -h / | tail -1 | awk '{print $2}')"
echo ""

# EC2 Metadaten
echo "EC2 Information:"
echo "Instance ID: $(ec2-metadata --instance-id | cut -d' ' -f2)"
echo "Instance Type: $(ec2-metadata --instance-type | cut -d' ' -f2)"
echo "Public IP: $(ec2-metadata --public-ipv4 | cut -d' ' -f2)"
echo ""

# Installierte Pakete
echo "Wichtige Pakete:"
packages=("nginx" "postgresql" "redis-server" "python3" "nodejs")
for pkg in "${packages[@]}"; do
    if dpkg -l | grep -q "^ii  $pkg"; then
        version=$(dpkg -l | grep "^ii  $pkg" | awk '{print $3}')
        echo -e "${GREEN}✓${NC} $pkg ($version)"
    else
        echo -e "${RED}✗${NC} $pkg nicht installiert"
    fi
done

echo ""
echo "Verifizierung abgeschlossen: $(date)"
EOF

chmod +x /usr/local/bin/verify-setup

# Abschließende Verifizierung ausführen
print_info "Führe abschließende Verifizierung aus..."
/usr/local/bin/verify-setup > /var/log/setup-verification.log 2>&1

# Setup-Abschluss
print_status "success" "User Data Script abgeschlossen!"
echo "Logs verfügbar unter:"
echo "  - /var/log/user-data.log"
echo "  - /var/log/cloud-init-output.log"
echo "  - /var/log/setup-verification.log"
```

## Teil 4: Debugging und Troubleshooting

### Übung 4.1: Debug-fähiges User Data Script

```bash
#!/bin/bash
# User Data Script mit umfassenden Debug-Funktionen

# Debug-Modus aktivieren
DEBUG=${DEBUG:-true}
DRY_RUN=${DRY_RUN:-false}

# Logging Setup
LOG_DIR="/var/log/ec2-userdata"
mkdir -p $LOG_DIR
MAIN_LOG="$LOG_DIR/main.log"
ERROR_LOG="$LOG_DIR/errors.log"
DEBUG_LOG="$LOG_DIR/debug.log"

# Logging-Funktionen
log() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] $@" | tee -a $MAIN_LOG
}

log_error() {
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] ERROR: $@" | tee -a $ERROR_LOG >&2
}

log_debug() {
    if [ "$DEBUG" = "true" ]; then
        echo "[$(date '+%Y-%m-%d %H:%M:%S')] DEBUG: $@" >> $DEBUG_LOG
    fi
}

# Fehlerbehandlung
trap 'error_handler $? $LINENO' ERR

error_handler() {
    local exit_code=$1
    local line_number=$2
    log_error "Script fehlgeschlagen mit Exit Code $exit_code in Zeile $line_number"
    
    # Kontext sammeln
    log_error "Letzter Befehl: $BASH_COMMAND"
    log_error "Stack Trace:"
    local frame=0
    while caller $frame; do
        ((frame++))
    done | tee -a $ERROR_LOG
    
    # System-Status bei Fehler
    log_error "System Status:"
    df -h >> $ERROR_LOG
    free -m >> $ERROR_LOG
    ps aux | head -20 >> $ERROR_LOG
    
    exit $exit_code
}

# Funktion für sichere Befehlsausführung
safe_execute() {
    local cmd="$@"
    log_debug "Ausführung: $cmd"
    
    if [ "$DRY_RUN" = "true" ]; then
        log "DRY RUN: $cmd"
        return 0
    fi
    
    local start_time=$(date +%s)
    
    if output=$($cmd 2>&1); then
        local end_time=$(date +%s)
        local duration=$((end_time - start_time))
        log_debug "Erfolgreich ($duration Sekunden): $cmd"
        [ ! -z "$output" ] && log_debug "Output: $output"
        return 0
    else
        local exit_code=$?
        log_error "Fehlgeschlagen: $cmd"
        log_error "Output: $output"
        return $exit_code
    fi
}

# Systeminfo sammeln
log "=== System Information ==="
log "Hostname: $(hostname)"
log "OS: $(lsb_release -d | cut -f2)"
log "Kernel: $(uname -r)"
log "CPU: $(nproc) cores"
log "Memory: $(free -h | grep Mem | awk '{print $2}')"
log "Disk: $(df -h / | tail -1 | awk '{print $2}')"

# EC2 Metadaten mit Fehlerbehandlung
log "=== EC2 Metadata ==="
for metadata in instance-id instance-type public-ipv4 availability-zone; do
    if value=$(curl -s --connect-timeout 2 http://169.254.169.254/latest/meta-data/$metadata 2>/dev/null); then
        log "$metadata: $value"
    else
        log_error "Konnte $metadata nicht abrufen"
    fi
done

# Hauptinstallation
log "=== Hauptinstallation startet ==="

# Paketliste definieren
PACKAGES=(
    "nginx"
    "postgresql"
    "redis-server"
    "python3-pip"
    "monitoring-tools"  # Absichtlich falsches Paket für Fehlertest
)

# Pakete installieren mit Fehlerbehandlung
for package in "${PACKAGES[@]}"; do
    log "Installiere $package..."
    
    if safe_execute "apt-get install -y $package"; then
        log "✓ $package erfolgreich installiert"
        
        # Paket-spezifische Konfiguration
        case $package in
            "nginx")
                safe_execute "systemctl start nginx"
                safe_execute "systemctl enable nginx"
                ;;
            "postgresql")
                safe_execute "systemctl start postgresql"
                safe_execute "systemctl enable postgresql"
                ;;
            "redis-server")
                safe_execute "systemctl start redis-server"
                safe_execute "systemctl enable redis-server"
                ;;
        esac
    else
        log_error "✗ $package Installation fehlgeschlagen"
        # Entscheiden, ob kritisch
        if [[ " nginx postgresql " =~ " $package " ]]; then
            log_error "Kritisches Paket $package fehlt - Abbruch"
            exit 1
        fi
    fi
done

# Erstelle Diagnose-Script
cat > /usr/local/bin/ec2-diagnose << 'EOF'
#!/bin/bash

echo "EC2 User Data Diagnose Tool"
echo "==========================="
echo ""

# Logs anzeigen
echo "Letzte User Data Log-Einträge:"
tail -20 /var/log/ec2-userdata/main.log 2>/dev/null || echo "Kein Log gefunden"
echo ""

echo "Letzte Fehler:"
tail -10 /var/log/ec2-userdata/errors.log 2>/dev/null || echo "Keine Fehler"
echo ""

# Cloud-Init Status
echo "Cloud-Init Status:"
cloud-init status --long 2>/dev/null || echo "Cloud-Init Status nicht verfügbar"
echo ""

# Service Status
echo "Service Status:"
for service in nginx postgresql redis-server; do
    systemctl is-active $service &>/dev/null && echo "✓ $service" || echo "✗ $service"
done
echo ""

# Netzwerk Tests
echo "Netzwerk Tests:"
curl -s --connect-timeout 2 http://169.254.169.254/latest/meta-data/instance-id &>/dev/null && \
    echo "✓ EC2 Metadata erreichbar" || echo "✗ EC2 Metadata nicht erreichbar"

ping -c 1 8.8.8.8 &>/dev/null && echo "✓ Internet erreichbar" || echo "✗ Internet nicht erreichbar"
echo ""

# Disk und Memory
echo "Ressourcen:"
df -h / | tail -1
free -h | grep Mem
echo ""

# Log-Dateien
echo "Verfügbare Log-Dateien:"
ls -la /var/log/ec2-userdata/ 2>/dev/null
ls -la /var/log/cloud-init*.log 2>/dev/null
EOF

chmod +x /usr/local/bin/ec2-diagnose

# Abschluss
log "=== Installation abgeschlossen ==="
log "Diagnose-Tool verfügbar: /usr/local/bin/ec2-diagnose"
log "Logs unter: $LOG_DIR"

# Finale Verifizierung
/usr/local/bin/verify-setup 2>&1 | tee -a $MAIN_LOG

# CloudWatch Metriken senden (optional)
if command -v aws &>/dev/null; then
    aws cloudwatch put-metric-data \
        --namespace "EC2/UserData" \
        --metric-name "SetupComplete" \
        --value 1 \
        --dimensions Instance=$INSTANCE_ID \
        --region $REGION 2>/dev/null || log_debug "CloudWatch Metrik konnte nicht gesendet werden"
fi

log "User Data Script beendet: $(date)"
```

## Teil 5: Best Practices Checkliste

### Übung 5.1: Template für Production-Ready User Data

```bash
#!/bin/bash
# Production-Ready User Data Template

#############################################
# KONFIGURATION
#############################################
SCRIPT_VERSION="1.0.0"
ENVIRONMENT="${ENVIRONMENT:-production}"
LOG_RETENTION_DAYS=30
MAX_RETRY_ATTEMPTS=3
HEALTH_CHECK_URL="http://localhost/health"

#############################################
# FUNKTIONEN
#############################################

# ... (Logging und Error-Handling Funktionen von oben)

# Retry-Funktion
retry() {
    local max_attempts=$1
    local delay=$2
    local command="${@:3}"
    local attempt=0
    
    until [ $attempt -ge $max_attempts ]; do
        log_debug "Versuch $((attempt+1))/$max_attempts: $command"
        
        if eval "$command"; then
            return 0
        fi
        
        attempt=$((attempt+1))
        [ $attempt -lt $max_attempts ] && sleep $delay
    done
    
    log_error "Befehl fehlgeschlagen nach $max_attempts Versuchen: $command"
    return 1
}

# Cleanup-Funktion
cleanup() {
    log "Führe Cleanup aus..."
    
    # Temporäre Dateien löschen
    rm -f /tmp/userdata-*
    
    # Alte Logs rotieren
    find $LOG_DIR -name "*.log" -mtime +$LOG_RETENTION_DAYS -delete
    
    # Sensitive Daten entfernen
    history -c
    > ~/.bash_history
}

# Signal-Handler
trap cleanup EXIT

#############################################
# HAUPTSKRIPT
#############################################

log "=== User Data Script v$SCRIPT_VERSION gestartet ==="
log "Environment: $ENVIRONMENT"

# 1. System-Updates mit Retry
retry $MAX_RETRY_ATTEMPTS 5 "apt-get update -y"

# 2. Installationen
# ... (Ihre Installationen hier)

# 3. Health Check
log "Führe Health Check aus..."
retry 5 10 "curl -f $HEALTH_CHECK_URL"

# 4. Benachrichtigung (optional)
if [ "$ENVIRONMENT" = "production" ]; then
    # SNS-Benachrichtigung senden
    aws sns publish \
        --topic-arn "arn:aws:sns:region:account:topic" \
        --message "EC2 Instance $INSTANCE_ID erfolgreich gestartet" \
        2>/dev/null || log_debug "SNS-Benachrichtigung fehlgeschlagen"
fi

log "=== Script erfolgreich beendet ==="
```

## Abschlussaufgabe

Erstellen Sie ein vollständiges User Data Script für eine Laravel-Anwendung mit:
1. PHP 8.2, Composer, MySQL
2. NGINX mit SSL (Let's Encrypt)
3. Redis für Caching
4. Automatisches Git-Deploy
5. Umfassende Verifizierung
6. CloudWatch Integration
7. Backup-Einrichtung

## Troubleshooting-Tipps

### Logs überprüfen:
```bash
# Cloud-Init Logs
sudo cat /var/log/cloud-init.log
sudo cat /var/log/cloud-init-output.log

# Eigene Logs
sudo tail -f /var/log/user-data.log

# System Logs
sudo journalctl -u cloud-init
```

### Häufige Fehler:
1. **Timeout**: Scripts sollten < 16 KB sein
2. **Encoding**: Immer UTF-8 verwenden
3. **Shebang**: `#!/bin/bash` nicht vergessen
4. **Berechtigungen**: Root-Rechte beachten
5. **Netzwerk**: Warten bis Netzwerk bereit

### Test-Kommandos:
```bash
# User Data abrufen
curl http://169.254.169.254/latest/user-data

# Cloud-Init Status
cloud-init status
cloud-init analyze show

# Manuell ausführen
sudo cloud-init clean
sudo cloud-init init
```