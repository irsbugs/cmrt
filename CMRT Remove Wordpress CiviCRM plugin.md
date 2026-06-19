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





