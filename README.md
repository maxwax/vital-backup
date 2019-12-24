### vital-backup
A simple but flexible bash script to perform backups of critical files

This script is part of my disaster recovery plan.  In the event my Linux laptop is inoperable or inaccessible, I can boot USB drives that contain encrypted backups of my most important data like keystores and insurance documents.

vital-backup makes it easy to define the sources of that critical data and multiple targets which should receive backups.  Once defined, vital-backup will use tar to archive this data on multiple mounted encrypted devices.

This script only performs the data archiving process.  See below for more information on the complete USB drive setup.

To use:

* Modify the config file to define one or more "source" directories you wish to backup
* Modify the config file to define one or more "target" mount points where you wish to archive data
* Modify the config file to define one or more "exclude" objects which should be skipped

#### Syntax

Backup one or more personal directories to one or more targets

```bash
$ vital-backup
```

Backup personal data and system data to all targets

```bash
$ sudo vital-backup
```

Backup to only one device. This allows you to run multiple copies of vital-backup in parallel

```bash
$ vital-backup <named_target>
```

```bash
$ vital-backup UsbVault1
```


