# Migrate CiviCRM - 2

2026-06-24 

## Introduction

This is a continuation of [CMRT Migrate CiviCRM](CMRT Migrate CiviCRM.md)

## Documantation

* https://www.beeches.it/civicrm-migration-guide-wordpress-to-standalone/
* https://lab.civicrm.org/extensions/standalonemigrate
* https://civicrm.com/spark/

## Summary of Database Analysis

A backup of the cmrailtrail Spark Essentials 6.15.3 database named *civiusa*, was compared to the database of a fresh installation of CiviCRM Standalone 6.15.3 named *civi*.

The following four tables are missing from *civiusa*
* civicrm_role
* civicrm_session
* civicrm_totp
* civicrm_user_role


Comparison of 159 files prefixed with civicrm_ in civi vs civicrm

* 157 tables have identical column counts which suggest they could be used without modification as migrated tables in the Standalone CiviCRM
* The table *civicrm_participant* has 21 tables in *civi* and 22 tables *civiusa* The extra column in *civiusa* is *cart id*.
* The table *civicrm_uf_match* has 14 columns in *civi* but only 6 columns in *civiusa*. However *civiusa* has the drupal table *users* with some of the missing columns. It appears that by merging the *civiusa* tables *civicrm_uf_match* and *users*, then a replacement *civicrm_uf_match* table could be created for *civi*.

This document will detail the attempt generate *civicrm_participant* and *civicrm_uf_match* as suitable replacement tables in *civi* database

## Approach

Extract just the from the table creatng and adding of data from the *civi* and *civiusa* databases.


