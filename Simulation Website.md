# Simulation Website

Building a WordPress/CiviCRM local website that is a simulation of the Ventraip / cmrailttrail.org.au website

The computer that hosts this simulation website is expected to be in the same local network as the computer you normally use. 

The simulation computer will only provide support for IPV4 i.e. no IPV6, and http i.e. no https.

## Computer Hardware - Minimum Specifications

* CPU: Quad core, >= 2.5GHz
* RAM: >= 4GB
* Disk: Solid State Sata Disk (SSD). 128GB seems to be the minimum available these days.
* Ethernet: 1000Mb/sec at a static ip address. If a cable can be connected from the computer to the router.
* Wifi: If not using ethernet, then the wifi connection to the router needs a static ip address.
* Operating System: Linux. Recommend Ubuntu Mate 24.04.x

## Installation Steps

* Download Operating System iso file. E.g. `https://ubuntu-mate.org/download/`
* Copy iso to make a bootable USB drive.
* Boot the USB drive.
* Install Ubuntu on SSD
* Set initial account to be `cmrailtr` with a User name of `Administrator`
* Set a static/fixed address to the router on the ethernet or wifi connection. e.g. 192.168.1.100
* Perform updates to get the latest patches.
* Install openssh-server.
* Install Apache2 and change Owner and Group from `www-data` to `cmrailtr`.
* Install MariaDB. `mariadb-server` and `mariadb-client`
* Install WordPress. With top-level directory in home folder. All files nd folders have the Owner and Group of `cmrailtr`.
* WordPress database is: 
* Rename `wordpress` top-level directory as `public_html`
* Install CiviCRM with its own database.


### On the computer you normally use on your local network
* Make sure that openssh-client is installed.
* Check you can *ssh* into the simulation computer. `$ ssh cmrailtr@192.168.1.100`
* Check you can *scp* and transfer files between computers.

## Tailoring:
In the home folder create a bin folder for bash and Python scripts. `$ mkdir bin`
In the home folder create a backup folder. `$ mkdir civicrm_backup`

```
[cmrailtr@s03dd public_html]$ mysql -u root -p
Enter password:
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)
[cmrailtr@s03dd public_html]$

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'cmrailtr_czhn1' );

/** MySQL database username */
define( 'DB_USER', 'cmrailtr_czhn1' );

/** MySQL database password */
define( 'DB_PASSWORD', '[ Secret ]' );

cmrailtr_civicrm

Data tables prefix: bsen_ instead of wp
```
```
    Account Name: cmrailtr
    WordPress top level directory. Default is wordpress: public_html
    WordPress Maria database name. default is wordpress: cmrailtr_czhn1
    WordPress MariaDB database User name: cmrailtr_czhn1
    WordPress tables prefix. Default is wp_: bsen_
    CiviCRM MariaDB database name. Default is civicrm: cmrailtr_civicrm
    CiviCRM tables prefix: civicrm_

```
```
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civicrm   |
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
3 rows in set (0.004 sec)
```

For CiviCRM Installation:

https://github.com/irsbugs/cmrt/blob/main/CiviCRM%20Installation.md

User name for dataabase = cmrailtr_czhn1

mysql://cmrailtr_czhn1:HiDDEN@localhost:3306/cmailtr_civicrm

Username  Host Localhost 192.168.1.101
cmrailtr@CMRT-Demo:~$ 

### Computer Connections

Secure SHell SSH and SCP Secure CoPy

### Install Apache, MariaDB, PHP
```
$ sudo apt install apache2 ghostscript libapache2-mod-php mariadb-server

The following NEW packages will be installed:
  apache2 apache2-bin apache2-data apache2-utils galera-4 gawk libapache2-mod-php libapache2-mod-php8.3 libapr1t64
  libaprutil1-dbd-sqlite3 libaprutil1-ldap libaprutil1t64 libconfig-inifiles-perl libdbd-mysql-perl libdbi-perl
  libhtml-template-perl libmariadb3 libmysqlclient21 libsigsegv2 liburing2 mariadb-client mariadb-client-core mariadb-common
  mariadb-plugin-provider-bzip2 mariadb-plugin-provider-lz4 mariadb-plugin-provider-lzma mariadb-plugin-provider-lzo
  mariadb-plugin-provider-snappy mariadb-server mariadb-server-core mysql-common php-common php8.3-cli php8.3-common
  php8.3-opcache php8.3-readline pv socat

```
Note that the above includes five PHP modules:
```
php-common, php8.3-cli, php8.3-common, php8.3-opcache, php8.3-readline
```
In the above the php8.3.common library includes the following 33 php modules:
```
php-calendar, php-ctype, php-exif, php-ffi, php-fileinfo, php-ftp, php-iconv, php-pdo, php-phar, php-posix, php-shmop, php-sockets, php-sysvmsg, php-sysvsem, php-sysvshm, php-tokenizer, php8.3-calendar, php8.3-ctype, php8.3-exif, php8.3-ffi, php8.3-fileinfo, php8.3-ftp, php8.3-gettext, php8.3-iconv, php8.3-pdo, php8.3-phar, php8.3-posix, php8.3-shmop, php8.3-sockets, php8.3-sysvmsg, php8.3-sysvsem, php8.3-sysvshm, php8.3-tokenizer
```
Also note that the php8.3-xml library contains these 11 php modules:
```
php-dom, php-simplexml, php-xml, php-xmlreader, php-xmlwriter, php-xsl, php8.3-dom, php8.3-simplexml, php8.3-xmlreader, php8.3-xmlwriter, php8.3-xsl
```

### Apache Sites Available

The `/etc/apache2` directory has a `sites-available` sub-directory:

```
cmrailtr@CMRT-Demo:~$ ls -l /etc/apache2/sites-available/
total 12
-rw-r--r-- 1 root root 1286 Mar 19  2024 000-default.conf
-rw-r--r-- 1 root root 4573 Mar 19  2024 default-ssl.conf
```
Into this directory is copied the file *wordpress.conf*, which is edited to contain:
```
<VirtualHost *:80>
    DocumentRoot /home/cmrailtr/public_html
    <Directory /home/cmrailtr/public_html>
        Options FollowSymLinks
        AllowOverride Limit Options FileInfo
        DirectoryIndex index.php
        Require all granted
    </Directory>
    <Directory /home/cmrailtr/public_html/wp-content>
        Options FollowSymLinks
        Require all granted
    </Directory>
</VirtualHost>
```
The above file sets the path to the website via `/home/cmrailtr/` directories. When WordPress is installed it creates a top-evel direcory of `wordpress` This is then renamed to `public_html`

### Apache Environmental Variables

The `/etc/apache2` directory contains the file `envvars` i.e. environmental variables. This file is edited so the User and Group are `cmrailtr`. Later, with the installation of WordPress, all WordPress files and folders will have the owner and group of `cmrailtr`. This makes it easier to do backup's etc., of WordPress from the home directory. The changes to `envvars` are:
```
export APACHE_RUN_USER=www-data
export APACHE_RUN_GROUP=www-data
```
To:
```
export APACHE_RUN_USER=cmrailtr
export APACHE_RUN_GROUP=cmrailtr
```

### Install WordPress

The latest WordPress distribution zip file is copied to the ~/ home directory.

```
cmrailtr@CMRT-Demo:~$ file wordpress-6.8.1.zip
wordpress-6.8.1.zip: Zip archive data, at least v1.0 to extract, compression method=store
```
The command `unzip` with `-q` for quiet is used to extract all files and folders and place them off the toplevel directory `wordpress`:
```
cmrailtr@CMRT-Demo:~$ unzip -q wordpress-6.8.1.zip
```
The total folders and files for Wordpress 6.8.1 was: 344 directories, 3228 files 

The top-level directory is then renamed using the `mv` command from `wordpress` to `public_htnl`:
```
cmrailtr@CMRT-Demo:~$ mv /home/cmrailtr/wordpress /home/cmrailtr/public_html
```
A listing of the first level of the `public_html` directory is as follows:
```
cmrailtr@CMRT-Demo:~$ ls -l public_html
total 232
-rw-r--r--  1 cmrailtr cmrailtr   405 Feb  6  2020 index.php
-rw-r--r--  1 cmrailtr cmrailtr 19903 Mar  6 14:24 license.txt
-rw-r--r--  1 cmrailtr cmrailtr  7425 Mar  7 08:45 readme.html
-rw-r--r--  1 cmrailtr cmrailtr  7387 Feb 13  2024 wp-activate.php
drwxr-xr-x  9 cmrailtr cmrailtr  4096 Apr 30 16:41 wp-admin
-rw-r--r--  1 cmrailtr cmrailtr   351 Feb  6  2020 wp-blog-header.php
-rw-r--r--  1 cmrailtr cmrailtr  2323 Jun 14  2023 wp-comments-post.php
-rw-r--r--  1 cmrailtr cmrailtr  3336 Oct 15  2024 wp-config-sample.php
drwxr-xr-x  4 cmrailtr cmrailtr  4096 Apr 14 23:37 wp-content
-rw-r--r--  1 cmrailtr cmrailtr  5617 Aug  2  2024 wp-cron.php
drwxr-xr-x 30 cmrailtr cmrailtr 12288 Apr 30 16:41 wp-includes
-rw-r--r--  1 cmrailtr cmrailtr  2502 Nov 26  2022 wp-links-opml.php
-rw-r--r--  1 cmrailtr cmrailtr  3937 Mar 11  2024 wp-load.php
-rw-r--r--  1 cmrailtr cmrailtr 51414 Feb  3 16:55 wp-login.php
-rw-r--r--  1 cmrailtr cmrailtr  8727 Feb  8 16:00 wp-mail.php
-rw-r--r--  1 cmrailtr cmrailtr 30081 Mar  4 13:06 wp-settings.php
-rw-r--r--  1 cmrailtr cmrailtr 34516 Mar 10 18:16 wp-signup.php
-rw-r--r--  1 cmrailtr cmrailtr  5102 Oct 18  2024 wp-trackback.php
-rw-r--r--  1 cmrailtr cmrailtr  3205 Nov  8  2024 xmlrpc.php 
```
The above directory contains 3 subdirectories, `wp-admin`, `wp-content` and `wp-includes`.
Note that the above folder contains the file `wp-config-sample.php`. This is edited and renamed as `wp-config.php`. See below.  

### Creating wp-config.php 

The `wp-config-sample.php` file is edited as follows and saved as `wp-config.php`:

```
/** The name of the database for WordPress */
define( 'DB_NAME', 'database_name_here' );

/** Database username */
define( 'DB_USER', 'username_here' );

/** Database password */
define( 'DB_PASSWORD', 'password_here' );
```
Is changed to:
```
/** The name of the database for WordPress */
define( 'DB_NAME', 'cmrailtr_czhn1' );

/** Database username */
define( 'DB_USER', 'cmrailtr_czhn1' );

/** Database password */
define( 'DB_PASSWORD', 'W.VDf-HIDDEN-TH40' );
```
The table prefix is also changed from `wp)` to `bsen_`, so it matches the table prefix used on cmrailtrail.org.au website:
 ```
 * $table_prefix = 'wp_';
 */
$table_prefix = 'bsen_';
```
This document provides infomation on wp-config: https://developer.wordpress.org/advanced-administration/wordpress/wp-config/#table-prefix

### Create the WordPress database

mysql> CREATE DATABASE wordpress;
...changed to...
mysql> CREATE DATABASE cmrailtr_czhn1;


mysql> CREATE USER wordpress@localhost IDENTIFIED BY '<your-password>';
...Changed to...
mysql> CREATE USER cmrailtr_czhn1@localhost IDENTIFIED BY 'W.VDfqMNL4CNg2SasTH40';

mysql> GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
    -> ON wordpress.*
    -> TO wordpress@localhost;
...changed to...

mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, ALTER ON cmrailtr_czhn1.* TO cmrailtr_czhn1@localhost;
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, ALTER ON cmrailtr_czhn1.* TO 'cmrailtr_czhn1'@'localhost' WITH GRANT OPTION;

mysql> FLUSH PRIVILEGES;


===

After install folders and fiels = 351 directories, 3306 files
