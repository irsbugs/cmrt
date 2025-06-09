# CiviCRM Installation

CiviCRM, a Customer (or Constituent) Relationship Management (CRM) application was installed as a plugin to the WordPress Content Management System (CMS).

Installation Commenced: 2025-06-03

Installation by: Ian and Ken Stewart

This document is a record of the installation activities.

## Introduction

[Ventraip](https://ventraip.com.au/) is the Australian based company that provides the web-hosting and domain name services for the CMRT website: https://cmrailtrail.org.au

Ventraip run their hosting servers using [CloudLinux OS](https://cloudlinux.com/). 
The current version of Linux is: **3.10.0-962.3.2.lve1.5.81.el7.x86_64**. 
The CloudLinux version is (from `$ cat /etc/os-release`: **7.9** which was released in 2020.

As of June 2025, the latest CloudLinux is 9.6 which was released in May 2025.

Ventraip apparently use [*LiteSpeed Web Server*](https://www.litespeedtech.com/) (LSWS) as the web server as their [LiteSpeed Cache for WordPress](https://www.litespeedtech.com/products/cache-plugins/wordpress-acceleration) (LSCWP), currently at V7.1, has been installed as a plugin to WordPress. 

Logging into the CMRT account on a Ventraip server is via a web-based login panel at: https://vip.ventraip.com.au/login

Login requires two part authentication.

Upon logging in *C-Panel* may be activated. This gains access to many applications including management of PHP, Databases, Mail, etc. C-Panel also includes a *Terminal* application that allows bash comands to be executed.

The user account provided by Ventraip is **cmrailtr**. Files created in this account have the owner and group name: **cmrailtr**.
Files normally have the permission of: **644**, and directories a permision of: **755**.

[WordPress](https://wordpress.com/) has been installed as the Content Management System (CMS). The term *CMS* is sometimes refered to by CiviCRM as the *User Framework*.

It is not known who initially installed WordPress on the website, and any of the rational that was used in namings that were applied.

Assignment of Names.
* Account Name: **cmrailtr**
* WordPress top level directory. Default is *wordpress*: **public_html**
* WordPress Maria database name. default is *wordpress*: **cmrailtr_czhn1**
* WordPress MariaDB database User name: **cmrailtr_czhn1**
* WordPress tables prefix. Default is *wp_*: **bsen_**
* CiviCRM MariaDB database name. Default is *civicrm*: **cmrailtr_civicrm**
* CiviCRM tables prefix: **civicrm_** 

The linux path to WordPress is: `/home/cmrailtr/public_html`
The files and directories in the top-level WordPress directory are:
```
/home
└── cmrailtr
    └── public_html
        ├── index.php
        ├── license.txt
        ├── readme.html
        ├── wp-activate.php
        ├── wp-admin       <--- Directory
        ├── wp-blog-header.php
        ├── wp-comments-post.php
        ├── wp-config.php
        ├── wp-config-sample.php
        ├── wp-content     <--- Directory
        ├── wp-cron.php
        ├── wp-includes    <--- Directory
        ├── wp-links-opml.php
        ├── wp-load.php
        ├── wp-login.php
        ├── wp-mail.php
        ├── wp-settings.php
        ├── wp-signup.php
        ├── wp-trackback.php
        └── xmlrpc.php
```
CiviCRM is installed off the `plugins` directory:
```
/home
└── cmrailtr
    └── public_html
        ├── wp-content
        │   ├── plugins     <--- Staging directory for latest civicrm.zip distribution file.
        │   │   ├── civicrm <--- Top level directory of CiviCRM
        │   │   │   ├── assets
        │   │   │   ├── civicrm
        │   │   │   ├── includes
        │   │   │   ├── languages
        │   │   │   ├── tests
        │   │   │   ├── wp-cli
        │   │   │   └── wp-rest
        ...snip...
```

## CiviCRM Installation for WordPress - Preparation

Before commencing the CiviCRM installaton the current WordPress installation should be checked. Adjustments may need to be made to WordPress for the civiCRM installation to be performaed correctly.

Refer to these documents:

* [WordPress - Advanced Administration Handbook](https://developer.wordpress.org/advanced-administration/)
* [WordPress Hosting Team Handbook](https://make.wordpress.org/hosting/handbook/)
* [CiviCRM Installation Requirements](https://docs.civicrm.org/installation/en/latest/requirements/) 
* [CiviCRM Installation Guide](https://docs.civicrm.org/installation/en/latest/)
* [CiviCRM Installtion on WordPress](https://docs.civicrm.org/installation/en/latest/wordpress/)


## Checks of WordPress:

* Check that WordPress is up-to-date and no upgrades are pending.

## Check the PHP revision.
* In Wikipedia the [PHP](https://en.wikipedia.org/wiki/PHP) topic has a table of the PHP release revisions.
* CMRT were running PHP V7.4 which stopped being supported in November 2022.
* CMRT was upgraded to PHP V8.3 which is supported through until the end of 2027.
* The PHP version upgrade is performed in the *C-Panel - Software Section* using the application *php - Select PHP Version*. In this *PHP Selector* applicaton the *Current PHP Version* drop-down menu allows selection of the latest supported version of PHP, which was V8.3.

## [Check PHP Extensions](https://make.wordpress.org/hosting/handbook/server-environment/#php-extensions)

* The *C-Panel PHP Selector* application allows selecting or deselecting the PHP Extensions installed. For V8.3 there are 132 extensions.
* The *WordPress Handbook* provides a section on [PHP Extensions](https://make.wordpress.org/hosting/handbook/server-environment/#php-extensions). The PHP extensions are in six catagories:
  
    * Required - 2 - json, mysqli or mysqlnd
    * Highly recommended - 13 - curl, dom, exif, fileinfo, hash, igbinary, imagick, intl, mbstring, openssl, pcre, xml, zip.
    * Recommended - 4 - apcu, memcached, opcache, redis.
    * Optional - 1 - timezonedb.
    * Remaining PHP modules WordPress may use - 9 - bcmath, filter, image, iconv, shmop, simplexml, sodium, xmlreader, zlib.
    * Extensions used for file changes - 3 - ssh2, ftp, sockets.
 
* For CMRT all 32 PHP Extensions listed above from the Handbook's six catagories were applied. Some Extensions that had been applied for some other reason reason, were left applied.
  
* The [CiviCRM Installation Guide](https://docs.civicrm.org/installation/en/latest/requirements/#required-for-civicrm-core) lists the following PHP Extensions as required: bcmath, curl, dom, fileinfo, intl, mbstring, zip. All of these extension have already been installed as requirments of WordPress. One additional extension is required for the CiviSMTP service. This extension is: soap.

#[PHP Configuration](https://docs.civicrm.org/installation/en/latest/requirements/#php-configuration)

The following PHP directives are the recommended minimums. Typically Operating Systems would define these changes to the directives in the file `/etc/php/8.3/apache2/php.ini` with the following commands:
```
    memory_limit 256M
    max_execution_time 240
    max_input_time 120
    post_max_size 50M
    upload_max_filesize 50M
```
In CloudLinux the file that sets the PHP directive is `/etc/cl.selector.conf.d/php.conf`:
A selection of directives from this php.conf:
```
Directive = max_execution_time
Default   = 300
Type      = value
Comment   = The maximum time in seconds a script is allowed to run before it is terminated.

Directive = max_input_time
Default   = 120
Type      = value
Comment   = The maximum time in seconds a script is allowed to parse input data.

Directive = memory_limit
Default   = 256M
Type      = list
Range     = 64M,128M,192M,256M,368M,512M,756M,1G,1.5G,2G
Comment   = The maximum amount of memory in bytes a script is allowed to allocate. Set the value to -1 to have no memory limit (notrecommended). Use shortcuts for byte values: K (kilo), M (mega), and G (giga). For example, 128M

Directive = post_max_size
Default   = 128M
Type      = list
Range     = 2M,4M,8M,16M,32M,64M,128M,192M,256M,368M,512M
Comment   = The maximum size in bytes of data that can be posted with the POST method. Typically, should be larger than upload_max_filesize and smaller than memory_limit. Use shortcuts for byte values: K (kilo), M (mega), and G (giga). For example, 16M.

Directive = upload_max_filesize
Default   = 128M
Type      = list
Range     = 2M,4M,8M,16M,32M,64M,128M,256M,512M,756M,1G
Comment   = The maximum size in bytes of an uploaded file. Use shortcuts for byte values: K (kilo), M (mega), and G (giga). For example, 128M.
```
The PHP directives were at, or above, the recommended settings in the [CiviCRM Installation Guide](https://docs.civicrm.org/installation/en/latest/requirements/#php-configuration). Note that *root* access would be required to edit this file: 
```
[cmrailtr@s03dd ~]$ ls /etc/cl.selector.conf.d/php.conf -l
-rw-r--r-- 1 root root 12071 Apr 14  2022 /etc/cl.selector.conf.d/php.conf
```

## System Packages

The WordPress Hosting Handbook has a section on [System Packages](https://make.wordpress.org/hosting/handbook/server-environment/#system-packages) that WordPress requires. These are: curl, Ghost Script, ImageMagick, OpenSSL, WebP AVIF.

On the CMRT C-Panel Terminal these are checks made for these System Packages:

curl: Recommend >= 8.4
```
[cmrailtr@s03dd ~]$ curl -V
curl 7.29.0 (x86_64-redhat-linux-gnu) libcurl/7.29.0 NSS/3.90 zlib/1.2.7 libidn/1.28 libssh2/1.8.0
Protocols: dict file ftp ftps gopher http https imap imaps ldap ldaps pop3 pop3s rtsp scp sftp smtp smtps telnet tftp
Features: AsynchDNS GSS-Negotiate IDN IPv6 Largefile NTLM NTLM_WB SSL libz unix-sockets
```
Ghost Script: Recommend >= 10.0
```
[cmrailtr@s03dd ~]$ ghostscript -v
GPL Ghostscript 9.25 (2018-09-13)
Copyright (C) 2018 Artifex Software, Inc.  All rights reserved.
```

ImageMagick: Recommend >= 8.4
```
[cmrailtr@s03dd ~]$ gs -version
GPL Ghostscript 9.25 (2018-09-13)
Copyright (C) 2018 Artifex Software, Inc.  All rights reserved.
```

OpenSSL: Recommend >= 3.0
```
[cmrailtr@s03dd ~]$ openssl version
OpenSSL 1.0.2k-fips  26 Jan 2017
```

WebP
```
[cmrailtr@s03dd ~]$ webp -version
bash: webp: command not found
[cmrailtr@s03dd ~]$ cwebp -version
bash: cwebp: command not found
```

AVIF
```
[cmrailtr@s03dd ~]$ avif
bash: avif: command not found
```

MariaDB: Recommend 10.6 LTS, 10.11 LTS, 11.4 LTS
```
[cmrailtr@s03dd ~]$ mysql --help
mysql  Ver 15.1 Distrib 10.6.19-MariaDB, for Linux (x86_64) using readline 5.1
Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.
```

Utilities that the [CiviCRM Installation Guide](https://docs.civicrm.org/installation/en/latest/wordpress/) suggests using:
wget:
```
[cmrailtr@s03dd ~]$ wget --version
GNU Wget 1.14 built on linux-gnu.
```
unzip:
```
[cmrailtr@s03dd ~]$ unzip -v
UnZip 6.00 of 20 April 2009, by Info-ZIP.  Maintained by C. Spieler.  Send
bug reports using http://www.info-zip.org/zip-bug.html; see README for details.
```
zip:
```
[cmrailtr@s03dd ~]$ zip -v
Copyright (c) 1990-2008 Info-ZIP - Type 'zip "-L"' for software license.
This is Zip 3.0 (July 5th 2008), by Info-ZIP.
```
In Summary:  For Cloudinux 7.9: curl, Ghost Script, ImageMagick, OpenSSL, are all below the recommended revision. WebP and AVIF do not appear to be installed. 

The current latest CloudLinux 9.6 DVD release, https://repo.cloudlinux.com/cloudlinux/9/iso/x86_64/ has a manifest file which indicates curl, Ghost Script, ImageMagick are still below the WordPress recommended revision. OpenSSL at 3.2.2-6 is above recomended. Also available are libwebp 1.2.0-8 and libavif 0.11.1-4. Therefore there would be benefits in upgrading the CloudLinux to the leatest version.

## CiviCRM Database

Ventraip with CloudLinux 7.9, currently supply the MariaDB 10.6.19 LTS SQL database.

[From:](https://docs.civicrm.org/installation/en/latest/wordpress/) *CiviCRM may be configured to use your existing WordPress database, or a separate (new) database. Using a separate database is generally preferred - as it makes backups and upgrades easier.*

C-Panel, in the *Databases* section provides the *MySQL® Database Wizard* utility. This was used to create a new seperate database for CiviCRM. The database was named: **cmrailtr_civicrm**. It was configured to use the same **cmrailtr_czhn1** username and password as the WordPress database.

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
In the web-based part of the CiviCRM installation the link to the CiviCRM database must be provided. This link is:
```
mysql://cmrailtr_czhn1:password@localhost:3306/cmrailtr_civicrm
```

## [CiviCRM Database Permissions](https://docs.civicrm.org/installation/en/latest/requirements/#mysql-permissions).

These were granted while using the *MySQL® Database Wizard* to create the CiviCRM database. Permissions enabled for *cmrailtr_czhn1* are:
```
ALTER ROUTINE, ALTER, CREATE ROUTINE, CREATE TEMPORARY TABLES,
CREATE VIEW, CREATE, DELETE, DROP, INDEX, INSERT, LOCK TABLES,
REFERENCES, SELECT, SHOW VIEW TRIGGER, UPDATE,
```

`EVENT` and `EXECUTE` are the two permissions missing from the above list. They would be present if `ALL PERMISSIONS` were granted.


## [TimeZone Support](https://docs.civicrm.org/installation/en/latest/requirements/#mysql-timezones):

Check the timezone of MariaDB:
```
MariaDB [(none)]> SELECT @@system_time_zone;
+--------------------+
| @@system_time_zone |
+--------------------+
| AEST               |
+--------------------+

MariaDB [(none)]> SELECT TIMEDIFF(NOW(), UTC_TIMESTAMP);
+--------------------------------+
| TIMEDIFF(NOW(), UTC_TIMESTAMP) |
+--------------------------------+
| 10:00:00                       |
+--------------------------------+
```
Verify that the timezone data has been installed on WordPress. As seen below MariaDB was able to convert the Melbourne time to Auckland time at +2 hours.

```
MariaDB [(none)]> SELECT CONVERT_TZ("2025-06-03 14:30:00", "Australia/Melbourne", "Pacific/Auckland");
+------------------------------------------------------------------------------+
| CONVERT_TZ("2025-06-03 14:30:00", "Australia/Melbourne", "Pacific/Auckland") |
+------------------------------------------------------------------------------+
| 2025-06-03 16:30:00                                                          |
+------------------------------------------------------------------------------+
```

## CiviCRM Download and Installation of the zip distribution file

Check the latest version of CiviCRM: https://civicrm.org/download

In CMRT's case, the latest CiviCRM zip distribution was 6.2.0. The download and unzipping was performed using the C-Panel Terminal:
```
[cmrailtr@s03dd ~]$ cd public_html
[cmrailtr@s03dd public_html]$ cd wp-content
[cmrailtr@s03dd wp-content]$ cd plugins
[cmrailtr@s03dd plugins]$ wget https://download.civicrm.org/civicrm-6.2.0-wordpress.zip
[cmrailtr@s03dd plugins]$ unzip -q civicrm-6.2.0-wordpress.zip
```
After unzipping, the listing of the CiviCRM top-level directory: `/home/cmrailtr/public_html/wp-content/plugins/civicrm/`
```
[cmrailtr@s03dd plugins]$ ls -l civicrm
total 100
drwxr-xr-x  6 cmrailtr cmrailtr  4096 Feb 28  2023 assets
drwxr-xr-x 24 cmrailtr cmrailtr  4096 May  8 16:23 civicrm
-rw-r--r--  1 cmrailtr cmrailtr 45233 May  8 16:23 civicrm.php
drwxr-xr-x  5 cmrailtr cmrailtr  4096 Feb  7 13:37 includes
drwxr-xr-x  2 cmrailtr cmrailtr  4096 Feb  9  2024 languages
-rw-r--r--  1 cmrailtr cmrailtr  5367 Feb  9  2024 phpcs.xml
-rw-r--r--  1 cmrailtr cmrailtr   821 Feb  9  2024 phpunit.xml.dist
-rw-r--r--  1 cmrailtr cmrailtr  2075 Feb 28  2023 README.md
-rw-r--r--  1 cmrailtr cmrailtr  2036 Aug  8  2024 readme.txt
drwxr-xr-x  3 cmrailtr cmrailtr  4096 Feb 28  2023 tests
-rw-r--r--  1 cmrailtr cmrailtr  1007 Feb 28  2023 uninstall.php
drwxr-xr-x  3 cmrailtr cmrailtr  4096 Feb  9  2024 wp-cli
drwxr-xr-x  5 cmrailtr cmrailtr  4096 Feb  7 13:37 wp-rest
```
The remainder of the CiviCMR Installation is provided through WordPress. 

## Installation Continued via WordPress Administrator

The following steps were performed:

* Login via https://cmrailtrail.org.au/wp-admin
* Goto *Plugins*.
* CiviCRM will be on the list of plugins. Click on *activate*.
* The CiviCRM Installation screen will be displayed. It has the following parts:
    * Localization
    * System Requirements - If modifications need to be made before the installation can proceed.
    * Sample data
    * Components
    * Environment
    * Install / Refresh Button

 The CiviCRM installation screen:

 ![CiviCRM Installation Main Screen](images/install/civicrm-installation-screen.png)
 

 The Localization section is used to set the time to Australia/Melbourne:
 
 ![CiviCRM Installation Localization](images/install/localization.png)

The Sample Date section allows adding demo data of about 100 fictious contacts to the CivCRM database.

 ![CiviCRM Installation Sample Data](images/install/sample-data.png)

If *System Requirements* are not met, then their error messages are displayed and the error condition must be removed in order to progress. In the following case the pointer to the database has not been set to point to the separate CiviCRM database.

 ![CiviCRM Installation System Requirements](images/install/system-requirements.png)

The above errors were corrected by changing the *Environment* setting of the *CiviCRM Database* to: `mysql://cmrailtr_czhn1:HiDDEN@localhost:3306/cmailtr_civicrm` and then clicking on the *Refresh* button.

![CiviCRM Installation Environment](images/install/environment.png)

The *Components* section allows selection/de-selection of the components of CiviCRM. The default is for 5 of the 8 components to be selected. 

![CiviCRM Installation Components Before](images/install/components-before.png)

For the CMRT installation all 8 components were selected.

![CiviCRM Installation Components After](images/install/components-after.png)

There is also the Users section in which *Synchronize all existing users* may be checked or unchecked. This was changed to unchecked.

![CiviCRM Installation Users](images/install/users-selected.png)

If all the errors have been removed then the *Refresh* button is relabelled as the *Install* button. Click this to complete the CiviCRM installation.

![CiviCRM Installation Submit](images/install/submit.png)

## CiviCRM Status

The WordPress/CiviCRM dash-panel is displayed after the installation completes and will display colour coded status alert information. Actions are required to modify CiviCRM which will clear these status alerts.


## CloudLinux Python

Ventraip's CloundLinux V7.9 has python V2.7.5 available at the C-Panel Terminal:
```
[cmrailtr@s03dd ~]$ python
Python 2.7.5 (default, Oct  3 2024, 19:11:33)
[GCC 4.8.5 20150623 (Red Hat 4.8.5-44)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```
Python 2 was released in 2000, and went end-of-life in 2020. Python 3, first released in 2008, is the supported version. It's most recent release was Version 3.13.4 in June 2025. 

[PyMySQL](https://pypi.org/project/PyMySQL/) is a Python library that provides connection to a MySQL/MariaDB database. It requires Python >= 3.7, MariaDB >= 10.4, or MySQL >= 5.7. A similar Python library product is [MySQL-Connector](https://pypi.org/project/mysql-connector-python/), but PyMySQL seems to be the preference in CloudLinux 9.6.

An example of PyMySQL performing the SQL command *SHOW DATABASES;*
```
import pymysql.cursors

# Connect to the database
connection = pymysql.connect(
        host=HOST,
        user=USER,
        password=PASSWORD,
        database=DATABASE,
        cursorclass=pymysql.cursors.DictCursor
        )

# Show databases;
with connection:
    with connection.cursor() as cursor:
        sql = "SHOW DATABASES"
        cursor.execute(sql,) # ('webmaster@python.org', 'very-secret'))
        result = cursor.fetchall()
        print(result)

# The returned result is a list of dictionaries:
# [{'Database': 'civicrm'}, {'Database': 'information_schema'}, {'Database': 'wordpress'}]
#
# Without the 'cursorclass=pymysql.cursors.DictCursor' as part of the connect(), the returned result is a tuple of tuples.
# (('civicrm',), ('information_schema',), ('wordpress',))
```
The latest CloudLinux V9.6 ships with:

* Python 3.8 with PyMySQL 0.7.11 (Apr 2017)
* Python 3.11 with PyMySQL 1.0.2-2 (Jan 2021)
* Python 3.12 with PyMySQL 1.1.0-3 (Jun 2023).
  
The PyPI repository contains [PyMySQL](https://pypi.org/project/PyMySQL/)

EOF.

Notes:
Version: 6.2.0 Build Time: Wed, 07 May 2025 23:24:21 -0700
Version: 6.3.0 Build Time: Wed, 04 Jun 2025 22:57:43 -0700
Version: 6.3.1 Build Time: Thu, 05 Jun 2025 16:29:12 -0700

https://civicrm.org/core-stats
Detailed extension statistics are only available to members and partners. Login or Become a member. Why? 
