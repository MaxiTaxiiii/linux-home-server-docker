
## Linux Home Server

Verfasser: **Maksymilian Saferyjski 2CHIT**

Datum: **13.01.2025**

## 1. Einführung
Ich bin mir sicher, dass wir alle mit Windows oder Mac schon bekannt sind. Jedes Betriebssystem hat seine Vor- und Nachteile, aber das heutzutage am meistgenutzte Betriebssystem für Computer, die als Server fungieren, ist Linux. Linux ist open source, kostenlos und hat keine strengen Voraussetzungen, was Hardware betrifft. Nachteil jedoch ist, dass Programme die, in Windows oder Mac funktionieren, werden höchstwahrscheinlich nicht auf Linux funktionieren. Aufgrund dass Linux open source ist, gibt es verschiedene Distributions, die man nutzen kann. In dieser EK werden ich mich mit Ubuntu auseinandersetzen und ein nützlichen Home Server zusammenbastelln.
## 2. Projektbeschreibung
Es wurde ein Ubuntu Home Server realisiert, mit dem Samba, Home Assistant, Sonarr, PiVPN und Plex eingerichtet wurde. Dies wurde mit verschiedenen Mitteln erreicht, wie z.B. Docker oder dem APT Manager.
## 3. Theorie

Linux Terminal 

Docker 

Netzwerktechnik

## 4. Arbeitsschritte
**Ubuntu installieren**

Ubuntu ISO-Datei aus dem Internet herunterladen und auf einen USB-Stick mit balenaEtcher flashen

In den USB-Stick reinbooten bzw VM starten

Ubuntu vollständig installieren

**OpenSSH**

Weil Server meistens keine grafische Oberfläche haben, werden sie mit OpenSSH ferngesteuert
Als Voraussetzung braucht unser Server eine statische IP-Adresse, dies kann ganz einfach gemacht werden indem man auf die Netzwerkeinstellungen geht

```Einstellungen -> Netzwerk -> auf das kleine Zahnrad -> IPv4```

Statische IPv4 einstellen z.B.

 ```Adresse: 192.168.0.50 Subnetzmaske: 255.255.255.0 Gateway: 192.168.0.1 DNS: 1.1.1.1 ```

Netzwerk neustarten und nun haben wir eine statische IP-Adresse

Um OpenSSH zu installieren muss man in das Terminal eintauchen

Package Manager auf den neusten Stand bringen

```sudo apt update```

OpenSSH installieren

```sudo apt install openssh-server```

Prüfen ob OpenSSH läuft

```sudo systemctl status ssh```

Umsteigen aufs externe Gerät und Powershell öffnen

In Powershell eingeben:

```ssh benutzername@IP-Adresse des Servers z.B. 192.168.0.50```

Passwort eingeben

Nun können wir unseren Server fernsteuern, aber nur wenn wir uns in dem selben LAN befinden wie der Server

**Samba Fileshare**

Prüfen ob wir auf dem neusten Stand sind

```sudo apt update```

Samba installieren

```sudo apt install samba```

Prüfen ob Samba auch wirklich installiert ist

```samba --version```

Ein Ordner für Samba erstellen

z.B. ```mkdir maksymilian-share```

Nun müssen wir noch Samba konfigurieren, damit er diesen Ordner auch wirklich nutzt

```sudo nano /etc/samba/smb.conf```

Nach ganz unten scrollen und folgende Zeilen hinzufügen

```
[maksymilian-share]
    comment = Maksymilian Samba Share
    path = \home\maksymilian\maksymilian-share
    read only = no
    browsable = yes
```

```strg-x + y + enter``` um zu speichern und schließen

Samba neustarten

```sudo service smbd restart```

Firewall konfigurieren damit Samba das Netzwerk ohne Probleme navigieren kann

```sudo ufw allow samba```

Benutzername und Passwort für Samba festlegen

```sudo smbpasswd -a maksymilian```

Passwort festlegen

Nun sollten wir in der Lage sein, mit unserem Server, Dateien auszutauschen

Um dies zu überprüfen, geht man in den File Explorer -> diesen PC -> Netzlaufwerk verbinden

<img src="img/image.png" alt="Netzlaufwerk" style="zoom:33%;"/>

Nach Eingabe unserer Logindaten sollten wir nun in der Lage sein, auf unseren Samba Share zuzugreifen

<img src="img/image2.png" alt="Netzlaufwerk" style="zoom:33%;"/>

Nun können wir mit unserem Server Dateien austauschen

**Plex**


















