# CiviCRM Installation

CiviCRM, a Customer Relationship Management (CRM) application was installed as a plugin to the Wordpress Content Management System (CMS).

Installation Date: 2025-06-03

Installation by: Ian and Ken Stewart

This document is a record of the installation activities.

## Introduction

Ventraip https://ventraip.com.au/ is the Australian based company that povides the web-hosting 
and domain name services for the CMRT website: https://cmrailtrail.org.au

Ventraip run their hosting servers using [CloudLinux OS](https://cloudlinux.com/). 
The current version of Linux is: **3.10.0-962.3.2.lve1.5.81.el7.x86_64 x86_64**. 
The CloudLinux version is (from `$ cat /etc/os-release`: **7.9**

As of June 2025, the latest CloudLinux 9.6 was released in May 2025.

Ventraip use [*LiteSpeed Web Server*](https://www.litespeedtech.com/) (LSWS) as the web server.

Logging into the CMRT account on a Ventraip server is via a web-based login panel at: https://vip.ventraip.com.au/login

Login requires two part authentication.

Upon logging in *C-Panel* may be activated. This gains access to applications that manage PHP, Databases, Mail, etc. 
This includes a *Terminal* allowing bash comands may be executed.

The user account provided by Ventraip is *cmrailtr*. Files created in this account have the owner and group name: *cmrailtr*
Files normally have a priv of: 644, and directory priv's are: 755.

Wordpress has been installed as the Content Management System (CMS). The term *CMS* is sometimes refered to by CiviCRM as the *User Framework*.

It is not known who initially installed Wordpress on the website, and any of the rational that was used in namings that were applied.

Wordpress Naming.
* Account Name: **cmrailtr**
* Wordpress top level directory. Default is *wordpress*: **public_html**
* Wordpress Maria database name. default is *wordpress*: **cmrailtr_czhn1**
* Wordpress MariaDB database User name: **cmrailtr_czhn1**
* Wordpress tables prefix. Default is *wp_*: **bsen_**
* CiviCRM MariaDB database name. Default is *civicrm*: **cmrailtr_civicrm**
* CiviCRM tables prefix: **civicrm_** 

The linux path to Wordpress is: `/home/cmrailtr/public_html`
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
        │   ├── plugins  <--- Staging directory for latest civicrm.zip distribution file.
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

## CiviCRM Installation for Wordpress - Preparation

Before commencing the CiviCRM installaton the current Wordpress installation should be checked. Adjustments may need to be made to Wordpress for the civiCRM installation to be performaed correctly.

Refer to these documents:

* [Wordpress - Advanced Administration Handbook](https://developer.wordpress.org/advanced-administration/)
* [WordPress Hosting Team Handbook](https://make.wordpress.org/hosting/handbook/)
* [CiviCRM Installation Guide](https://docs.civicrm.org/installation/en/latest/)
* [Install CiviCRM on Wordpress](https://docs.civicrm.org/installation/en/latest/wordpress/)
* [CiviCRM Installation Requirements](https://docs.civicrm.org/installation/en/latest/requirements/)


## Checks of Wordpress:

* Check that Wordpress is up-to-date and no upgrades are pending.

## Check the PHP revision.
* In Wikipedia the [PHP](https://en.wikipedia.org/wiki/PHP) topic has a table of the PHP release revisions.
* CMRT were running PHP V7.4 which stopped being supported in November 2022.
* CMRT was upgraded to PHP V8.3 which is supported through until the end of 2027.
* The PHP version upgrade is performed in the *C-Panel - Software Section* using the a-plication *php - Select PHP Version*. In this *PHP Selector* applicaton the *Current PHP Version* drop-down menu allows selection of the latest supported version of PHP, which was V8.3.

## [Check PHP Extensions](https://make.wordpress.org/hosting/handbook/server-environment/#php-extensions)

* The *C-Panel PHP Selector* application allows selecting or deselecting the PHP Extensions installed. For V8.3 there are 132 extensions.
* The *Wordpress Handbook* provides a section on [PHP Extensions](https://make.wordpress.org/hosting/handbook/server-environment/#php-extensions). The PHP extensions are in six catagories:
  
    * Required - 2 - json, mysqli or mysqlnd
    * Highly recommended - 13 - curl, dom, exif, fileinfo, hash, igbinary, imagick, intl, mbstring, openssl, pcre, xml, zip.
    * Recommended - 4 - apcu, memcached, opcache, redis.
    * Optional - 1 - timezonedb.
    * Remaining PHP modules WordPress may use - 9 - bcmath, filter, image, iconv, shmop, simplexml, sodium, xmlreader, zlib.
    * Extensions used for file changes - 3 - ssh2, ftp, sockets.
 
* For CMRT all 32 PHP Extensions listed above from the Handbook's six catagories were applied. Some Extensions that had been applied for some other reason reason, were left applied.
  
* The [CiviCRM Installation Guide](https://docs.civicrm.org/installation/en/latest/requirements/#required-for-civicrm-core) lists the following PHP Extensions as required: bcmath, curl, dom, fileinfo, intl, mbstring, zip. All of these extension have already been installed as requirments of Wordpress. One additional extension is required for the CiviSMTP service. This extension is: soap.

#[PHP Configuration](https://docs.civicrm.org/installation/en/latest/requirements/#php-configuration)

The following PHP directives is the recommended minimum. Typically Operating Systems would define these changes to the directives in the file `/etc/php/8.3/apache2/php.ini` with the following commands:
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

The WordPress HostingHandbook has a section on [System Packages](https://make.wordpress.org/hosting/handbook/server-environment/#system-packages) that Wordpress requires. These are: curl, Ghost Script, ImageMagick, OpenSSL, WebP AVIF.

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
In Summary:  For Cloudinux 7: curl, Ghost Script, ImageMagick, OpenSSL, are all below the recommended revision. WebP and AVIF do not appear to be installed. 

The current latest CloudLinux 9.6 DVD release, https://repo.cloudlinux.com/cloudlinux/9/iso/x86_64/ has a manifest file which indicates curl, Ghost Script, ImageMagick are still below the WordPress recommended revision. OpenSSL at 3.2.2-6 is above recomended. Also available are libwebp 1.2.0-8 and libavif 0.11.1-4.


## CiviCRM Database

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

These were set when using the *MySQL® Database Wizard* to create the CiviCRM database. Permissions enabled for *cmrailtr_czhn1* are:
```
ALTER ROUTINE, ALTER, CREATE ROUTINE, CREATE TEMPORARY TABLES,
CREATE VIEW, CREATE, DELETE, DROP, INDEX, INSERT, LOCK TABLES,
REFERENCES, SELECT, SHOW VIEW TRIGGER, UPDATE,
```

`EVENT` and `EXECUTE` are the two permissions missing from `ALL PERMISSIONS`.


## [TimeZone Support](https://docs.civicrm.org/installation/en/latest/requirements/#mysql-timezones):

Check the timezone of MariaDB
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

In CMRT's case, the latest CiviCRM zip distribution was 6.2.0. The download and unzipping was performed using the C-Panel Terminal.

```
[cmrailtr@s03dd ~]$ cd public_html
[cmrailtr@s03dd public_html]$ cd wp-content
[cmrailtr@s03dd wp-content]$ cd plugins
[cmrailtr@s03dd plugins]$ wget https://download.civicrm.org/civicrm-6.2.0-wordpress.zip
[cmrailtr@s03dd plugins]$ unzip -q civicrm-6.2.0-wordpress.zip
```
Listing of the CiviCRM top-level directory: `/home/cmrailtr/public_html/wp-content/plugins/civicrm/`
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

## Installation Continued via Wordpress Administrator

The folloowing steps were performed:

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

 ![CiviCRM Installation Main Screen](image/install/civicrm-installation-screen.png)
 
  


The remainder of the CiviCMR Installation is provided through the WordPress 
Version: 6.2.0 Build Time: Wed, 07 May 2025 23:24:21 -0700
Version: 6.3.0 Build Time: Wed, 04 Jun 2025 22:57:43 -0700
Version: 6.3.1 Build Time: Thu, 05 Jun 2025 16:29:12 -0700

https://civicrm.org/core-stats

Detailed extension statistics are only available to members and partners. Login or Become a member. Why? 
