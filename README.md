# WSL-Windows-Subsystem-for-Linux
WSL ist ein Programm in Windows, mit dem du Linux direkt in Windows verwenden kannst – ohne extra Installation oder virtuelle Maschine. 


Verfasser: **Niklas Prager**

Datum: **18.06.2026**

## 1. Einführung

Linux-Werkzeuge werden in der Informatik und Systemtechnik häufig verwendet, da viele Entwicklungs-, Analyse- und Administrationsaufgaben effizient über die Kommandozeile ausgeführt werden können. Mit dem Windows Subsystem for Linux (WSL) kann eine Linux-Umgebung direkt unter Windows betrieben werden, wodurch Linux-Befehle genutzt werden können, ohne ein zweites Betriebssystem oder eine klassische virtuelle Maschine einzurichten [1], [2].

## 2. Projektbeschreibung

In diesem Projekt wurde WSL unter Windows aktiviert und Ubuntu als Linux-Distribution installiert. Danach wurden grundlegende Linux-Befehle zur Navigation und Speicheranalyse ausgeführt, `grep` und `pdfgrep` zum Durchsuchen von Dateien verwendet und zusätzlich eine grafische Oberfläche mit XFCE und XRDP eingerichtet, damit die Linux-Umgebung auch per Remote Desktop genutzt werden kann.

## 3. Theorie

### 3.1 Was ist WSL?

WSL ist eine Funktion von Windows, mit der eine GNU/Linux-Umgebung direkt auf einem Windows-System ausgeführt werden kann. Laut Microsoft können damit Linux-Kommandos, Werkzeuge und Anwendungen ohne den Overhead einer klassischen virtuellen Maschine verwendet werden [1], [2]. Für dieses Projekt wurde Ubuntu eingesetzt, da Ubuntu offiziell für WSL unterstützt wird und sich einfach über den Microsoft Store beziehungsweise über `wsl --install` einrichten lässt [1], [3].

### 3.2 Linux-Navigation und Unterschiede zu Windows

Für die Navigation im Linux-Terminal werden vor allem folgende Befehle verwendet:

- `pwd` – zeigt das aktuelle Verzeichnis an
- `ls` – listet Dateien und Ordner auf
- `cd Ordnername` – wechselt in ein Verzeichnis
- `cd ..` – geht eine Ebene zurück
- `mkdir Name` – erstellt ein Verzeichnis
- `rm Datei` – löscht eine Datei

Der wichtigste Unterschied zu Windows besteht darin, dass Linux Pfade mit `/` trennt, während unter Windows `\\` verwendet wird. Außerdem arbeitet Linux mit einer einzigen Verzeichnisstruktur, die bei `/` beginnt. Windows ist hingegen typischerweise in Laufwerke wie `C:` oder `D:` gegliedert. In WSL werden Windows-Laufwerke unter `/mnt/` eingebunden, also beispielsweise `C:` unter `/mnt/c` [2].

### 3.3 Aufbau des Dateisystems in WSL

Das Linux-Dateisystem enthält typische Verzeichnisse wie `/home`, `/etc`, `/usr` oder `/var`. Benutzerdateien liegen normalerweise im Home-Verzeichnis, also zum Beispiel unter `/home/night`. Windows-Dateien bleiben auf dem Windows-Dateisystem, können in WSL aber über `/mnt/c`, `/mnt/d` usw. erreicht werden [2].

Der Unterschied zu Windows besteht darin, dass Linux kein Laufwerkskonzept im selben Sinn verwendet, sondern eine zusammenhängende Verzeichnisstruktur besitzt. Dadurch wirkt das Dateisystem konsistenter, während Windows stärker auf Laufwerksbuchstaben basiert.

### 3.4 Vorteile von WSL

WSL bietet mehrere Vorteile:

1. Linux-Befehle und Werkzeuge können direkt unter Windows verwendet werden [1], [2].
2. Es ist keine vollständige virtuelle Maschine erforderlich, wodurch weniger Ressourcen benötigt werden [1], [2].
3. Windows-Dateien können aus der Linux-Umgebung heraus direkt verwendet werden, etwa über `/mnt/c` [2].
4. Paketverwaltung mit `apt` ermöglicht eine schnelle Installation zusätzlicher Werkzeuge wie `pdfgrep` [3], [4].
5. WSL eignet sich gut für Entwicklung, Automatisierung, Skripting und Dateianalyse [1], [2].

### 3.5 grep und pdfgrep

`grep` ist ein Werkzeug, das Zeilen aus Textdateien oder Eingaben ausgibt, die zu einem bestimmten Muster passen. Es ist ein klassisches Unix/Linux-Werkzeug zur Textsuche [5]. In der vorliegenden Aufgabenstellung wurde `grep` verwendet, um Dateinamen oder Ausgaben einzuschränken.

`pdfgrep` funktioniert ähnlich, durchsucht jedoch PDF-Dateien direkt. Laut Dokumentation unterstützt `pdfgrep` viele aus GNU grep bekannte Optionen, darunter `-i` für eine Suche ohne Beachtung der Groß- und Kleinschreibung und `-n` zur Ausgabe der Seitenzahl statt einer Zeilennummer [6], [7].

### 3.6 grep in Windows

Ein direktes GNU-`grep` ist unter Windows standardmäßig nicht vorinstalliert. Eine funktional ähnliche Alternative in PowerShell ist `Select-String`. Im Rahmen dieses Projekts wurde jedoch ausschließlich `grep` innerhalb der Ubuntu-Umgebung von WSL eingesetzt.

### 3.7 Remote Desktop mit XRDP und XFCE

Für manche Aufgaben ist eine grafische Oberfläche angenehmer als reines Arbeiten im Terminal. Zu diesem Zweck wurde in WSL die Desktop-Umgebung XFCE installiert und mit XRDP kombiniert. XRDP stellt einen RDP-Dienst bereit, auf den mit der Windows-Anwendung „Remotedesktopverbindung“ zugegriffen werden kann [8], [9].

## 4. Arbeitsschritte

### 4.1 Aktivierung von WSL in Windows

Zuerst wurde in den Windows-Features das **Windows-Subsystem für Linux** aktiviert. Zusätzlich wurde die **Plattform für virtuelle Computer** aktiviert, da aktuelle WSL-Installationen auf dieser Basis arbeiten [1], [3]. Danach wurde das System neu gestartet.

![Aktivierung von WSL in den Windows-Features](Bilder/winFeautures)

### 4.2 Installation von Ubuntu

Anschließend wurde Ubuntu installiert. In der vorliegenden Durchführung wurde die Standard-Distribution **Ubuntu** verwendet.

Nach dem ersten Start wurde ein Linux-Benutzername und ein Passwort erstellt. Dieses Passwort wird später auch für `sudo`-Befehle und für die Anmeldung über XRDP benötigt [1], [3].

![Installation von Ubuntu über den Microsoft Store](Bilder/Ubuntu-Micr)

![Erster Start von Ubuntu und Anlegen von Benutzername und Passwort](Bilder/Ubuntu-start)


### 4.5 Speicherverbrauch mit `du` anzeigen und sortieren

Die Aufgabenstellung verlangte die Anzeige des Festplattenverbrauchs und eine Sortierung nach Größe. Dafür wurde zuerst `du` verwendet:

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

Dabei wird die Ausgabe von `du` per Pipe (`|`) an `sort` übergeben. Mit `-h` kann `sort` Größenangaben wie K, M oder G korrekt auswerten [5].

![Speicherverbrauch mit du und sort](Bilder/Ubuntu-Festplatte)

### 4.6 Verwendung von `grep`

`grep` wurde verwendet, um eine Ausgabe einzuschränken. Ein einfaches Beispiel bestand darin, nur PDF-Dateien aus einer Dateiliste anzuzeigen:

```bash
ls | grep pdf
```

Falls Dateiendungen in unterschiedlichen Schreibweisen vorkommen, kann die Suche ohne Berücksichtigung der Groß- und Kleinschreibung durchgeführt werden:

```bash
ls | grep -i pdf
```

Zur Einschränkung auf systemtechnikrelevante Dateien wäre beispielsweise eine Filterung nach bestimmten Dateitypen oder Begriffen möglich:

```bash
ls | grep -Ei "pdf|txt|log"
```

`grep` durchsucht dabei die Eingabe nach einem Muster und gibt nur passende Zeilen aus [5].

![Beispiel für grep im Terminal](images/07_grep.png)

### 4.7 Installation von `pdfgrep`

Um Inhalte in PDF-Dateien durchsuchen zu können, wurde `pdfgrep` installiert:

```bash
sudo apt install pdfgrep
```

Die Hilfe dazu kann mit folgender Anweisung aufgerufen werden:

```bash
man pdfgrep
```

Die Manpage beschreibt die verfügbaren Optionen und zeigt, dass `pdfgrep` weitgehend an GNU grep angelehnt ist [6], [7].

![Installation von pdfgrep](images/08_pdfgrep_installation.png)

### 4.8 Herunterladen und Vorbereiten der PDF-Dateien

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

![PDF-Dateien im Zielordner](images/09_pdf_folder.png)

### 4.9 Durchsuchen der PDFs nach „kapazitiv“

Gefordert war eine Suche nach dem Begriff **kapazitiv** unter Verwendung von Optionen zum Caching, zur Ignorierung der Groß-/Kleinschreibung sowie zur Anzeige von Dateinamen und Seitenzahlen. Dafür wurde folgender Befehl verwendet:

```bash
pdfgrep -i -n -H --cache "kapazitiv" *.pdf
```

Bedeutung der Optionen:

- `-i` – Groß-/Kleinschreibung ignorieren
- `-n` – Seitennummer ausgeben
- `-H` – Dateiname ausgeben
- `--cache` – interne Zwischenspeicherung verwenden

Damit wurden alle PDF-Dateien im aktuellen Ordner gleichzeitig durchsucht. Das Platzhalterzeichen `*.pdf` steht für alle Dateien mit der Endung `.pdf` [6], [7].

![Suche nach kapazitiv mit pdfgrep](images/10_pdfgrep_kapazitiv.png)

### 4.10 Durchsuchen aller PDFs in einem Ordner

Sollen alle PDFs in einem Ordner durchsucht werden, kann ebenfalls das Platzhalterzeichen verwendet werden:

```bash
pdfgrep -i -n -H --cache "kapazitiv" *.pdf
```

Sollen Unterordner rekursiv einbezogen werden, kann zusätzlich mit `-r` oder `-R` gearbeitet werden. Die Dokumentation zeigt ausdrücklich, dass `pdfgrep` rekursive Suchen in Verzeichnissen unterstützt [6], [7]. Ein Beispiel dafür ist:

```bash
pdfgrep -R -i -n -H --cache "kapazitiv" .
```

### 4.11 Weitere Suchbegriffe

Zusätzlich wurden weitere Begriffe getestet, wie in der Aufgabenstellung gefordert:

```bash
pdfgrep -i -n -H --cache "ultraschall" *.pdf
pdfgrep -i -n -H --cache "microcontroller" *.pdf
pdfgrep -i -n -H --cache "arduino" *.pdf
pdfgrep -i -n -H --cache "piezo" *.pdf
```

Damit konnten relevante Stellen in den bereitgestellten PDF-Dateien schnell gefunden werden.

![Weitere Suchbegriffe mit pdfgrep](images/11_pdfgrep_more_terms.png)

### 4.12 Installation einer grafischen Oberfläche

Da in der Aufgabenstellung zusätzlich eine grafische Oberfläche gefordert war, wurden die vorgegebenen Befehle in WSL **einzeln** ausgeführt.

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

Zuerst wurde das System aktualisiert, danach wurden XFCE und XRDP installiert. Anschließend wurde eine Sicherung der Datei `xrdp.ini` erstellt und die Konfiguration entsprechend der Aufgabenstellung angepasst. Abschließend wurde der XRDP-Dienst gestartet.

![Installation von XFCE und XRDP](images/12_xfce_xrdp_install.png)

### 4.13 Bearbeitung von `startwm.sh`

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

![Bearbeitung von startwm.sh in nano](images/13_startwm_sh.png)

### 4.14 Verbindung über Remote Desktop

Nach der Konfiguration wurde in Windows die Anwendung **Remote Desktop Connection** beziehungsweise **Remotedesktopverbindung** geöffnet. Anschließend wurde eine Verbindung mit

```text
localhost:3389
```

beziehungsweise

```text
localhost:3390
```

hergestellt, je nachdem welcher Port in der Konfiguration verwendet wurde.

![Verbindung mit Remote Desktop](images/14_rdp_connection.png)

![Erfolgreicher XFCE-Desktop in WSL](images/15_xfce_desktop.png)

## 5. Zusammenfassung

Im Projekt wurde erfolgreich eine Linux-Umgebung mit WSL unter Windows eingerichtet. Die grundlegende Navigation im Linux-Dateisystem, die Analyse des Speicherverbrauchs sowie die Verwendung von `grep` und `pdfgrep` konnten praktisch durchgeführt werden. Besonders relevant war dabei der Zugriff auf Windows-Dateien über `/mnt/c`, da die bereitgestellten PDF-Dateien auf der Windows-Festplatte gespeichert waren.

Zusätzlich wurde eine grafische Oberfläche mit XFCE und XRDP eingerichtet. Dabei trat zunächst ein typisches Konfigurationsproblem auf, bei dem nur ein leerer blauer Bildschirm angezeigt wurde. Durch die Anpassung der Sitzungskonfiguration mit `startxfce4`, `xfce4-session` und dem Start von `dbus` konnte dieses Problem behoben werden. Insgesamt wurde gezeigt, dass WSL eine sehr praktische Lösung darstellt, um Linux-Werkzeuge direkt unter Windows zu verwenden und sowohl im Terminal als auch grafisch damit zu arbeiten.

## 6. Quellen

[1] Microsoft, "Install WSL," *Microsoft Learn*. [Online]. Verfügbar unter: https://learn.microsoft.com/en-us/windows/wsl/install. [Zugriff: 18. Juni 2026].

[2] Microsoft, "Windows Subsystem for Linux Documentation," *Microsoft Learn*. [Online]. Verfügbar unter: https://learn.microsoft.com/en-us/windows/wsl/. [Zugriff: 18. Juni 2026].

[3] Canonical, "Install Ubuntu on WSL 2," *Ubuntu on WSL documentation*. [Online]. Verfügbar unter: https://ubuntu.com/wsl/docs/latest/howto/install-ubuntu-wsl2/. [Zugriff: 18. Juni 2026].

[4] Ubuntu Documentation, "Official Ubuntu Documentation," *Ubuntu Documentation*. [Online]. Verfügbar unter: https://help.ubuntu.com/. [Zugriff: 18. Juni 2026].

[5] Free Software Foundation, "GNU Grep 3.12," *GNU Project*. [Online]. Verfügbar unter: https://www.gnu.org/software/grep/manual/grep.html. [Zugriff: 18. Juni 2026].

[6] Ubuntu Manpage, "pdfgrep - search PDF files for a regular expression," *Ubuntu Manpages*. [Online]. Verfügbar unter: https://manpages.ubuntu.com/manpages/noble/man1/pdfgrep.1.html. [Zugriff: 18. Juni 2026].

[7] pdfgrep Project, "pdfgrep Documentation," *pdfgrep.org*. [Online]. Verfügbar unter: https://pdfgrep.org/doc.html. [Zugriff: 18. Juni 2026].

[8] LinuxVox, "Installing xrdp on Ubuntu: A Comprehensive Guide," *LinuxVox*. [Online]. Verfügbar unter: https://linuxvox.com/blog/install-xrdp-ubuntu/. [Zugriff: 18. Juni 2026].

[9] GoLinuxCloud, "How to install XRDP with XFCE4 on Ubuntu?," *GoLinuxCloud*. [Online]. Verfügbar unter: https://www.golinuxcloud.com/install-xrdp-with-xfce4-on-ubuntu/. [Zugriff: 18. Juni 2026].

