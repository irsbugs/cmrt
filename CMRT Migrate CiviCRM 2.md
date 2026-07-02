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


## Review of the four tables missing from *civiusa*

The four missing tables are selected for *civi*  and displayed below

### civicrm_user_role

```
ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civi.cnf --execute='SHOW COLUMNS FROM civicrm_user_role';
+---------+------------------+------+-----+---------+----------------+
| Field   | Type             | Null | Key | Default | Extra          |
+---------+------------------+------+-----+---------+----------------+
| id      | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| user_id | int(10) unsigned | YES  | MUL | NULL    |                |
| role_id | int(10) unsigned | YES  | MUL | NULL    |                |
+---------+------------------+------+-----+---------+----------------+
ian@hp:~/ken8/mysql_data/usa_civi$

ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civi.cnf --execute='SELECT id, user_id, role_id FROM civicrm_user_role';
+----+---------+---------+
| id | user_id | role_id |
+----+---------+---------+
|  3 |       2 |       2 |
|  4 |       1 |       2 |
+----+---------+---------+
```

### civicrm_totp

Contain no data

```
ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civi.cnf --execute='SHOW COLUMNS FROM civicrm_totp';
+---------+------------------+------+-----+---------+----------------+
| Field   | Type             | Null | Key | Default | Extra          |
+---------+------------------+------+-----+---------+----------------+
| id      | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| user_id | int(10) unsigned | NO   | MUL | NULL    |                |
| seed    | varchar(512)     | NO   |     | NULL    |                |
| hash    | varchar(20)      | NO   |     | "sha1"  |                |
| period  | int(1) unsigned  | NO   |     | 30      |                |
| length  | int(1) unsigned  | NO   |     | 6       |                |
+---------+------------------+------+-----+---------+----------------+
ian@hp:~/ken8/mysql_data/usa_civi$ 

EMPTY
ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civi.cnf --execute='SELECT id, user_id, seed, hash, period, length FROM civicrm_totp';
ian@hp:~/ken8/mysql_data/usa_civi$ 
```

### civicrm_role

```
ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civi.cnf --execute='SHOW COLUMNS FROM civicrm_role';
+-------------+------------------+------+-----+---------+----------------+
| Field       | Type             | Null | Key | Default | Extra          |
+-------------+------------------+------+-----+---------+----------------+
| id          | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| name        | varchar(60)      | NO   |     | NULL    |                |
| label       | varchar(128)     | NO   |     | NULL    |                |
| permissions | text             | NO   |     | NULL    |                |
| is_active   | tinyint(1)       | NO   |     | 1       |                |
+-------------+------------------+------+-----+---------+----------------+
ian@hp:~/ken8/mysql_data/usa_civi$ 

$ mysql --defaults-file=/home/ian/.my_civi.cnf --execute='SELECT id, name, label, permissions, is_active FROM civicrm_role';

| id | name     | label                               | permissions  | is_active |

|  1 | everyone | Everyone, including anonymous users | 

access CiviMail subscribe/unsubscribe pages
make online contributions
view event info
register for events
access password resets
authenticate with password 

|         1 |

|  2 | admin    | Administrator                       | 
all CiviCRM permissions and ACLs 

|         1 |

|  3 | staff    | Staff                               |  (77 permissions...)
access AJAX API
access CiviCRM
access Contact Dashboard
access uploaded files
add contacts
view my contact
view all contacts
edit all contacts
edit my contact
delete contacts
import contacts
access deleted contacts
merge duplicate contacts
edit groups
manage tags
administer Tagsets
view all activities
delete activities
add contact notes
view all notes
access CiviContribute
delete in CiviContribute
edit contributions
make online contributions
view my invoices
access CiviEvent
delete in CiviEvent
edit all events
edit event participants
register for events
view event info
view event participants
gotv campaign contacts
interview campaign contacts
manage campaign
release campaign contacts
reserve campaign contacts
sign CiviCRM Petition
access CiviMail
access CiviMail subscribe/unsubscribe pages
delete in CiviMail
view public CiviMail content
access CiviMember
delete in CiviMember
edit memberships
access all cases and activities
access my cases and activities
add cases
delete in CiviCase
access CiviPledge
delete in CiviPledge
edit pledges
access CiviReport
access Report Criteria
administer reserved reports
save Report Criteria
profile create
profile edit
profile listings
profile listings and forms
profile view
close all manual batches
close own manual batches
create manual batch
delete all manual batches
delete own manual batches
edit all manual batches
edit own manual batches
export all manual batches
export own manual batches
reopen all manual batches
reopen own manual batches
view all manual batches
view own manual batches
access all custom data
access contact reference field
scms:view user account 

|         1 |

```

### civicrm_session

```
ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civi.cnf --execute='SHOW COLUMNS FROM civicrm_session';
+---------------+----------+------+-----+---------+----------------+
| Field         | Type     | Null | Key | Default | Extra          |
+---------------+----------+------+-----+---------+----------------+
| id            | int(11)  | NO   | PRI | NULL    | auto_increment |
| session_id    | char(64) | NO   | UNI | NULL    |                |
| data          | longtext | YES  |     | NULL    |                |
| last_accessed | datetime | YES  |     | NULL    |                |
+---------------+----------+------+-----+---------+----------------+
ian@hp:~/ken8/mysql_data/usa_civi$ 

Without "data"...

ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civi.cnf --execute='SELECT id, session_id, last_accessed FROM civicrm_session';
+-----+------------------------------------------------------------------+---------------------+
| id  | session_id                                                       | last_accessed       |
+-----+------------------------------------------------------------------+---------------------+
|   1 | b45c9b30b6a9c40cdf909d489775448d2964acddf129307d115710edafa4d244 | 2026-06-04 08:58:21 |
| 202 | 0f6933406eb0c823d026ea842dce99e4e0577c0451e7ae1b308ed5441a9aff95 | 2026-06-17 10:14:53 |
| 207 | 792414aff6979955724cf493f3d5924c580d7828f7e5a69a58622cba9daead90 | 2026-06-17 10:14:43 |
| 323 | 70fdc4de1db50ac2fb4bddedad6b7b4d51abb0ef2b12fef97e20721fdfa57c72 | 2026-06-25 21:48:54 |
| 344 | 3e24b3bae57fc87ee263495e695b28a956e3c6828352d9b7204ddf70c61f25a8 | 2026-06-25 22:01:58 |
| 353 | 1d9354d0a5e5e1dca1d7bf1c4044dfb376f4ed03c82d5d9d291490964169edd2 | 2026-06-25 22:03:42 |
| 369 | ec14fd793c0822da3c74e26d835cc241e2bfa23956894e7b51ab1f5cbf704cdb | 2026-06-25 22:57:27 |
| 373 | d63f84e9f43ebe0fed4ab658312ea823adec9be5480f9d9c9264a702ddb0be05 | 2026-07-02 10:14:21 |
+-----+------------------------------------------------------------------+---------------------+
ian@hp:~/ken8/mysql_data/usa_civi$ 


With "data"...

ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civi.cnf --execute='SELECT id, session_id, data, last_accessed FROM civicrm_session';

| id  | session_id                                                       |data             | last_accessed       |

|   1 | b45c9b30b6a9c40cdf909d489775448d2964acddf129307d115710edafa4d244 | CiviCRM|a:2:{s:12:"qfPrivateKey";
s:44:"mzSnN4LiFkfmlUjslR1VT96CwOkxig8INkB62ZhniLA="; 
s11:"qfSessionID";
s64:"b45c9b30b6a9c40cdf909d489775448d2964acddf129307d115710edafa4d244";}
| 2026-06-04 08:58:21 |

| 202 | 0f6933406eb0c823d026ea842dce99e4e0577c0451e7ae1b308ed5441a9aff95 | CiviCRM|a:0:{} | 2026-06-17 10:14:53 |
| 207 | 792414aff6979955724cf493f3d5924c580d7828f7e5a69a58622cba9daead90 | CiviCRM|a:0:{} | 2026-06-17 10:14:43 |
| 323 | 70fdc4de1db50ac2fb4bddedad6b7b4d51abb0ef2b12fef97e20721fdfa57c72 | CiviCRM|a:0:{} | 2026-06-25 21:48:54 |
| 344 | 3e24b3bae57fc87ee263495e695b28a956e3c6828352d9b7204ddf70c61f25a8 | CiviCRM|a:0:{} | 2026-06-25 22:01:58 |
| 353 | 1d9354d0a5e5e1dca1d7bf1c4044dfb376f4ed03c82d5d9d291490964169edd2 | CiviCRM|a:0:{} | 2026-06-25 22:03:42 |
| 369 | ec14fd793c0822da3c74e26d835cc241e2bfa23956894e7b51ab1f5cbf704cdb | CiviCRM|a:0:{} | 2026-06-25 22:57:27 |

| 373 | d63f84e9f43ebe0fed4ab658312ea823adec9be5480f9d9c9264a702ddb0be05 | CiviCRM|a:16:{s:4:"ufID";i:1;
s:6:"userID";i:2;
s:10:"lcMessages";
s:5:"en_AU";
s:10:"lastAccess";i:1782944026;
s:7:"authSrc";i:4;
s:12:"qfPrivateKey";
s:44:"oAtBV72+RxHnjFNorFgzivkC3OG+Ufe0qgxnKe3Jvpc=";
s:11:"qfSessionID";
s:64:"d63f84e9f43ebe0fed4ab658312ea823adec9be5480f9d9c9264a702ddb0be05";
s:8:"entryURL";
s:51:"http://civi.local.pc/civicrm/contact/search?reset=1";
s:7:"view.id";i:2;
s:16:"CRM_Utils_Recent";a:2:{i:0;a:16:{s:5:"title";
s:16:"Standalone Admin";
s:3:"url";
s:39:"/civicrm/contact/view?reset=1&amp;cid=2";
s:8:"view_url";
s:39:"/civicrm/contact/view?reset=1&amp;cid=2";
s:2:"id";i:2;
s:9:"entity_id";i:2;
s:4:"type";
s:7:"Contact";
s:11:"entity_type";
s:7:"Contact";
s:10:"contact_id";i:2;
s:11:"contactName";
s:16:"Standalone Admin";
s:7:"subtype";N;
s:9:"isDeleted";b:0;
s:10:"is_deleted";b:0;
s:9:"image_url";N;
s:8:"edit_url";
s:56:"/civicrm/contact/add?reset=1&amp;action=update&amp;cid=2";
s:10:"delete_url";N;
s:4:"icon";
s:7:"fa-user";}i:1;a:16:{s:5:"title";
s:11:"Ian Stewart";
s:3:"url";
s:39:"/civicrm/contact/view?reset=1&amp;cid=3";
s:8:"view_url";
s:39:"/civicrm/contact/view?reset=1&amp;cid=3";
s:2:"id";i:3;
s:9:"entity_id";i:3;
s:4:"type";
s:7:"Contact";
s:11:"entity_type";
s:7:"Contact";
s:10:"contact_id";i:3;
s:11:"contactName";
s:11:"Ian Stewart";
s:7:"subtype";N;
s:9:"isDeleted";b:0;
s:10:"is_deleted";b:0;
s:9:"image_url";N;
s:8:"edit_url";
s:56:"/civicrm/contact/add?reset=1&amp;action=update&amp;cid=3";
s:10:"delete_url";
s:59:"/civicrm/contact/view/delete?reset=1&amp;delete=1&amp;cid=3";
s:4:"icon";
s:7:"fa-user";}}s:11:"userContext";a:1:{i:0;
s:39:"/civicrm/contact/view?reset=1&amp;cid=2";}s:29:"CRM_Contact_Page_View_Summary";a:6:{s:3:"key";
s:77:"CRMContactControllerSearchDOiZ2FvdTZ2RG6dWe7mYsLtPTshe7bS5RRC5ADknZ2umNA_6633";
s:3:"cid";i:2;
s:6:"action";i:16;
s:11:"contactType";
s:10:"Individual";
s:14:"contactSubtype";
s:0:"";
s:13:"selectedChild";
s:7:"summary";}s:32:"CRM_Activity_Form_ActivityLinks_";a:3:{s:8:"entryURL";
s:164:"http://civi.local.pc/civicrm/contact/view?reset=1&amp;cid=2&amp;key=CRMContactControllerSearchDOiZ2FvdTZ2RG6dWe7mYsLtPTshe7bS5RRC5ADknZ2umNA_6633&amp;context=search";
s:5:"qfKey";N;
s:3:"cid";i:2;}s:21:"CRM_Profile_Page_View";a:3:{s:2:"id";i:1;
s:18:"is_show_email_task";i:1;
s:3:"gid";i:7;}s:24:"CRM_Profile_Page_Dynamic";a:3:{s:11:"multiRecord";N;
s:8:"recordId";N;
s:9:"allFields";N;}s:22:"CRM_Admin_Page_Options";a:2:{s:5:"gName";
s:8:"acl_role";
s:6:"action";i:16;}}_CRM_Activity_Form_ActivityLinks__container|a:4:{s:8:"defaults";a:0:{}s:9:"constants";a:0:{}s:6:"values";a:1:{s:13:"ActivityLinks";a:0:{}}s:5:"valid";a:1:{s:13:"ActivityLinks";N;}} 

| 2026-07-02 10:14:21 |


```
