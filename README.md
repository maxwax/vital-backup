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

#### Emergency Drives

Process

* Partition a USB drive with a 2G Linux boot partition
* Partition the rest of the drive for data
* Use a Linux tool like Fedora Linux's LiveUSBCreator to install a LiveBoot of Linux on the first 2G partition.
* Test the USB drive by booting Linux with it
* Use an encryption tool like LUKS to encrypt the data partition:

```bash
# cryptsetup -y -v luksFormat /dev/mydevice_partition2
```
You'll be prompted by cryptsetup to confirm this action and specify a passphrase.

* Once formatted, open the encrypted device and map it to a temporary /dev/mapper point

```bash
# cryptsetup luksOpen /dev/mydevice_partition2 mydev-encrypted
```
* Format the encrypted partition with a filesystem:

```bash
# mkfs.ext4 -v -m 0 -L UsbDriveData /dev/mapper/mydev-encrypted
```
* Make a mount point and mount the filesystem

```bash
# mkdir /mnt/UsbDriveData
# mount /dev/mapper/mydev-encrypted /mnt/UsbDriveData
```

* Add some sources to the config file and specify "target /mnt/UsbDataDrive", then run vital-backup

```bash
# vital-backup
```
* Unmount the filesystem, close the encrypted device, sync any unwritten data, and store the USB drive in a safe place.

```bash
# umount /mnt/UsbDataDrive
# cryptsetup luksClose /dev/mapper/mydev-encrypted
```
