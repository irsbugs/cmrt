# Performing a Backup of CiviCRM

With CiviCRM for Wordpress, the CiviCRM files are in subdirectories off the `wordpress/wp-content/plugins/civicrm/` directory.

Using the tree utility, this is a simplified view of the CiviCRM files in relation to the website and Wordpress directories. 
```
/srv
└── www
    └── wordpress
        ├── wp-content
            ├── plugins
                ├── civicrm <-- CiviCRM plugin for Wordpress
                    ├── <-- 2667 directories and 14698 files for CiviCRM version 5.62.1
```

## Example of backing up the CiviCRM directories and files to a *zip* file.

Login to your CiviCRM administrator account. E.g. civiadmin.
```
$ mkdir civicrm_backup

$ cd /srv/www/wordpress/wp-content/plugins/

:/srv/www/wordpress/wp-content/plugins$ sudo zip -rq civicrm_backup_2025-05-17.zip civicrm/

:/srv/www/wordpress/wp-content/plugins$ mv civicrm_backup_2025-05-17.zip ~/civicrm_backup/

:/srv/www/wordpress/wp-content/plugins$ cd ~/civicrm_backup

:~/civicrm_backup$ ls -l
-rw-r--r--  1 root     root     68177948 May 17 18:34 civicrm_backup_2025-05-17.zip

:~/civicrm_backup$ id
uid=1000(civiadmin) gid=1000(civiadmin) groups=4(adm),20(dialout),24(cdrom),27(sudo),30(dip),
    46(plugdev),120(lpadmin),132(lxd),133(sambashare)

:~/civicrm_backup$ sudo chown civiadmin: civicrm_backup_2025-05-17.zip
[sudo] password for civiadmin: 

:~/civicrm_backup$ ls -l

-rw-r--r--  1 civiadmin civiadmin 68177948 May 17 18:34 civicrm_backup_2025-05-17.zip
```
Copy civicrm_backup_2025-05-17.zip to a USB stick for storage off-site.


## Above example with explanations:

Example of backing up the CiviCRM directories and files to a *zip* file.

Have a user account in which you can administer and store CiviCRM backups, etc.
Login to your CiviCRM administrator account. E.g. civiadmin.
The account need to have *superuser do* / *substitute user, do* (sudo) privilege.

Create a directory for placing the backup of the current CiviCRM

`$ mkdir civicrm_backup`

Change to the plugin directory. This has  the civicrm directory. 
Off this directory are all the CiviCRM folders and files

`$ cd /srv/www/wordpress/wp-content/plugins/`

Use the zip utility to backup to the zip to the file `civicrm_backup_yyyy-mm-dd.zip`. 
Two of the zip options that are used:

* -r   recurse into directories`
* -q   quiet operation
  
The civicrm directory and all subdirectores and their files will be zipped.

`:/srv/www/wordpress/wp-content/plugins$ sudo zip -rq civicrm_backup_2025-05-17.zip civicrm/`

Note that The *user* and *group* id's of all files in the backup is *www-data*

Move the backup zip file to your administrator home directory: `civcrm_backup`
sudo is required as the owner of the zip file is root.

`:/srv/www/wordpress/wp-content/plugins$ sudo mv civicrm_backup_2025-05-17.zip ~/civicrm_backup/`

Return to your home directory where the zip file is located.

`:/srv/www/wordpress/wp-content/plugins$ cd ~/civicrm_backup`

Check the file size and note that its owner and group are root.
```
:~/civicrm_backup$ ls -l
-rw-r--r--  1 root     root     68177948 May 17 18:34 civicrm_backup_2025-05-17.zip
```

Check what are your user (uid) and group (gid) names. E.g 
```
:~/civicrm_backup$ id
uid=1000(civiadmin) gid=1000(civiadmin) groups=4(adm),20(dialout),24(cdrom),27(sudo),30(dip),
    46(plugdev),120(lpadmin),132(lxd),133(sambashare)
```

Change the backup zip file to have the user and group of your account.

`:~/civicrm_backup$ sudo chown civiadmin: civicrm_backup_2025-05-17.zip`

Check the user and group changed

```
:~/civicrm_backup$ ls -l
-rw-r--r--  1 civiadmin civiadmin 68177948 May 17 18:34 civicrm_backup_2025-05-17.zip
```

If you plug in a USB storage device, then you can copy this zip file without needing to use sudo.

## Checking the backup zip file. (Optional)

Unzip the backup zip file to sub-directories off your civicrm_backup/civicrm directory.
The unzip options used are:

* -q  quiet mode (-qq => quieter)
* -X  restore UID/GID info. (This is "www-data"). 

`:~/civicrm_backup$ unzip -qX civicrm_backup_2025-05-17.zip`

Check the top levels of the unzipped directories

```
:~/civicrm_backup$ ls -l
total 66592
drwxr-xr-x 10 www-data  www-data      4096 Jun 17  2023 civicrm
-rw-r--r--  1 civiadmin civiadmin 68177948 May 17 18:34 civicrm_backup_2025-05-17.zip

:~/civicrm_backup$ ls -l civicrm
total 84
drwxr-xr-x  6 www-data www-data  4096 Feb 28  2023 assets
drwxr-xr-x 24 www-data www-data  4096 Jun 17  2023 civicrm
-rw-r--r--  1 www-data www-data 38952 Jun 17  2023 civicrm.php
drwxr-xr-x  4 www-data www-data  4096 Feb 28  2023 includes
drwxr-xr-x  2 www-data www-data  4096 Feb 28  2023 languages
-rw-r--r--  1 www-data www-data   690 Feb 28  2023 phpunit.xml.dist
-rw-r--r--  1 www-data www-data  2075 Feb 28  2023 README.md
-rw-r--r--  1 www-data www-data  2036 Jun 17  2023 readme.txt
drwxr-xr-x  3 www-data www-data  4096 Feb 28  2023 tests
-rw-r--r--  1 www-data www-data  1007 Feb 28  2023 uninstall.php
drwxr-xr-x  2 www-data www-data  4096 Feb 28  2023 wp-cli
drwxr-xr-x  5 www-data www-data  4096 Jun 17  2023 wp-rest
```

Use the tree utility of CiviCRM, but only display 1 level 
```
:~/civicrm_backup$ tree -L 1 civicrm
civicrm
├── assets
├── civicrm
├── civicrm.php
├── includes
├── languages
├── phpunit.xml.dist
├── README.md
├── readme.txt
├── tests
├── uninstall.php
├── wp-cli
└── wp-rest

8 directories, 5 file
```

Use the tree utility to produce a full tree of all directories and files.
Totals for directories and file are at the bottom. The output will be over 15000 lines long.
```
:~/civicrm_backup$ tree civicrm
civicrm
├── assets
...snip...
└── wp-rest
    ├── Autoloader.php
    ...snip...
    ├── Plugin.php
    └── README.md

2667 directories, 14698 files
```
