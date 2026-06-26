# Linux Forensik Checkliste

## 1. Wer existiert auf dem System?
cat /etc/passwd

## 2. Wann wurde er erstellt? (Datum in shadow)
sudo grep benutzername /etc/shadow

## 3. Hat er eine echte Shell?
grep benutzername /etc/passwd | cut -d: -f7

## 4. Ist er in root, sudo oder adm Gruppe?
grep benutzername /etc/group

## 5. Wo liegt sein Heimordner und was ist drin?
ls -la /home/benutzername

## 6. Login-Historie prüfen: Wer hat sich wann eingeloggt?
sudo last

# Fehlgeschlagene Logins: Wer hat versucht reinzukommen?
sudo last -f /var/log/btmp

# Fokus auf: unbekannte Benutzer, ungewöhnliche Zeiten, fremde IPs


## 7. Installierte Programme
# Was zuletzt installiert wurde:
cat /var/log/dpkg.log | tail -20

# Was gerade installiert ist - komplette Liste:
dpkg --list

# Nur Security-relevante Tools suchen:
dpkg --list | grep -E "netcat|nmap|wireshark|metasploit"
# Liste bei Bedarf erweitern


## 8. Versteckte Tools finden 
# Angreifer kann Tools umbenennen und mit . verstecken

#1. Laufende Prozesse prüfen:
ps aux

#2. Netzwerkverbindungen prüfen:
ss -tulnp

#3. Dateien nach Inhalt prüfen, nicht nach Name:
file /tmp/.systemd-helper (Beispiel)

#4. Neue Dateien finden:
find / -newer /etc/passwd -type f 2>/dev/null

# Findet alle Dateien die neuer sind als passwd - also die nach dem ersten System-Setup erstellt wurden  
