# CiviCRM Installation

CiviCRM, a Customer Relationship Management (CRM) application was installed as a plugin to the Wordpress Content Management System (CMS).

Installation Date: 2025-06-03

Installation by: Ian and Ken Stewart

This document is a record of the installation activities.

## Introduction

Ventraip *https://ventraip.com.au/* is the Australian based company that povides the web-hosting 
and domain name services for the CMRT website: *https://cmrailtrail.org.au*

Ventraip run their hosting servers using [CloudLinux OS](https://cloudlinux.com/). 
The current version of Linux is: 3.10.0-962.3.2.lve1.5.81.el7.x86_64 x86_64. This suggests that CloudLinux 7 is used.
The latest CloudLinux 9.6 release was in May 2025.

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

The linux path to Wordpress is: /home/cmrailtr/public_html
```
/home
└── cmrailtr
    └── public_html
        ├── index.php
        ├── license.txt
        ├── readme.html
        ├── wp-activate.php
        ├── wp-admin
        ├── wp-blog-header.php
        ├── wp-comments-post.php
        ├── wp-config.php
        ├── wp-config-sample.php
        ├── wp-content
        ├── wp-cron.php
        ├── wp-includes
        ├── wp-links-opml.php
        ├── wp-load.php
        ├── wp-login.php
        ├── wp-mail.php
        ├── wp-settings.php
        ├── wp-signup.php
        ├── wp-trackback.php
        └── xmlrpc.php


/home
└── cmrailtr
    └── public_html
        ├── wp-admin
        │   ├── css
        │   ├── ...snip...
        │   └── user
        ├── wp-content
        │   ├── languages
        │   ├── plugins
        │   ├── themes
        │   ├── upgrade
        │   └── uploads
        └── wp-includes
            ├── assets
             ...snip...

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

Refer to these documents on Wordpress:

* [Wordpress - Advanced Administration Handbook](https://developer.wordpress.org/advanced-administration/)
* [WordPress Hosting Team Handbook](https://make.wordpress.org/hosting/handbook/)

https://make.wordpress.org/hosting/handbook/server-environment/#php-extensions

Checks of Wordpress:

* Check that Wordpress is up-to-date and no upgrades are pending.

## Check the PHP revision.
* In Wikipedia the [PHP](https://en.wikipedia.org/wiki/PHP) topic has a table of the PHP release revisions.
* CMRT were running PHP V7.4 which stopped being supported in November 2022.
* CMRT was upgraded to PHP V8.3 which is supported through until the end of 2027.
* The PHP version upgrade is performed in the *C-Panel - Software Section* using the a-plication *php - Select PHP Version*. In this *PHP Selector* applicaton the *Current PHP Version* drop-down menu allows selection of the latest supported version of PHP, which was V8.3.

## Check PHP Extensions

* The *C-Panel PHP Selector* application allows selecting or deselecting the PHP Extensions installed. For V8.3 there are 132 extensions.
* The *Wordpress Handbook* provides a section on [PHP Extensions](https://make.wordpress.org/hosting/handbook/server-environment/#php-extensions). The PHP extensions are in six catagories:
  
    * Required - 2 - json, mysqli or mysqlnd
    * Highly recommended - 13 - curl, dom, exif, fileinfo, hash, igbinary, imagick, intl, mbstring, openssl, pcre, xml, zip.
    * Recommended - 4 - apcu, memcached, opcache, redis.
    * Optional - 1 - timezonedb.
    * Remaining PHP modules WordPress may use - 9 - bcmath, filter, image, iconv, shmop, simplexml, sodium, xmlreader, zlib.
    * Extensions used for file changes - 3 - ssh2, ftp, sockets.
 
* For CMRT all 32 PHP Extensions listed above from the Handbook's six catagories were applied. Some Extensions that had been applied for some other reason reason, were left applied.
  
* The [CiviCRM Installation Guide](https://docs.civicrm.org/installation/en/latest/requirements/#required-for-civicrm-core) lists the following PHP Extensions as required: bcmath, curl, dom, fileinfo, intl, mbstring, zip. All of these extension have already been installed as requirments of Wordpress. One additional extension is required for the CIviSMTP service. This extension is: soap.

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
[cmrailtr@s03dd ~]$ convert -version
Version: ImageMagick 6.9.10-68 Q16 x86_64 2023-10-25 https://imagemagick.org
Copyright: © 1999-2019 ImageMagick Studio LLC
License: https://imagemagick.org/script/license.php
Features: Cipher DPC Modules OpenMP(3.1)
Delegates (built-in): bzlib cairo fontconfig freetype gslib jng jp2 jpeg lcms ltdl lzma openexr pangocairo png ps rsvg tiff wmf x xml zlib
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

wget <--
```
[cmrailtr@s03dd ~]$ wget --version
GNU Wget 1.14 built on linux-gnu.
```

MariaDB: Recommend 10.6 LTS, 10.11 LTS, 11.4 LTS
```
[cmrailtr@s03dd ~]$ mysql --help
mysql  Ver 15.1 Distrib 10.6.19-MariaDB, for Linux (x86_64) using readline 5.1
Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.
```


*  Refer to the PHP documentation in the Wordpress Hosting Handbooks [Server Environment section](https://make.wordpress.org/hosting/handbook/server-environment/#php)

Wordpress on the CMRT website, was running PHP verson 7.4.


CiviCRM provide an [Installaton Guide](https:/

/docs.civicrm.org/installation/en/latest/) which contains a section on
[Install CiviCRM on Wordpress](https://docs.civicrm.org/installation/en/latest/wordpress/)

[Installation Requirements](https://docs.civicrm.org/installation/en/latest/requirements/)

