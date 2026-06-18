# WSL-Windows-Subsystem-for-Linux
WSL ist ein Programm in Windows, mit dem du Linux direkt in Windows verwenden kannst – ohne extra Installation oder virtuelle Maschine. 


Verfasser: **Niklas Prager**

Datum: **18.06.2026**

## 1. Einführung

Linux-Werkzeuge werden in der Informatik und Systemtechnik häufig verwendet, da viele Entwicklungs-, Analyse- und Administrationsaufgaben effizient über die Kommandozeile ausgeführt werden können. Mit dem Windows Subsystem for Linux (WSL) kann eine Linux-Umgebung direkt unter Windows betrieben werden, wodurch Linux-Befehle genutzt werden können, ohne ein zweites Betriebssystem oder eine klassische virtuelle Maschine einzurichten.

## 2. Projektbeschreibung

In diesem Projekt wurde WSL unter Windows aktiviert und Ubuntu als Linux-Distribution installiert. Danach wurden grundlegende Linux-Befehle zur Navigation und Speicheranalyse ausgeführt, `grep` und `pdfgrep` zum Durchsuchen von Dateien verwendet und zusätzlich eine grafische Oberfläche mit XFCE und XRDP eingerichtet, damit die Linux-Umgebung auch per Remote Desktop genutzt werden kann.

## 3. Theorie

### 3.1 Was ist WSL?

WSL ist eine Funktion von Windows, mit der eine GNU/Linux-Umgebung direkt auf einem Windows-System ausgeführt werden kann. Dadurch können Linux-Kommandos, Werkzeuge und Anwendungen ohne den Overhead einer klassischen virtuellen Maschine verwendet werden. Für dieses Projekt wurde Ubuntu eingesetzt, da Ubuntu offiziell für WSL unterstützt wird und sich einfach über den Microsoft Store beziehungsweise über `wsl --install` einrichten lässt.

### 3.2 Linux-Navigation und Unterschiede zu Windows

Für die Navigation im Linux-Terminal werden vor allem folgende Befehle verwendet:

- `pwd` – zeigt das aktuelle Verzeichnis an
- `ls` – listet Dateien und Ordner auf
- `cd Ordnername` – wechselt in ein Verzeichnis
- `cd ..` – geht eine Ebene zurück
- `mkdir Name` – erstellt ein Verzeichnis
- `rm Datei` – löscht eine Datei

Der wichtigste Unterschied zu Windows besteht darin, dass Linux Pfade mit `/` trennt, während unter Windows `\` verwendet wird. Außerdem arbeitet Linux mit einer einzigen Verzeichnisstruktur, die bei `/` beginnt. Windows ist hingegen typischerweise in Laufwerke wie `C:` oder `D:` gegliedert. In WSL werden Windows-Laufwerke unter `/mnt/` eingebunden, also beispielsweise `C:` unter `/mnt/c`.

### 3.3 Aufbau des Dateisystems in WSL

Das Linux-Dateisystem enthält typische Verzeichnisse wie `/home`, `/etc`, `/usr` oder `/var`. Benutzerdateien liegen normalerweise im Home-Verzeichnis, also zum Beispiel unter `/home/night`. Windows-Dateien bleiben auf dem Windows-Dateisystem, können in WSL aber über `/mnt/c`, `/mnt/d` usw. erreicht werden.

Der Unterschied zu Windows besteht darin, dass Linux kein Laufwerkskonzept im selben Sinn verwendet, sondern eine zusammenhängende Verzeichnisstruktur besitzt. Dadurch wirkt das Dateisystem konsistenter, während Windows stärker auf Laufwerksbuchstaben basiert.

### 3.4 Vorteile von WSL

WSL bietet mehrere Vorteile:

1. Linux-Befehle und Werkzeuge können direkt unter Windows verwendet werden.
2. Es ist keine vollständige virtuelle Maschine erforderlich, wodurch weniger Ressourcen benötigt werden.
3. Windows-Dateien können aus der Linux-Umgebung heraus direkt verwendet werden, etwa über `/mnt/c`.
4. Paketverwaltung mit `apt` ermöglicht eine schnelle Installation zusätzlicher Werkzeuge wie `pdfgrep`.
5. WSL eignet sich gut für Entwicklung, Automatisierung, Skripting und Dateianalyse.

### 3.5 grep und pdfgrep

`grep` ist ein Werkzeug, das Zeilen aus Textdateien oder Eingaben ausgibt, die zu einem bestimmten Muster passen. Es ist ein klassisches Unix/Linux-Werkzeug zur Textsuche. Im Projekt wurde `grep` verwendet, um Dateinamen oder Ausgaben einzuschränken.

`pdfgrep` funktioniert ähnlich, durchsucht jedoch PDF-Dateien direkt. Dabei können Optionen wie `-i` für eine Suche ohne Beachtung der Groß- und Kleinschreibung und `-n` zur Ausgabe der Seitenzahl verwendet werden.

### 3.6 grep in Windows

Ein direktes GNU-`grep` ist unter Windows standardmäßig nicht vorinstalliert. Eine funktional ähnliche Alternative in PowerShell ist `Select-String`. Im Rahmen dieses Projekts wurde jedoch ausschließlich `grep` innerhalb der Ubuntu-Umgebung von WSL eingesetzt.

### 3.7 Remote Desktop mit XRDP und XFCE

Für manche Aufgaben ist eine grafische Oberfläche angenehmer als reines Arbeiten im Terminal. Zu diesem Zweck wurde in WSL die Desktop-Umgebung XFCE installiert und mit XRDP kombiniert. XRDP stellt einen RDP-Dienst bereit, auf den mit der Windows-Anwendung „Remotedesktopverbindung“ zugegriffen werden kann.

## 4. Arbeitsschritte

### 4.1 Aktivierung von WSL in Windows

Zuerst wurde in den Windows-Features das **Windows-Subsystem für Linux** aktiviert. Zusätzlich wurde die **Plattform für virtuelle Computer** aktiviert. Danach wurde das System neu gestartet.

![Aktivierung von WSL in den Windows-Features](Bilder/winFeautures)

### 4.2 Installation von Ubuntu

Anschließend wurde Ubuntu über den Microsoft Store installiert. Beim ersten Start wurde `wsl` geöffnet und ein Linux-Benutzername sowie ein Passwort erstellt. Dieses Passwort wird später auch für `sudo`-Befehle und für die Anmeldung über XRDP benötigt.

![Installation von Ubuntu über den Microsoft Store](Bilder/Ubuntu-Micr)

![Erster Start von Ubuntu und Anlegen von Benutzername und Passwort](Bilder/Ubuntu-start)

### 4.3 System aktualisieren

Nach dem ersten Start wurde das System aktualisiert:

```bash
sudo apt-get update
sudo apt-get upgrade
```

Mit `sudo apt-get update` werden die Paketquellen aktualisiert. Mit `sudo apt-get upgrade` werden installierte Pakete auf neuere Versionen angehoben.



### 4.4 Speicherverbrauch mit `du` anzeigen und sortieren

Zur Anzeige des Festplattenverbrauchs wurde zuerst `du` verwendet:

```bash
du -h
```

Die Option `-h` sorgt für eine menschenlesbare Darstellung, also zum Beispiel in KB oder MB.

Anschließend wurde die Ausgabe nach Größe sortiert:

```bash
du -h | sort -h
```

Um die größten Einträge zuerst zu sehen, wurde die Ausgabe umgekehrt sortiert:

```bash
du -h | sort -hr
```

Dabei wird die Ausgabe von `du` per Pipe (`|`) an `sort` übergeben. Mit `-h` kann `sort` Größenangaben wie K, M oder G korrekt auswerten.

![Speicherverbrauch mit du und sort](Bilder/Ubuntu-Festplatte)

### 4.5 Verwendung von `grep`

`grep` wurde verwendet, um eine Ausgabe einzuschränken. Ein einfaches Beispiel bestand darin, nur PDF-Dateien aus einer Dateiliste anzuzeigen:

```bash
ls | grep pdf
```

Falls Dateiendungen in unterschiedlichen Schreibweisen vorkommen, kann die Suche ohne Berücksichtigung der Groß- und Kleinschreibung durchgeführt werden:

```bash
ls | grep -i pdf
```

Zur Einschränkung auf systemtechnikrelevante Dateien kann beispielsweise nach passenden Dateitypen oder Begriffen gefiltert werden:

```bash
ls | grep -Ei "pdf|txt|log"
```

`grep` durchsucht dabei die Eingabe nach einem Muster und gibt nur passende Zeilen aus.

![Beispiel für grep im Terminal](Bilder/grep-auspr)

### 4.6 Installation von `pdfgrep`

Um Inhalte in PDF-Dateien durchsuchen zu können, wurde `pdfgrep` installiert:

```bash
sudo apt install pdfgrep
```

Die Hilfe dazu kann mit folgender Anweisung aufgerufen werden:

```bash
man pdfgrep
```

Zusätzlich kann die Paketliste vor der Installation noch einmal aktualisiert werden:

```bash
sudo apt-get update
```

![Installation von pdfgrep](Bilder/pdfgrep-downl)

### 4.7 Herunterladen und Vorbereiten der PDF-Dateien

Im nächsten Schritt wurden die PDF-Dateien **Sensornetzwerke**, **Sensoren** sowie **Sensoren und Sensorschnittstellen** aus dem Theorie-Kurs heruntergeladen und im selben Ordner gespeichert.

Danach wurde in WSL in dieses Verzeichnis gewechselt. Da sich die Dateien auf der Windows-Festplatte befanden, wurde ein Pfad unter `/mnt/c/` verwendet, zum Beispiel:

```bash
cd /mnt/c/Users/Name/Downloads/Sensorik
```

Anschließend wurde kontrolliert, ob die PDF-Dateien im Ordner vorhanden waren:

```bash
ls
ls | grep -i pdf
```



### 4.8 Durchsuchen der PDFs nach „kapazitiv“

Für die Suche nach dem Begriff **kapazitiv** wurde folgender Befehl verwendet:

```bash
pdfgrep -i -n -H --cache "kapazitiv" *.pdf
```

Bedeutung der Optionen:

- `-i` – Groß-/Kleinschreibung ignorieren
- `-n` – Seitennummer ausgeben
- `-H` – Dateiname ausgeben
- `--cache` – interne Zwischenspeicherung verwenden

Damit werden alle PDF-Dateien im aktuellen Ordner gleichzeitig durchsucht. Das Platzhalterzeichen `*.pdf` steht für alle Dateien mit der Endung `.pdf`.

![Suche nach kapazitiv mit pdfgrep](Bilder/pdfgrep-benutzt)

### 4.9 Durchsuchen aller PDFs in einem Ordner

Sollen alle PDFs in einem Ordner durchsucht werden, kann ebenfalls das Platzhalterzeichen verwendet werden:

```bash
pdfgrep -i -n -H --cache "kapazitiv" *.pdf
```

Falls auch Unterordner einbezogen werden sollen, kann rekursiv gesucht werden:

```bash
pdfgrep -R -i -n -H --cache "kapazitiv" .
```

### 4.10 Weitere Suchbegriffe

Zusätzlich wurden weitere Begriffe getestet:

```bash
pdfgrep -i -n -H --cache "ultraschall" *.pdf
pdfgrep -i -n -H --cache "microcontroller" *.pdf
pdfgrep -i -n -H --cache "arduino" *.pdf
pdfgrep -i -n -H --cache "piezo" *.pdf
```

Damit konnten relevante Stellen in den bereitgestellten PDF-Dateien schnell gefunden werden.


### 4.11 Installation einer grafischen Oberfläche

Für die grafische Oberfläche wurden in WSL nacheinander folgende Befehle ausgeführt:

```bash
sudo apt update && sudo apt full-upgrade
sudo apt install xfce4 xfce4-goodies
sudo apt install xrdp
sudo cp /etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini.bak
sudo sed -i 's/3389/3390/g' /etc/xrdp/xrdp.ini
sudo sed -i 's/max_bpp=32/#max_bpp=32\nmax_bpp=128/g' /etc/xrdp/xrdp.ini
sudo sed -i 's/xserverbpp=24/#xserverbpp=24\nxserverbpp=128/g' /etc/xrdp/xrdp.ini
sudo /etc/init.d/xrdp start
```

Zuerst wurde das System aktualisiert, danach wurden XFCE und XRDP installiert. Anschließend wurde eine Sicherung der Datei `xrdp.ini` erstellt und die Konfiguration angepasst. Abschließend wurde der XRDP-Dienst gestartet.

![Installation von XFCE und XRDP](Bilder/RemoteDesktopGUI-anfang)

### 4.12 Bearbeitung von `startwm.sh`

Danach wurde mit folgendem Befehl ein Editor direkt im Terminal geöffnet:

```bash
sudo nano /etc/xrdp/startwm.sh
```

In der Datei wurden die letzten beiden Zeilen mit `#` auskommentiert. Danach wurde `startxfce4` am Ende eingefügt.

Beispiel:

```bash
# test -x /etc/X11/Xsession && exec /etc/X11/Xsession
# exec /bin/sh /etc/X11/Xsession
startxfce4
```

Die Datei wurde mit **STRG + O** gespeichert und mit **STRG + X** wieder geschlossen.

![Bearbeitung von startwm.sh in nano](Bilder/RemoteDesktopGUI-geändert)

### 4.13 Verbindung über Remote Desktop

Nach der Konfiguration wurde in Windows die Anwendung **Remote Desktop Connection** beziehungsweise **Remotedesktopverbindung** geöffnet. Anschließend wurde eine Verbindung mit

```text
localhost:3389
```

beziehungsweise

```text
localhost:3390
```

hergestellt.

Nach der Anmeldung mit dem Ubuntu-Benutzer und dem gesetzten Passwort konnte die grafische Oberfläche verwendet werden.

![Starten mit Remote Desktop](Bilder/winRemoteDesk-start)

![Verbindung mit Remote Desktop](Bilder/RemoteDesktopGUI-passwort)

![Erfolgreicher XFCE-Desktop in WSL](Bilder/RemoteDesktopGUI-ende)



### 4.14 Fragestellungen

#### Welche Befehle werden verwendet, um in Linux zu navigieren, und wie unterscheiden sie sich von Windows?

In Linux werden vor allem `pwd`, `ls` und `cd` verwendet. Während Windows stark mit grafischer Navigation und Laufwerksbuchstaben wie `C:` arbeitet, beginnt Linux immer bei `/` und verwendet eine einheitliche Verzeichnisstruktur.

#### Wie ist das Filesystem in WSL aufgebaut und was ist der Unterschied zu Windows?

WSL verwendet ein Linux-Dateisystem mit typischen Verzeichnissen wie `/home`, `/etc` und `/usr`. Windows-Laufwerke werden zusätzlich unter `/mnt/` eingebunden, zum Beispiel `/mnt/c`. Im Unterschied dazu arbeitet Windows primär mit Laufwerksbuchstaben und einer stärker getrennten Struktur.

#### Welche Vorteile hat WSL?

WSL ermöglicht die Nutzung von Linux-Werkzeugen direkt unter Windows, ohne eine klassische virtuelle Maschine einzurichten. Außerdem kann auf Windows-Dateien direkt zugegriffen werden und Werkzeuge wie `grep`, `pdfgrep` oder der Paketmanager `apt` stehen unmittelbar zur Verfügung.

## 5. Zusammenfassung

Im Projekt wurde erfolgreich eine Linux-Umgebung mit WSL unter Windows eingerichtet. Die grundlegende Navigation im Linux-Dateisystem, die Analyse des Speicherverbrauchs sowie die Verwendung von `grep` und `pdfgrep` konnten praktisch durchgeführt werden. Besonders relevant war dabei der Zugriff auf Windows-Dateien über `/mnt/c`, da die bereitgestellten PDF-Dateien auf der Windows-Festplatte gespeichert waren.

Zusätzlich wurde eine grafische Oberfläche mit XFCE und XRDP eingerichtet. Damit konnte die Linux-Umgebung nicht nur im Terminal, sondern auch über eine grafische Sitzung verwendet werden. Insgesamt wurde gezeigt, dass WSL eine sehr praktische Lösung darstellt, um Linux-Werkzeuge direkt unter Windows einzusetzen und typische Aufgaben aus der Systemtechnik effizient umzusetzen.

## 6. Quellen

- Microsoft, "Install WSL," *Microsoft Learn*. Verfügbar unter: https://learn.microsoft.com/en-us/windows/wsl/install
- Microsoft, "Windows Subsystem for Linux Documentation," *Microsoft Learn*. Verfügbar unter: https://learn.microsoft.com/en-us/windows/wsl/
- Canonical, "Install Ubuntu on WSL 2," *Ubuntu on WSL documentation*. Verfügbar unter: https://ubuntu.com/wsl/docs/latest/howto/install-ubuntu-wsl2/
- Ubuntu Documentation, "Official Ubuntu Documentation," *Ubuntu Documentation*. Verfügbar unter: https://help.ubuntu.com/
- Free Software Foundation, "GNU Grep 3.12," *GNU Project*. Verfügbar unter: https://www.gnu.org/software/grep/manual/grep.html
- Ubuntu Manpage, "pdfgrep - search PDF files for a regular expression," *Ubuntu Manpages*. Verfügbar unter: https://manpages.ubuntu.com/manpages/noble/man1/pdfgrep.1.html
- pdfgrep Project, "pdfgrep Documentation," *pdfgrep.org*. Verfügbar unter: https://pdfgrep.org/doc.html
- LinuxVox, "Installing xrdp on Ubuntu: A Comprehensive Guide," *LinuxVox*. Verfügbar unter: https://linuxvox.com/blog/install-xrdp-ubuntu/
- GoLinuxCloud, "How to install XRDP with XFCE4 on Ubuntu?," *GoLinuxCloud*. Verfügbar unter: https://www.golinuxcloud.com/install-xrdp-with-xfce4-on-ubuntu/


