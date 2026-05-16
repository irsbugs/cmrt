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
