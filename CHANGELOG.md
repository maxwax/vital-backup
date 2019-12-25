# CHANGLOG for 'vital-backup' script

## 1.1.0 New config file location and --config option

* By default, look for config file at /etc/vital-backups.conf for system wide use. This is part of an effort to stop running it as root and use sudo.

* Add a --config parameter so a user could do a backup of vital user files only
using a local configuration file.

* Updated example configuration file to match the one I'm actually using now.

## 1.0.0 Github Update

* Adding Semantic Version for automated releases

* Adding install.sh script to allow automated installs
