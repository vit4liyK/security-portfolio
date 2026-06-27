# Nmap Grundlagen

## Was ist Nmap?
Nmap ist ein Tool, das Netzwerke scannt. Es sendet
Pakete an Geräte und findet heraus welche Ports offen
sind und ob Schwachstellen existieren.

Es wird von Pentestern, Administratoren und
Angreifern benutzt.

## Was sind Ports?
Ports sind wie Türen in einem System. Jeder Dienst
hat seine eigene Tür:
Port 80 ist HTTP
Port 443 ist HTTPS
Port 22 ist SSH
Port 445 ist SMB

Ein offener Port bedeutet die Tür ist offen und
ein Dienst läuft dahinter.

Ein Dienst ist ein Programm, das im Hintergrund läuft
und auf Anfragen wartet. Beispiele:
Webserver (Apache) -> wartet auf Anfragen für Webseiten
SSH-Dienst -> wartet auf Verbindungen für Terminal-Zugriff
Datenbankdienst (MySQL) -> wartet auf Datenbankabfragen
DNS-Dienst -> wartet auf Namensauflösungen


## Scans die ich gemacht habe

### Netzwerk scannen
nmap 10.0.2.0/24
Sucht nach allen aktiven Geräten im Subnetz.

### OS und Versionen erkennen
sudo nmap -O -sV 10.0.2.2
Zeigt das OS und welche Software-Versionen auf den 
offenen Ports laufen.

### Schwachstellen scannen
sudo nmap -sV --script vuln 10.0.2.2
Sucht nach bekannten Schwachstellen auf den offenen Ports.


## Was ist CVE?
CVE steht für Common Vulnerabilities and Exposures.
Es ist eine weltweite Datenbank aller bekannten Sicherheitslücken.
Jede Lücke bekommt eine eindeutige Nummer: CVE-Jahr-Nummer.
Der CVSS-Score zeigt wie gefährlich die Lücke ist - von 0 bis 10. Ab 9.0 ist es Critical.


## WannaCry
WannaCry war Ransomware, die sich automatisch verbreitet hat.
Sie hat CVE-2017-0144 ausgenutzt - eine kritische
Schwachstelle in Port 445 (SMB). Ohne Login konnte ein Angreifer Code ausführen.
WannaCry hat alle Dateien verschlüsselt und Lösegeld gefordert.
300.000 Computer in 150 Ländern wurden infiziert.
Ein Researcher hat den Angriff gestoppt, indem er eine Domain
für 10 Dollar registriert hat - der Kill-Switch.
