# Anleitung: Bernd als neuen Mitarbeiter unter Linux anlegen

1. **Damit Bernd Support‑Tickets annehmen kann, gründen wir die Helpdesk‑Abteilung.**

```bash
sudo groupadd helpdesk
```

2. **Für spätere Systempflege legen wir außerdem die Gruppe der Administratoren an.**

```bash
sudo groupadd administrator
```

3. **Jetzt bekommt Bernd sein Konto, primär der Helpdesk‑Gruppe zugeordnet, mit Home‑Verzeichnis und Bash‑Shell.**

```bash
sudo useradd -m -s /bin/bash -g helpdesk bernd
```

4. **Wir vergeben ein Passwort, damit er sich anmelden kann.**

```bash
sudo passwd bernd
```

5. **Ein Check bestätigt seine UID, GID und Gruppen.**

```bash
id bernd
```

6. **Bernd erhält zusätzlich Administrator‑Rechte.**

```bash
sudo usermod -aG administrator bernd
```

7. **Wir prüfen seine Doppelrolle.**

```bash
groups bernd
```

8. **Das Team braucht einen gemeinsamen Helpdesk‑Ordner.**

```bash
sudo mkdir -p /srv/helpdesk
```

9. **Der Ordner gehört der Helpdesk‑Gruppe und bekommt das Set‑GID‑Bit – aber noch keine Schreibrechte für die Gruppe.**

```bash
sudo chown :helpdesk /srv/helpdesk
sudo chmod g+s /srv/helpdesk
```

10. **Bernd versucht eine Ticketliste anzulegen – und scheitert an den fehlenden Schreibrechten:**

```bash
sudo -u bernd touch /srv/helpdesk/ticketliste.txt
# touch: cannot touch '/srv/helpdesk/ticketliste.txt': Permission denied
```

11. **Wir bemerken den Fehler und gewähren der Gruppe jetzt Schreibrechte; Set‑GID bleibt erhalten.**

```bash
sudo chmod 2775 /srv/helpdesk    # rwxrwsr-x
```

12. **Ein kurzer Blick bestätigt die neuen Rechte (s für Set‑GID, w für group‑write).**

```bash
ls -ld /srv/helpdesk
```

13. **Nun gelingt Bernds Testdatei ohne Fehlermeldung.**

```bash
sudo -u bernd touch /srv/helpdesk/ticketliste.txt
```

14. **Wir kontrollieren Besitzer und Gruppe der Datei.**

```bash
ls -l /srv/helpdesk/ticketliste.txt
```

15. **Für sensible Logs richten wir einen separaten Admin‑Ordner ein – ebenfalls mit Set‑GID und richtigen Rechten.**

```bash
sudo mkdir -p /srv/admin
sudo chown :administrator /srv/admin
sudo chmod 2775 /srv/admin
```

16. **Bernd legt dort eine Wartungsdatei an.**

```bash
sudo -u bernd touch /srv/admin/maintenance.log
```

17. **Ein Überblick über beide Dateien zeigt korrekte Gruppen und Berechtigungen.**

```bash
stat --format='%n: %A %U:%G' /srv/helpdesk/ticketliste.txt /srv/admin/maintenance.log
```

18. **Wenn Bernd später nur noch Admin ist, entfernen wir ihn aus der Helpdesk‑Gruppe.**

```bash
sudo gpasswd -d bernd helpdesk
```
Wenn du jetzt id bernd machst wird dir immer noch die helpdesk Gruppe angezeigt. Da die helpdesk Gruppe die primäre Gruppe von Bernd ist.
Ändere die Primäre Gruppe auf Administrator und prüfe das Ergebnis mit id bernd

```bash
id bernd
```

```bash
sudo usermod -g administrator bernd
```
19. **Verlässt Bernd das Unternehmen, löschen wir sein Konto samt Home‑Verzeichnis.**

```bash
sudo userdel -r bernd
# Hinweis: Eine Warnung wie "mail spool not found" ist normal.
```

20. **Direkt danach inspizieren wir die Dateien: Der Besitzer erscheint jetzt nur noch als numerische UID (z. B. 1001), weil der Benutzer nicht mehr existiert, während die Gruppen­namen weiterhin aufgelöst werden.**

```bash
stat --format='%n: %A %U:%G' /srv/helpdesk/ticketliste.txt /srv/admin/maintenance.log
```

21. **Sobald die Helpdesk‑Abteilung Geschichte ist, räumen wir auch deren Gruppe auf.**

```bash
sudo groupdel helpdesk
```

22. **Ein letzter Blick zeigt nun sowohl UID als auch GID nur noch als Zahlen, da weder Benutzer noch Gruppe existieren.**

```bash
stat --format='%n: %A %U:%G' /srv/helpdesk/ticketliste.txt /srv/admin/maintenance.log
```

23. **Wir listen jetzt alle Dateien und Verzeichnisse auf, die keinem gültigen Benutzer (*nouser*) oder keiner gültigen Gruppe (*nogroup*) mehr gehören.**

```bash
sudo find /srv \( -nouser -o -nogroup \) -print
```

24. **Alle verwaisten Dateien weisen wir wieder dem Standard‑Benutzer `ubuntu` und der Administrator‑Gruppe zu.**

```bash
sudo chown -R ubuntu:administrator /srv/helpdesk /srv/admin
```

25. **Zum Schluss verifizieren wir, dass die Eigentümer eindeutig aufgelöst werden.**

```bash
stat --format='%n: %A %U:%G' /srv/helpdesk/ticketliste.txt /srv/admin/maintenance.log
```
