# Simulation Website

Building a WordPress/CiviCRM local website that is a simulation of the Ventraip / cmrailttrail.org.au website.

The computer that hosts this simulation website is expected to be in the same local network as the computer you normally use. 

The simulation computer will only provide support for IPV4, i.e. no IPV6, and http, i.e. no https.

## Computer Hardware - Minimum Specifications

* CPU: Quad core, >= 2.5GHz
* RAM: >= 4GB
* Disk: Solid State Sata Disk (SSD). 128GB seems to be the minimum available these days.
* Ethernet: 1000Mb/sec at a static ip address. If a cable can be connected from the computer to the router.
* Wifi: If not using ethernet, then the wifi connection to the router needs a static ip address.
* Operating System: Linux. Recommend Ubuntu Mate 24.04.x

## Summary of Installation Steps

* Download Operating System iso file. E.g. `https://ubuntu-mate.org/download/`
* Copy iso to make a bootable USB drive.
* Boot the USB drive.
* Install Ubuntu on computer with a SSD.
* Set initial user name to be `Administrator` with an account name of `cmrailtr`.
* Set a static/fixed address to the router on the ethernet or wifi connection. e.g. 192.168.1.100
* Perform updates to get the latest patches.
* Install openssh-server.
* Install PHP modules.
* Install Apache2 and change Owner and Group from `www-data` to `cmrailtr`.
* Install MariaDB. `mariadb-server` and `mariadb-client`
* Install WordPress zip file, with the top-level directory in the home folder. All WordPress files and folders have the Owner and Group of `cmrailtr`.
* WordPress database is: `cmrailtr_czhn1`
* WordPress user is: `cmrailtr_czhn1`
* Rename `wordpress` top-level directory as `public_html`
* Install CiviCRM with its own database.

### Summary of variables that change:

In installing WordPress and CiviCRM to simulate the cmrailtrail.org.au website the following is a summary of the variables that are used:

*    Account Name: `cmrailtr`
*    WordPress top level directory`public_html`. Default is `wordpress`. 
*    WordPress Maria database name:`cmrailtr_czhn1`. 
*    WordPress MariaDB database User name: `cmrailtr_czhn1`
*    WordPress tables prefix: `bsen_`. Default is `wp_`: 
*    CiviCRM MariaDB database name: `cmrailtr_civicrm`
*    CiviCRM tables prefix: `civicrm_`

### Tailoring:
In the home folder create a bin folder for bash and Python scripts. `$ mkdir bin`
In the home folder create a backup folder. `$ mkdir civicrm_backup`

### SSH installed on your normal computer.

Assuming that there is a computer that you normally use, and the simulation computer will be another computer on the same local network. From your normal computer you will need to make a terminal connection to the simulation computer to perform instllation and backup tasks, etc. This is done with `openssh`, which also provides copying files between computers.

* Make sure that `openssh-client` is installed.
* Check you can *ssh* into the simulation computer. E.g. `$ ssh cmrailtr@192.168.1.100`
* Check you can *scp* and transfer files between computers.


### Computer Connections

The simulation computer should be setup with a fixed IP address. Use `sudo apt install openssh-server` to install the `openssh-server`, which will also install `openssh-client`.

These utilities should exist on both computers: **SSH** - **S**ecure **SH**ell and **SCP** - **S**ecure **C**o**P**y.

Use **SSH** to provide on your normal computer, a terminal screen into the simulation computer. You need to know the fixed ip address of the simulation computer. E.g. 192.168.1.101.

1. Open a MATE Terminal on your normal computer. `Ctrl-Alt-t`

2.  ```
    ssh cmrailtr@192.168.1.101
    cmrailtr@192.168.1.101's password:
    cmrailtr@CMRT-Demo:~$
    ```
    
3. The commands you now type are executed on the simulation computer.

Use **SCP** to copy a file, E.g. `wordpress.conf`, from your normal computer to the simulation computer.

1.  Open a MATE Terminal on your normal computer. `Ctrl-Alt-t`

2.  ```
    $ scp wordpress.conf cmrailtr@192.168.1.101:
    cmrailtr@192.168.1.101's password: 
    wordpress.conf  100%  410    55.3KB/s   00:00
    ```
3. The `wordpress.conf` file is now in the simulation computers ~/ home directory.

Use **SCP** on your normal computer to copy a file, E.g. `wordpress_backup.zip`, from the ~/ home folder on the simulation computer to your normal computer.

1.  Open a MATE Terminal on your normal computer. `Ctrl-Alt-t`

2.  ```
    $ scp cmrailtr@192.168.1.101:wordpress_backup.zip wordpress_backup.zip
    cmrailtr@192.168.1.101's password: 

    $ ls wordpress_backup.zip
    wordpress_backup.zip
    ```
3.  The `wordpress_backup.zip` has not been copied from the simulation computer to the normal computer. This is one way to move backups off-site of the web-site hosting computers.
   

### Install  PHP, Apache2, MariaDB

Apache2 is the http web server, MariaDB is the SQL database, and PHP the PHP: Hypertext Preprocessor. 

A single apt install command installs most of the component needed by WordPress:
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
### PHP modules

In the above `apt install` the `php8.3.common` library includes the following 33 php modules:
```
php-calendar, php-ctype, php-exif, php-ffi, php-fileinfo, php-ftp, php-iconv, php-pdo, php-phar, php-posix, php-shmop, php-sockets, php-sysvmsg, php-sysvsem, php-sysvshm, php-tokenizer, php8.3-calendar, php8.3-ctype, php8.3-exif, php8.3-ffi, php8.3-fileinfo, php8.3-ftp, php8.3-gettext, php8.3-iconv, php8.3-pdo, php8.3-phar, php8.3-posix, php8.3-shmop, php8.3-sockets, php8.3-sysvmsg, php8.3-sysvsem, php8.3-sysvshm, php8.3-tokenizer
```
Also note that the php8.3-xml library contains these 11 php modules:
```
php-dom, php-simplexml, php-xml, php-xmlreader, php-xmlwriter, php-xsl, php8.3-dom, php8.3-simplexml, php8.3-xmlreader, php8.3-xmlwriter, php8.3-xsl
```
### PHP Modules Installed

The command line utility `php` may be used to determine the PHP modules installed with the command:
```
cmrailtr@CMRT-Demo:~$ php -m
```
Another way to check which PHP modules are installed is to get a listing of the `/etc/php/8.3/mods-available folder`:
```
cmrailtr@CMRT-Demo:~$ ls /etc/php/8.3/mods-available
apcu.ini      ftp.ini        mysqli.ini     shmop.ini      xml.ini
bcmath.ini    gettext.ini    mysqlnd.ini    simplexml.ini  xmlreader.ini
calendar.ini  iconv.ini      opcache.ini    soap.ini       xmlwriter.ini
ctype.ini     igbinary.ini   pdo.ini        sockets.ini    xsl.ini
curl.ini      imagick.ini    pdo_mysql.ini  ssh2.ini       zip.ini
dom.ini       intl.ini       phar.ini       sysvmsg.ini
exif.ini      mbstring.ini   posix.ini      sysvsem.ini
ffi.ini       memcached.ini  readline.ini   sysvshm.ini
fileinfo.ini  msgpack.ini    redis.ini      tokenizer.ini
```

### Apache2

Ventraip who use CloudLinux as the hosting OS for the cmrailtrail.org.au website, appear to use *LiteSpeed* as their HTTP Server. LiteSpeed is a propriatory application and users of the cmrailtr account do not have the privileges to access it. In the simulation computer, *Apache2* is used as a replacement for LiteSpeed.

Apache2 is an HTTP server software that handles requests from clients, typically web browsers, using the Hypertext Transfer Protocol (HTTP). It serves web pages and other resources by responding to requests with the appropriate content or error messages. 

### Apache2 Sites Available

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
The above file sets the path to the website via `/home/cmrailtr/` directories. When WordPress is installed it creates a top-evel direcory of `wordpress` This is then renamed to `public_html` to match the cmrailtrail.org.au website layout.

### Apache2 Environmental Variables

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

This document provides information on wp-config: https://developer.wordpress.org/advanced-administration/wordpress/wp-config/

The `wp-config-sample.php` file is edited and saved as `wp-config.php`:
Changed From:
```
/** The name of the database for WordPress */
define( 'DB_NAME', 'database_name_here' );

/** Database username */
define( 'DB_USER', 'username_here' );

/** Database password */
define( 'DB_PASSWORD', 'password_here' );
```
Changed to:
```
/** The name of the database for WordPress */
define( 'DB_NAME', 'cmrailtr_czhn1' );

/** Database username */
define( 'DB_USER', 'cmrailtr_czhn1' );

/** Database password */
define( 'DB_PASSWORD', 'W.---HIDDEN---40' );
```
The table prefix is also changed from `wp_` to `bsen_`, so it matches the table prefix used on cmrailtrail.org.au website:
 ```
 * $table_prefix = 'wp_';
 */
$table_prefix = 'bsen_';
```
Various keys are required. These are obtained by accessing the web-page:
```
https://api.wordpress.org/secret-key/1.1/salt/
```
The 8 lines of data from the web-page are pasted into the `wp-config.php` file.


### Create the WordPress database

Connect to MariaDB and use the mysql database:
```
cmrailtr@CMRT-Demo:~$ sudo mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
...
MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.006 sec)

MariaDB [(none)]> USE mysql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [mysql]> 
```
Create the WordPress database with the name `cmrailtr_czhn1` that is used on cmrailtrail.org.au:
```
mysql> CREATE DATABASE cmrailtr_czhn1;
```
Create a User, who happens to have the same name as the WordPress database, so they can access the `cmrailtr_czhn1` database without needing to use sudo privilege:
```
mysql> CREATE USER cmrailtr_czhn1@localhost IDENTIFIED BY 'W.---HIDDEN---40';
```
Grant privileges to the User `cmrailtr_czhn1`:
```
MariaDB [mysql]> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, ALTER ON cmrailtr_czhn1.* TO 'cmrailtr_czhn1'@'localhost' WITH GRANT OPTION;
```
Flush the privileges
```
MariaDB [mysql]> FLUSH PRIVILEGES;
```
Quit the database and restart mysql for good measure:
```
$ sudo systemctl restart mysql 
```
Connect to the WordPress database `cmrailtr_czhn1` as user `cmrailtr_czhn1`
```
cmrailtr@CMRT-Demo:~$ mysql --user=cmrailtr_czhn1 --password=W.---HIDDEN---40 --database=cmrailtr_czhn1
...snip...
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Server version: 10.11.13-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04
```
Show databases and not that User `cmrailtr_czhn1` has access to `cmrailtr_czhn1` database:
```
MariaDB [cmrailtr_czhn1]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
2 rows in set (0.001 sec)
```
Show tables and note that they are all prefixed with `bsen_` rather than `wp_`:
```
MariaDB [cmrailtr_czhn1]> SHOW TABLES;
+--------------------------+
| Tables_in_cmrailtr_czhn1 |
+--------------------------+
| bsen_commentmeta         |
| bsen_comments            |
| bsen_links               |
| bsen_options             |
| bsen_postmeta            |
| bsen_posts               |
| bsen_term_relationships  |
| bsen_term_taxonomy       |
| bsen_termmeta            |
| bsen_terms               |
| bsen_usermeta            |
| bsen_users               |
+--------------------------+
12 rows in set (0.001 sec)
```

After the installation of WordPress a total of 351 directories and 3306 files are created.

The remainder of the WordPress installation is performed via a Browser.

Select the Language - English (Australian)
![language](images/simulation/s1-language.png)

Create an Account name that you use to log into the WordPress, then click *Install WordPress*.
During the install, 7 more WordPress directories and 78 files are added. Many of these files are to do with support for English (Australian).
![account](images/simulation/s2-account.png)

Successfully Installed WordPress. Click to Log In 
![success](images/simulation/s3-success.png)

Enter the Username and Password that you provided
![login](images/simulation/s4-login.png)

This is the WordPress Administraton screen. By selecting Tools --> Site Health --> Status, the status of the WordPress installation may be observed
![status](images/simulation/s5-status.png)

On the above screen click on *Info* to get details about WordPress, the server, the database, etc.
![info](images/simulation/s6-info.png)


For the installation of the CiviCRM Installation proceed to the [documentation](CiviCRM%20Installation.md)

## Notes For CiviCRM Installation:
https://github.com/irsbugs/cmrt/blob/main/CiviCRM%20Installation.md
Change database pointer with CiviCRM installation...
mysql://cmrailtr_czhn1:HiDDEN@localhost:3306/cmailtr_civicrm

