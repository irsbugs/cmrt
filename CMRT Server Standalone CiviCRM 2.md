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
