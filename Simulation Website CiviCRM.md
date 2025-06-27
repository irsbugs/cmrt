# Installation of CiviCRM on the Simulation Website

The document [Simulation Website](Simulation%20Website.md) contains information on the preparation and installation of WordPress to simulate the configuration on the *Ventraip - cmrailtrail.org.au* website. This document details the adding of CiviCRM onto this Ubuntu 24.04 based simulation website.




    memory_limit 256M  - line 445
    max_execution_time 240 - l419
    max_input_time 120 - l429
    
    post_max_size 50M l715
    upload_max_filesize 50M l870



ian@hp:~$ scp cmrailtr@192.168.1.101:/etc/php/8.3/apache2/php.ini php.ini
cmrailtr@192.168.1.101's password: 
php.ini                                       100%   72KB 293.4KB/s   00:00    
ian@hp:~$ ls -l php.ini
-rw-r--r-- 1 ian ian 73718 Jun 27 10:57 php.ini
ian@hp:~$ pluma php.ini
ian@hp:~$ 
ian@hp:~$ scp php.ini cmrailtr@192.168.1.101:/etc/php/8.3/apache2/php.ini
cmrailtr@192.168.1.101's password: 
scp: dest open "/etc/php/8.3/apache2/php.ini": Permission denied
scp: failed to upload file php.ini to /etc/php/8.3/apache2/php.ini
ian@hp:~$ sudo scp php.ini cmrailtr@192.168.1.101:/etc/php/8.3/apache2/php.ini
[sudo] password for ian: 
cmrailtr@192.168.1.101's password: 
scp: dest open "/etc/php/8.3/apache2/php.ini": Permission denied
scp: failed to upload file php.ini to /etc/php/8.3/apache2/php.ini
ian@hp:~$ sudo scp php.ini cmrailtr@192.168.1.101:php.ini
cmrailtr@192.168.1.101's password: 
php.ini                                       100%   72KB 706.7KB/s   00:00    
ian@hp:~$ 

    
    
    cmrailtr@CMRT-Demo:~$ ls -l /etc/php/apache2/
ls: cannot access '/etc/php/apache2/': No such file or directory
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


=====
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

MariaDB [(none)]> SELECT CONVERT_TZ("2025-06-03 14:30:00", "Australia/Melbourne", "Pacific/Auckland");
+------------------------------------------------------------------------------+
| CONVERT_TZ("2025-06-03 14:30:00", "Australia/Melbourne", "Pacific/Auckland") |
+------------------------------------------------------------------------------+
| NULL                                                                         |
+------------------------------------------------------------------------------+
1 row in set (0.000 sec)

MariaDB [(none)]> SELECT CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland",
"Australia/Melbourne");
+------------------------------------------------------------------------------+
| CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland", "Australia/Melbourne") |
+------------------------------------------------------------------------------+
| NULL                                                                         |
+------------------------------------------------------------------------------+
1 row in set (0.000 sec)

MariaDB [(none)]> quit
Bye


cmrailtr@CMRT-Demo:~$ sudo mysql_tzinfo_to_sql /usr/share/zoneinfo | sudo mysql -u root mysql
cmrailtr@CMRT-Demo:~$ 

MariaDB [(none)]> SELECT CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland",
    -> "Australia/Melbourne");
+------------------------------------------------------------------------------+
| CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland",
"Australia/Melbourne") |
+------------------------------------------------------------------------------+
| 2025-06-03 12:30:00                                                          |
+------------------------------------------------------------------------------+
1 row in set (0.001 sec)


=====


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

MariaDB [mysql]> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES, TRIGGER, CREATE ROUTINE, ALTER ROUTINE, REFERENCES, CREATE VIEW, SHOW VIEW ON cmrailtr_civicrm.* TO 'cmrailtr_czhn1'@'localhost' IDENTIFIED BY 'W.VDfqMNL4CNg2SasTH40';
Query OK, 0 rows affected (0.011 sec)

MariaDB [mysql]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.001 sec)

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

MariaDB [(none)]> 
MariaDB [(none)]> use cmrailtr_civicrm
Database changed
MariaDB [cmrailtr_civicrm]> show tables;
Empty set (0.000 sec)

MariaDB [cmrailtr_civicrm]> quit
Bye
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
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ cp ~/civicrm-6.2.0-wordpress.zip civicrm-6.2.0-wordpress.zip
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ ls -l
total 46360
drwxr-xr-x 4 cmrailtr cmrailtr     4096 Apr 14 23:37 akismet
-rw-rw-r-- 1 cmrailtr cmrailtr 47456829 Jun 27 12:14 civicrm-6.2.0-wordpress.zip
-rw-r--r-- 1 cmrailtr cmrailtr     2646 Mar  6 00:18 hello.php
-rw-r--r-- 1 cmrailtr cmrailtr       28 Jun  5  2014 index.php

cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ unzip -q civicrm-6.2.0-wordpress.zip
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ 

cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ tree -L 2
.
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

=====

cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ ls -l
total 46364
drwxr-xr-x  4 cmrailtr cmrailtr     4096 Apr 14 23:37 akismet
drwxr-xr-x 10 cmrailtr cmrailtr     4096 May  8 06:37 civicrm
-rw-rw-r--  1 cmrailtr cmrailtr 47456829 Jun 27 12:14 civicrm-6.2.0-wordpress.zip
-rw-r--r--  1 cmrailtr cmrailtr     2646 Mar  6 00:18 hello.php
-rw-r--r--  1 cmrailtr cmrailtr       28 Jun  5  2014 index.php
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ rm civicrm-6.2.0-wordpress.zip 
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ ls
akismet  civicrm  hello.php  index.php
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ 

=====

Switch to Wordpress
192.168.1.101/wp-admin

--> Plugins --> civicrm --> activate

mysql://USER:PASS@HOST/DB

mysql://cmrailtr_czhn1:W---HIDDEN----0@localhost:3306/cmrailtr_civicrm

===

cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ tree civicrm
$ 
2792 directories, 18272 files

===

cmrailtr@CMRT-Demo:~/public_html$ tree -d -L 3
.
├── wp-admin
│   ├── css
│   │   └── colors
│   ├── images
│   ├── includes
│   ├── js
│   │   └── widgets
│   ├── maint
│   ├── network
│   └── user
├── wp-content
│   ├── languages
│   │   ├── plugins
│   │   └── themes
│   ├── plugins
│   │   ├── akismet
│   │   └── civicrm
│   ├── themes
│   │   ├── twentytwentyfive
│   │   ├── twentytwentyfour
│   │   └── twentytwentythree
│   ├── upgrade
│   └── uploads
│       ├── 2025
│       └── civicrm
└── wp-includes
    ├── ID3
    ├── IXR
    ├── PHPMailer
    ├── Requests
    │   ├── library
    │   └── src
    ├── SimplePie
    │   ├── library
    │   └── src
    ├── Text
    │   └── Diff
    ├── assets
    ├── block-bindings
    ├── block-patterns
    ├── block-supports
    ├── blocks
    │   ├── archives
    │   ├── audio
    │   ├── avatar
    │   ├── block
    │   ├── button
    │   ├── buttons
    │   ├── calendar
    │   ├── categories
    │   ├── code
    │   ├── column
    │   ├── columns
    │   ├── comment-author-name
    │   ├── comment-content
    │   ├── comment-date
    │   ├── comment-edit-link
    │   ├── comment-reply-link
    │   ├── comment-template
    │   ├── comments
    │   ├── comments-pagination
    │   ├── comments-pagination-next
    │   ├── comments-pagination-numbers
    │   ├── comments-pagination-previous
    │   ├── comments-title
    │   ├── cover
    │   ├── details
    │   ├── embed
    │   ├── file
    │   ├── footnotes
    │   ├── freeform
    │   ├── gallery
    │   ├── group
    │   ├── heading
    │   ├── home-link
    │   ├── html
    │   ├── image
    │   ├── latest-comments
    │   ├── latest-posts
    │   ├── legacy-widget
    │   ├── list
    │   ├── list-item
    │   ├── loginout
    │   ├── media-text
    │   ├── missing
    │   ├── more
    │   ├── navigation
    │   ├── navigation-link
    │   ├── navigation-submenu
    │   ├── nextpage
    │   ├── page-list
    │   ├── page-list-item
    │   ├── paragraph
    │   ├── pattern
    │   ├── post-author
    │   ├── post-author-biography
    │   ├── post-author-name
    │   ├── post-comments-form
    │   ├── post-content
    │   ├── post-date
    │   ├── post-excerpt
    │   ├── post-featured-image
    │   ├── post-navigation-link
    │   ├── post-template
    │   ├── post-terms
    │   ├── post-title
    │   ├── preformatted
    │   ├── pullquote
    │   ├── query
    │   ├── query-no-results
    │   ├── query-pagination
    │   ├── query-pagination-next
    │   ├── query-pagination-numbers
    │   ├── query-pagination-previous
    │   ├── query-title
    │   ├── query-total
    │   ├── quote
    │   ├── read-more
    │   ├── rss
    │   ├── search
    │   ├── separator
    │   ├── shortcode
    │   ├── site-logo
    │   ├── site-tagline
    │   ├── site-title
    │   ├── social-link
    │   ├── social-links
    │   ├── spacer
    │   ├── table
    │   ├── tag-cloud
    │   ├── template-part
    │   ├── term-description
    │   ├── text-columns
    │   ├── verse
    │   ├── video
    │   └── widget-group
    ├── certificates
    ├── css
    │   └── dist
    ├── customize
    ├── fonts
    ├── html-api
    ├── images
    │   ├── crystal
    │   ├── media
    │   └── smilies
    ├── interactivity-api
    ├── js
    │   ├── codemirror
    │   ├── crop
    │   ├── dist
    │   ├── imgareaselect
    │   ├── jcrop
    │   ├── jquery
    │   ├── mediaelement
    │   ├── plupload
    │   ├── swfupload
    │   ├── thickbox
    │   └── tinymce
    ├── l10n
    ├── php-compat
    ├── pomo
    ├── rest-api
    │   ├── endpoints
    │   ├── fields
    │   └── search
    ├── sitemaps
    │   └── providers
    ├── sodium_compat
    │   ├── lib
    │   ├── namespaced
    │   └── src
    ├── style-engine
    ├── theme-compat
    └── widgets

176 directories
cmrailtr@CMRT-Demo:~/public_html$ 
```

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
