# Übung 05: Festplatten, Mounts und Devices (LPI-konform)

## Lernziele
Nach dieser Übung können Sie:
- Block Devices identifizieren und analysieren
- Partitionen erstellen und verwalten (MBR und GPT)
- Verschiedene Dateisysteme erstellen und formatieren
- Dateisysteme mounten und in /etc/fstab konfigurieren
- LVM (Logical Volume Manager) verstehen und anwenden
- Swap-Speicher verwalten
- RAID-Grundlagen verstehen

## Vorbereitung
```bash
# Arbeitsverzeichnis erstellen
mkdir -p ~/disk-exercises
cd ~/disk-exercises

# Prüfen ob wir in einer VM sind (empfohlen für diese Übungen)
echo "WARNUNG: Diese Übungen verändern Partitionen! Nur in einer VM ausführen!"
```

## Teil 1: Block Devices verstehen

### Übung 1.1: Devices identifizieren
```bash
# 1. Alle Block Devices anzeigen
lsblk
lsblk -f  # Mit Dateisystem-Info
lsblk -o NAME,SIZE,TYPE,MOUNTPOINT,FSTYPE,UUID

# 2. Detaillierte Informationen
sudo fdisk -l
sudo parted -l

# 3. Device-Dateien untersuchen
ls -la /dev/sd*
ls -la /dev/nvme*  # Für NVMe SSDs
ls -la /dev/vd*   # Für virtuelle Disks (KVM)

# 4. Kernel-Nachrichten zu Disks
dmesg | grep -E 'sd[a-z]|nvme'

# 5. Disk-Statistiken
cat /proc/partitions
df -h
df -i  # Inode-Nutzung
```

### Übung 1.2: Device-Informationen sammeln
```bash
# 1. Detaillierte Hardware-Infos
sudo hdparm -I /dev/sda | less  # Nur für IDE/SATA
sudo smartctl -a /dev/sda       # SMART-Daten

# 2. UUID und Labels anzeigen
sudo blkid
ls -la /dev/disk/by-uuid/
ls -la /dev/disk/by-label/
ls -la /dev/disk/by-id/

# 3. Mount-Informationen
mount | column -t
findmnt
findmnt -D  # Mit Dateisystem-Optionen
cat /proc/mounts
```

## Teil 2: Partitionierung

### Übung 2.1: MBR-Partitionierung mit fdisk
```bash
# ACHTUNG: Nur auf Test-Disk ausführen!
# Beispiel mit /dev/sdb (anpassen!)

# 1. Aktuelle Partitionstabelle anzeigen
sudo fdisk -l /dev/sdb

# 2. Interaktive Partitionierung starten
sudo fdisk /dev/sdb

# fdisk-Befehle:
# p - Partitionstabelle anzeigen
# n - Neue Partition
# d - Partition löschen  
# t - Partitionstyp ändern
# w - Änderungen schreiben
# q - Ohne Speichern beenden

# 3. Beispiel: Neue Partitionen erstellen
# Im fdisk-Prompt:
n  # Neue Partition
p  # Primary
1  # Partitionsnummer
   # Enter für Start-Default
+2G  # 2GB Größe

n  # Zweite Partition
p  # Primary
2  # Partitionsnummer
   # Enter für Start-Default
+1G  # 1GB Größe

t  # Typ ändern
2  # Partition 2
82 # Linux Swap

p  # Anzeigen
w  # Schreiben

# 4. Kernel über neue Partitionstabelle informieren
sudo partprobe /dev/sdb
```

### Übung 2.2: GPT-Partitionierung mit gdisk
```bash
# GPT für Disks > 2TB oder UEFI-Systeme

# 1. GPT-Partitionen erstellen
sudo gdisk /dev/sdb

# gdisk-Befehle ähnlich wie fdisk:
# p - print
# n - new
# d - delete
# w - write
# ? - Hilfe

# 2. Beispiel-Session:
o  # Neue GPT-Tabelle
Y  # Bestätigen

n  # Neue Partition
1  # Nummer
   # Enter für Start
+512M  # EFI System Partition
ef00   # EFI System Type

n  # Root Partition
2
   # Enter
+10G
8300  # Linux filesystem

n  # Home Partition
3
   # Enter
   # Enter (Rest der Disk)
8300

p  # Anzeigen
w  # Schreiben
Y  # Bestätigen
```

### Übung 2.3: Partitionierung mit parted
```bash
# Parted für scriptbare Partitionierung

# 1. Interaktiver Modus
sudo parted /dev/sdb
(parted) print
(parted) mklabel gpt  # oder msdos für MBR
(parted) mkpart primary ext4 1MiB 2GiB
(parted) mkpart primary linux-swap 2GiB 3GiB
(parted) mkpart primary ext4 3GiB 100%
(parted) print
(parted) quit

# 2. Nicht-interaktiver Modus (für Scripts)
sudo parted -s /dev/sdb mklabel gpt
sudo parted -s /dev/sdb mkpart primary ext4 1MiB 2GiB
sudo parted -s /dev/sdb mkpart primary linux-swap 2GiB 3GiB
sudo parted -s /dev/sdb mkpart primary ext4 3GiB 100%

# 3. Alignment prüfen
sudo parted /dev/sdb align-check optimal 1
```

## Teil 3: Dateisysteme

### Übung 3.1: Dateisysteme erstellen
```bash
# 1. ext4 (Standard Linux-Dateisystem)
sudo mkfs.ext4 /dev/sdb1
sudo mkfs.ext4 -L "DATA" /dev/sdb3  # Mit Label
sudo mkfs.ext4 -m 1 /dev/sdb3       # 1% reserviert statt 5%

# 2. ext3 (älteres System)
sudo mkfs.ext3 /dev/sdb1

# 3. XFS (für große Dateien)
sudo mkfs.xfs /dev/sdb1
sudo mkfs.xfs -L "BIGDATA" /dev/sdb1

# 4. Btrfs (modernes CoW-Dateisystem)
sudo mkfs.btrfs /dev/sdb1
sudo mkfs.btrfs -L "SNAPSHOT" /dev/sdb1

# 5. FAT32 (für USB-Sticks, Windows-Kompatibilität)
sudo mkfs.vfat -F 32 /dev/sdb1
sudo mkfs.vfat -F 32 -n "USB" /dev/sdb1

# 6. NTFS (Windows)
sudo mkfs.ntfs /dev/sdb1
sudo mkfs.ntfs -Q -L "WINDOWS" /dev/sdb1  # Quick format

# 7. Swap
sudo mkswap /dev/sdb2
sudo mkswap -L "SWAP01" /dev/sdb2
```

### Übung 3.2: Dateisystem-Eigenschaften anpassen
```bash
# 1. ext4 tunen
sudo tune2fs -l /dev/sdb1  # Eigenschaften anzeigen
sudo tune2fs -L "NEWLABEL" /dev/sdb1  # Label ändern
sudo tune2fs -m 2 /dev/sdb1  # Reserved blocks auf 2%
sudo tune2fs -c 50 /dev/sdb1  # fsck nach 50 mounts
sudo tune2fs -i 180d /dev/sdb1  # fsck alle 180 Tage

# 2. Dateisystem prüfen
sudo fsck /dev/sdb1
sudo fsck.ext4 -f /dev/sdb1  # Force check
sudo e2fsck -f /dev/sdb1     # Ausführliche Prüfung

# 3. XFS Eigenschaften
sudo xfs_info /dev/sdb1
sudo xfs_admin -L "NEWLABEL" /dev/sdb1
```

## Teil 4: Mounting

### Übung 4.1: Manuelles Mounten
```bash
# 1. Mount-Punkte erstellen
sudo mkdir -p /mnt/{data,backup,usb}

# 2. Einfaches mounten
sudo mount /dev/sdb1 /mnt/data
sudo mount -t ext4 /dev/sdb1 /mnt/data  # Mit Dateisystem-Typ

# 3. Mount-Optionen
sudo mount -o ro /dev/sdb1 /mnt/backup  # Read-only
sudo mount -o noexec,nosuid /dev/sdb1 /mnt/data  # Sicherheit
sudo mount -o uid=1000,gid=1000 /dev/sdb1 /mnt/usb  # Für FAT32

# 4. Bind-Mounts
sudo mount --bind /home/user/docs /mnt/docs
sudo mount --rbind /home /mnt/home-backup  # Rekursiv

# 5. Mount-Status prüfen
mount | grep sdb
findmnt /mnt/data
df -h /mnt/data

# 6. Unmounten
sudo umount /mnt/data
sudo umount -l /mnt/data  # Lazy unmount
sudo umount -f /mnt/data  # Force unmount
```

### Übung 4.2: /etc/fstab konfigurieren
```bash
# 1. Backup erstellen
sudo cp /etc/fstab /etc/fstab.backup

# 2. UUIDs ermitteln
sudo blkid

# 3. fstab editieren
sudo nano /etc/fstab

# Beispiel-Einträge:
# UUID=xxxx-xxxx /mnt/data ext4 defaults 0 2
# UUID=yyyy-yyyy /mnt/backup ext4 ro,noatime 0 2
# UUID=zzzz-zzzz none swap sw 0 0
# /dev/sdb1 /mnt/usb vfat uid=1000,gid=1000,umask=022 0 0

# 4. fstab testen
sudo mount -a  # Alle fstab-Einträge mounten
sudo findmnt --verify  # fstab-Syntax prüfen

# 5. Systemd mount units (modern)
sudo systemctl list-units --type=mount
sudo systemctl status mnt-data.mount
```

### Übung 4.3: Spezielle Mount-Optionen
```bash
# 1. Performance-Optionen
sudo mount -o noatime,nodiratime /dev/sdb1 /mnt/data

# 2. Quota aktivieren
sudo mount -o usrquota,grpquota /dev/sdb1 /mnt/data
sudo quotacheck -cug /mnt/data
sudo quotaon /mnt/data

# 3. Verschlüsselte Devices
sudo cryptsetup luksFormat /dev/sdb1
sudo cryptsetup open /dev/sdb1 encrypted
sudo mkfs.ext4 /dev/mapper/encrypted
sudo mount /dev/mapper/encrypted /mnt/secure

# 4. Loop Devices
dd if=/dev/zero of=disk.img bs=1M count=100
sudo losetup /dev/loop0 disk.img
sudo mkfs.ext4 /dev/loop0
sudo mount /dev/loop0 /mnt/loop
```

## Teil 5: LVM (Logical Volume Manager)

### Übung 5.1: LVM einrichten
```bash
# 1. Physical Volumes erstellen
sudo pvcreate /dev/sdb1 /dev/sdb2
sudo pvs
sudo pvdisplay

# 2. Volume Group erstellen
sudo vgcreate vg_data /dev/sdb1 /dev/sdb2
sudo vgs
sudo vgdisplay vg_data

# 3. Logical Volumes erstellen
sudo lvcreate -L 2G -n lv_home vg_data
sudo lvcreate -L 1G -n lv_var vg_data
sudo lvcreate -l 100%FREE -n lv_data vg_data
sudo lvs
sudo lvdisplay

# 4. Dateisysteme auf LVs erstellen
sudo mkfs.ext4 /dev/vg_data/lv_home
sudo mkfs.ext4 /dev/vg_data/lv_var
sudo mkfs.xfs /dev/vg_data/lv_data

# 5. Mounten
sudo mkdir -p /mnt/lvm/{home,var,data}
sudo mount /dev/vg_data/lv_home /mnt/lvm/home
sudo mount /dev/vg_data/lv_var /mnt/lvm/var
sudo mount /dev/vg_data/lv_data /mnt/lvm/data
```

### Übung 5.2: LVM verwalten
```bash
# 1. LV vergrößern
sudo lvextend -L +500M /dev/vg_data/lv_home
sudo resize2fs /dev/vg_data/lv_home  # ext4
sudo xfs_growfs /mnt/lvm/data        # xfs

# 2. VG erweitern
sudo pvcreate /dev/sdc1
sudo vgextend vg_data /dev/sdc1

# 3. Snapshots
sudo lvcreate -L 500M -s -n snap_home /dev/vg_data/lv_home
sudo mount /dev/vg_data/snap_home /mnt/snapshot

# 4. LV entfernen
sudo umount /mnt/lvm/home
sudo lvremove /dev/vg_data/lv_home
```

## Teil 6: Swap-Verwaltung

### Übung 6.1: Swap einrichten
```bash
# 1. Swap-Partition
sudo mkswap /dev/sdb2
sudo swapon /dev/sdb2
sudo swapon -s  # Status

# 2. Swap-Datei
sudo dd if=/dev/zero of=/swapfile bs=1M count=1024
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# 3. Swap-Prioritäten
sudo swapon -p 10 /dev/sdb2
sudo swapon -p 5 /swapfile

# 4. In fstab eintragen
echo "UUID=xxxx-xxxx none swap sw,pri=10 0 0" | sudo tee -a /etc/fstab
echo "/swapfile none swap sw,pri=5 0 0" | sudo tee -a /etc/fstab

# 5. Swap-Nutzung überwachen
free -h
cat /proc/swaps
vmstat 1 5
```

## Teil 7: RAID-Grundlagen

### Übung 7.1: Software-RAID mit mdadm
```bash
# 1. RAID 1 (Mirror) erstellen
sudo mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1

# 2. RAID-Status
cat /proc/mdstat
sudo mdadm --detail /dev/md0

# 3. Dateisystem auf RAID
sudo mkfs.ext4 /dev/md0
sudo mount /dev/md0 /mnt/raid

# 4. RAID-Konfiguration speichern
sudo mdadm --detail --scan >> /etc/mdadm/mdadm.conf

# 5. RAID überwachen
sudo mdadm --monitor --scan --daemonize

# 6. Disk-Fehler simulieren
sudo mdadm --fail /dev/md0 /dev/sdb1
sudo mdadm --remove /dev/md0 /dev/sdb1
sudo mdadm --add /dev/md0 /dev/sdb1
```

## Teil 8: Erweiterte Übungen

### Übung 8.1: Disk-Performance testen
```bash
# 1. hdparm Test
sudo hdparm -tT /dev/sda

# 2. dd Test
dd if=/dev/zero of=/mnt/data/testfile bs=1G count=1 oflag=direct

# 3. fio Benchmark
sudo apt install fio
fio --name=randwrite --ioengine=libaio --rw=randwrite --bs=4k --direct=1 --size=1G --numjobs=1 --runtime=60 --group_reporting --filename=/mnt/data/testfile

# 4. iostat Monitoring
iostat -x 1
iotop
```

### Übung 8.2: Automatisierungs-Script
```bash
#!/bin/bash
# auto-mount.sh - Automatisches Mount-Script

# Funktion zum sicheren Mounten
safe_mount() {
    local device=$1
    local mountpoint=$2
    local fstype=$3
    
    # Prüfen ob Device existiert
    if [ ! -b "$device" ]; then
        echo "Error: Device $device nicht gefunden"
        return 1
    fi
    
    # Mount-Punkt erstellen
    sudo mkdir -p "$mountpoint"
    
    # Versuche zu mounten
    if sudo mount -t "$fstype" "$device" "$mountpoint"; then
        echo "Erfolgreich gemountet: $device -> $mountpoint"
        df -h "$mountpoint"
    else
        echo "Mount fehlgeschlagen: $device"
        return 1
    fi
}

# Alle nicht gemounteten Partitionen finden
echo "Suche nicht gemountete Partitionen..."
lsblk -rpo NAME,TYPE,MOUNTPOINT | while read name type mount; do
    if [ "$type" == "part" ] && [ -z "$mount" ]; then
        echo "Gefunden: $name (nicht gemountet)"
        # Hier könnte auto-mount Logic folgen
    fi
done
```

### Übung 8.3: Disaster Recovery
```bash
# 1. Backup der Partitionstabelle
sudo sfdisk -d /dev/sda > partition-backup-sda.txt
sudo sgdisk --backup=gpt-backup-sda /dev/sda  # Für GPT

# 2. Restore der Partitionstabelle
sudo sfdisk /dev/sda < partition-backup-sda.txt
sudo sgdisk --load-backup=gpt-backup-sda /dev/sda

# 3. Dateisystem-Backup mit dd
sudo dd if=/dev/sda1 of=/backup/sda1.img bs=4M status=progress

# 4. MBR Backup
sudo dd if=/dev/sda of=mbr-backup.img bs=512 count=1

# 5. Vollständiges System-Backup
sudo tar -cvpzf backup.tar.gz --exclude=/backup --exclude=/proc --exclude=/tmp --exclude=/mnt --exclude=/dev --exclude=/sys /
```

## Praxis-Projekt: Storage-Management-System

Erstellen Sie ein vollständiges Storage-Management-Setup:

```bash
#!/bin/bash
# storage-setup.sh - Komplettes Storage-Setup

set -e

echo "=== Storage Management System Setup ==="

# 1. LVM Setup
echo "Erstelle LVM-Struktur..."
sudo pvcreate /dev/sdb /dev/sdc
sudo vgcreate vg_storage /dev/sdb /dev/sdc

# Logical Volumes
sudo lvcreate -L 5G -n lv_system vg_storage
sudo lvcreate -L 10G -n lv_data vg_storage
sudo lvcreate -L 2G -n lv_backup vg_storage
sudo lvcreate -L 1G -n lv_swap vg_storage

# 2. Dateisysteme
echo "Erstelle Dateisysteme..."
sudo mkfs.ext4 -L "SYSTEM" /dev/vg_storage/lv_system
sudo mkfs.xfs -L "DATA" /dev/vg_storage/lv_data
sudo mkfs.ext4 -L "BACKUP" /dev/vg_storage/lv_backup
sudo mkswap -L "SWAP" /dev/vg_storage/lv_swap

# 3. Mount-Punkte
echo "Erstelle Mount-Struktur..."
sudo mkdir -p /storage/{system,data,backup}

# 4. fstab aktualisieren
echo "Aktualisiere /etc/fstab..."
cat << EOF | sudo tee -a /etc/fstab
# Storage Management System
/dev/vg_storage/lv_system /storage/system ext4 defaults,noatime 0 2
/dev/vg_storage/lv_data /storage/data xfs defaults,noatime 0 2
/dev/vg_storage/lv_backup /storage/backup ext4 defaults,noatime 0 2
/dev/vg_storage/lv_swap none swap sw 0 0
EOF

# 5. Alles mounten
echo "Mounte Dateisysteme..."
sudo mount -a
sudo swapon -a

# 6. Status anzeigen
echo "=== Storage Status ==="
df -h | grep storage
echo ""
sudo vgdisplay vg_storage
echo ""
sudo lvs vg_storage
echo ""
swapon -s

echo "Storage-Setup abgeschlossen!"
```

## Troubleshooting-Befehle

```bash
# Disk-Probleme diagnostizieren
dmesg | grep -i error
journalctl -xe | grep -i "i/o error"
smartctl -H /dev/sda

# Mount-Probleme lösen
lsof /mnt/data  # Zeigt Prozesse die das Unmount verhindern
fuser -mv /mnt/data
umount -l /mnt/data  # Lazy unmount

# Dateisystem-Reparatur
fsck -y /dev/sdb1  # Automatisch reparieren
xfs_repair /dev/sdb1  # Für XFS

# LVM-Probleme
vgscan
vgchange -ay  # Alle VGs aktivieren
pvck /dev/sdb  # Physical Volume prüfen

# Performance-Probleme
iostat -x 1
iotop -o
hdparm -tT /dev/sda
```

## Abschluss-Checkliste

- [ ] Block Devices mit lsblk, fdisk -l identifizieren
- [ ] MBR und GPT Partitionen erstellen
- [ ] Verschiedene Dateisysteme (ext4, xfs, btrfs) formatieren
- [ ] Manuelles Mounten und /etc/fstab konfigurieren
- [ ] LVM-Setup mit PV, VG, LV erstellen
- [ ] Swap-Speicher einrichten und verwalten
- [ ] Basis-RAID-Konfiguration verstehen
- [ ] Performance-Tests durchführen
- [ ] Backup-Strategien implementieren