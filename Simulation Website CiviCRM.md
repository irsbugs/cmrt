# Installation of CiviCRM on the Simulation Website

The document [Simulation Website](Simulation%20Website.md) contains information on the preparation and installation of WordPress to simulate the configuration on the *Ventraip - cmrailtrail.org.au* website. This document details the adding of CiviCRM onto this Ubuntu 24.04 based simulation website.


## Edit the Apach2 php.ini file.

Some parameters in the file `/etc/php/8.3/apache2/php.ini` need to be increased for CiviCRM. 

These are the parameters that need increasing and line number in the `php.ini` file where they were found:
```
Line 417: max_execution_time = 240
Line 429: max_input_time = 120
Line 445: memory_limit = 256M    
Line 713: post_max_size = 50M
Line 865: upload_max_filesize =  50M 
```

## Using pluma on normal computer to edit php.ini

Copy the php.ini file from the simulation computer to the normal computer
```
ian@hp:~$ scp cmrailtr@192.168.1.101:/etc/php/8.3/apache2/php.ini php.ini
cmrailtr@192.168.1.101's password: 
php.ini                                       100%   72KB 293.4KB/s   00:00    
```
Use *pluma* to edit the file and apply the above changes:
```
ian@hp:~$ pluma php.ini
```
Copy the edited file back to the `home` folder on the simulaton computer: 
```
ian@hp:~$ sudo scp php.ini cmrailtr@192.168.1.101:php.ini
cmrailtr@192.168.1.101's password: 
php.ini                                       100%   72KB 706.7KB/s   00:00    
```

Connect to the simulation computer `home` folder and copy the `php.ini` so it replaces the `/etc/php/8.3/apache/php.ini` file
```
cmrailtr@CMRT-Demo:~$ ls -l /etc/php/8.3/apache2/
total 76
drwxr-xr-x 2 root root  4096 Jun 19 11:48 conf.d
-rw-r--r-- 1 root root 73718 Mar 19 23:08 php.ini

cmrailtr@CMRT-Demo:~$ ls -l php.ini
-rw-r--r-- 1 cmrailtr cmrailtr 74053 Jun 27 11:12 php.ini

cmrailtr@CMRT-Demo:~$ sudo cp php.ini /etc/php/8.3/apache2/php.ini
[sudo] password for cmrailtr: 

cmrailtr@CMRT-Demo:~$ ls -l /etc/php/8.3/apache2/
total 80
drwxr-xr-x 2 root root  4096 Jun 19 11:48 conf.d
-rw-r--r-- 1 root root 74053 Jun 27 11:15 php.ini
cmrailtr@CMRT-Demo:~$ ls -l /etc/php/8.3/apache2/
```

## Connect to Database as root
```
cmrailtr@CMRT-Demo:~$ sudo mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 36
Server version: 10.11.13-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_czhn1     |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.008 sec)
```

## Check if Timezone Data has been installed
```
MariaDB [(none)]> SELECT @@system_time_zone;
+--------------------+
| @@system_time_zone |
+--------------------+
| NZST               |
+--------------------+
1 row in set (0.000 sec)

MariaDB [(none)]> SELECT TIMEDIFF(NOW(), UTC_TIMESTAMP);
+--------------------------------+
| TIMEDIFF(NOW(), UTC_TIMESTAMP) |
+--------------------------------+
| 12:00:00                       |
+--------------------------------+
1 row in set (0.000 sec)

MariaDB [(none)]> SELECT CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland",
"Australia/Melbourne");
+------------------------------------------------------------------------------+
| CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland", "Australia/Melbourne") |
+------------------------------------------------------------------------------+
| NULL                                                                         |
+------------------------------------------------------------------------------+
1 row in set (0.000 sec)
```
NULL so Timezone data is not installed:

## Execute command to install Timezone data

From the command prompt execute:
```
cmrailtr@CMRT-Demo:~$ sudo mysql_tzinfo_to_sql /usr/share/zoneinfo | sudo mysql -u root mysql
```

Check Timezone
```
MariaDB [(none)]> SELECT CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland",
    -> "Australia/Melbourne");
+------------------------------------------------------------------------------+
| CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland", "Australia/Melbourne") |
+------------------------------------------------------------------------------+
| 2025-06-03 12:30:00                                                          |
+------------------------------------------------------------------------------+
```
Not NULL. Know that Melbourne is 2 hours behind Auckland.


## Create the CiviCRM Database
```
MariaDB [(none)]> use mysql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [mysql]> show databases;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_czhn1     |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.001 sec)

MariaDB [mysql]> CREATE DATABASE cmrailtr_civicrm;
Query OK, 1 row affected (0.007 sec)

MariaDB [mysql]> show databases;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civicrm   |
| cmrailtr_czhn1     |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
6 rows in set (0.000 sec)
```

Grant the privileges to the User of CiviCRM, `cmrailtr_czhn1`:
```
MariaDB [mysql]> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES, TRIGGER, CREATE ROUTINE, ALTER ROUTINE, REFERENCES, CREATE VIEW, SHOW VIEW ON cmrailtr_civicrm.* TO 'cmrailtr_czhn1'@'localhost' IDENTIFIED BY 'W---HIDDEN---0';
Query OK, 0 rows affected (0.011 sec)

MariaDB [mysql]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.001 sec)
```

## Check Login by User 

The User `cmrailtr_czhn1` does not need sudo priv to login.
However, they have restricted view of only three of the six databases.
```
cmrailtr@CMRT-Demo:~$ mysql -u cmrailtr_czhn1 -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 41
Server version: 10.11.13-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civicrm   |
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
3 rows in set (0.001 sec)
```

## Review the `cmrailtr_civicrm` Database before CiviCRM install
```
MariaDB [(none)]> use cmrailtr_civicrm
Database changed
MariaDB [cmrailtr_civicrm]> show tables;
Empty set (0.000 sec)
```


cmrailtr@CMRT-Demo:~$ 
cmrailtr@CMRT-Demo:~$ 
cmrailtr@CMRT-Demo:~$ ls
Desktop    civicrm-6.2.0-wordpress.zip             snap
Documents  email_to_craig                          test
Downloads  enabled                                 tor-browser
Music      ian@192.168.1.100                       wordpress-6.8.1.zip
Pictures   index.php                               wordpress.conf
Public     php.ini                                 wp-config.php
Templates  protonvpn-stable-release_1.0.8_all.deb
Videos     public_html
cmrailtr@CMRT-Demo:~$ cd public_html/wp-content/plugins/
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ ls -l
total 12
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ cp ~/civicrm-6.2.0-wordpress.zip
cp: missing destination file operand after '/home/cmrailtr/civicrm-6.2.0-wordpress.zip'
Try 'cp --help' for more information.
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ cp ~/civicrm-6.2.0-wordpress.zip *
cp: target 'index.php': Not a directory

## Unzip CiviCRM

The CiviCRM for WordPress zip file has been downloaded to the `home` folder. From the `home` folder the directory is changed to be:
`/home/cmrailtr/public_html/wp-content/plugins`. The zip file is then copied to the `plugins` folder:
```
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ cp ~/civicrm-6.2.0-wordpress.zip civicrm-6.2.0-wordpress.zip

cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ ls -l
total 46360
drwxr-xr-x 4 cmrailtr cmrailtr     4096 Apr 14 23:37 akismet
-rw-rw-r-- 1 cmrailtr cmrailtr 47456829 Jun 27 12:14 civicrm-6.2.0-wordpress.zip
-rw-r--r-- 1 cmrailtr cmrailtr     2646 Mar  6 00:18 hello.php
-rw-r--r-- 1 cmrailtr cmrailtr       28 Jun  5  2014 index.php
```
The unzip command is used with the quiet option.
```
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ unzip -q civicrm-6.2.0-wordpress.zip
```
From the `plugins` folder, the unzipping created a `civicrm` folder. Off the `civicrm` folder:
```
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ tree civicrm
...snip...
2792 directories, 18272 files
```
The top two levels of directories of the plugin folder then looked like this:
```
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ tree -L 2

/home/cmrailtr/public_html/wp-content/plugins
├── akismet
│   ├── LICENSE.txt
│   ├── _inc
│   ├── akismet.php
│   ├── changelog.txt
│   ├── class.akismet-admin.php
│   ├── class.akismet-cli.php
│   ├── class.akismet-rest-api.php
│   ├── class.akismet-widget.php
│   ├── class.akismet.php
│   ├── index.php
│   ├── readme.txt
│   ├── views
│   └── wrapper.php
├── civicrm
│   ├── README.md
│   ├── assets
│   ├── civicrm
│   ├── civicrm.php
│   ├── includes
│   ├── languages
│   ├── phpcs.xml
│   ├── phpunit.xml.dist
│   ├── readme.txt
│   ├── tests
│   ├── uninstall.php
│   ├── wp-cli
│   └── wp-rest
├── civicrm-6.2.0-wordpress.zip
├── hello.php
└── index.php

12 directories, 20 files
```
The zip file is no longer required and was removed.
```
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ rm civicrm-6.2.0-wordpress.zip 
```

## Switch to Wordpress wp-admin to complete the CiviCRM installation:

Open a browser and login to the WordPress Admin account on the simulation computer. E.g. `http://192.168.1.101/wp-admin`

In the WordPress main screen go to --> Plugins --> civicrm --> activate

The CiviCRM Installation will be performed in the browser...

Initial Installation Screen - Errors are due to the link to the CiviCRM Database defaulted to the WordPress database
![civicrm1](/images/simulation_civicrm/civicrm1.png)

Editing the link so that the `cmrailtr_civicrm` database is used via user `cmrailtr_czhn1`
CiviCRMmysql://cmrailtr_czhn1:W----HIDDEN-----0@localhost:3306/cmrailtr_civicrm
![civicrm2](/images/simulation_civicrm/civicrm2.png)

CiviCRM Installer screen with out any errors. Top.
![civicrm3](/images/simulation_civicrm/civicrm3.png)

CiviCRM Installer screen with out any errors. Bottom.  5 Components selected and 3 unselected.
![civicrm4](/images/simulation_civicrm/civicrm4.png)

Change to all 8 components selected. No sample data.
![civicrm5](/images/simulation_civicrm/civicrm5.png)
Environment with CiviCRM Database set to `cmrailtr_civicrm`:

![civicrm6](/images/simulation_civicrm/civicrm6.png)

Installation Success screen
![civicrm7](/images/simulation_civicrm/civicrm7.png)

CiviCRM Home screen - with System Status: Warnings
![civicrm8](/images/simulation_civicrm/civicrm8.png)

CiviCRM System Status Screen - Top.
![civicrm9](/images/simulation_civicrm/civicrm9.png)

CiviCRM System Status Screen - Bottom.
![civicrm10](/images/simulation_civicrm/civicrm10.png)
