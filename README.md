# simple setup mit sftp

- sftp client, z.B. die Integration im PHPStorm oder filezilla/winscp
  - Die Integration bietet Änderungsverfolgung auch ohne git und kann einen Diff beim Deployment erstellen bzw. nur "neue" Änderungen hochladen
- Datenbank Client, z.B. die Integration im PHPStorm
  - MYSQL Workbench etc.
  - Alternativ die Verwaltungsoberfläche vom Hoster nutzen um DB Dump zu ziehen
  - Im schlimmsten Fall muss phpmyadmin oder adminer genutzt werden
- Setup mit .ddev https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/

# Einrichtung von einem neuen Projekt

- neues Verzeichnis erstellen, `mkdir neues-projekt-123` und hinein wechseln `cd neues-projekt-123`
  - optional: `git init .` um git zu initialisieren
- ALLE Files vom Server in den Projektordner synchronisieren
  - z.B. in einem Wordpress Projekt sieht die Dateistruktur dann so aus: `neues-projekt-123/wp-config.php` 
- DB-dump ziehen
- ddev config
  - ddev fragt nach 
    - Projektname (in der Regel einfach bestätigen), 
    - Docroot (in der Regel einfach bestätigen) 
    - Project Type (Wordpress/Laravel sollten autom. erkannt werden)
  - die `.ddev/config.yaml` anpassen
    - php-version auf die gleiche Version wie Server
    - mariadb/mysql version auf die gleiche Version wie Server
    - webserver_type auf apache-fpm (meistens wird noch apache-fpm genutzt, ansonsten bei nginx belassen)
- ddev start
  - **Hinweise beachten!** z.B: An existing user-managed wp-config.php file has been detected!....
- datenbank dump einspielen mit `ddev import-db`
- ddev launch -> fertig

# Tipps

- Schneller erster Download aller Projektdateien: den Ordner vorher auf dem Server packen mit tar (eigentlich immer verfügbar), z.B. `tar -zcvpf backup-webdirectory.tgz /pfad/zum/projekt/auf/server`, dann dass Archiv runterladen. Manche Verwaltungsoberflächen bieten direkt eine "Backup" auf diese Weise
- git nutzen! Mit einer sinnvollen .gitignore bei der Assets wie Bilder und die wp-config (!!) oder .env ausgeschlossen werden!

# Hinweise:

Mit ddev können parallel viele Projekte mit unterschiedlichen PHP und DB Versionen laufen.
Es kann zu Konflikten mit Ports (80/443) kommen, wenn XAMPP/MAMP nebenbei läuft. 