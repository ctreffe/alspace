---
updated: 2021-06-14
author: ctreffe
author_url: https://github.com/ctreffe
---

# Installation von Alfred3 und Mortimer unter Debian 10

Die folgende Anleitung setzt die Verfügbarkeit eis Servers mit aktueller Debian-Installation voraus. Diese Maschine sollte über eine feste IP-Adresse sowie über eine DNS-Adresse (Domain) verfügen. Letzteres ist für die Erstellung eines SSL-Zertifikats mit Let's Encrypt notwendig.

## Einrichtung von Debian - Optionale Software

* Wir benötigen von Beginn an einen geeigneten Texteditor, um das
  Betriebssystem einrichten zu können. Falls man dafür mit _Vim_ arbeiten möchte, muss man den Editor als erstes installieren. Dazu loggen wir uns mit dem Root-User über Remote-Konsole oder SSH in unsere VM ein und nehmen dann die Installation vor:

  ```bash
  apt-get update

  apt-get install vim
  ```

* Es folgt die Konfiguration von Benutzerrechten sowie ggf. die
  Einrichtung zusätzlicher Benutzer im System. Dazu installieren wir
  erst einmal _sudo_, wobei wir als root auf der VM eingeloggt sein müssen (via Remote-Console). Dann fügen wir die gewünschten Benutzer zur neuen Benutzergruppe _sudo_ hinzu:

  ```bash
  # Neuen Benutzer anlegen
  adduser <BENUTZERNAME>
  
  # Sudo installieren
  apt-get install sudo
  
  # Benutzer zur Gruppe der sudoer hinzufügen
  adduser <BENUTZERNAME> sudo
  ```

  Die so angelegten und autorisierten Benutzeraccounts können nun mittels _sudo_ Befehle mit erhöhter Berechtigung ausführen.

  __ACHTUNG:__ Es sollten ausschließlich Benutzeraccounts mit sicheren Passwörtern und von vertrauenswürdigen Benutzer:innen zu _sudo_ hinzugefügt werden, insbesondere wenn der Server über SSH erreichbar ist. Vor allem sollte der Benutzeraccount, unter dem die Python-Umgebung für Mortimer und Alfred läuft, nicht zur Gruppe der Sudoer gehören, auch wenn die Installation dadurch etwas umständlicher wird.

## Einrichten von Debian - SSH

* Als nächstes richten wir unseren _SSH_-Zugang zur VM und dem darauf
  installierten System ein, um danach nicht mehr auf die Remote-Console
  von vSphere angewiesen zu sein. Wir bearbeiten die dazu die Datei
  _/etc/ssh/sshd\_config_, in der wir den Wert _PermitRootLogin_ auf
  _no_ und den Wert _Port_ auf einen von uns gewünschten Custom-Port setzen (der im Vorfeld ggf. auch in einer vorhandenen Firewall freigeschaltet werden muss):

  ```bash
  # $OpenBSD: sshd_config,v 3.103 2018/04/09 20:41:22 tj Exp $
  
  # This is the sshd server system-wide configuration file.  See
  # sshd_config(5) for more information.
  
  # This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin
  
  # The strategy used for options in the default sshd_config shipped with
  # OpenSSH is to specify options with their default value where
  # possible, but leave them commented.  Uncommented options override the
  # default value.
  
  Port <CUSTOM-PORT NAME>
  #AddressFamily any
  #ListenAddress 0.0.0.0
  #ListenAddress ::
  
  #HostKey /etc/ssh/ssh_host_rsa_key
  #HostKey /etc/ssh/ssh_host_ecdsa_key
  #HostKey /etc/ssh/ssh_host_ed25519_key
  
  # Ciphers and keying
  #RekeyLimit default none
  
  # Logging
  #SyslogFacility AUTH
  #LogLevel INFO
  
  # Authentication:
  
  #LoginGraceTime 2m
  PermitRootLogin no
  #StrictModes yes
  #MaxAuthTries 6
  #MaxSessions 10
  
  #PubkeyAuthentication yes
  
  # Expect .ssh/authorized_keys2 to be disregarded by default in future.
  #AuthorizedKeysFile     .ssh/authorized_keys .ssh/authorized_keys2
  
  #AuthorizedPrincipalsFile none
  
  #AuthorizedKeysCommand none
  #AuthorizedKeysCommandUser nobody
  
  # For this to work you will also need host keys in /etc/ssh/  ssh_known_hosts
  #HostbasedAuthentication no
  # Change to yes if you don't trust ~/.ssh/known_hosts for
  # HostbasedAuthentication
  #IgnoreUserKnownHosts no
  # Don't read the user's ~/.rhosts and ~/.shosts files
  #IgnoreRhosts yes
  
  # To disable tunneled clear text passwords, change to no here!
  #PasswordAuthentication yes
  #PermitEmptyPasswords no
  
  # Change to yes to enable challenge-response passwords (beware issues   with
  # some PAM modules and threads)
  ChallengeResponseAuthentication no
  
  # Kerberos options
  #KerberosAuthentication no
  #KerberosOrLocalPasswd yes
  #KerberosTicketCleanup yes
  #KerberosGetAFSToken no
  
  # GSSAPI options
  #GSSAPIAuthentication no
  #GSSAPICleanupCredentials yes
  #GSSAPIStrictAcceptorCheck yes
  #GSSAPIKeyExchange no
  
  # Set this to 'yes' to enable PAM authentication, account processing,
  # and session processing. If this is enabled, PAM authentication will
  # be allowed through the ChallengeResponseAuthentication and
  # PasswordAuthentication.  Depending on your PAM configuration,
  # PAM authentication via ChallengeResponseAuthentication may bypass
  # the setting of "PermitRootLogin without-password".
  # If you just want the PAM account and session checks to run without
  # PAM authentication, then enable this but set PasswordAuthentication
  # and ChallengeResponseAuthentication to 'no'.
  UsePAM yes
  
  #AllowAgentForwarding yes
  #AllowTcpForwarding yes
  #GatewayPorts no
  X11Forwarding yes
  #X11DisplayOffset 10
  #X11UseLocalhost yes
  #PermitTTY yes
  PrintMotd no
  #PrintLastLog yes
  #TCPKeepAlive yes
  #PermitUserEnvironment no
  #Compression delayed
  #ClientAliveInterval 0
  #ClientAliveCountMax 3
  #UseDNS no
  #PidFile /var/run/sshd.pid
  #MaxStartups 10:30:100
  #PermitTunnel no
  #ChrootDirectory none
  #VersionAddendum none
  
  # no default banner path
  #Banner none
  
  # Allow client to pass locale environment variables
  AcceptEnv LANG LC_*
  
  # override default of no subsystems
  Subsystem       sftp    /usr/lib/openssh/sftp-server
  
  # Example of overriding settings on a per-user basis
  #Match User anoncvs
  #       X11Forwarding no
  #       AllowTcpForwarding no
  #       PermitTTY no
  #       ForceCommand cvs server
  ```
  
  Nun sollte der Server z.B. mit Putty über den neuen Port erreichbar sein.

  __ACHTUNG:__ Es ist absolut nicht empfehlenswert SSH auf dem Standardport zu lassen, weil dies den Server leichter angreifbar macht. Genau so sollte generell kein Root-Zugriff mittels SSH erlaubt werden.

## Einrichtung des Apache Webservers

* Als erstes möchten wir die Anzeige von Verzeichnisinhalten für das
  Server-Rootverzeichnis _/var/www/_ deaktivieren und müssen dafür die
  Datei _/etc/apache2/apache2.conf_ wie folgt anpassen:

  ```bash
  # Vorher
  <Directory /var/www/>
          Options Indexes FollowSymLinks
          AllowOverride None
          Require all granted
  </Directory>
  
  # Nachher
  <Directory /var/www/>
          Options -Indexes +FollowSymLinks
          AllowOverride None
          Require all granted
  </Directory>
  ```

* Danach aktivieren wir zunächst die SSL-Verschlüsselung für unseren
  Server. Dazu verwenden wir _Let's Encrypt_ bzw. [Certbot](https://certbot.eff.org/) und folgen der Anleitung für einen Apache Server auf Debian:

  ```bash
  sudo apt-get update
  # Installation von snapd
  sudo apt-get install snapd # Hiernach muss man sich neu einloggen

  sudo snap install core
  sudo snap refresh core

  # Nun ggf. alle bisherigen Certbot-Pakete entfernen (siehe Webseite)

  # Certbot installieren

  sudo snap install --classic certbot
  sudo ln -s /snap/bin/certbot /usr/bin/certbot

  # Aktivieren von SSL und Laden des Zertifikats für Apache

  sudo certbot --apache
  ```

  Nun sollte _Certbot_ erfolgreich installiert worden sein und stellt für uns Folgendes zur Verfügung:

  - Eine Beispielkonfiguration für einen Virtualhost für Apache in der
    Datei _/etc/apache2/sites-enabled/000-default-le-ssl.conf_. Diese
    Datei kann nun editiert und erweitert werden.

    _ACHTUNG:_ Virtuelle Hosts auf dem Webserver werden entweder anhand unterschiedlicher IP-Adressen oder unterschiedlicher Domainnamen (In der vHost-Konfiguration über das Argument _ServerName_ festgelegt) identifiziert, so dass Anfragen an den jeweiligen virtuellen Host weitergeleitet werden können. Da die VM in der Regel nur eine IP-Adresse zugewiesen bekommt und auch nur eine Subdomain erhält ist es in der Regel nicht möglich mit mehreren vHost-Konfigurationen auf dem Server zu arbeiten (außer man erstellt zusätzliche Subdomains).

  - Eine automatisierte Zertifikaterneuerung, so dass kein manuelles
    Update der Zertifikate notwendig ist. Dies kann man mit folgendem Befehl prüfen:

    ```bash
    # Es sollte in der sich hierdurch öffnenden Liste ein Eintrag für
    # snap.certbot.renew.timer auftauchen
    systemctl list-timers
    ```
  __ACHTUNG:__ Die beiden Konfigurationsdateien _000-default.conf_ und _default-ssl.conf_ sollten nach der Ausführung von _certbot_ aktiviert sein und müssen nicht verändert werden. Erstere enthält Regeln zur automatischen Weiterleitung, falls jemand den Server mit _HTTP_ statt _HTTPS_ aufruft und Letztere enthält Standardeinstellungen für die SSL-Verbindungen mit dem Server.

* Nach der erfolgreichen Installation von _Certbot_ können wir damit
  beginnen die Konfiguration des Webservers schrittweise anzupassen. Wir beginnen mit einer Überarbeitung der Datei _/etc/apache2/sites-enabled/000-default-le-ssl.conf_. Diese sieht direkt nach der Installation wie folgt aus:

  ```bash
  <Directory /var/www/>
          Options Indexes FollowSymLinks
          AllowOverride None
          Require all granted
  </Directory>
  <IfModule mod_ssl.c>
  <VirtualHost *:443>
          # The ServerName directive sets the request scheme, hostname and port that
          # the server uses to identify itself. This is used when creating
          # redirection URLs. In the context of virtual hosts, the ServerName
          # specifies what hostname must appear in the request's Host: header to
          # match this virtual host. For the default virtual host (this file) this
          # value is not decisive as it is used as a last resort host regardless.
          # However, you must set it for any further virtual host explicitly.
          #ServerName www.example.com
  
          ServerAdmin webmaster@localhost
          DocumentRoot /var/www/html
  
          # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
          # error, crit, alert, emerg.
          # It is also possible to configure the loglevel for particular
          # modules, e.g.
          #LogLevel info ssl:warn
  
          ErrorLog ${APACHE_LOG_DIR}/error.log
          CustomLog ${APACHE_LOG_DIR}/access.log combined
  
          # For most configuration files from conf-available/, which are
          # enabled or disabled at a global level, it is possible to
          # include a line for only one particular virtual host. For example the
          # following line enables the CGI configuration for this host only
          # after it has been globally disabled with "a2disconf".
          #Include conf-available/serve-cgi-bin.conf
  
  
  ServerName SERVERNAME
  SSLCertificateFile PATH_TO_FILE
  SSLCertificateKeyFile PATH_TO_FILE
  Include /etc/letsencrypt/options-ssl-apache.conf
  </VirtualHost>
  </IfModule>
  ```
  
  Wie wir sehen hat _Certbot_ die relevanten Einstellungen unten in die Konfigurationsdatei eingefügt. Wir verschieben diese nun teilweise und passen einen anderen Teil der Einstellungen an. Dabei verschieben wir den Wert ServerName nach oben, geben eine geeignete Admin-Mailadresse an und setzen das DocumentRoot von _/var/www/html_ auf _/var/www_. Außerdem löschen wir die _<Directory>_-Anweisung oben in der Konfigurationsdatei, da wir die entsprechenden Einstellungen bereits in der Apache2 Basiskonfiguration vorgenommen hatten und die Settings hier unsere vorherigen überschreiben würden:

  ```bash
  <IfModule mod_ssl.c>
  <VirtualHost *:443>
          # The ServerName directive sets the request scheme, hostname and port that
          # the server uses to identify itself. This is used when creating
          # redirection URLs. In the context of virtual hosts, the ServerName
          # specifies what hostname must appear in the request's Host: header to
          # match this virtual host. For the default virtual host (this file) this
          # value is not decisive as it is used as a last resort host regardless.
          # However, you must set it for any further virtual host explicitly.
          #ServerName www.example.com
          ServerName SERVERNAME
          ServerAdmin ADMIN-MAIL
          DocumentRoot /var/www
  
          # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
          # error, crit, alert, emerg.
          # It is also possible to configure the loglevel for particular
          # modules, e.g.
          #LogLevel info ssl:warn
  
          ErrorLog ${APACHE_LOG_DIR}/error.log
          CustomLog ${APACHE_LOG_DIR}/access.log combined
  
          # For most configuration files from conf-available/, which are
          # enabled or disabled at a global level, it is possible to
          # include a line for only one particular virtual host. For example the
          # following line enables the CGI configuration for this host only
          # after it has been globally disabled with "a2disconf".
          #Include conf-available/serve-cgi-bin.conf
            
          # Additional Let's Encrypt SSL Settings
          SSLCertificateFile PATH_TO_FILE
          SSLCertificateKeyFile PATH_TO_FILE
          Include /etc/letsencrypt/options-ssl-apache.conf
  </VirtualHost>
  </IfModule>
  ```

  Die so angepasste Konfigurationsdatei können wir in der Folge für die Einrichtung aller weiteren Funktionen verwenden.

## Installation und Einrichtung der MongoDB

Anleitung für die Installation unter Debian:

https://docs.mongodb.com/manual/tutorial/install-mongodb-on-debian/

Nur zur Dokumentation folgen hier die Befehle aus der Installationsanleitung, man sollte ich aber immer nach der Anleitung unter dem angegebenen Link richten, um die neueste Version von MongoDB zu installieren:

```bash
# The following is only necessary on some but not all systems
sudo apt-get install gnupg

# Import the public key used by the package management system
wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -

# The previous command will return OK

# Create a /etc/apt/sources.list.d/mongodb-org-4.4.list file for MongoDB.
echo "deb http://repo.mongodb.org/apt/debian buster/mongodb-org/4.4 main" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list

# Reload local package database
sudo apt-get update

# Install the MongoDB packages
sudo apt-get install -y mongodb-org
```

Nun sollte die MongoDB zur Einrichtung bereit sein. Wir nehmen zunächst grundlegende Einstellungen in der Konfigurationsdatei _/etc/mongod.conf_ vor. Hier die unveränderte Datei:

```bash
# Where and how to store data.
storage:
  dbPath: /var/lib/mongodb
  journal:
    enabled: true


# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1

```

Aus Sicherheitsgründen ist es wichtig, dass wir unsere MongoDB-Instanz nicht am Standardport für MongoDB-Server betreiben, vor allem falls wir die MongoDB auch für andere Systeme als den Server selbst erreichbar machen wollen. 

__ACHTUNG:__ Im Normalfall ist es für den Betrieb von _Mortimer_ nicht notwendig und aus Sicherheitsgründen auch nicht empfehlenswert, anderen Systemen direkten Zugriff auf die MongoDB zu ermöglichen. Lokale Alfred-Experimente, die ihre Daten mittels MongoDB SavingAgent speichern, sollten dafür vorzugsweise einen anderen Server nutzen. Ist die Erreichbarkeit der MongoDB von anderen Systemen aus dennoch gewünscht, kann der Befehl `bindIp: 127.0.0.1` in der obigen Konfigurationsdatei durch den Befehl `bindIpAll: true` ersetzt werden. Dadurch kann die MongoDB auf dem eingestellten Port über die IP-Adresse der VM erreicht werden.

Wir passen für den sicheren Betrieb von _Mortimer_ lediglich die Eigenschaft _port_ wie folgt an:

```bash
# Where and how to store data.
storage:
  dbPath: /var/lib/mongodb
  journal:
    enabled: true


# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# network interfaces
net:
  port: <CUSTOM-PORT>
  bindIp: 127.0.0.1

```

### Erstellen eines DB Administrators

Wir müssen uns zunächst mit der Datenbank verbinden, wenn diese nicht im Auth-Modus gestartet ist. Dazu kann man nach dem Start der Datenbank den Befehl _mongo_ benutzen:

```bash

sudo service mongod start
mongo

# Alternativ bei eingestelltem Custom-Port
mongo -port CUSTOM-PORT

```

Nun muss zunächst ein Administrator in der Datenbank _admin_ erstellt werden. Dieser erhält die Superuser-Rolle _userAdminAnyDatabase_. 

```json
use admin

db.createUser(
  {
    user: "USERNAME",
    pwd: "PASSWORD",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
```

Zusätzlich soll dieser Benutzer noch Lese- und Schreibrechte auf allen Datenbanken erhalten:

```json
db.grantRolesToUser("USERNAME",[{ "role" : "readWriteAnyDatabase", "db" : "admin" }])
```

Nach der Einrichtung des Administrators kann man diese im Auth-Modus starten. Dazu passen wir die Datei _/etc/mongod.conf_ an, indem wir den Abschnitt _security_ aktivieren (Kommentarzeichen entfernen) und wie folgt erweitern:

```bash
security:
  authorization: enabled

```

Nach einem Neustart der Datenbank können wir uns erneut mit dem Befehl _mongo_verbinden und dabei bereits die notwendigen Daten zur Authentifizierung übergeben:

 ```bash
mongo admin -port CUSTOM-PORT -u USERNAME -p PASSWORD

 ```

Durch diesen Befehl verbindet sich die Mongoshell sofort mit der Datenbank _admin_ und authentifiziert sich. 

_Achtung:_ Falls der Benutzername oder das Passwort wegen der Verwendung von Sonderzeichen als String (also mit Anführungsstrichen) übergeben werden muss ist darauf zu achten, dass hier einfache Anführungszeichen verwendet werden, da der Befehl _mongo_ mit doppelten Anführungszeichen scheinbar nicht zurecht kommt!

Alternativ kann man auch mit einem Standardaufruf von _mongo_ erst die Shell aufrufen und sich dann über den Befehl _db.auth()_ authentifizieren:

```bash
use admin

db.auth("USERNAME", "PASSWORD")

```

 Mit dem Befehl _show users_ können wir uns nun das Ergebnis der Einrichtung anzeigen lassen:

```json
show users

```

### Anlegen der Datenbankuser für Mortimer und Alfred

Für die Installation und den sicheren Betrieb von Alfred und Mortimer ist die Erstellung eines separaten Benutzers mit eingeschränkten Zugriffsrechten erforderlich. Mit dem Benutzer _mortimer-user_ wird die Erstellung und Verwaltung von Collections sowie individuellen Datenbankaccounts für Mortimer-User gesteuert:

```shell
db.createUser(
  {
    user: "mortimer-user",
    pwd: "PASSWORD",
    roles: [ 
        { role: "userAdminAnyDatabase", db: "admin" }, 
        { role: "readWrite", db: "mortimer" },
        { role: "readWrite", db: "alfred" }
    ]
  }
)
```

_Achtung:_ Der Mortimer-User braucht Lese- und Schreibrechte sowohl für die Mortimer-Datenbank als auch für die Alfred-Datenbank!

## Einrichtung der virtuellen Umgebung für Mortimer und Alfred

Im nächsten Schritt werden Mortimer und Alfred in eine virtuelle Pythonumgebung installiert, die wir aus der bei Debian standardmäßig mitgelieferten Version von Python 3 heraus einrichten. Dadurch wird zwar nicht die aktuellste Python-Version genutzt, aber die Einrichtung ist wesentlich einfacher und weniger fehleranfällig.

Wir beginnen die Einrichtung mit der Installation der Pakete _pip_ und _virtualenv_ für Python 3. Wenn die Installation erfolgreich war, sollte uns danach der Befehl _pip3_ zur Verfügung stehen:

```bash
sudo apt-get install python3-pip

pip3 list # zeigt alle installierten Pakete an
```

Nun installieren wir das Paket _virtualenv_, welches die Einrichtung virtueller Pythonumgebungen ermöglicht. Wir verwenden dabei _sudo_, damit das Paket im Anschluss von allen Benutzern verwendet werden kann:

```bash
sudo pip3 install virtualenv
```

Danach richten wir einen neuen Debian-User ein, der explizit _NICHT_ in die Gruppe der sudoer aufgenommen wird. Dieser Nutzer hat also relativ wenig Rechte auf dem Server, was für den sicheren Betrieb von Mortimer von Vorteil ist, auch wenn damit an anderer Stelle ein Mehraufwand einhergeht:

```bash
sudo adduser alfred
```

Wir können uns nun mit dem neuen Benutzeraccount auf dem Server anmelden und nun mittels _virtualenv_ eine neue Pythonumgebung erstellen, in die wir anschließend _Mortimer_ und _Alfred_ installieren:

```bash
python3 -m virtualenv /home/alfred/.virtualenvs/alfred3
```

## Mortimer und Alfred installieren und einrichten

Die neu eingerichtete Umgebung muss aktiviert werden, bevor wir mit der Installation fortfahren können:

```bash
source /home/alfred/.virtualenvs/alfred3/bin/activate
```

Nun können wir mit _pip_ sowohl _Mortimer_ als auch _Alfred_ aus dem Python Package Index (PyPI) installieren. Zuvor bietet sich eine Aktualisierung von _pip_ an:
 
```bash
pip3 install --upgrade pip

pip3 install alfred3

pip3 install mortimer
```

Nachdem nun alle notwendigen Komponenten installiert sind, kann ein neues Verzeichnis für Mortimer angelegt werden:

```bash
# Zunächst erstellen wir ein Oberverzeichnis für Web-Applikationen
mkdir /home/alfred/www

# Es folgt die Erstellung des Mortimer-Verzeichnisses
mkdir /home/alfred/www/mortimer3
```

__TODO:__ In diesem Verzeichnis werden zukünftig per Kommandozeile die zwei notwendigen Konfigurationsdateien für _Mortimer_ und _Alfred_ erstellt. Die _alfred.conf_ wird angepasst und bleibt im Verzeichnis, die _mortimer.conf_ wird nach der erforderlichen Anpassung nach in den Ordner _/etc_ verschoben (also /etc/mortimer.conf), wofür man sich allerdings wieder mit einem Benutzeraccount aus der Gruppe der _sudoers_ anmelden muss.

Hier aktuelle Beispiele für beide Dateien:

### alfred.conf:

```
########################################################################
# ALFRED DEFAULT CONFIGURATION #########################################
########################################################################

# SECTION: metadata ----------------------------------------------------
# Information about the experiment and its author.
# The information placed here is used in data saving, especially
# if you use your own mongo saving agent. The version is relevant
# for codebook data.
# ----------------------------------------------------------------------
[metadata]
title = default_title           # Experiment title
author = default_author         # Experiment author
version = 0.1                   # Experiment version
exp_id = default_id             # Experiment id. MUST be unique when using a mongo saving agent


# SECTION: general -----------------------------------------------------
# General settings that affect the whole experiment.
# ----------------------------------------------------------------------
[general]
fullscreen = false              # If true (and Chrome is available), the exp starts in fullscreen kiosk mode
debug = false                   # If true, the exp starts in debug mode
force_input = false             # If true, input elements are force input by default


# SECTION: data --------------------------------------------------------
# General configuration for data collection and export.
# ----------------------------------------------------------------------
[data]
save_client_info = true         # If true, information about participants' technichal setup will be saved
record_move_history = true      # If true, information about partcipants' moves through the exp will be saved

export_exp_data = true          # If true, the main exp data will be exported to csv after each *local* session
export_unlinked_data = true     # If true, unlinked data will be exported to csv after each *local* session
export_codebook = true          # If true, codebook data will be exported to csv after each *local* session
export_move_history = true      # If true, movement data will be exported to csv after each *local* session

csv_directory = data            # The directory (relative to exp directory) in which csv data files will be created
csv_delimiter = ;               # The delimiter to use in exported csv files


# SECTION: navigation --------------------------------------------------
# Defines the texts on alfreds navigation buttons.
# ----------------------------------------------------------------------
[navigation]
forward = Weiter                # Text on the "forward" button
backward = Zurück               # Text on the "backward" button
finish = Beenden                # Text on the "finish" button


# SECTION: layout ------------------------------------------------------
# General configuration of the appearance of your alfred experiment.
# ----------------------------------------------------------------------
[layout]
website_title = alfred3 Experiment          # The title of the exp website (displayed for example as tab heading)
style = goe                                 # The basic color style to use
static_folder = _static                     # Name of directory (relative to exp directory) in which alfred looks for additional .css files for styling

responsive = true                           # Whether the alfred layout should adapt to participants' screen size automatically
responsive_width = 85, 75, 65, 55           # Comma-separated list of relative page widths on sm, md, lg, xl screen sizes
fixed_width = 920px                         # Page width if "responsive = false"

show_progress = true                        # If true, alfred will show a progress bar
fix_progress_top = true                     # If true, the progress bar will float at the top of the page when scrolling down

logo_text =                                 # Text to display at the right border of the header
logo = _static/logo.png                     # Image to use as a logo
footer_text =                               # Text to use in the footer
header_color =                              # Color of the header bar (RGB, Hex, CSS color keywords)
background_color =                          # Background color (RGB, Hex, CSS color keywords)


# SECTION: layout_base -------------------------------------------------
# Specific configuration for the layout style "base"
# ----------------------------------------------------------------------
[layout_base]
logo =
logo_text = alfred<br>A library for rapid experiment development


# SECTION: layout_goe --------------------------------------------------
# Specific configuration for the layout style "goe"
# ----------------------------------------------------------------------
[layout_goe]
logo =
logo_text = Georg-Elias-Müller Institut für Psychologie


# SECTION: webserver ---------------------------------------------------
# Webserver configuration
# QUESTIONING - the option might be removed in future releases
# ----------------------------------------------------------------------
[webserver]
basepath = /mortimer3


# SECTION: log ---------------------------------------------------------
# Configration of alfred's logging behavior.
# ----------------------------------------------------------------------
[log]
path = log              # Directory in which to place the log file
level = info            # Log level. Can be debug, info, warning, error, critical


# SECTION: debug -------------------------------------------------------
# Configuration of alfred's behavior in debug mode
# ----------------------------------------------------------------------
[debug]
set_default_values = true               # If true, default values will be set automatically in debug mode
disable_minimum_display_time = true     # If true, page's minimum display time behavior will be disabled
reduce_countdown = true                 # If true, the timeout of pages inheriting from TimeoutPage will be reduced
reduced_countdown_time = 1              # The time (in seconds) to which the countdown will be reduced if "reduce_countdown = true"
log_level_override = true               # If true, the log_level defined in section [debug] will override the one from [log] in debug mode
log_level = debug                       # Log level in debug mode, if "log_level_override = true". Can be debug, info, warning, error, critical
disable_saving = false                  # If true, alfred will not save data in debug mode

code_in_templates = false               # If true, CSS and JS will be inserted directly into the exp html document, making the .html file standalone

# Default values used in debug mode
Input_default = input
TextEntry_default = testText
TextArea_default = TextArea
RegEntry_default = testReg
NumberEntry_default = 10

SingleChoice_default = 1
SingleChoiceList_default = 1
SingleChoiceButtons_default = 1
SingleChoiceBar_default = 1

# debug default values for MultipleChoice type elements are determined by the elements

# SECTION: hints -------------------------------------------------------
# Default texts used by alfred to inform participants about
# events in an experiment
# ----------------------------------------------------------------------
[hints]
# hints for specific elements if they are force input and have not received input
no_inputTextEntry = Bitte geben Sie etwas ein.
no_inputTextArea = Bitte geben Sie etwas ein.
no_inputRegEntry = Bitte geben Sie etwas ein.
no_inputNumberEntry = Bitte geben Sie etwas ein.
no_inputPassword = Bitte geben Sie etwas ein.
no_inputSingleChoice = Bitte wählen Sie eine Antwortmöglichkeit aus.
no_inputMultipleChoice = Bitte wählen Sie mindestens eine Option aus.

# Displayed if the exp realizes at the end of a section that a force input element was not filled out
# (only relevant if you customize a section's validation methods)
no_input_section_validation = Auf den {n} Seiten dieses Abschnitts fehlt mindestens eine Eingabe.

# Displayed if the input of a RegEntry element does not match the required expression
match_RegEntry = Bitte überprüfen Sie Ihre Eingabe.

# A combination of the hints below is displayed if the input of a NumberEntry element does not fulfill the required conditions
match_NumberEntry = Bitte überprüfen Sie Ihre Eingabe.
min_NumberEntry = Das Minimum ist {min}.
max_NumberEntry = Das Maximum ist {max}.
ndecimals_NumberEntry = Sie können {ndecimals} Nachkommastellen verwenden.
decimal_signs_NumberEntry = Erlaubte Dezimaltrennzeichen sind: {decimal_signs}

# Displayed, if the number of selected options does not meet the requirements of a MultipleChoice type element
select_MultipleChoiceElement = Bitte wählen sie mindestens {min} und maximal {max} Felder aus.

# Page hints ---

# Displayed, if a jump is tried and the current page's section does not allow it
jumpfrom_forbidden = Von der aktuellen Seite kann nicht gesprungen werden.

# Displayed, if a jump is tried and the target page's section does not allow it
jumpto_forbidden = Die Zielseite kann nicht durch Sprung erreicht werden.

# Displayed, if a jump is tried and the target page cannot be found
jump_page_not_found = Die Zielseite wurde nicht gefunden.

# Displayed if a participants jumps over a page that must be shown
page_must_be_shown = Eine verpflichtende Seite wurde übersprungen.

# Displayed, if a participant tries to move forward before a page's minimum display time has expired
minimum_display_time = Sie können diese Seite frühestens nach {mdt} Sekunden verlassen

[exp_condition]
path = save

# SECTION: local_saving_agent ------------------------------------------
# Configuration of alfred's local saving agent
# ----------------------------------------------------------------------
[local_saving_agent]
use = false                     # If true, alfred will use this saving agent
assure_initialization = true    # If true, alfred will abort in case initialization of this saving agent fails
path = save/exp                 # Directory path (relative to exp directory) in which to save the raw .json files
name = data                     # Name of the saving agent
level = 1                       # Activation level, works like a threshold. Only tasks with higher level than the level given here will be saved. Usually, there's no need to change this setting. Don't touch it, if you don't fully understand it.


# SECTION: fallback_local_saving_agent ---------------------------------
# Configuration of a fallback local saving agent that takes effect, if
# the main local saving agent fails for any reason.
# ----------------------------------------------------------------------
[fallback_local_saving_agent]
use = false                     # same as for [local_saving_agent]
assure_initialization = false   # same as for [local_saving_agent]
path = save/fallback_save1      # same as for [local_saving_agent]
name = data_fallback            # same as for [local_saving_agent]
level = 1                       # same as for [local_saving_agent]


# SECTION: level2_fallback_local_saving_agent --------------------------
# Configuration of a second fallback local saving agent that takes
# effect if both the main and the fallback agent fail.
# ----------------------------------------------------------------------
[level2_fallback_local_saving_agent]
use = false                     # same as for [local_saving_agent]
assure_initialization = false   # same as for [local_saving_agent]
path = save/fallback_save2      # same as for [local_saving_agent]
name = data_level2_fallback     # same as for [local_saving_agent]
level = 1                       # same as for [local_saving_agent]


# SECTION: local_saving_agent_unlinked ---------------------------------
# Configuration of a saving agent for unlinked data
# ----------------------------------------------------------------------
[local_saving_agent_unlinked]
use = false                     # same as for [local_saving_agent]
path = save/unlinked            # same as for [local_saving_agent]
name = local_unlinked           # same as for [local_saving_agent]
level = 1

# If true, values (not variable names) saved by this agent will be encrypted.
# For save encryption, you must define a secret encryption
# key in secrets.conf or an environment variable. If you don't define
# an encryption key, alfred will raise an error when encryption is tried
encrypt = false
decrypt_csv_export = true       # If true, encrypted .json files will be decrypted upon export to csv

# SECTION: failure_local_saving_agent ----------------------------------
# Configuration of a last-resort failsage local saving agent. This one
# takes effect, if all other options are exhausted
# ----------------------------------------------------------------------
[failure_local_saving_agent]
use = true                      # same as for [local_saving_agent]
path = save/failure_save        # same as for [local_saving_agent]
name = failure_save             # same as for [local_saving_agent]
assure_initialization = true    # same as for [local_saving_agent]
level = 1                       # same as for [local_saving_agent]


# SECTION: mortimer_specific -------------------------------------------
# Configuration settings that are overwritten by mortimer, if the
# experiment runs on mortimer. No need to alter these manually.
# ----------------------------------------------------------------------
[mortimer_specific]
session_id =
runs_on_mortimer = true
```

Entscheidend ist hier die Deaktivierung der lokalen SavingAgents, da die Experimentaldaten und insbesondere auch die personenbezogenen Daten ausschließlich in der MongoDB gespeichert werden sollten. Außerdem muss der richtige _basepath_ in der Sektion _webserver_ eingestellt werden. Der Wert _runs\_on\_mortimer_ sollte auf _true_ gesetzt werden. Die Datei enthält außerdem alle wichtigen Standardeinstellungen, die von Mortimer bei Alfred-Experimenten per Default übernommen werden. Insbesondere Layout-Einstellungen und Standard-Themes lassen sich hier anpassen.

#### mortimer.conf:

```
# General flask settings
SECRET_KEY = "SecretKey"
PAROLE = "Parole"

# MongoDB settings
MONGODB_SETTINGS = {
    "host": "localhost",
    "port": CUSTOMPORT,
    "db": "mortimer",
    "username": "mortimer",
    "password": "PASSWORD",
    "authentication_source": "admin",
}

ALFRED_DB = "alfred"
ALFRED_LOGFILE = "/home/alfred/alfred.log"

# Mail settings
MAIL_USE = True
MAIL_SERVER = "HOST"
MAIL_PORT = 587
MAIL_USE_TLS = True
MAIL_USERNAME = "USERNAME"
MAIL_PASSWORD = "PASSWORD"
MAIL_SENDER_ADDRESS = "mail@any.com"

# Flask-Dropzone settings:
DROPZONE_ALLOWED_FILE_CUSTOM = True
DROPZONE_ALLOWED_FILE_TYPE = ".pdf, image/*, .txt, .xml, .pem, .mp3, .mp4, .ogg, .csv, .html, .css, .js, .py, .xlsx, .md"
DROPZONE_MAX_FILE_SIZE = 20
DROPZONE_MAX_FILES = 10
DROPZONE_UPLOAD_ON_CLICK = True
DROPZONE_UPLOAD_BTN_ID = "upload"
DROPZONE_UPLOAD_MULTIPLE = True
DROPZONE_PARRALEL_UPLOAD = True
DROPZONE_TIMEOUT = 300000 # 5 minutes
```
 
In dieser Datei sollte vor allem auf die Übernahme der korrekten Benutzerdaten für die MongoDB geachtet werden. Außerdem braucht jede Instanz von Mortimer einen geeigneten _Secret\_Key_ (Must be URL-safe base64-encoded 32-byte key for fernet encryption in STR (NOT in bytes)).

## Mortimer über den Apache 2 Webserver erreichbar machen

Zunächst muss (mit einem Benutzeraccount, der _sudoer_ ist) die Erweiterung _mod\_wsgi_ für Apache installiert werden. Dabei ist es wichtig, dass wir die korrekte Erweiterung für Python 3 und die mitgelieferte Version des Apache Webservers unter Debian installieren. Im  Anschluss wird die Erweiterung durch einen Neustart des Webservers aktiviert:

```bash
sudo apt-get install libapache2-mod-wsgi-py3

sudo a2enmod wsgi

sudo systemctl restart apache2
```

Nun kann die von CertBot bereits erstellte und von uns angepasste vHost-Konfiguration für den Webserver erweitert werden:

```
<IfModule mod_ssl.c>
<VirtualHost *:443>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com
        ServerName <SERVERNAME>
        ServerAdmin <SERVERADMIN>
        DocumentRoot /var/www

        <Directory /var/www/files>
                Options -Indexes -FollowSymLinks -MultiViews
                AllowOverride None
                Order allow,deny
                allow from all
        </Directory>

        # Mortimer and Alfred specific settings

        WSGIDaemonProcess mortimer3 user=alfred group=alfred python-path=/home/alfred/.virtualenvs/alfred3/lib/python3.7/site-packages:/home/alfred/www/mortimer3

        WSGIScriptAlias /mortimer3 /home/alfred/www/mortimer3/wsgi.py

        <Location /mortimer3>
                WSGIProcessGroup mortimer3
        </Location>

        <Directory /home/alfred/www/mortimer3>
                <Files wsgi.py>
                        Require all granted
                </Files>
        </Directory>

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf


        # Additional Let's Encrypt SSL Settings added by Certbot
        Include /etc/letsencrypt/options-ssl-apache.conf
        SSLCertificateFile /etc/letsencrypt/live/alfredo3.psych.bio.uni-goettingen.de/fullchain.pem
        SSLCertificateKeyFile /etc/letsencrypt/live/alfredo3.psych.bio.uni-goettingen.de/privkey.pem
</VirtualHost>
</IfModule>
```

_Wichtig_ ist hier der korrekte Pfad zu den _site-packages_, der die jeweilige Versionsnummer von Python 3 sowie den Pfad zu unserer vorher erstellten virtuellen Python-Umgebung und auch einen Verweis auf den neuen Ordner für Mortimer enthält.

Bevor Mortimer über den Webserver aufrufbar ist benötigen wir nun noch ein Python-Skript, welches wir, wiederum eingeloggt als der User _alfred_, unter _/home/alfred/www/mortimer3/wsgi.py_ erstellen:

```bash
vim /home/alfred/www/mortimer3/wsgi.py
```

Hier wiederum eine Standardvorlage:

```python
import os

os.environ["ALFRED_CONFIG_FILE"] = "/home/alfred/alfred.conf"

from mortimer import create_app

application = create_app()
```

Wenn alle Konfigurationsdateien erstellt und angepasst wurden, kann die neue Mortimer-Konfiguration für den Webserver aktualisiert werden, wozu wieder ein Benutzer mit erhöhten Zugriffsrechten benötigt wird. Durch einen Neustart sollte Mortimer im Anschluss erreichbar werden:

```bash
sudo a2dissite 000-default-le-ssl

sudo a2ensite 000-default-le-ssl

sudo systemctl restart apache2
```

Mortimer sollte nun erreichbar und einsatzbereit sein.