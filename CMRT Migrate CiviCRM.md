# Migrating CiviCRM from civicrm.com platform to CiviCRM Standalone

2026-06-22

## Introduction

Investigation into migrating CiviCRM from the *Spark Essentials* Drupal plugin of the CiviCRM application used by civicrm.org in USA, to the VentraIP sub-domain crm.cmrailtrial.org.au CiviCRM Standalone application. For simplicity the version in USA that we migtage from will be called *civiusa* and the Standalone version we are migrating to will bew called *civi*

Simulation of the migration was performed to Ian's local PC which has CiviCRM Standalone installed i.e. *civi*. The local PC is at: *civi.local.pc* with directory tree: *~/civicrm-standalone/*. The MySql database is *civi* associated with *~/.my_civi.cnf*. Using the *upgrade_civicrm* python utility the local PC's CiviCRM Standalone was upgraded to be at 6.15.3. This *civi* has had the extension *Mozaico* added. The local PC has not had any data loaded to it, except for the *Admin contact* and *default organization*. It has not been configured to accept memberships, or questionaires, etc. 

The *civiusa* application is at *cmrailtrail.civicrm.org*. It was recently upgraded to run 6.15.3 of what is understood to be a variant of CiviCRM plugin for Drupal. Using *Administer --> Backups* a 78MB backup tar file was created on *civiusa* and downloaded to the local PC on 2026-06-22. This backup file was extracted from its tar archive and it included the file *database.sql* at 16MB. A mysql database was locally created called *civiusa* with associated *~/.my_civiusa.cnf*. *Civiusa* contains the data for about 500 contacts and 100 memberships. It can perform bulk emails, has Custom questionaire data, etc.

Initially the investigation is to determine the differences in the database tables between *civiusa* and *civi*.

A python utility was written to perfom mysql commands and extract the tables and associated properties from both the *civi* and the *civiusa* databases.

The table data collected by this program was written to *civi_database.json* and *civiusa_database.json* files. These json files are for tables that begin with the prefix *civicrm_*. For *civi* this is the cases for all tables. For *civiusa* there are other tables which are assumed to relate to Drupal. This table data is stored in *civiusa_other_database.json*.

Comparison of the two sets of collected data should help to determine what is involved in the migration.

## MySQL table features

A MySQL has various features that can be retrieved to allow it to be compared with another table of the same name. These features are not determined by wherther of not data has been added to the table.

Upon connecting to a mysql database, *civi* or *civiusa*, all the unique names of the tables for the database can be retrieved with the mysql command *SHOW TABLES;*. Each table has a set of columns. All the columns properties for a table can be retrieved with *SHOW COLUMNS FROM table_name*. There are six properties:
*Field, Type, Null, Key, Default, Extra*. For example, for the table *civicrm_contact* there are a total of 51 columns. The following is a selection of eigth of these columns to highlight their different column properties.
```
$ mysql --defaults-file=/home/ian/.my_civi.cnf --execute='SHOW COLUMNS FROM civicrm_contact';
+--------------------------------+------------------+------+-----+---------------------+-------------------------------+
| Field                          | Type             | Null | Key | Default             | Extra                         |
+--------------------------------+------------------+------+-----+---------------------+-------------------------------+
| id                             | int(10) unsigned | NO   | PRI | NULL                | auto_increment                |
| external_identifier            | varchar(64)      | YES  | UNI | NULL                |                               |
| first_name                     | varchar(64)      | YES  | MUL | NULL                |                               |
| last_name                      | varchar(64)      | YES  | MUL | NULL                |                               |
| do_not_email                   | tinyint(1)       | NO   |     | 0                   |                               |
| image_URL                      | text             | YES  |     | NULL                |                               |
| birth_date                     | date             | YES  |     | NULL                |                               |
| created_date                   | timestamp        | YES  | MUL | NULL                |                               |
| modified_date                  | timestamp        | YES  | MUL | current_timestamp() | on update current_timestamp() |
+--------------------------------+------------------+------+-----+---------------------+-------------------------------+
```
Note although these are properties of *columns* they are displayed as *rows* of property data. If the data is displayed with the mysql command *SELECT * FROM civicrm_contact;* then all 51 columns are displayed horizontally, with the *Field* as the column header, and the rows display the data for each individual contact.

In the above table, some observations are:
* The field *id* is an integer that auto-increments. Each new contact added gets the next integer. If a contact is deleted then its *id* integer can not be recovered for use with another contact.
* The *first_name* and *last_name* have a data type of *varchar(64)*. This means each name can be a variable length string up to 64 characters in length.
* *do_not_email* type of *tinyint(1)* is from -128 to +127 or 0 to 255, but it is often used as a boolean with values 0 and 1.
* *birth_date* uses the data type of *date*.
* *timestamp* stores its data as *yyyy--mm-dd hh:mm:ss*. Another method is to use *(int(11)* and store the seconds since the linux epoch of 1 Jan 1970.


## Initial Table Information

Using a python utility to retrieve both *civi* and *civiusa* the following is a summary of the data:

### Civi

* Total tables from database /home/ian/.my_civi.cnf: 163
* All elements in civi_table_list are unique
* All elements in other_table_list are unique
* Table list total: 163, CiviCRM table list: 163, Other table_list: 0
* Length of data_dict_civi: 163
* Length of data_dict_other: 0  <-- Using CiviCRM Standalone so no CMS related tables.
* Database information written to: civi_database.json
* Database information written to: civi_other_database.json
* Total differnet types: 49
* Total number of fields: 1853

### Civiusa

* Total tables from database /home/ian/.my_civiusa.cnf: 259
* All elements in civi_table_list are unique
* All elements in other_table_list are unique
* Table list total: 259, CiviCRM table list: 187, Other table_list: 72
* Length of data_dict_civi: 187
* Length of data_dict_other: 72  <-- These are assumed to be tables related to the Drupal CMS platform.
* Database information written to: civiusa_database.json
* Database information written to: civiusa_other_database.json
* Total differnet types: 48
* Total number of fields: 2048

### Compare Civi vs. Civiusa

* civi civicrm_ prefixed tables: 163
* civiusa civicrm_ prefixed tables:  187
  
* civi civicrm_ prefixed tables in civiusa: 159
* civi civicrm_ prefixed tables not in civiusa: 4
  
* civiusa civicrm_ prefixed tables in civi: 159
* civiusa civicrm_ prefixed tables not in civi: 28

### Tables in civi with civcrm_ prefix that are not in civiusa. - 4
```
civicrm_role
civicrm_session
civicrm_totp
civicrm_user_role
```

### Tables in civiusa with civicrm_ prefix that are not in civi. - 28
```
civicrm_cxn
civicrm_firewall_ipaddress
civicrm_grant
civicrm_iats_faps_journal
civicrm_iats_journal
civicrm_iats_request_log
civicrm_iats_response_log
civicrm_iats_ukdd_validate
civicrm_iats_verify
civicrm_login_security_device
civicrm_mailing_event_forward
civicrm_mosaico_msg_template
civicrm_paymentprocessor_webhook
civicrm_stripe_customers
civicrm_stripe_paymentintent
civicrm_stripe_plans
civicrm_stripe_subscriptions
civicrm_value_cmrt_voluntee_11
civicrm_value_contribution_page_terms_and_conditions_7
civicrm_value_contribution_terms_and_conditions_acceptan_8
civicrm_value_event_terms_and_conditions_7
civicrm_value_event_terms_and_conditions_acceptance_9
civicrm_value_individual_in_8
civicrm_value_member_engage_9
civicrm_value_member_involv_10
civicrm_value_organization__7
civicrm_value_payment_detai_6
civicrm_value_sla_acceptance_4
```
Many of these extra tables are attributed to Civiusa having been setup to support memberships payments, questionaires, etc.


### Summary of the Data types in the databases where the table prefix is civicrm_
```
Data Type        Civi  Civiusa
------------------------------
blob                1        1
char(2)             1        1
char(22)            3        3
char(3)             2        2
char(64)            1        0
date               21       25
datetime           55       63
decimal(10,8)       1        1
decimal(18,9)       2        2
decimal(20,2)      35       41
double              3        8
Int(1) unsigned     2        0
int(10)             0        3
Int(10) unsigned  629      692
int(11)            50       49
longtext           25       28
mediumblob          1        1
text              123      142
timestamp          72       79
tinyint(1)        254        9
tinyint(4)          3      258
varchar(10)         9        9
varchar(100)        1        2
varchar(1024)       2        4
varchar(12)        10       11
varchar(127)        1        1
varchar(128)       46       47
varchar(15)         1        1
varchar(16)        11       11
varchar(20)         2        1
varchar(2048)       4        4
varchar(24)         1        1
varchar(25)         0        1
varchar(254)        3        3
varchar(255)      260      322
varchar(3)         15       19
varchar(32)        18       19
varchar(4)          7        8
varchar(40)         1        1
varchar(45)         1        1
varchar(5)          4        4
varchar(50)         2        2
varchar(512)        8        7
varchar(6)          1        1
varchar(60)         2        0
varchar(63)         1        1
varchar(64)       121      122
varchar(70)         1        1
varchar(8)         31       31
varchar(9)          1        1
varchar(96)         4        4
------------------------------
  51             1224     2048
```

### Tables in Civiusa database that do not begin with 'civicrm_' = 72 

Assumed to be Drupal CMS related.
However, some of these may be used as replacements for the four tables missing from *civi*: civicrm_role, civicrm_session, civicrm_totp, civicrm_user_role

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
