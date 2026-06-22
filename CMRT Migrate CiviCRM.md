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
* Total different data types: 51  <-- Two extras are: *int(10)* and *varchar(25)*
* Total number of civicrm fields: 2066


### Summary of the Data types in the databases
```
Civiusa				    Civi
---------------------------------
blob				    blob
char(2)				    char(2)
char(22)				char(22)
char(3)			    	char(3)
char(64)				char(64)
date				    date
datetime				datetime
decimal(10,8)			decimal(10,8)
decimal(18,9)			decimal(18,9)
decimal(20,2)			decimal(20,2)
double				    double
int(1) unsigned		    int(1) unsigned
int(10)				    
int(10) unsigned	    int(10) unsigned
int(11)				    int(11)
longtext				longtext
mediumblob				mediumblob
text				    text
timestamp				timestamp
tinyint(1)				tinyint(1)
tinyint(4)				tinyint(4)
varchar(10)				varchar(10)
varchar(100)			varchar(100)
varchar(1024)			varchar(1024)
varchar(12)				varchar(12)
varchar(127)			varchar(127)
varchar(128)			varchar(128)
varchar(15)				varchar(15)
varchar(16)				varchar(16)
varchar(20)				varchar(20)
varchar(2048)			varchar(2048)
varchar(24)				varchar(24)
varchar(25)				
varchar(254)			varchar(254)
varchar(255)			varchar(255)
varchar(3)				varchar(3)
varchar(32)				varchar(32)
varchar(4)				varchar(4)
varchar(40)				varchar(40)
varchar(45)				varchar(45)
varchar(5)				varchar(5)
varchar(50)				varchar(50)
varchar(512)			varchar(512)
varchar(6)				varchar(6)
varchar(60)				varchar(60)
varchar(63)				varchar(63)
varchar(64)				varchar(64)
varchar(70)				varchar(70)
varchar(8)				varchar(8)
varchar(9)				varchar(9)
```

### Tables in Civiusa database that do not begin with 'civicrm_' = 72 

Assumed to be Drupal CMS related.
```
actions
authmap
backup_iats_customer_codes
batch
block
block_custom
block_node_type
block_role
blocked_ips
cache
cache_admin_menu
cache_block
cache_bootstrap
cache_field
cache_filter
cache_form
cache_image
cache_menu
cache_page
cache_path
cache_update
comment
date_format_locale
date_format_type
date_formats
field_config
field_config_instance
field_data_body
field_data_comment_body
field_revision_body
field_revision_comment_body
file_managed
file_usage
filter
filter_format
flood
history
image_effects
image_styles
menu_custom
menu_links
menu_router
node
node_access
node_comment_statistics
node_revision
node_type
queue
rdf_mapping
registry
registry_file
role
role_permission
search_dataset
search_index
search_node_links
search_total
semaphore
sequences
sessions
shortcut_set
shortcut_set_users
system
taxonomy_index
taxonomy_term_data
taxonomy_term_hierarchy
taxonomy_vocabulary
url_alias
users
users_roles
variable
watchdog
```
