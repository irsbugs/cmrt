# Migrating CiviCRM from civicrm.com platform to CiviCRM Standalone

2026-06-22

## Introduction

Details of migrating CiviCRM from the civicrm / Drupal plugin application in USA to the VentraIP sub-domain crm.cmrailtrial.org.au CiviCRM Standalone application.

Simulation of the migration was performed on Ian's local PC which has CiviCRM Standalone installed. The local PC is at: *civi.local.pc* with directory tree: *~/civicrm-standalone/*. The MySql database is *civi* assiciated with *~/.my_civi.cnf*. Using the *upgrade_civicrm* python utility the local PC's CiviCRM Standalone was upgraded to be at 6.15.3. The local PC has not had any data loaded to it or been configured to accept memberships, or questionaires, etc.

The *civiusa* application is at *cmrailtrail.civicrm.org*. It was recently upgraded to run 6.15.3 of CiviCRM plugin for Drupal. Using *Administer --> Backups* a 78MB backup tar file was created and downloaded to the local PC on 2026-06-22. This file was extracted from its tar archive and it included the file *database.sql* at 16MB. A mysql database called *civiusa* with associated *~/.my_civiusa.cnf*. Civiusa contains the data for about 500 contacts and 100 memberships. It can perform bulk emails, has Custom questionaire data, etc.

A python utility was written to perfom mysql commands and extract the tables and associated properties from both the *civi* and the *civiusa* databases.

The table data collected by this program was written to *civi_database.json* and *civiusa_database.json* files.

Comparison of the two sets of collected data should help to determine what is involved in the migration.

## Initial Table Information

### Civi

* Tables that do not begin with *civicrm_* = 0
* Tables that begin with *civicrm_* = 163
* Database information written to: civi_database.json
* Total different data types: 49
* Total number of civicrm fields: 1853

### Civiusa

* Tables that do not begin with *civicrm_* = 72  <-- These are assumed to be tables related to the Drupal CMS platform
* Tables that begin with *civicrm_* = 187  <-- 24 Extra are assumed to relate to memberships, questionaires, etc.
* Database information written to: civiusa_database.json
* Total different data types: 51  <-- Two extras are: *int(10) unsigned* and *varchar(25)*
* Total number of civicrm fields: 2066



