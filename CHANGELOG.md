# CHANGLOG for 'vital-backup' script

## 1.3.0 Fix total size required calculations

* The total size required to backup a collection of directories was incorrect.  Using the du option -sh the size to backup a directory was 57G.  Using the -sb option to calculate a size in bytes then divide by the size (in bytes) of a gigabyte would result in 135G being reported.  This may have to do with the directory containing multiple hard links to the same data as in a .git directory ?
* Replacing the use of -sb with "-s -B1" to summarize in 1 byte units reports an accurate number of bytes of data and the calculation is accurate at 56.84 G of space.
* This greatly helps identify the amount of space requird on the target and whether one can simply proceed with a backup or if one has to make more space available first.

## 1.2.0 unknown

## 1.1.0 New config file location and --config option

* By default, look for config file at /etc/vital-backups.conf for system wide use. This is part of an effort to stop running it as root and use sudo.

* Add a --config parameter so a user could do a backup of vital user files only
using a local configuration file.

* Updated example configuration file to match the one I'm actually using now.

## 1.0.0 Github Update

* Adding Semantic Version for automated releases

* Adding install.sh script to allow automated installs
