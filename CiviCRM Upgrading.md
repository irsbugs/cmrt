# CiviCRM Upgrading

## Introduction

New releases of CiviCRM for WordPress occur about once a month. Although WordPress has an automatic facility to perform upgrades, the CiviCRM package is currently not designed to be automatically upgraded by WorPress. In wp-admin --> Plugins --> CiviCRM it states: *Auto-updates are not available for this plugin*.

Documents on performing an upgrade are:
* [Upgrading CiviCRM for WordPress](https://docs.civicrm.org/sysadmin/en/latest/upgrade/wordpress/)
* [Upgrades](https://docs.civicrm.org/sysadmin/en/latest/upgrade/)

## Downloading

* Check what is the current version of CiviCRM. From the WordPress wp-admin screen, click on Plugins and look for CiviCRM and its Version. E.g. 6.2.0
* Check what is the current latest version of CiviCRM. Goto: https://civicrm.org/download
* If CiviCRM needs upgrading then click on *Download CiviCRM for WordPress* and the *civicrm-x.x.x-wordpress.zip* file will be downloaded.
* The zip file needs to be moved to the folder: <wordpress_root>/wp-content/plugins/
* Alternatively right-click on *Download CiviCRM for WordPress* and copy the link. E.g. https://download.civicrm.org/civicrm-6.3.1-wordpress.zip
* Change your directory to be: <wordpress_root>/wp-content/plugins/
* Use wget to download the zip file to the plugins folder. E.g. $ wget https://download.civicrm.org/civicrm-6.3.1-wordpress.zip
```
root@hp:/srv/www/wordpress/wp-content# cd plugins
root@hp:/srv/www/wordpress/wp-content/plugins# wget https://download.civicrm.org/civicrm-6.3.1-wordpress.zip
--2025-06-15 19:46:38--  https://download.civicrm.org/civicrm-6.3.1-wordpress.zip
Resolving download.civicrm.org (download.civicrm.org)... 140.211.167.152, 2605:bc80:3010:102:0:3:1:0
Connecting to download.civicrm.org (download.civicrm.org)|140.211.167.152|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://storage.googleapis.com/civicrm/civicrm-stable/6.3.1/civicrm-6.3.1-wordpress.zip [following]
--2025-06-15 19:46:39--  https://storage.googleapis.com/civicrm/civicrm-stable/6.3.1/civicrm-6.3.1-wordpress.zip
Resolving storage.googleapis.com (storage.googleapis.com)... 142.250.76.123, 142.250.67.27, 142.250.204.27, ...
Connecting to storage.googleapis.com (storage.googleapis.com)|142.250.76.123|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 47554179 (45M) [application/zip]
Saving to: ‘civicrm-6.3.1-wordpress.zip’

civicrm-6.3.1-wordpress.zip 100%[===========================================>]  45.35M   806KB/s    in 2m 7s   

2025-06-15 19:48:47 (365 KB/s) - ‘civicrm-6.3.1-wordpress.zip’ saved [47554179/47554179]
```
## PrePare wordPress

Login to wordPress as an administrator. Remain logged in until upgrade is complete.

## Backup 

Ideally.. 
The backup operations should be done by Python or Bash scripts located in the folder ~/bin/. Thus it is available for execution to the command line from any directory.

Off the /home/ folder is located the folder ~/civicrm_backup/ This is where the backup's will be placed.

It may be useful to change directory to ~/civicrm_backup/ so the backup operations run with more simplified commands.






The tar program is used to create archives of many files, but it doesn't have its own compression routines. But by using the appropriate options with tar, it will cause tar to push the archive file through gzip. That way a compressed archive file is created containing a multi-file / multi-directory archive.

* Backup the existing civicrm from the folder  <wordpress_root>/wp-content/plugins/
* 
```
ian@hp:~$ echo backup_civicrm_$(date "+%Y-%m-%d_%H:%M:%S")_tar.gz
backup_civicrm_2025-06-15_20:40:12_tar.gz

ian@hp:~$ echo backup_civicrm_tar.gz_$(date "+%Y-%m-%d_%H:%M:%S")
backup_civicrm_tar.gz_2025-06-15_21:03:51

ian@hp:~$ echo civicrm_backup_tar.gz_$(date "+%Y-%m-%d_%H:%M:%S")
civicrm_backup_tar.gz_2025-06-15_21:04:05



tar -czvf level1.tar.gz level1

The tar options are:

    c: Create an archive.
    z: Push the files through gzip.
    v: Verbose mode. Print in the terminal window what tar is up to.
    f level1.tar.gz: Filename to use for the archive file.

```
ian@hp:~$ sudo -s -u www-data
www-data@hp:/home/ian$ whoami
www-data

www-data@hp:/home/ian$ mkdir test1
mkdir: cannot create directory ‘test1’: Permission denied

www-data@hp:/srv/www/wordpress$ touch test
www-data@hp:/srv/www/wordpress$ ls -l

-rw-rw-r--  1 www-data www-data     0 Jun 16 07:58 test

www-data@hp:/srv/www/wordpress$ cd ~/
www-data@hp:~$ whoami
www-data
www-data@hp:~$ ls
html
www-data@hp:~$ ls -l
total 4
drwxr-xr-x 3 root root 4096 May 27 12:51 html
www-data@hp:~$ 


