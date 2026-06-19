# Removal of the CiviCRM plugin to Wordpress

## Introduction

The VentraIP website was initially setup using Wordpress. The CiviCRM plugin for Wordpress was added in May 2025, using CiviCRM V6.2.0

```
[cmrailtr@s03dd ~]$ cat public_html/wp-content/plugins/civicrm/civicrm/xml/version.xml
<?xml version="1.0" encoding="iso-8859-1"?>
<version>
  <version_no>6.2.0</version_no>
  <releaseDate>2025-05-07</releaseDate>
</version>
[cmrailtr@s03dd ~]$
```

The name of the CiviCRM database was set to: *cmrailtr_civicrm*.
A MySQL configuration database was created at: *~/.my_civicrm.cnf*

In November 2025 CMRT switched to using the CiviCRM service provided by *civicrm.org*. This web-based application was located at *cmrailtrail.civicrm.org*.

In 2026 a sub-domain of *cmrialtrail.org.au* was created called: *crm.cmrailtrail.org.au*

In this sub-domain was installed CiviCRM Standalone version. It uses the database name of: *cmrailtr_civi*

The CiviCRM for Wordpress had the following extensions installed:
* AuthX
* Civi- Campaign, Case, Contributre, Event, Mail, Member, Pledge, Report,
* CKEditor4
* CiviCRM CKEditor4 Plugin.
* Message Administration
* Rich interface for browsing, editing, previewing, and translating message templates
* Form Core
* Core functionality for rendering and processing dynamic forms
* FlexMailer
* Flexible APIs for email delivery
* SearchKit
* Create searches for a wide variety of CiviCRM entities
* RiverLea CiviCRM Theme Framework
* CiviCRM Theme package with CSS Variable defined variations ('streams').

Note: Not installed. Mosaico. An open-source responsive email template editor


Summary of databases
```
MariaDB [(none)]> show DATABASES;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civi      |  <--- CiviCRM Standalone DB.
| cmrailtr_civicrm   |  <--- Database for CiviCRM plugin to Wordpress - to be removed.
| cmrailtr_czhn1     |  <--- Wordpress DB.
| information_schema |
+--------------------+
```

## Removal of CiviCRM from Wordpress

Perform a backup of the WordPress and CiviCRM databases:
```
mysqldump --defaults-file=/home/cmrailtr/.my_wordpress.cnf --databases cmrailtr_czhn1 > backup_wordpress_2026-06-19_17:20:00.sql
mysqldump --defaults-file=/home/cmrailtr/.my_wordpress.cnf --databases cmrailtr_civicrm > backup_civicrm_2026-06-19_17:20:00.sql
```

Check size of Wordpress website directory tree, html_public:
```
[cmrailtr@s03dd ~]$ du -h --summarize public_html
3.3G    public_html
```
No backup of the website tree as there is not enough disk space free in the VentraIP account.

Check the size of the civicrm directory tree:
```
[cmrailtr@s03dd ~]$ du -h --summarize public_html/wp-content/plugins/civicrm
259M    public_html/wp-content/plugins/civicrm
```

Remove CiviCRM from Wordpress
    * Log into *cmrailtrail.org.au/wp-admin*
    * In dashboard click on *Plugins* / *Installed Pluging*
    * For *CiviCRM* click on *Deactivate*. No change in size of files off /plugins/civicrm/. Dashpanel no longer supports CiviCRM.
    * For *CiviCRM* click on *Delete*. Message: *CiviCRM was successfully deleted.* No longer a *civicrm* directory off public_html/wp-content/plugins/

Remove CiviCRM Database 
```
mysql --defaults-file=/home/cmrailtr/.my_wordpress.cnf --execute='SHOW DATABASES;'+--------------------+
| Database           |
+--------------------+
| cmrailtr_civi      |
| cmrailtr_civicrm   | <--- To be removed
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
```
DROP DATABASE;
```
[cmrailtr@s03dd ~]$ mysql -u cmrailtr_czhn1 -p
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 361476
Server version: 10.6.27-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> SHOW DAATABASES;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'DAATABASES' at line 1
MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civi      |
| cmrailtr_civicrm   |
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
4 rows in set (0.005 sec)

MariaDB [(none)]> DROP DATABASE cmrailtr_civicrm;
Query OK, 179 rows affected (0.526 sec)

MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civi      |
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
3 rows in set (0.004 sec)

MariaDB [(none)]>
```
Remove the configuration file for accessing the MySQL CiviCRM database
```
[cmrailtr@s03dd ~]$ cd ~/
[cmrailtr@s03dd ~]$ rm .my_civicrm.cnf
``` 
Check Website *cmrailtrail.org.au* is OK.    
