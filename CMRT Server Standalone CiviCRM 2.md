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

## Unzip

```
drwxr-xr-x 2 cmrailtr cmrailtr 4096 May 14 19:13 cgi-bin
-rw-r--r-- 1 cmrailtr cmrailtr 1143 May 14 20:45 error_log
-rw-rw-r-- 1 cmrailtr cmrailtr  146 May 14 20:26 index.html
-rw-rw-r-- 1 cmrailtr cmrailtr  361 May 14 20:52 index.php
drwxr-xr-x 3 cmrailtr cmrailtr 4096 May 14 19:14 .well-known

[cmrailtr@s03dd ~]$ ls -lA civicrm-standalone/
drwxr-xr-x 2 cmrailtr cmrailtr 4096 May 14 19:13 cgi-bin
-rw-r--r-- 1 cmrailtr cmrailtr 1143 May 14 20:45 error_log
drwxr-xr-x 3 cmrailtr cmrailtr 4096 May 14 19:14 .well-known


[cmrailtr@s03dd ~]$ tar -xzf civicrm-6.14.0-standalone.tar.gz #<-- Takes about 30 secs
[cmrailtr@s03dd ~]$

[cmrailtr@s03dd ~]$ ls civicrm-standalone/
cgi-bin  civicrm.standalone.php  core  error_log  ext  index.php  private  public

cgi-bin  civicrm.standalone.php  core  error_log  ext  .htaccess  index.php  private  public  .well-known

[cmrailtr@s03dd civicrm-standalone]$ ls -l
total 36
drwxr-xr-x  2 cmrailtr cmrailtr 4096 May 14 19:13 cgi-bin
-rw-r--r--  1 cmrailtr cmrailtr 1160 May  7 08:21 civicrm.standalone.php
drwxr-xr-x 24 cmrailtr cmrailtr 4096 May  7 08:21 core
-rw-r--r--  1 cmrailtr cmrailtr 1143 May 14 20:45 error_log
drwxr-xr-x  2 cmrailtr cmrailtr 4096 May  7 08:21 ext
-rw-r--r--  1 cmrailtr cmrailtr 1039 May  7 08:21 index.php
drwxr-xr-x  2 cmrailtr cmrailtr 4096 May  7 08:21 private
drwxr-xr-x  2 cmrailtr cmrailtr 4096 May  7 08:21 public

```
Note that dir's core, ext private, public are all chmod 755. - Should have access for thge webserver


## Switch to browser

Should use index.php.

Server: 127.0.0.1:3306

Username: civicrm_admin
Pdw: redfred4

Whats this?... Error messaggews when no database defined...
We are not able to install the software. Please review the errors and warnings below.
Severity 	Section 	Name 	Details
Error 	Database 	CiviCRM InnoDB support 	Could not determine if MySQL has InnoDB support. Assuming none.
Error 	Database 	CiviCRM MySQL AutoIncrementIncrement 	Could not connect to database
Error 	Database 	CiviCRM MySQL Lock Tables 	Could not connect to database
Error 	Database 	CiviCRM MySQL Temp Tables 	Could not connect to database
Error 	Database 	CiviCRM MySQL Trigger 	Could not connect to database
Error 	Database 	CiviCRM MySQL connection 	Access denied for user ''@'localhost' (using password: NO)
Error 	Database 	CiviCRM MySQL utf8mb4 Support 	Could not connect to database
Error 	Database 	CiviCRM Mysql thread stack 	Could not connect to database
Warning 	Database 	CiviCRM MySQL Version 	Cannot determine the version of MySQL installed. Please ensure at least version 5.7 is installed.
Warning 	Database 	db.password 	The property "db.password" is blank. This may be correct in some controlled environments; it could also be a mistake or a symptom of an insecure configuration.


====

Defin...

## Database
Server: 127.0.0.1:3306
Database: cmrailtr_civi
Username: cmrailtr_czhn1
Password: W-19-0

## Administrative Account
Administrative User: civicrm_admin
Administrative: r-6-4
Administrative: stwrtn@gmail.com

Note: Only added the default 5 extensions. The other 3 can be added via Administrator --> System Settings --> Extensions

CiviCRM Settings File 	/home/cmrailtr/civicrm-standalone/private/civicrm.settings.php
CiviCRM Source Code 	/home/cmrailtr/civicrm-standalone/core

```
[cmrailtr@s03dd civicrm-standalone]$  mysql --defaults-file=/home/cmrailtr/.my_civi.cnf
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 881084
Server version: 10.6.19-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [cmrailtr_civi]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civi      |
| cmrailtr_civicrm   |
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
4 rows in set (0.006 sec)

MariaDB [cmrailtr_civi]> SHOW TABLES;
+------------------------------------------+
| Tables_in_cmrailtr_civi                  |
+------------------------------------------+
| civicrm_acl                              |
| civicrm_acl_cache                        |
| civicrm_acl_contact_cache                |
| civicrm_acl_entity_role                  |

...snip...

| civicrm_user_job                         |
| civicrm_user_role                        |
| civicrm_website                          |
| civicrm_word_replacement                 |
| civicrm_worldregion                      |
+------------------------------------------+
162 rows in set (0.001 sec)
```

## Files in Core

Most of the CiviCRM-Standalone distribution files untar into the *core* directory. This core directory has over 2900 subdirectories and contains a total of over 18300 files.
Based on the file extensions these are the extension who have totals greater than 100:
```
* .php  8972
* .js   4106
* .svg  2070
* .tpl  1251
* .md   1060
* .png  1018
* .html  573
* .css   522
* .json  354
* .txt   259
* .xml   218
* .scss  148
* .gif   124
* .hlp   113
```

## Mosiaico

This provides drag and drop construction of mails. This was installed via:

Administrator --> System Settings --> Extensions --> *Add New*


## C-Panel SSH

Deleted previous public and Private key

 SSH Access
Generating a Public Key

RSA vs DSA: RSA and DSA are encryption algorithms used to encrypt your key. DSA is faster for Key Generation and Signing and RSA is faster for Verification.

Key Name (This value defaults to “id_rsa”.):
Key Password: Sg(D3+lH0Bp=B]   <-- Same as cmrailtr account password

Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/cmrailtr/.ssh/id_rsa.
Your public key has been saved in /home/cmrailtr/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:NLbEOsfpBqmm9RenNmS4JqDlZEzrpILNyPPuGPctnTw 
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|       .         |
|        *        |
|  .    B +       |
| o .  =.S        |
|  O  ..=+ .      |
|o# o+ o+++       |
|*oO+oo+E=        |
|..*+ +o+..       |
+----[SHA256]-----+

-rw-r--r-- 1 cmrailtr cmrailtr    1 May 17 08:13 authorized_keys
-rw------- 1 cmrailtr cmrailtr 1766 May 17 08:22 id_rsa
-rw-r--r-- 1 cmrailtr cmrailtr  382 May 17 08:22 id_rsa.pub

[cmrailtr@s03dd .ssh]$ cat id_rsa
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,E675FBC3A0E619BB6023D42FD696AD12

gpqTfuBrBPPEf3kVmEili0u2icfZzzRwyYwjI8gmLJZttUDCNWyuXdX/XWx0mZXL
A/1Q6ZipxPqoE1eDQvZbsSHsoyfo3PcKqD8xoCXvKCt7HKzdbrynQgRNX4j3kecX
LaKmTbyoyFSiaOs/LwzXZKS+xyX7l1aHr123qEd52civvcQ1XPp5yIH69XMZCINk
jY2UwT9f3CkVPjNaoCa7bJTNwDXY7uotwjkiBxDs3Wzp9yXrgtzhjaO9E5eDMiG7
5funrxFceImDMHuQMtHsbxtJ+5+qvhPuWldfYKbHXiHzQF2T0WfYVkD+GcTkt+NV
+fPHPgIYLtX/JwVgtr6bpoXTOVRorRUENUPnMohrAJEUgxyBUxe8QiZcOLWTdCek
6fwXbMrfwchWBTYd9muKUeKqpHhX3pRGN3CNop1ddPa3iU927wTRzZEaEpVLAIuy
eYcC937os6oF7wToWreq/vG5TdOt4kuYVp4FluXYigoyd2KSElmugAagbCrXkIdX
pG7q+GfwiosGDaMWH181ZwZkM5uTNHxhaJsACOkxY7TGh0SsC9kUu4rlXVqMiL0R
QzIz2cbzRC+QgttbV9ecnDwQIWJJJgzKEKUVCZqRsIGQd/Wx1rX/aOZwsXntINOr
MOE2m7MsyiaeabOJH+ujZ1knH+MIdC5ime6P6SIdgUxS/gQ5brx8wwh4BNhpId1X
m+izrP5/0RVDe+/B9F0d5QGXUIxwpjlRpM7dRr+/OFCk1xXV34jqLZE/gHTviQ6t
hTHonr8qBoUSBvpIg1skzwuT3Ef4zsdeU2y7DrlLS3udEpzcthDCns/OuA4q4bs9
c5CGVgM8Kbt5JSK23yM2EvRWaUdP/u/ynz6ghhcwhp8rOZ2ceoCVdfYrtn/QUNk/
GUluBHn62r654XtzS3DGnWiaqlyb3rZbu6mkxMjARnIq80OjK/cbzC6IMH3wf9ft
h6TWpj2/7H8hT+reoEAq80bUI2HRVpL0R0s8dsjsYTOlpodoudNmommLi6BULB9F
o2H3Rm4TOERr5a4Wx6HlZ4OGWjZJqlxKeH63nH4sRRaKz/cjwpOxh+55JbjQ200K
TFYJ0iqfRmwAfYRaf/PtPV8aLr48hZCUSUDycQtE/Ph/561xINktcxShCflePx1U
Jo3lVRmu6t/BdZ2FitaGcULpygrugMKk+PtqQx9YvNqW1zM6BLoPacvSOlyzzowB
5Sy6LDzQgSJW+hFccnC2C0WaKFim48RLpFELLuv+xtdf3yn9EnpLClPtMhb05LPy
1soZZt+DquTECSQv5wOwenQ+GaHNkOqyy1SE3Y6dBAZhY1PRuEra3l+68Eub3afm
8rFeaNk9pMjDoQCpTrnPLUkfuoG+cCOFec8Xp394DRS95Qo9NvRlD6bSlqaF4KmW
/oo5CacMiN5EkfZ38kUpBwLC1VcgpMQCuV0ED8mhTi4b6XYEuGbRofct3QN0Ur5G
hL7HuPUdoCVCPw0tyjkSioDksgwIKjecyEdZIJMs9pAedMftCq/4YwT/3P+m2tSA
3k66iuDkSt3W8i/aJ/r497NuOY7E/iyz9ivkmMEb1Prd/UC9xNaGq8so2xToPq8o
-----END RSA PRIVATE KEY-----


[cmrailtr@s03dd .ssh]$ cat id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDK0uqNzckGl2NPDP1muiXJRpDa0Qrnawd74rGzdVBjUEuQjHXeJ6Bunua7dB2vaJRe2fOEo8QrrzuOcsojeMX3+/GzF+claUfj8xJ93SEuhBL3DCBCpBdqq/1sUZYXzZaeeWoIhElnq6tH9h6pvVfPhDyEotHd8ypkqzKITlop/Cr3pR8fZ7iOQG5qJmMIbPk1znWSJILLV3kjQptARuT6ALSRvF+YK8jO4gsLBjSeAiZgEAxXH8yas+t0J/QetkYKtah+nw+c/50QUhyJcgAK6sIRBPBV6OXupA/LXMO5iwmkrc2YpMWxAMnkV/0cfVN72UbHojTsTQJjKrGcgyJj
[cmrailtr@s03dd .ssh]$


cmrailtr@s03dd

[cmrailtr@s03dd .ssh]$ ping s03dd
PING s03dd.syd6.hostingplatform.net.au (110.232.143.15) 56(84) bytes of data.
64 bytes from s03dd.syd6.hostingplatform.net.au (110.232.143.15): icmp_seq=1 ttl=64 time=0.065 ms

ian@hp:~$ ssh cmrailtr@s03dd.syd6.hostingplatform.net.au
ssh: connect to host s03dd.syd6.hostingplatform.net.au port 22: Network is unreachable

ian@hp:~$ ssh cmrailtr@cmrailtrail.org.au

## Ian PC setting up CiviCRM Standalone 
```

(nikola-2025-env) ian@hp:/etc/apache2/sites-available$ cat nano civicrm.conf
cat: nano: No such file or directory
<VirtualHost *:80>
    # CiviCRM Standalone Configuration.
    # civicrm.conf - Ian Stewart 2026-05-12. 
    # Resides in: /etc/apache2/sites-available/ 
    # Uses path: /home/ian/civicrm-standalone as civicrm-standalone is top level of .tar.gz distribution
    #ServerName crm.cmrailtrail.local.pc
    Servername civi.local.pc
    # CiviCRM Standalone uses a modern directory structure where only the public is exposed to the web.
    DocumentRoot /home/ian/civicrm-standalone

    <Directory /home/ian/civicrm-standalone>
        Options -Indexes +FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    # Ensure Authorization headers are passed to PHP (needed for CiviCRM API)
    SetEnvIf Authorization "(.*)" HTTP_AUTHORIZATION=$1

    ErrorLog ${APACHE_LOG_DIR}/crm_error.log
    CustomLog ${APACHE_LOG_DIR}/crm_access.log combined
</VirtualHost>
(nikola-2025-env) ian@hp:/etc/apache2/sites-available$ 


===
(nikola-2025-env) ian@hp:/etc/apache2$ cat envvars
# envvars - default environment variables for apache2ctl

# this won't be correct after changing uid
unset HOME

# for supporting multiple apache2 instances
if [ "${APACHE_CONFDIR##/etc/apache2-}" != "${APACHE_CONFDIR}" ] ; then
	SUFFIX="-${APACHE_CONFDIR##/etc/apache2-}"
else
	SUFFIX=
fi

# Since there is no sane way to get the parsed apache2 config in scripts, some
# settings are defined via environment variables and then used in apache2ctl,
# /etc/init.d/apache2, /etc/logrotate.d/apache2, etc.
export APACHE_RUN_USER=www-data
export APACHE_RUN_GROUP=www-data

====

ian@hp:/etc$ cat hosts
127.0.0.1	localhost
127.0.1.1	hp

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

# Add domain name resolver for civi. CiviCRM Standalone Ian 2026-06-04
127.0.0.1 civi.local.pc


=====



(nikola-2025-env) ian@hp:/etc$ sudo a2enmod rewrite
Module rewrite already enabled

(nikola-2025-env) ian@hp:/etc$ sudo systemctl restart apache2



ian@hp:~$ sudo mysql -u root -p 
[sudo] password for ian: 
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 42
Server version: 10.11.14-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| civicrm            |
| ian_test_1         |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| wordpress          |
+--------------------+
7 rows in set (0.004 sec)

MariaDB [(none)]> Use mysql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [mysql]> Use mysql
Database changed
MariaDB [mysql]> CREATE DATABASE civi;
Query OK, 1 row affected (0.001 sec)
MariaDB [mysql]> 
MariaDB [mysql]> CREATE USER cmrailtr_czhn1@localhost IDENTIFIED BY 'W.---HIDDEN---40';
MariaDB [mysql]> 
MariaDB [mysql]> CREATE USER ian@localhost IDENTIFIED BY 'ian';
ERROR 1396 (HY000): Operation CREATE USER failed for 'ian'@'localhost'
MariaDB [mysql]> history
    -> ;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near 'history' at line 1
MariaDB [mysql]> CREATE USER ian@localhost IDENTIFIED BY 'ian';
ERROR 1396 (HY000): Operation CREATE USER failed for 'ian'@'localhost'
MariaDB [mysql]> CREATE USER civi@localhost IDENTIFIED BY 'ian';
Query OK, 0 rows affected (0.008 sec)


 I thinnk Ian already exists
MariaDB [mysql]> CREATE USER ian@localhost IDENTIFIED BY 'ian';
ERROR 1396 (HY000): Operation CREATE USER failed for 'ian'@'localhost'
MariaDB [mysql]> CREATE USER civi@localhost IDENTIFIED BY 'ian';
Query OK, 0 rows affected (0.008 sec)





MariaDB [mysql]> GRANT ALL ON ian.* TO civi@localhost
    -> ;
Query OK, 0 rows affected (0.005 sec)



MariaDB [(none)]> CREATE USER 'ian'@'localhost' IDENTIFIED BY 'ian';
ERROR 1396 (HY000): Operation CREATE USER failed for 'ian'@'localhost'
MariaDB [(none)]> CREATE USER 'fred'@'localhost' IDENTIFIED BY 'fred';
Query OK, 0 rows affected (0.002 sec)

MariaDB [(none)]> GRANT ALL on civi.* to 'fred'@'localhost';
Query OK, 0 rows affected (0.003 sec)



ian@hp:~$ nano .my_civi.cnf

ian@hp:~$ cat .my_civi.cnf
# ~/.my_civi.cnf
# mysql configuration file for Civicrm Standalone.
# 2026-06-04
# Ian
# Resides in: ~/.my_civi.cnf 
# Based on content of: Setup prior to installation of civicrm
# $ mysql --defaults-file=/home/ian/.my_civi.cnf  --execute='show databases; show tables;'
#
[client]
host=localhost
user=fred
#user=wordpress
password=fred

[mysql]
database=civi # For CiviCRM standalone


ian@hp:~$ mysql --defaults-file=/home/ian/.my_civi.cnf
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 48
Server version: 10.11.14-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.



MariaDB [civi]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| civi               |
| information_schema |
+--------------------+
2 rows in set (0.000 sec)


CiviCRM Browser install

127.0.0.1:3306
civi
fred
fred


Administrative User: admin  <---user account is: admin  Creates Individual Contact: Standalone Admin
Administrative Password: fred
Administrative Email: stwrtn@gmail.com

Creates Individual Contact: Standalone Admin
and Default Organization

CiviCRM Settings File 	/home/ian/civicrm-standalone/private/civicrm.settings.php
CiviCRM Source Code 	/home/ian/civicrm-standalone/core


Browser: http://civi.local.pc/civicrm/home = 127.0.0.1



```

