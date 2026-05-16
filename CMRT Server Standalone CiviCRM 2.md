# Server for Wordpress and Standalone CiviCRM 2

Continuation. From Database requirements

2026-05-13
Ian


## MySql / MariaDB

### Interactive connection
```
$ mysql -u cmrailtr_czhn1 -p
Enter password: W-19-0
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 799223
Server version: 10.6.19-MariaDB MariaDB Server

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
```
It is a litte confusing as the Wordpress database name of *cmrailtr_czhn1* is also same as its username of *cmrailtr_czhn1*.
For CiviCRM Standalone the database name of *cmrailtr_civi* with the username of *cmrailtr_czhn1*. 
For both the passwortc is the same: W-19-0

### Using configuration files for command line access to databases.
```
 mysql --defaults-file=/home/cmrailtr/.my_civicrm.cnf --execute='SHOW DATABASES;'
 mysql --defaults-file=/home/cmrailtr/.my_wordpress.cnf --silent --disable-column-names --execute='SHOW DATABASES; SHOW TABLES;'
```

### Interactive using configuration files:
```
mysql --defaults-file=/home/cmrailtr/.my_wordpress.cnf
```

### Prefixes to tables:
* Wordpress: bsen
* CiviCRM: civicrm

Make new data with prefix of *civi

### WordPress. Using bsen_users table
```
MariaDB [cmrailtr_czhn1]> SELECT ID, user_login, user_nicename, user_email FROM bsen_users;
+----+--------------------+--------------------+----------------------------------+
| ID | user_login         | user_nicename      | user_email                       |
+----+--------------------+--------------------+----------------------------------+
|  1 | CMRT_Admin         | admin              | admin@cmrailtrail.org.au         |
|  8 | Janice             | janice             | janice@cmrailtrail.org.au        |
| 14 | CMRT_Committee     | cmrt_committee     | committee@cmrailtrail.org.au     |
| 15 | CMRT_President     | cmrt_president     | president@cmrailtrail.org.au     |
| 16 | CMRT_Secretary     | cmrt_secretary     | secretary@cmrailtrail.org.au     |
| 17 | CMRT_Treasurer     | cmrt_treasurer     | treasurer@cmrailtrail.org.au     |
| 18 | CMRT_Vicepresident | cmrt_vicepresident | vicepresident@cmrailtrail.org.au |
+----+--------------------+--------------------+----------------------------------+
```

### Check timezone working OK
```
MariaDB [cmrailtr_czhn1]> SELECT NOW();
+---------------------+
| NOW()               |
+---------------------+
| 2026-05-16 17:42:46 |
+---------------------+
1 row in set (0.000 sec)

MariaDB [cmrailtr_czhn1]> SELECT CONVERT_TZ("2001-02-03 04:05:00", "GMT", "America/New_York");
+--------------------------------------------------------------+
| CONVERT_TZ("2001-02-03 04:05:00", "GMT", "America/New_York") |
+--------------------------------------------------------------+
| 2001-02-02 23:05:00                                          |
+--------------------------------------------------------------+
1 row in set (0.001 sec)
```
### Grants

| Grants for cmrailtr_czhn1@localhost                                                                                             |

| GRANT USAGE ON *.* TO `cmrailtr_czhn1`@`localhost` IDENTIFIED BY PASSWORD '*A8FBC9C940B24F8F25A5A4E8AEC9C458C19B8385'                                                                                             |

| GRANT ALL PRIVILEGES 
ON `cmrailtr\_czhn1`.* TO `cmrailtr_czhn1`@`localhost`

| GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, REFERENCES, INDEX, ALTER, 
CREATE TEMPORARY TABLES, LOCK TABLES, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, 
ALTER ROUTINE, TRIGGER 
ON `cmrailtr\_civicrm`.* TO `cmrailtr_czhn1`@`localhost` 

| GRANT EXECUTE, ALTER ROUTINE 
ON FUNCTION `cmrailtr_civicrm`.`civicrm_strip_non_numeric` TO `cmrailtr_czhn1`@`localhost`

### CiviCRM Installation guide recommendation
```
GRANT
  SELECT,
  INSERT,
  UPDATE,
  DELETE,
  CREATE,
  DROP,
  INDEX,
  ALTER,
  CREATE TEMPORARY TABLES,
  LOCK TABLES,
  TRIGGER,
  CREATE ROUTINE,
  ALTER ROUTINE,
  REFERENCES,
  CREATE VIEW,
  SHOW VIEW
ON civicrm.*
TO 'civicrm_user'@'localhost'
IDENTIFIED BY 'realpasswordhere';
```

converted to

```
GRANT
  SELECT,
  INSERT,
  UPDATE,
  DELETE,
  CREATE,
  DROP,
  INDEX,
  ALTER,
  CREATE TEMPORARY TABLES,
  LOCK TABLES,
  TRIGGER,
  CREATE ROUTINE,
  ALTER ROUTINE,
  REFERENCES,
  CREATE VIEW,
  SHOW VIEW
ON cmrailtr_civi.*
TO 'cmrailtr_czhn1'@'localhost'
IDENTIFIED BY 'W.VDfqMNL4CNg2SasTH40';
```

The Installation guide on the CIviCRM Standalone page 

Recommended:
```
Now, you can configure a database (civicrm), user (civicrm), and password (__TOP_SECRET__):

mysql> CREATE DATABASE civicrm CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

mysql> CREATE USER 'civicrm'@'localhost' IDENTIFIED BY '__TOP_SECRET__';

mysql> GRANT ALL on civicrm.* to 'civicrm'@'localhost';
```

Actual entries
```
Now, you can configure a database (cmrailtr_civi), user (cmrailtr_czhn1), and password (W-19-0):

mysql> CREATE DATABASE cmrailtr_civi CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

mysql> CREATE USER 'cmrailtr_czhn1'@'localhost' IDENTIFIED BY 'W-19-0';

mysql> GRANT ALL on cmrailtr_civi.* to 'cmrailtr_czhn1'@'localhost';

```

```
[cmrailtr@s03dd ~]$ mysql -u cmrailtr_czhn1 -p
Enter password:
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 842085
Server version: 10.6.19-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>

MariaDB [(none)]> CREATE DATABASE cmrailtr_civi CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

====





ERROR 1044 (42000): Access denied for user 'cmrailtr_czhn1'@'localhost' to database 'cmrailtr_civi'
MariaDB [(none)]>

```
Uable to log in. Dont' know root password to create another database.
Need to keep using current database
```
[cmrailtr@s03dd ~]$ mysql -u root -p
Enter password:
ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)

```

## Used C-Panel: Mysql Databases

* Created the database *cmrailtr_civi*
* Add User *cmrailtr_czhn1* to database *cmrailtr_civi*
* User cmrailtr_czhn1 granted ALL PRIVELEGES to *cmrailtr_civi*

Using the recomendation in CiviCRM Standalone document, then All PRIV compared to select PRIV will be missing EVENT and EXECUTE

* ALTER
* ALTER ROUTINE
* CREATE
* CREATE ROUTINE
* CREATE TEMPORARY TABLES
* CREATE VIEW
* DELETE
* DROP
EVENT
EXECUTE
* INDEX
* INSERT
* LOCK TABLES
* REFERENCES
* SELECT
* SHOW VIEW
* TRIGGER
* UPDATE 

Opted for ALL PRIVILEGES

```
MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civi      | <-- CiviCRM Standalone
| cmrailtr_civicrm   | <-- CiviCRM plugin
| cmrailtr_czhn1     | <-- WordPress
| information_schema |
+--------------------+

MariaDB [(none)]> use cmrailtr_civi
Database changed
MariaDB [cmrailtr_civi]> SHOW TABLES;
Empty set (0.000 sec)
```

-rw-------  1 cmrailtr cmrailtr   617 Apr  9 10:03 .my_civicrm.cnf
-rw-------  1 cmrailtr cmrailtr  4133 May 16 19:52 .mysql_history
-rw-------  1 cmrailtr cmrailtr   627 Apr  9 09:43 .my_wordpress.cnf


-rw-------  1 cmrailtr cmrailtr   617 May 16 19:54 .my_civi.cnf
-rw-------  1 cmrailtr cmrailtr   617 Apr  9 10:03 .my_civicrm.cnf
-rw-------  1 cmrailtr cmrailtr  4133 May 16 19:52 .mysql_history
-rw-------  1 cmrailtr cmrailtr   627 Apr  9 09:43 .my_wordpress.cnf

### Created a .my_civi.cnf file.

Able to execute commands on cmrailtr_civi database from the command line...

[cmrailtr@s03dd ~]$ mysql --defaults-file=/home/cmrailtr/.my_civi.cnf --execute='SHOW DATABASES;'
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civi      |
| cmrailtr_civicrm   |
| cmrailtr_czhn1     |
| information_schema |
+--------------------+

## Step 6. Configure your webserver¶

Now you need to configure your webserver to point to your CiviCRM Standalone project folder.

The exact steps vary based on your specific environment. Here are some typical tasks for common environments:
Web hosting: Point a new subdomain to your Standalone project folder

This has been done by VentraIP staff.

## Step 7. Configure webserver permissions¶

Your webserver will need to be able to write to at least your public and private directories. If you wish to install extensions through the web UI on your site, the webserver will also need to write to the ext directory.

On many webhosts the webserver will be able to write to all directories, and you won't need to do anything.

If you have ssh access to your server, you may need to set the user permissions directly.
Permissions: Grant write access to public, private and ext directories on Linux server

This should have been done by ther VentraIP folks


## Step 8. Run the installer¶

The installer verifies requirements, prepares the database, and initializes the configuration file. You may run the installer through the web interface (which is simpler) or the command-line interface (which has more options).
Run installer via web UI

## Next steps...

Log in and review users and permissions¶

You should now be able to log in to your site at e.g. https://your-site.test/civicrm/login. Use the administrator username and password you created during install.

Head to Adminster >> Users and Permissions to configure users and roles for your site.
Review the checklist¶

The Configuration Checklist provides a convenient way to work through the settings that need to be reviewed and configured for a new site. You can link to this checklist from the installation success page AND you can visit it at any time from Administer » Administration Console » Configuration Checklist.
Test-drive CiviCRM¶

Start exploring your new CiviCRM Standalone site. Please report any issues you find in the Issue Tracker

## Download CiviCREM Standalone

```
[cmrailtr@s03dd ~]$ wget https://download.civicrm.org/civicrm-6.14.0-standalone.tar.gz
--2026-05-16 20:15:53--  https://download.civicrm.org/civicrm-6.14.0-standalone.tar.gz
Resolving download.civicrm.org (download.civicrm.org)... 2001:41d0:725:7100:100::, 51.77.81.200
Connecting to download.civicrm.org (download.civicrm.org)|2001:41d0:725:7100:100::|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://storage.googleapis.com/civicrm/civicrm-stable/6.14.0/civicrm-6.14.0-standalone.tar.gz [following]
--2026-05-16 20:15:55--  https://storage.googleapis.com/civicrm/civicrm-stable/6.14.0/civicrm-6.14.0-standalone.tar.gz
Resolving storage.googleapis.com (storage.googleapis.com)... 2404:6800:4006:804::201b, 2404:6800:4006:801::201b, 2404:6800:4006:805::201b, ...
Connecting to storage.googleapis.com (storage.googleapis.com)|2404:6800:4006:804::201b|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 36465377 (35M) [application/x-tar]
Saving to: ‘civicrm-6.14.0-standalone.tar.gz’

100%[=======================================================================================================>] 36,465,377  8.04MB/s   in 5.1s

2026-05-16 20:16:00 (6.88 MB/s) - ‘civicrm-6.14.0-standalone.tar.gz’ saved [36465377/36465377]

[cmrailtr@s03dd ~]$
[cmrailtr@s03dd ~]$ ls -l civicrm-6.14.0-standalone.tar.gz
-rw-rw-r-- 1 cmrailtr cmrailtr 36465377 May  7 08:24 civicrm-6.14.0-standalone.tar.gz

```

TODO: SSH?
