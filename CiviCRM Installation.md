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
* Wordpress Maria database name: **cmrailtr_czhn1**
* Wordpress MariaDB database User name: **cmrailtr_czhn1**
* Wordpress tables prefix. Default is *wp_*: **bsen_**
* CiviCRM MariaDB database name: **cmrailtr_civicrm**
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


        ├── wp-admin
        ├── wp-content
        └── wp-includes

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
        │   ├── languages
        │   │   ├── plugins
        │   │   └── themes
        │   ├── plugins  <--- Staging directory for latest civicrm.zip distribution file.
        │   │   ├── akismet
        │   │   └── civicrm <--- Top level directory of CiviCRM
        ...snip...



```
The path to Wordpress is...



