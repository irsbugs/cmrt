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

## Removal of CiviCRM for Wordpress

* Perform a backup of the WordPress and CiviCRM databases:
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

