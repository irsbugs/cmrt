# CiviCRM Upgrading

## Introduction

New releases of CiviCRM for WordPress occur about once a month. Although WordPress has an automatic facility to perform upgrades, the CiviCRM package is currently not designed to be automatically upgraded by WordPress. I.e. In wp-admin --> Plugins --> CiviCRM it states: *Auto-updates are not available for this plugin*.

This document describes the manual process of upgrading CiviCRM.

## Logging In

To perform the upgrade of CiviCRM it is necessary to log in to the Ventraip *cmrailtr* account. Use this link:

https://vip.ventraip.com.au/login

...and then provide a Username and Password and also satisfy the two factor authentication process.

Upon logging in go to: Web Hosting --> cPanel --> Tools --> Terminal.

*Terminal* will be at the home, *~/*, folder for the *cmrailtr* account. All folders and files will have *cmrailtr* as their *owner*. This includes the *public-html* folder, which is the top-level directory for WordPress.

By having all the WordPress / CiviCRM folders and files owned by *cmrailtr*, then it removes *Permission denied* errors and the need to use an elevated privilege when performing the upgrade.

### Folders and Files

* ~/bin/ this folder may contain bash or Python scripts to perform back-up, etc. These scripts may be executed from anywhere in the account.
* ~/civicrm_backup/ this folder is where backups of the CiviCRM files and database will be placed.
* ~/public_html/ this folder is the top-level directory of WordPress
* ~/public_html/wp-content/plugins/ this folder is the staging directory for new version zip files of CiviCRM.
* ~/public_html/wp-content/plugins/civicrm/ this folder is the top-level directory of CiviCRM.



### WordPress / CiviCRM web hosting on other systems.

If WordPress / CiviCRM are not hosted by Ventraip, then you are likely to have an *admim* account to perform the upgrade, and find the owner of the WordPress / CiviCRM folders and files to be *www-data*. 

Apache2 is the generator of the *www-data* User and Group naming. These are defined by environmental vasariales in the file `/etc/apache2/envvars`:
```
export APACHE_RUN_USER=www-data
export APACHE_RUN_GROUP=www-data
```
The CMRT website uses the User and Group name of *cmrailtr*. To simulate this when using the apache2 web server edit /etc/apache2/envvars` as follows:
```
export APACHE_RUN_USER=cmrailtr
export APACHE_RUN_GROUP=cmrailtr
```
The main account to log into the sumilation CMRT site should be *cmrailtr*. Thus all creating of files done in this account will have the Owner = *cmrailtr* and Group = *cmrailtr* 





Your IP address has changed. Please log in again.


Documents on performing an upgrade are:
* [Upgrading CiviCRM for WordPress](https://docs.civicrm.org/sysadmin/en/latest/upgrade/wordpress/)
* [Upgrades](https://docs.civicrm.org/sysadmin/en/latest/upgrade/)

## Directory and File Protections

In the cmtrailtrail.org.au 

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
This took to being /var/www with html as a folder off www

Maybe this was created before 


www-data@hp:~$ whoami
www-data
www-data@hp:~$ ls
html
www-data@hp:~$ ls -l
total 4
drwxr-xr-x 3 root root 4096 May 27 12:51 html
www-data@hp:~$ 

www-data@hp:~$ cd html
www-data@hp:~/html$ ls
apache2_default_page_index.html  info.php	wordpress
index.html			 latest.tar.gz
index.nginx-debian.html		 phpmyadmin
www-data@hp:~/html$ 

ian:x:1000:

www-data:x:33:civi-admin

ian@hp:~$ cat /etc/groups
cat: /etc/groups: No such file or directory
ian@hp:~$ cat /etc/group | grep ian
adm:x:4:syslog,ian,civi-admin
dialout:x:20:ian,civi-admin
cdrom:x:24:ian,civi-admin
sudo:x:27:ian,fred,civi-admin
dip:x:30:ian,civi-admin
plugdev:x:46:ian,civi-admin
lpadmin:x:120:ian,civi-admin
lxd:x:132:ian
ian:x:1000:

sambashare:x:133:ian,civi-admin

=====
Adding www-html to ian
From: ian:x:1000:
To: ian:x:1000:www-data <-- www-data Now added to ian.

ian@hp:~$ cat /etc/group | grep www-data
www-data:x:33:civi-admin
ian@hp:~$ 

ian@hp:~$ sudo usermod -a -G ian www-data
[sudo] password for ian: 

ian@hp:~$ cat /etc/group | grep ian
adm:x:4:syslog,ian,civi-admin
dialout:x:20:ian,civi-admin
cdrom:x:24:ian,civi-admin
sudo:x:27:ian,fred,civi-admin
dip:x:30:ian,civi-admin
plugdev:x:46:ian,civi-admin
lpadmin:x:120:ian,civi-admin
lxd:x:132:ian
ian:x:1000:www-data <-- www-data Now added to ian.
sambashare:x:133:ian,civi-admin


ian@hp:~$ sudo -s -u www-data
www-data@hp:/home/ian$ touch test1
touch: cannot touch 'test1': Permission denied
www-data@hp:/home/ian$ touch test2

May need to log out and log back in...

www-data@hp:/home/ian$ id
uid=33(www-data) gid=33(www-data) groups=33(www-data),1000(ian)
www-data@hp:/home/ian$ 

www-data@hp:/home/ian$ id ian
uid=1000(ian) gid=1000(ian) groups=1000(ian),4(adm),20(dialout),24(cdrom),27(sudo),30(dip),46(plugdev),120(lpadmin),132(lxd),133(sambashare)

Not yet assigned.

