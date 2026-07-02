# CMRT Migrate CiviCRM - 2

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
Using crm.cmrailtrail.org.au civi database:

This has staff (role=3), admin (role=2), and fundraising(role=4)

```
[cmrailtr@s03dd ~]$ mysql --defaults-file=/home/cmrailtr/.my_civi.cnf --execute='SELECT * FROM civicrm_user_role;'
+----+---------+---------+
| id | user_id | role_id |
+----+---------+---------+
|  3 |       2 |       2 |
|  4 |       1 |       2 |
|  7 |       3 |       3 |
|  8 |       4 |       2 |
|  9 |    NULL |       3 |
| 10 |    NULL |       4 |
| 11 |    NULL |       3 |
| 12 |       3 |       4 |
+----+---------+---------+
```

### civicrm_totp

Contains no data

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

### civicrm_role on crm.cmrailtrail.org.au

```
[cmrailtr@s03dd ~]$ mysql --defaults-file=/home/cmrailtr/.my_civi.cnf --execute='SELECT id, name, label, is_active FROM civicrm_role;'
+----+------------------+-------------------------------------+-----------+
| id | name             | label                               | is_active |
+----+------------------+-------------------------------------+-----------+
|  1 | everyone         | Everyone, including anonymous users |         1 |
|  2 | admin            | Administrator                       |         1 |
|  3 | staff            | Staff                               |         1 |
|  4 | campaign_manager | Campaign Manager                    |         1 |
+----+------------------+-------------------------------------+-----------+****
```
This additionally has...

```
| id | name             | label                               | permissions  | is_active |
|  4 | campaign_manager | Campaign Manager                    | 
administer CiviCampaign
manage campaign 

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

### civicrm_sessions on crm.railtrail.org.au

```
[cmrailtr@s03dd ~]$  mysql --defaults-file=/home/cmrailtr/.my_civi.cnf --execute='SHOW COLUMNS FROM civicrm_session';
+---------------+----------+------+-----+---------+----------------+
| Field         | Type     | Null | Key | Default | Extra          |
+---------------+----------+------+-----+---------+----------------+
| id            | int(11)  | NO   | PRI | NULL    | auto_increment |
| session_id    | char(64) | NO   | UNI | NULL    |                |
| data          | longtext | YES  |     | NULL    |                |
| last_accessed | datetime | YES  |     | NULL    |                |
+---------------+----------+------+-----+---------+----------------+

Witrhout "data"
[cmrailtr@s03dd ~]$  mysql --defaults-file=/home/cmrailtr/.my_civi.cnf --execute='SELECT id, session_id, last_accessed FROM civicrm_session';
+------+------------------------------------------------------------------+---------------------+
| id   | session_id                                                       | last_accessed       |
+------+------------------------------------------------------------------+---------------------+
|    1 | 8ff83e81d04f9962160671c8d2b6cd15f798504f0638d0e2081efb4b10a387b9 | 2026-05-16 21:06:31 |
|   19 | 14fc8379735546eed5ae5b99eb87a6581848862934addefe2841ca70bc41291d | 2026-05-16 21:18:42 |
|   25 | a27cb4192055b5e8b5a2001e5fb812aa7034259402b7b13675a9bd9daf99c67e | 2026-05-17 07:26:06 |
|   28 | 1fcddbced78cf5b051448de5ac6f2426880ce1a92cce611b44b8d76798ac7f03 | 2026-05-17 04:11:33 |
|   30 | 309db7bd5ba13a6c65c680299331bde7d306021f2af12ff634e208bc605549c9 | 2026-05-17 05:09:38 |
|   31 | 1b95a8a121b3e51aab3de86fed3617f25c364ea95ae1e80f7d6da399836c49a5 | 2026-05-17 05:09:35 |
|   35 | 3a99bdac57f871553790349afabcbbdcec986d87dbbaa8e8a3719d6ad00a89dd | 2026-07-02 08:14:23 |
|   84 | a74138524a6031e97cd30fcd3afe6faa3e044de6499431e32d3ad9c09c1bd1ba | 2026-05-17 08:23:13 |
|   86 | 50b6098a43b8b6b70ca6317b62d31f15a0ec6a656bc6e1108f0c72ad954ae451 | 2026-05-17 08:22:13 |
|   87 | 89d2b8bff6efc5dc619bf4134ef04b12eff2230728d30292e2a356a7f9d0f662 | 2026-05-17 08:22:13 |
|   89 | daafd16064c352a93d6b8d76b0adf6c61d99e64894c6717acb8eee8c6f62d44e | 2026-06-29 07:51:09 |
|  192 | 8e074fc6fcc452de4f8e980c35165b850a066c1b47466afe5544bba7de095dea | 2026-05-17 17:12:59 |
|  193 | 72f05b42993ac7ad7b5cf60d45ba3b9bccaac1ef1465945ee9b732c05e06ad24 | 2026-05-17 17:12:59 |
|  194 | f227a2f114cde6a2edc822db12f43df5e8473a033ecaaa096d6c931a2817961a | 2026-05-17 17:13:00 |
|  195 | 62f8aa6259963afc6e5e8921f3b79ea6844ffd6c87f64310287ad72cbfbf4eab | 2026-05-17 17:13:00 |
|  196 | c364a55d0c17810c115202498d02720d3f5a0ed9a6b67b9aeb1aa7554b00fb67 | 2026-05-17 17:13:01 |
|  197 | 805dd40988cf9492c5493c939e301db66766f5981586a3f46b85053a1203e5ef | 2026-05-17 17:13:02 |
|  198 | d0dd2371a7258ab4881d01b9b1a3b7ce643e6c8a1d910447be5babdcb1e917b4 | 2026-05-17 17:13:02 |
|  199 | f497ef20ea13741de013565fb616b720be6c2d5e84a92ef3d853a390e7e785f5 | 2026-05-17 17:13:03 |
|  203 | 8506139fc1ccfbeee00251a5d9f05fa02b9a1da1617968e12abec5fc0576c7fe | 2026-05-18 00:35:41 |
|  204 | af8809c8e1f45b48ff677337aa832abf53972d25a7d90f12391faa262de34f53 | 2026-05-18 02:13:16 |
|  205 | 921298134c72fcf8e1b6a8254d15ff766721669a290c7bb26ef33fb1fe05cf67 | 2026-05-18 02:13:19 |
|  206 | d611d1d2ac0f90b38d7337bd6a6e31e099ca0c7a995d486da5d24660d04f6ee6 | 2026-05-18 02:13:20 |
|  207 | 317cd6c7ece9f62c424704f9e1e46ef3a9af1d5beac995ded2403c3c56475f6a | 2026-05-18 05:15:41 |
|  208 | cd134f3589c02423d57a441646bc8a67028afa923718e63572d1a709a7d837b8 | 2026-05-18 05:15:43 |
|  209 | edbec08964784cb6dc99ff2676f5a4552477133874905d572828da611ca99f98 | 2026-05-18 07:58:36 |
|  210 | 8dc366844bddb1e15374c84f3e5d16a28d46e56c69c478525c392c5d9e4352dd | 2026-05-18 07:58:37 |
|  211 | 132d0897a07bfbbc6628b93b917eb9edad0ce418fb0e75df1dbfe9264e554cf0 | 2026-05-18 10:48:18 |
|  212 | 48cae153800dba0991f0f2a131d296ba5fe9314954c48a4931a8cda10f980513 | 2026-05-18 10:48:18 |
|  213 | 4774c4b256d5c1a362acb92342b152218d08445c838a1628cf5931970a94e1af | 2026-05-18 10:48:20 |
|  214 | db2e58e696955336a61b649990e96a6c6f6adc93ff3813201f61a8270069b646 | 2026-05-18 10:48:20 |
|  215 | 6a55b6617c4e27e6752671ad98cc6c9acee506248aa819cf79e22a5dafd993f0 | 2026-05-18 11:06:41 |
|  216 | dc30a174ecdb5c7d642247fd6edc80995bfcf680cfff8f78ab6493fbe6f736e9 | 2026-05-18 11:06:49 |
|  218 | ec2a0d40f7e83c465b253605658405805c8e361448e2c4973d858b2d1585240f | 2026-05-18 13:53:03 |
|  219 | b7aa9371c36ba49e9692c2e60f657966da839a1b08f8d3e51ef434311b8b6724 | 2026-05-18 13:53:03 |
|  220 | 40c7d4df2e5398fc6c2061404eadf3388c7456cf6427ca9faed6d32c32a331bd | 2026-05-18 13:53:04 |
|  221 | 8d981d57c5c38f584ac08b2d082c59078f57d660d71e44e60be5e8f2030fc3cf | 2026-05-18 13:53:04 |
|  225 | 4ceed9c905d308a9d54cb603fdc95aed4ab617a3e250a067bf99b4b520f8bd1b | 2026-05-18 18:09:53 |
|  226 | 90eb6b798b19e25f280989f2b04e99eca428aaa45b7d71b6aba9869cb353331e | 2026-05-19 05:17:31 |
|  227 | a4366d366bf7e0b5c5cd61d2c38bbf9c476b0f37e2681767f1c8609537b57cd8 | 2026-05-19 05:17:32 |
|  228 | de98f1d4155696d24f93290bd9445eed1b1dbc134abd33fd6483f9bf8f96d950 | 2026-05-19 05:53:19 |
|  229 | d67fc35275692bcf0bdf8d1fef276115f70cc2cbec74536d73f0aafb0d229060 | 2026-05-19 05:53:24 |
|  231 | c7ab2c8ad99a10ea29e2ccb76c74ff3d96e80a84636af9e6fa8140657b97dc37 | 2026-05-19 08:20:48 |
|  232 | d38bc92b68a4f1ce496b5b72235ad1456496882b807f0bd08921b250f52131d0 | 2026-05-19 08:20:49 |
|  233 | 6b80f968c611ab2867f2d480e92907a2b4d69bd934c87873a96f5a5ccdda6510 | 2026-05-19 08:47:47 |
|  241 | a86c5a584ee6a8b4876c85d80fbcf68f5debc2b6959e673bc5eceeae5b874427 | 2026-05-19 10:29:47 |
|  246 | eeb98aead4c8b9a7f2cc7e50db33c110a4c9cb299bbc3bc70d4847837250ee89 | 2026-05-19 11:40:07 |
|  247 | 122978c9f54ce2ffc65b31f71f7bda2903d3e8a0835bfc53c5cb96aa1cdb1951 | 2026-05-19 11:40:07 |
|  248 | 30f614b2137087969e48fa9e2eeb04947f0af8935cf0145dd3afae19c68e1679 | 2026-05-19 11:40:09 |
|  249 | 96b7f786763a2054bda093636d67eb5a866226a14e61880da5721c0d278d69d1 | 2026-05-19 11:40:09 |
|  250 | e5ad209174ca5e3bbc5b8bf9dca2ca8636004ecc5bb3f6c75d3586ff33b36c2c | 2026-05-19 13:49:34 |
|  255 | c0eb8f49c6c2eb0b558724a8c834df04e85b887b85c65a6e6f63bb691e5bdd84 | 2026-05-19 15:13:24 |
|  256 | 954a473e1dee1d9089f03a1216b9214a063a582fdef802999e5fabba0abca5c2 | 2026-05-19 15:13:24 |
|  257 | 2bb83977e6c22d330f8be989e2616037e26c01fd62e9654ece810244352afc7e | 2026-05-19 15:13:25 |
|  258 | 83017ba911f22523f39793aa356791248e9dda8237786dd4d6d64836635a6c18 | 2026-05-19 15:13:25 |
|  262 | 1025af250d090aab1c87f3f1b3deb64fb9aae552efd71ff3df47dbfcde3c2ba8 | 2026-05-19 21:56:48 |
|  263 | 57438d03213baf2ca55e7bc3f197fb9ada1534e6199b34502ae2237b26c504db | 2026-05-20 01:18:21 |
|  264 | d61aad132e324f60a386bd743e21ef07bdb394e855df5622f0d8cc9e2e354bbc | 2026-05-20 01:38:40 |
|  265 | 8988681ecbdceac160dd1e7276743b9bad9371c8ef9e2eb427d2a387d29edd73 | 2026-05-20 01:38:42 |
|  266 | c46f55c72665bc2bb9e3098cd6f50d1685c75fd4e16eafe51488c4a4e6d70d36 | 2026-05-20 03:41:26 |
|  267 | d04bea78d4b3d081fd90a0d7781558c19dd957fa5e5b59cb64637dfeadcdf167 | 2026-05-20 03:41:26 |
|  268 | 58e5cd35992a994214817ab34b5eab0c450cdc82738dcd6b719db041f5e70c6f | 2026-05-20 03:53:23 |
|  440 | 6ae92b7fdb39ba30c906a3a9ccdf65925787615f53fe2912c667b8cfbc3e564d | 2026-05-21 19:30:48 |
|  441 | 8458976f3154069a79bcfe33c49cbc6462f4d06f328d5274cadbd8e7e9850a02 | 2026-05-21 19:30:48 |
|  473 | 9255da7cf7145112d55dee918fa9367563491b4d324effd7d0e1c6d871e593ab | 2026-05-22 03:27:53 |
|  474 | df1f39520abfa627f21610447fc2030bcb25b284ad13d7b05640eff22ae85e19 | 2026-05-22 03:27:53 |
|  615 | eb2cf0c42d0a8fe9056ed3f6a242ede42dc9cd316d4eec5f80d9d3216fa814f0 | 2026-05-22 18:18:47 |
|  616 | 7631a733adb415e6877d117b64dbff3f27bdc5f27699068c2d84fbe4289c9c69 | 2026-05-22 18:18:48 |
|  647 | 73dd8a5858d9b1da27b10565c13b3ab10cbea0b6a664a83657fefd7dc8518c77 | 2026-05-24 12:14:58 |
|  648 | 507ff9b1b5809a281303593d476999fbb3de8f8c9493997b7841485b0a5841ad | 2026-05-24 18:27:13 |
|  649 | e8edf481bc65320ddb229d35f49ea792474a60607950222dd391f6b66190491d | 2026-05-24 18:27:15 |
|  650 | da1234706c6eb1e86a652064ab3f53d76374a6eb9e9e67862a4d4eb407ec8dbf | 2026-05-24 18:27:15 |
|  651 | 84410d709cfa3db75b6c99aa87b41dc16e0c4fa1127a52a785733d3189a4cf4e | 2026-05-24 18:27:15 |
|  652 | 0d758d43a6c8e7a127b2b6a4890ca3828311be0ca7476c8a115da95dedfae0d8 | 2026-05-24 21:31:51 |
|  653 | bb071e2fe3791afa0ad374611086ac3d3a9badcac0ca56a37d13fb106426ada6 | 2026-05-25 06:53:16 |
|  654 | 7ecd2a1015c6abe8c6943d7fce436d82abd1208c36107c31a876a6329adf59c5 | 2026-05-25 06:53:19 |
|  658 | 08d8625d28a2fbcd4ee0fe7ea534e2bceabe84f9189024b3d38edf646cea8f37 | 2026-05-25 09:55:46 |
|  667 | ffc23160e361ee0c31dd7f52b8c91b3e2808e97ea9a711501bb720bea7b8658c | 2026-05-25 09:55:49 |
|  676 | b50f768a198b091cd3fd35c2bd957c88ae8499b3f8a94a8a89b1afcfe7360a07 | 2026-05-25 15:20:00 |
|  681 | 00c6ce946478be4c67a88d5cd9d1c2e7c49102b7f1414a7f320f04243a62e99a | 2026-05-25 15:37:04 |
|  682 | 0ee9779fb1f85956695ba81ff9ced8cc802412d404f22639a92b9470eca0154c | 2026-05-25 15:37:04 |
|  686 | 5337caeeb5afc24a9dd4357bc6e28b5fceeb42b3f86dea606f38ee9db9383d94 | 2026-05-25 21:47:58 |
|  687 | 66553e47c50293e07601cf9c2fabf3eb290980948d7c44c24b07354be1dc82c8 | 2026-05-26 03:46:15 |
|  688 | b98209450c21a0806bd8e878cdda72344be377eae00f9201962ca64a6a69a549 | 2026-05-26 03:46:26 |
|  689 | 1d63cb7c98e140501dfbe7eb1c5c85998fd4be7e741a46f61fb1fb06d77b459e | 2026-05-26 04:15:46 |
|  690 | c71410221e697fed4d99bf07f142503c6f6b5342685da99d1855ec7370a9c34a | 2026-05-26 04:15:48 |
|  836 | e5d83eda6fe45f8c4b1612c0ce8274091772fbebfdd8f63f5dcfa3407fb1e5ac | 2026-05-26 19:35:48 |
|  838 | 377e7a9c2e00d0891e613a8d35abc2e61ac7cfbeadca974e4c930811ccb45157 | 2026-05-26 19:35:57 |
|  960 | 550090454430e7afea5dbdfca795b5c71731bb3ae81c3abe3b2e6839a3b7754f | 2026-05-28 19:47:06 |
|  966 | 781b539be6c3b5fc0e5eee7989035f954b67dc45c576df06a851a6682e9251c3 | 2026-05-30 04:59:57 |
| 1097 | e18bfe27a88e78a7964d515991110f24775cb55e5364cf6d04e7f177c54cbb29 | 2026-05-31 22:05:33 |
| 1099 | 64b45c7a0dc71117460e880dbce4c9cb08cdcb001b30859256c6b95736186f4f | 2026-05-31 19:02:36 |
| 1100 | 3d06be3e6c6bf21f32c554e6201202bec3438b05f969986fb14eaff3562539b6 | 2026-05-31 19:02:36 |
| 1128 | 3c203a3e26e3a968dde70b4439d65d231d18944f0e5b8e06e81581044a23d072 | 2026-05-31 20:13:16 |
| 1136 | 25eb203aefe2e891244e9d01ed1ed0b27df826e16b27731780a28809a82a843c | 2026-05-31 20:46:50 |
| 1144 | e59f2d7f5dad016671ae2171aa7bf1cc5a446a6bd11063d73c473f485c4509e0 | 2026-05-31 20:47:20 |
| 1155 | 204b1910e7c15f3be8b0175008e74fadb621079777c2c78f6ff5fc40761635a8 | 2026-05-31 21:19:44 |
| 1156 | 25d34aacaaec069bd3b1861feb594ef8a66dc2d0eeec1f76fbdbc853bce05583 | 2026-05-31 21:19:44 |
| 1157 | 35e6afa9d97ed0398b08d72b1a4044fd59bd46cdb056b856a34309ada0ca8964 | 2026-05-31 21:20:03 |
| 1158 | bb2d025275a675b948e2a8f4f7b696a4b26cdccc935b810bdbe99da0bfde8a2b | 2026-05-31 21:20:30 |
| 1159 | 3875b49508273ab8394ff0e277ac8ceac617ef00cf62502e1b7bb5035907eabb | 2026-05-31 21:20:51 |
| 1163 | c5bb49045ae454db2663f19edfd99803f2a25896f0673bf041d10e886e53f11c | 2026-05-31 21:25:03 |
| 1169 | 4218a9116f8883280c8da9105a31471a2c7a4a53975bcd9a22b30a87105a54b4 | 2026-05-31 21:26:34 |
| 1178 | 810f900a35efa108083c45816f103dfc73f64a57acf249c70c77e617c8e66478 | 2026-05-31 21:32:09 |
| 1184 | 512b92357c9deecb213777d9a66efe3c9289636db03970f23dc56d9a5ac9589a | 2026-05-31 21:32:45 |
| 1196 | 09da06d5647c42771b78b7ea5036c7aa7dba77cb164b7b8a5a4ffa7c4ebb1785 | 2026-06-01 03:07:46 |
| 1197 | bc80c4a29ad70d1b0605c64d063c23985c696baf720a77631b4f6e1beaa97d6b | 2026-06-01 03:07:49 |
| 1254 | a4d3cee680ccb6f5eb1ada53e66566de975e9bb2de7664c0423998fd1af90708 | 2026-06-01 13:00:56 |
| 1255 | 91f6e3c1a9a85f23d9d9e059ee2df4c19f98e57e40cdcdec3d15ed75ff1ad6f7 | 2026-06-01 13:01:10 |
| 1269 | d161031817d758045977ea10e0fc2ce46cd749f8cd4ad3c9f12be5c40681d884 | 2026-06-01 15:32:38 |
| 1270 | cae6a43332159df49e9d513968fecad855857eafea3fb4478241e77d65ab3910 | 2026-06-01 15:32:41 |
| 1288 | efb560e8492329f8bdc1b11fc384a7ae308fd6d2525c0ccecf2c4ef172e96e8d | 2026-06-01 20:17:28 |
| 1292 | 9a44b9bc0896b7a1dde08c200c0f27136a90ad05c17b98caf9f271c243859d6d | 2026-06-01 20:16:04 |
| 1294 | b566027f65292ca99d229d7a4aa5709acba153f055e935d9dad44039ca384f15 | 2026-06-01 20:16:05 |
| 1307 | 7cf2445f06a2470fc614b84adf7db69335c841930e5442def279998ae35b940e | 2026-06-02 08:16:28 |
| 1314 | ee54b44359d25c7a9aebb93b5690daaf932ae13a954679dac8ed5a811a4542a4 | 2026-06-01 20:29:33 |
| 1339 | 851d819fa681a5c0c43cb172116c31bc293b959cea5e388b221e625fc2ba7b1b | 2026-06-01 21:01:23 |
| 1368 | db559fde476893a3a47fd1268a542eaf1320ad8d37808d2fb5f836bae43b8f57 | 2026-06-02 09:42:35 |
| 1373 | 135587155e361ac580fd85bf60b271d4f2d043e32226a7b598fa8b3acf5209e5 | 2026-06-02 10:00:23 |
| 1379 | daf1c0d789a217b3a0db00d805806ec0dd6f9cd58201e6c586269c951a9bb7da | 2026-06-02 10:17:59 |
| 1390 | 8516ef1430f7114fa57a681e98a678768773b44811264c9534f2172b4a27cdda | 2026-06-02 10:23:05 |
| 1396 | 1a2a382057cf3b82d56ca9ace47eea3399522cc2cd4a99dcf3b1b509aeec7019 | 2026-06-03 08:20:18 |
| 1401 | a4ea4eb2f88e9fa2c9d0fcb033dd9bde309575e989f88e47bd204d2931545875 | 2026-06-02 10:29:31 |
| 1404 | f85c577bac9028a3fa835798d2cd5318b9701cac219d8fa19a0ddeaf7132368b | 2026-06-02 14:41:46 |
| 1405 | e1fd488acb35d8215bfae654356259bb73f8995efe74dbe6a940773e6fa4004f | 2026-06-02 14:41:47 |
| 1506 | cf989b7ea30c1f3348482f6639fd0ac1d9e6ca603ad912eab9bba99d8bccce2c | 2026-06-08 08:06:11 |
| 1513 | abbf85576042f6099da984aa315b3c016f3fa25f3a49838f0b43422cb84e9704 | 2026-06-03 21:34:31 |
| 1514 | 68669ff2da80e46288ad4ee6b703b349fd950ba13f299b54619fe0430ecaa3dc | 2026-06-03 21:34:33 |
| 1515 | cba6ea2575738ae2cb58ac50efc89482ad90ba6e07f024c0d9b570b0b41e5b04 | 2026-06-03 23:23:12 |
| 1516 | 7d4cc744d266d83339d65583ff5afdbf9879b4aeafcb3835eca1287ef2afce7e | 2026-06-03 23:23:13 |
| 1517 | 16cee3bb5cd54083916a5130ed0895df733defeb0aa0f7cd8c062de2d743c832 | 2026-06-04 01:01:52 |
| 1533 | 82cb8296982ea4e245b27a7542cf3cb0d0cbfce07fb69680b5f2c358dfde340f | 2026-06-04 16:57:59 |
| 1534 | 17549df12bdb37ea1461ea240092d4d694c84a209c1ec780f33d95164c51ab8f | 2026-06-04 17:06:01 |
| 1537 | 8e172b5cf5c457384b4b6d04fe6210b51895764f87b184595ec83ae5e1ee7660 | 2026-06-04 22:12:44 |
| 1539 | 1b427203b856297381f6a1d7041bd6c4b5c9ea8d93bd303a26bf0af09cef0a5f | 2026-06-04 22:12:52 |
| 1541 | 23439f2055dfaead5b1b7e866a8c9f1994d82d28e90f8c652440a10b7b354e0b | 2026-06-05 02:05:44 |
| 1542 | 8e56c7727c5b6d7f5e1d42984cd577edebf258132502c85758b109d55715a058 | 2026-06-05 02:05:46 |
| 1602 | d1bda448ba0ffa9e34dfcff1bd9e07a34d575f25735c4cd908402f35f321c6c7 | 2026-06-16 01:02:36 |
| 1612 | 8731c42593c5bc4f0230924ffea0084f76cb25b285872e77f33180d245617654 | 2026-06-16 09:55:32 |
| 1613 | bfbba753b594e486c99329e6f08ea5cd096687f366089ee93bc48ee8e2a5c794 | 2026-06-16 15:29:20 |
| 1614 | a0f2ca5d720c883ed1afe2a97621afdcf0deeb0dfbb29af600a90e2c6f39ef70 | 2026-06-17 02:15:32 |
| 1615 | b6ba1c78cf203d55d340bdd1db7a96bc299593c08ec1df8a62b1ed12a0b9b590 | 2026-06-17 02:15:33 |
| 1619 | 0bcf41f41b709cbe7d2f2f24b63598d8881583b584f615692220217e061ab087 | 2026-06-18 00:14:36 |
| 1626 | eff91379c438e434380597d1acf5e4baf78d73724beefeec0044b4ab64f01aec | 2026-06-18 16:02:22 |
| 1627 | 4524a9a622ace5206b0939f4c556de813520db0dc2aae2783a0aeb2c2409f4f0 | 2026-06-18 16:02:17 |
| 1646 | 8510943f1e74687d59cf3b46def3af2162d31b020c53f878b8f4187a67ea2590 | 2026-06-20 06:51:48 |
| 1648 | 87b1043ea719931a964b19cb5d371a39282fe9546247a4c0ce4c9990d1d1d372 | 2026-06-19 23:43:35 |
| 1650 | 5879ad421c29d166192f8b983ef267aae4128f2c6752cd22956cfc16ad648151 | 2026-06-20 03:54:38 |
| 1651 | cfdbcc8234462764e40a70b9757f62fb95352be4fc0a2798350d8c2521bafe2e | 2026-06-20 03:54:39 |
| 1661 | 8a429e175e7df32819bd21bcfca18d1301dcf2dc71cbfe53cc9a0a34ae3e7591 | 2026-06-20 21:56:04 |
| 1662 | 6876089293b45d087a4dd8dd2a32e75240321f981ca008c831026a92fcc62003 | 2026-06-21 06:53:26 |
| 1690 | 32085f90787cc198766aedc5a0f5ee42852b17d0e6d162d90707f723b91b3278 | 2026-06-24 01:31:29 |
| 1692 | 1fb6e73223902d008f6b21e4e63529ee169975e460af07ebd7c402373830d74a | 2026-06-24 01:31:37 |
| 1701 | 182aa4606c336194e7d3e4768c7ff136444aa8c04f421f648b88a6d2b5fffb41 | 2026-06-24 13:10:54 |
| 1716 | 88d96f1acecb0fdbdbb0ed11fa69939e8928581fc1694f9efe09a6fe36be4b06 | 2026-06-25 16:30:31 |
| 1717 | 99aa7a66a17b7707b9f7824d4f1eabbcc8dbc0f71fad582a4b4e765894ec060a | 2026-06-25 16:30:32 |
| 1728 | 2f191b7ff0e5d1616cd8b681805b6f45c864857f45b062731926a8d07654acd6 | 2026-06-26 18:42:41 |
| 1729 | e55292df38eff7870254a2723ecc6f535c90148e1cb22cb9cb5e844a7b336570 | 2026-06-26 18:42:42 |
| 1801 | 0b9b228e74b7e4e3808c9a054793b146e3a49e03cf87bb53a3259608d4db3242 | 2026-06-27 23:19:17 |
| 1803 | 0e35b68c5176bfb90fbf432fd236b742b48e8519bb965051fb04517ed8e762f3 | 2026-06-28 05:17:37 |
| 1804 | 6c5ad1caa0e641446e7b4de8f0e0c4c54ad998af8efd5f1897db9d2ce00eca18 | 2026-06-28 05:17:37 |
| 1829 | 00c2eedda228d0a1d9e6623ce786a77c02a0b844005dedb70234da9100909a30 | 2026-06-29 01:31:27 |
| 1830 | 1bbe4a1f627f547798b7e2b237943f8dfbff3c86f592f64863e3208d070deafd | 2026-06-29 01:31:28 |
| 1844 | 0e38e67aa68fc3ef66435d0fe4b2b213558534da6aa550438c0f9ae05e65c16f | 2026-06-29 15:01:00 |
| 1845 | 9f3a586e10855bbcf3920381747e09fae197805c19f844d2bc8682cc6a5f506a | 2026-06-30 03:52:26 |
| 1846 | 553972c9b8876ad5dfbe234efb9df82864b2d39e08f306d75c1bd6760ba80a20 | 2026-06-30 03:52:26 |
| 1847 | 45ddaad2ef0c4d8545bec9326ebbe6f44a48f84a7bb97ec5740a64b4feb7b055 | 2026-06-30 03:52:27 |
| 1848 | c82abf5d65436408906b86c13a123e11cbe832b6f8792ca184cd0718ebb6c87d | 2026-06-30 03:52:27 |
| 1857 | 3833c71df54babe55583cfe54769d9b4835a502c57681d78907433d922e186e1 | 2026-06-30 09:29:45 |
| 1868 | 5bbaa2173fb0e13593abb55d42a3a7e2ec41883dcf4c393b725739adea3e84b2 | 2026-07-01 12:33:59 |
| 1869 | 5569c8138203c8554f97fb903237ea88eae6e62ba4d7e092cc72c5cb45ef236e | 2026-07-01 12:33:59 |
| 1870 | 2af5e0eb51eef2962f6655ad0a831cd23215548083cc295a2ee259f895db5aae | 2026-07-01 12:34:00 |
| 1871 | d5d91d97e5aacb86d6a3ed1492223722596d4959ccc995e3844ea64ad9d02f37 | 2026-07-01 12:34:00 |
| 1882 | 37fcb77e3e83dcf1e52d1d2e76e7d2ce299ce48af091fc0d98c872c3a3ea1d5e | 2026-07-02 17:41:59 |
| 1884 | e5a535879652852063ca83556420a9329661aaf9bddf0fe5969aeca51d5420d6 | 2026-07-02 17:42:04 |
+------+------------------------------------------------------------------+---------------------+

```
Sample with "data"

```
                                                          | 2026-05-19 13:49:34 |
|  255 | c0eb8f49c6c2eb0b558724a8c834df04e85b887b85c65a6e6f63bb691e5bdd84 | CiviCRM|a:0:{}                                                          | 2026-05-19 15:13:24 |
|  256 | 954a473e1dee1d9089f03a1216b9214a063a582fdef802999e5fabba0abca5c2 | CiviCRM|a:0:{}                                                          | 2026-05-19 15:13:24 |
|  257 | 2bb83977e6c22d330f8be989e2616037e26c01fd62e9654ece810244352afc7e | CiviCRM|a:0:{}                                                          | 2026-05-19 15:13:25 |
|  258 | 83017ba911f22523f39793aa356791248e9dda8237786dd4d6d64836635a6c18 | CiviCRM|a:0:{}                                                          | 2026-05-19 15:13:25 |
|  262 | 1025af250d090aab1c87f3f1b3deb64fb9aae552efd71ff3df47dbfcde3c2ba8 | CiviCRM|a:0:{}                                                          | 2026-05-19 21:56:48 |
|  263 | 57438d03213baf2ca55e7bc3f197fb9ada1534e6199b34502ae2237b26c504db | CiviCRM|a:0:{}                                                          | 2026-05-20 01:18:21 |
|  264 | d61aad132e324f60a386bd743e21ef07bdb394e855df5622f0d8cc9e2e354bbc | CiviCRM|a:0:{}                                                          | 2026-05-20 01:38:40 |
|  265 | 8988681ecbdceac160dd1e7276743b9bad9371c8ef9e2eb427d2a387d29edd73 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"4/ZE5va92emzgAcPj7XUCiChP+w3z03kM1N6pOywTFU=";s:11:"qfSessionID";s:64:"8988681ecbdceac160dd1e7276743b9bad9371c8ef9e2eb427d2a387d29edd73";}                                                          | 2026-05-20 01:38:42 |
|  266 | c46f55c72665bc2bb9e3098cd6f50d1685c75fd4e16eafe51488c4a4e6d70d36 | CiviCRM|a:0:{}                                                          | 2026-05-20 03:41:26 |
|  267 | d04bea78d4b3d081fd90a0d7781558c19dd957fa5e5b59cb64637dfeadcdf167 | CiviCRM|a:0:{}                                                          | 2026-05-20 03:41:26 |
|  268 | 58e5cd35992a994214817ab34b5eab0c450cdc82738dcd6b719db041f5e70c6f | CiviCRM|a:0:{}                                                          | 2026-05-20 03:53:23 |
|  440 | 6ae92b7fdb39ba30c906a3a9ccdf65925787615f53fe2912c667b8cfbc3e564d | CiviCRM|a:0:{}                                                          | 2026-05-21 19:30:48 |
|  441 | 8458976f3154069a79bcfe33c49cbc6462f4d06f328d5274cadbd8e7e9850a02 | CiviCRM|a:0:{}                                                          | 2026-05-21 19:30:48 |
|  473 | 9255da7cf7145112d55dee918fa9367563491b4d324effd7d0e1c6d871e593ab | CiviCRM|a:0:{}                                                          | 2026-05-22 03:27:53 |
|  474 | df1f39520abfa627f21610447fc2030bcb25b284ad13d7b05640eff22ae85e19 | CiviCRM|a:0:{}                                                          | 2026-05-22 03:27:53 |
|  615 | eb2cf0c42d0a8fe9056ed3f6a242ede42dc9cd316d4eec5f80d9d3216fa814f0 | CiviCRM|a:0:{}                                                          | 2026-05-22 18:18:47 |
|  616 | 7631a733adb415e6877d117b64dbff3f27bdc5f27699068c2d84fbe4289c9c69 | CiviCRM|a:0:{}                                                          | 2026-05-22 18:18:48 |
|  647 | 73dd8a5858d9b1da27b10565c13b3ab10cbea0b6a664a83657fefd7dc8518c77 | CiviCRM|a:0:{}                                                          | 2026-05-24 12:14:58 |
|  648 | 507ff9b1b5809a281303593d476999fbb3de8f8c9493997b7841485b0a5841ad | CiviCRM|a:0:{}                                                          | 2026-05-24 18:27:13 |
|  649 | e8edf481bc65320ddb229d35f49ea792474a60607950222dd391f6b66190491d | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"y5iGE0x5Unxc37NFGuQo0D3m53cVSiCHKfxHFaY38iU=";s:11:"qfSessionID";s:64:"e8edf481bc65320ddb229d35f49ea792474a60607950222dd391f6b66190491d";}                                                          | 2026-05-24 18:27:15 |
|  650 | da1234706c6eb1e86a652064ab3f53d76374a6eb9e9e67862a4d4eb407ec8dbf | CiviCRM|a:0:{}                                                          | 2026-05-24 18:27:15 |
|  651 | 84410d709cfa3db75b6c99aa87b41dc16e0c4fa1127a52a785733d3189a4cf4e | CiviCRM|a:0:{}                                                          | 2026-05-24 18:27:15 |
|  652 | 0d758d43a6c8e7a127b2b6a4890ca3828311be0ca7476c8a115da95dedfae0d8 | CiviCRM|a:0:{}                                                          | 2026-05-24 21:31:51 |
|  653 | bb071e2fe3791afa0ad374611086ac3d3a9badcac0ca56a37d13fb106426ada6 | CiviCRM|a:0:{}                                                          | 2026-05-25 06:53:16 |
|  654 | 7ecd2a1015c6abe8c6943d7fce436d82abd1208c36107c31a876a6329adf59c5 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"oCCcgtrZO9UfzB7cOEzdaTA2Nzhl9bA3RAgxRj1ci4A=";s:11:"qfSessionID";s:64:"7ecd2a1015c6abe8c6943d7fce436d82abd1208c36107c31a876a6329adf59c5";}                                                          | 2026-05-25 06:53:19 |
|  658 | 08d8625d28a2fbcd4ee0fe7ea534e2bceabe84f9189024b3d38edf646cea8f37 | CiviCRM|a:0:{}                                                          | 2026-05-25 09:55:46 |
|  667 | ffc23160e361ee0c31dd7f52b8c91b3e2808e97ea9a711501bb720bea7b8658c | CiviCRM|a:7:{s:4:"ufID";i:1;s:6:"userID";i:2;s:10:"lastAccess";i:1779666946;s:7:"authSrc";i:4;s:12:"qfPrivateKey";s:44:"61eAQRBQjbR5sDelWmjbnVe8DdkiCXLZcrsdDC/VAas=";s:11:"qfSessionID";s:64:"ffc23160e361ee0c31dd7f52b8c91b3e2808e97ea9a711501bb720bea7b8658c";s:11:"userContext";a:0:{}}                                                          | 2026-05-25 09:55:49 |
|  676 | b50f768a198b091cd3fd35c2bd957c88ae8499b3f8a94a8a89b1afcfe7360a07 | CiviCRM|a:0:{}                                                          | 2026-05-25 15:20:00 |
|  681 | 00c6ce946478be4c67a88d5cd9d1c2e7c49102b7f1414a7f320f04243a62e99a | CiviCRM|a:0:{}                                                          | 2026-05-25 15:37:04 |
|  682 | 0ee9779fb1f85956695ba81ff9ced8cc802412d404f22639a92b9470eca0154c | CiviCRM|a:0:{}                                                          | 2026-05-25 15:37:04 |
|  686 | 5337caeeb5afc24a9dd4357bc6e28b5fceeb42b3f86dea606f38ee9db9383d94 | CiviCRM|a:0:{}                                                          | 2026-05-25 21:47:58 |
|  687 | 66553e47c50293e07601cf9c2fabf3eb290980948d7c44c24b07354be1dc82c8 | CiviCRM|a:0:{}                                                          | 2026-05-26 03:46:15 |
|  688 | b98209450c21a0806bd8e878cdda72344be377eae00f9201962ca64a6a69a549 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"S1cblMLCYbKhRCCRKkc8xxcJQTsMRAWUwjZBo3xNKY8=";s:11:"qfSessionID";s:64:"b98209450c21a0806bd8e878cdda72344be377eae00f9201962ca64a6a69a549";}                                                          | 2026-05-26 03:46:26 |
|  689 | 1d63cb7c98e140501dfbe7eb1c5c85998fd4be7e741a46f61fb1fb06d77b459e | CiviCRM|a:0:{}                                                          | 2026-05-26 04:15:46 |
|  690 | c71410221e697fed4d99bf07f142503c6f6b5342685da99d1855ec7370a9c34a | CiviCRM|a:0:{}                                                          | 2026-05-26 04:15:48 |
|  836 | e5d83eda6fe45f8c4b1612c0ce8274091772fbebfdd8f63f5dcfa3407fb1e5ac | CiviCRM|a:0:{}                                                          | 2026-05-26 19:35:48 |
|  838 | 377e7a9c2e00d0891e613a8d35abc2e61ac7cfbeadca974e4c930811ccb45157 | CiviCRM|a:0:{}                                                          | 2026-05-26 19:35:57 |
|  960 | 550090454430e7afea5dbdfca795b5c71731bb3ae81c3abe3b2e6839a3b7754f | CiviCRM|a:0:{}                                                          | 2026-05-28 19:47:06 |
|  966 | 781b539be6c3b5fc0e5eee7989035f954b67dc45c576df06a851a6682e9251c3 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"QAUFRI9b+Xw4vrGWbbrXXwiKRjQI/skNXVie+bI+ZvI=";s:11:"qfSessionID";s:64:"781b539be6c3b5fc0e5eee7989035f954b67dc45c576df06a851a6682e9251c3";}                                                          | 2026-05-30 04:59:57 |
| 1097 | e18bfe27a88e78a7964d515991110f24775cb55e5364cf6d04e7f177c54cbb29 | CiviCRM|a:0:{}                                                          | 2026-05-31 22:05:33 |
| 1099 | 64b45c7a0dc71117460e880dbce4c9cb08cdcb001b30859256c6b95736186f4f | CiviCRM|a:0:{}                                                          | 2026-05-31 19:02:36 |
| 1100 | 3d06be3e6c6bf21f32c554e6201202bec3438b05f969986fb14eaff3562539b6 | CiviCRM|a:0:{}                                                          | 2026-05-31 19:02:36 |
| 1128 | 3c203a3e26e3a968dde70b4439d65d231d18944f0e5b8e06e81581044a23d072 | CiviCRM|a:0:{}                                                          | 2026-05-31 20:13:16 |
| 1136 | 25eb203aefe2e891244e9d01ed1ed0b27df826e16b27731780a28809a82a843c | CiviCRM|a:0:{}                                                          | 2026-05-31 20:46:50 |
| 1144 | e59f2d7f5dad016671ae2171aa7bf1cc5a446a6bd11063d73c473f485c4509e0 | CiviCRM|a:0:{}                                                          | 2026-05-31 20:47:20 |
| 1155 | 204b1910e7c15f3be8b0175008e74fadb621079777c2c78f6ff5fc40761635a8 | CiviCRM|a:0:{}                                                          | 2026-05-31 21:19:44 |
| 1156 | 25d34aacaaec069bd3b1861feb594ef8a66dc2d0eeec1f76fbdbc853bce05583 | CiviCRM|a:0:{}                                                          | 2026-05-31 21:19:44 |
| 1157 | 35e6afa9d97ed0398b08d72b1a4044fd59bd46cdb056b856a34309ada0ca8964 | CiviCRM|a:0:{}                                                          | 2026-05-31 21:20:03 |
| 1158 | bb2d025275a675b948e2a8f4f7b696a4b26cdccc935b810bdbe99da0bfde8a2b | CiviCRM|a:0:{}                                                          | 2026-05-31 21:20:30 |
| 1159 | 3875b49508273ab8394ff0e277ac8ceac617ef00cf62502e1b7bb5035907eabb | CiviCRM|a:0:{}                                                          | 2026-05-31 21:20:51 |
| 1163 | c5bb49045ae454db2663f19edfd99803f2a25896f0673bf041d10e886e53f11c | CiviCRM|a:0:{}                                                          | 2026-05-31 21:25:03 |
| 1169 | 4218a9116f8883280c8da9105a31471a2c7a4a53975bcd9a22b30a87105a54b4 | CiviCRM|a:0:{}                                                          | 2026-05-31 21:26:34 |
| 1178 | 810f900a35efa108083c45816f103dfc73f64a57acf249c70c77e617c8e66478 | CiviCRM|a:0:{}                                                          | 2026-05-31 21:32:09 |
| 1184 | 512b92357c9deecb213777d9a66efe3c9289636db03970f23dc56d9a5ac9589a | CiviCRM|a:0:{}                                                          | 2026-05-31 21:32:45 |
| 1196 | 09da06d5647c42771b78b7ea5036c7aa7dba77cb164b7b8a5a4ffa7c4ebb1785 | CiviCRM|a:0:{}                                                          | 2026-06-01 03:07:46 |
| 1197 | bc80c4a29ad70d1b0605c64d063c23985c696baf720a77631b4f6e1beaa97d6b | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"o0sdKc8MUTi2xHA/t0+5BhylYEHpsJD9XCGdmLhzm8E=";s:11:"qfSessionID";s:64:"bc80c4a29ad70d1b0605c64d063c23985c696baf720a77631b4f6e1beaa97d6b";}                                                          | 2026-06-01 03:07:49 |
| 1254 | a4d3cee680ccb6f5eb1ada53e66566de975e9bb2de7664c0423998fd1af90708 | CiviCRM|a:0:{}                                                          | 2026-06-01 13:00:56 |
| 1255 | 91f6e3c1a9a85f23d9d9e059ee2df4c19f98e57e40cdcdec3d15ed75ff1ad6f7 | CiviCRM|a:0:{}                                                          | 2026-06-01 13:01:10 |
| 1269 | d161031817d758045977ea10e0fc2ce46cd749f8cd4ad3c9f12be5c40681d884 | CiviCRM|a:0:{}                                                          | 2026-06-01 15:32:38 |
| 1270 | cae6a43332159df49e9d513968fecad855857eafea3fb4478241e77d65ab3910 | CiviCRM|a:1:{s:6:"status";a:1:{i:0;a:4:{s:4:"text";s:99:"There is a validation error with your HTML input. Your activity is a bit suspicious, hence aborting";s:5:"title";s:5:"Error";s:4:"type";s:5:"error";s:7:"options";N;}}}                                                          | 2026-06-01 15:32:41 |
| 1288 | efb560e8492329f8bdc1b11fc384a7ae308fd6d2525c0ccecf2c4ef172e96e8d | CiviCRM|a:0:{}                                                          | 2026-06-01 20:17:28 |
| 1292 | 9a44b9bc0896b7a1dde08c200c0f27136a90ad05c17b98caf9f271c243859d6d | CiviCRM|a:0:{}                                                          | 2026-06-01 20:16:04 |
| 1294 | b566027f65292ca99d229d7a4aa5709acba153f055e935d9dad44039ca384f15 | CiviCRM|a:0:{}                                                          | 2026-06-01 20:16:05 |
| 1307 | 7cf2445f06a2470fc614b84adf7db69335c841930e5442def279998ae35b940e | CiviCRM|a:0:{}                                                          | 2026-06-02 08:16:28 |
| 1314 | ee54b44359d25c7a9aebb93b5690daaf932ae13a954679dac8ed5a811a4542a4 | CiviCRM|a:0:{}                                                          | 2026-06-01 20:29:33 |
| 1339 | 851d819fa681a5c0c43cb172116c31bc293b959cea5e388b221e625fc2ba7b1b | CiviCRM|a:0:{}                                                          | 2026-06-01 21:01:23 |
| 1368 | db559fde476893a3a47fd1268a542eaf1320ad8d37808d2fb5f836bae43b8f57 | CiviCRM|a:0:{}                                                          | 2026-06-02 09:42:35 |
| 1373 | 135587155e361ac580fd85bf60b271d4f2d043e32226a7b598fa8b3acf5209e5 | CiviCRM|a:0:{}                                                          | 2026-06-02 10:00:23 |
| 1379 | daf1c0d789a217b3a0db00d805806ec0dd6f9cd58201e6c586269c951a9bb7da | CiviCRM|a:0:{}                                                          | 2026-06-02 10:17:59 |
| 1390 | 8516ef1430f7114fa57a681e98a678768773b44811264c9534f2172b4a27cdda | CiviCRM|a:0:{}                                                          | 2026-06-02 10:23:05 |
| 1396 | 1a2a382057cf3b82d56ca9ace47eea3399522cc2cd4a99dcf3b1b509aeec7019 | CiviCRM|a:0:{}                                                          | 2026-06-03 08:20:18 |
| 1401 | a4ea4eb2f88e9fa2c9d0fcb033dd9bde309575e989f88e47bd204d2931545875 | CiviCRM|a:0:{}                                                          | 2026-06-02 10:29:31 |
| 1404 | f85c577bac9028a3fa835798d2cd5318b9701cac219d8fa19a0ddeaf7132368b | CiviCRM|a:0:{}                                                          | 2026-06-02 14:41:46 |
| 1405 | e1fd488acb35d8215bfae654356259bb73f8995efe74dbe6a940773e6fa4004f | CiviCRM|a:1:{s:6:"status";a:1:{i:0;a:4:{s:4:"text";s:99:"There is a validation error with your HTML input. Your activity is a bit suspicious, hence aborting";s:5:"title";s:5:"Error";s:4:"type";s:5:"error";s:7:"options";N;}}}                                                          | 2026-06-02 14:41:47 |
| 1506 | cf989b7ea30c1f3348482f6639fd0ac1d9e6ca603ad912eab9bba99d8bccce2c | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"jEs5ywYv8QD96Pr1+2mq18PPLO4MKQHv5mqJ70vSFQk=";s:11:"qfSessionID";s:64:"cf989b7ea30c1f3348482f6639fd0ac1d9e6ca603ad912eab9bba99d8bccce2c";}                                                          | 2026-06-08 08:06:11 |
| 1513 | abbf85576042f6099da984aa315b3c016f3fa25f3a49838f0b43422cb84e9704 | CiviCRM|a:0:{}                                                          | 2026-06-03 21:34:31 |
| 1514 | 68669ff2da80e46288ad4ee6b703b349fd950ba13f299b54619fe0430ecaa3dc | CiviCRM|a:0:{}                                                          | 2026-06-03 21:34:33 |
| 1515 | cba6ea2575738ae2cb58ac50efc89482ad90ba6e07f024c0d9b570b0b41e5b04 | CiviCRM|a:0:{}                                                          | 2026-06-03 23:23:12 |
| 1516 | 7d4cc744d266d83339d65583ff5afdbf9879b4aeafcb3835eca1287ef2afce7e | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"TFoTZ/oeKlUCeTs6bwH6z3L2RbM6jpFpov8SgI4T4oc=";s:11:"qfSessionID";s:64:"7d4cc744d266d83339d65583ff5afdbf9879b4aeafcb3835eca1287ef2afce7e";}                                                          | 2026-06-03 23:23:13 |
| 1517 | 16cee3bb5cd54083916a5130ed0895df733defeb0aa0f7cd8c062de2d743c832 | CiviCRM|a:0:{}                                                          | 2026-06-04 01:01:52 |
| 1533 | 82cb8296982ea4e245b27a7542cf3cb0d0cbfce07fb69680b5f2c358dfde340f | CiviCRM|a:0:{}                                                          | 2026-06-04 16:57:59 |
| 1534 | 17549df12bdb37ea1461ea240092d4d694c84a209c1ec780f33d95164c51ab8f | CiviCRM|a:0:{}                                                          | 2026-06-04 17:06:01 |
| 1537 | 8e172b5cf5c457384b4b6d04fe6210b51895764f87b184595ec83ae5e1ee7660 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"lIE03d9igU7T6ZaioUAlRJ3UOwtMh9QqOmgj+Mxe9YY=";s:11:"qfSessionID";s:64:"8e172b5cf5c457384b4b6d04fe6210b51895764f87b184595ec83ae5e1ee7660";}                                                          | 2026-06-04 22:12:44 |
| 1539 | 1b427203b856297381f6a1d7041bd6c4b5c9ea8d93bd303a26bf0af09cef0a5f | CiviCRM|a:0:{}                                                          | 2026-06-04 22:12:52 |
| 1541 | 23439f2055dfaead5b1b7e866a8c9f1994d82d28e90f8c652440a10b7b354e0b | CiviCRM|a:0:{}                                                          | 2026-06-05 02:05:44 |
| 1542 | 8e56c7727c5b6d7f5e1d42984cd577edebf258132502c85758b109d55715a058 | CiviCRM|a:0:{}                                                          | 2026-06-05 02:05:46 |
| 1602 | d1bda448ba0ffa9e34dfcff1bd9e07a34d575f25735c4cd908402f35f321c6c7 | CiviCRM|a:0:{}                                                          | 2026-06-16 01:02:36 |
| 1612 | 8731c42593c5bc4f0230924ffea0084f76cb25b285872e77f33180d245617654 | CiviCRM|a:0:{}                                                          | 2026-06-16 09:55:32 |
| 1613 | bfbba753b594e486c99329e6f08ea5cd096687f366089ee93bc48ee8e2a5c794 | CiviCRM|a:0:{}                                                          | 2026-06-16 15:29:20 |
| 1614 | a0f2ca5d720c883ed1afe2a97621afdcf0deeb0dfbb29af600a90e2c6f39ef70 | CiviCRM|a:0:{}                                                          | 2026-06-17 02:15:32 |
| 1615 | b6ba1c78cf203d55d340bdd1db7a96bc299593c08ec1df8a62b1ed12a0b9b590 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"LwUo3MTitgKXuEiqCw95T4vzZ6ijzHORBAhwdyA4CWo=";s:11:"qfSessionID";s:64:"b6ba1c78cf203d55d340bdd1db7a96bc299593c08ec1df8a62b1ed12a0b9b590";}                                                          | 2026-06-17 02:15:33 |
| 1619 | 0bcf41f41b709cbe7d2f2f24b63598d8881583b584f615692220217e061ab087 | CiviCRM|a:0:{}                                                          | 2026-06-18 00:14:36 |
| 1626 | eff91379c438e434380597d1acf5e4baf78d73724beefeec0044b4ab64f01aec | CiviCRM|a:0:{}                                                          | 2026-06-18 16:02:22 |
| 1627 | 4524a9a622ace5206b0939f4c556de813520db0dc2aae2783a0aeb2c2409f4f0 | CiviCRM|a:0:{}                                                          | 2026-06-18 16:02:17 |
| 1646 | 8510943f1e74687d59cf3b46def3af2162d31b020c53f878b8f4187a67ea2590 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"P2b1vQypEd36siw7Wo8WapOejNIK3LukY3jchng8c8c=";s:11:"qfSessionID";s:64:"8510943f1e74687d59cf3b46def3af2162d31b020c53f878b8f4187a67ea2590";}                                                          | 2026-06-20 06:51:48 |
| 1648 | 87b1043ea719931a964b19cb5d371a39282fe9546247a4c0ce4c9990d1d1d372 | CiviCRM|a:0:{}                                                          | 2026-06-19 23:43:35 |
| 1650 | 5879ad421c29d166192f8b983ef267aae4128f2c6752cd22956cfc16ad648151 | CiviCRM|a:0:{}                                                          | 2026-06-20 03:54:38 |
| 1651 | cfdbcc8234462764e40a70b9757f62fb95352be4fc0a2798350d8c2521bafe2e | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"zuxFMVv1ikSql0RAFcuF8XuhOYYm0g/IRkcqEjUM4Tw=";s:11:"qfSessionID";s:64:"cfdbcc8234462764e40a70b9757f62fb95352be4fc0a2798350d8c2521bafe2e";}                                                          | 2026-06-20 03:54:39 |
| 1661 | 8a429e175e7df32819bd21bcfca18d1301dcf2dc71cbfe53cc9a0a34ae3e7591 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"EMzr4KQtDZlYgJ0vRzvkAYzn1II7UORKjb1vRe006u8=";s:11:"qfSessionID";s:64:"8a429e175e7df32819bd21bcfca18d1301dcf2dc71cbfe53cc9a0a34ae3e7591";}                                                          | 2026-06-20 21:56:04 |
| 1662 | 6876089293b45d087a4dd8dd2a32e75240321f981ca008c831026a92fcc62003 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"0DW7ndBD2A0EVFBV7WuXJQOx+YZXqMDKO+6QxJD6Crk=";s:11:"qfSessionID";s:64:"6876089293b45d087a4dd8dd2a32e75240321f981ca008c831026a92fcc62003";}                                                          | 2026-06-21 06:53:26 |
| 1690 | 32085f90787cc198766aedc5a0f5ee42852b17d0e6d162d90707f723b91b3278 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"Wbq0JgkF0EeE/thHKf40S1A4MLSLp4XbnrKTmnBc0Ns=";s:11:"qfSessionID";s:64:"32085f90787cc198766aedc5a0f5ee42852b17d0e6d162d90707f723b91b3278";}                                                          | 2026-06-24 01:31:29 |
| 1692 | 1fb6e73223902d008f6b21e4e63529ee169975e460af07ebd7c402373830d74a | CiviCRM|a:0:{}                                                          | 2026-06-24 01:31:37 |
| 1701 | 182aa4606c336194e7d3e4768c7ff136444aa8c04f421f648b88a6d2b5fffb41 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"ZvrT1pw4MLb3tBv11Gli2yxgvTcbz9RmD/POlQXKQcc=";s:11:"qfSessionID";s:64:"182aa4606c336194e7d3e4768c7ff136444aa8c04f421f648b88a6d2b5fffb41";}                                                          | 2026-06-24 13:10:54 |
| 1716 | 88d96f1acecb0fdbdbb0ed11fa69939e8928581fc1694f9efe09a6fe36be4b06 | CiviCRM|a:0:{}                                                          | 2026-06-25 16:30:31 |
| 1717 | 99aa7a66a17b7707b9f7824d4f1eabbcc8dbc0f71fad582a4b4e765894ec060a | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"88dTJx9wURZWAGleNRvALls68r6tLShqO8am1+wwY8s=";s:11:"qfSessionID";s:64:"99aa7a66a17b7707b9f7824d4f1eabbcc8dbc0f71fad582a4b4e765894ec060a";}                                                          | 2026-06-25 16:30:32 |
| 1728 | 2f191b7ff0e5d1616cd8b681805b6f45c864857f45b062731926a8d07654acd6 | CiviCRM|a:0:{}                                                          | 2026-06-26 18:42:41 |
| 1729 | e55292df38eff7870254a2723ecc6f535c90148e1cb22cb9cb5e844a7b336570 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"O4QHFRsPEIDp3FmmxQBY6c1v/lLMufwvpai7IaOc0Ac=";s:11:"qfSessionID";s:64:"e55292df38eff7870254a2723ecc6f535c90148e1cb22cb9cb5e844a7b336570";}                                                          | 2026-06-26 18:42:42 |
| 1801 | 0b9b228e74b7e4e3808c9a054793b146e3a49e03cf87bb53a3259608d4db3242 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"WDQYn0VuTvWMrYS4aO3vaXLlWLrqlp8X/35cH9r/o1s=";s:11:"qfSessionID";s:64:"0b9b228e74b7e4e3808c9a054793b146e3a49e03cf87bb53a3259608d4db3242";}                                                          | 2026-06-27 23:19:17 |
| 1803 | 0e35b68c5176bfb90fbf432fd236b742b48e8519bb965051fb04517ed8e762f3 | CiviCRM|a:0:{}                                                          | 2026-06-28 05:17:37 |
| 1804 | 6c5ad1caa0e641446e7b4de8f0e0c4c54ad998af8efd5f1897db9d2ce00eca18 | CiviCRM|a:0:{}                                                          | 2026-06-28 05:17:37 |
| 1829 | 00c2eedda228d0a1d9e6623ce786a77c02a0b844005dedb70234da9100909a30 | CiviCRM|a:0:{}                                                          | 2026-06-29 01:31:27 |
| 1830 | 1bbe4a1f627f547798b7e2b237943f8dfbff3c86f592f64863e3208d070deafd | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"ZlVZUwyQSEMO3KkXGcbhW88yD+/2y3Qe6LrwLf1JAFk=";s:11:"qfSessionID";s:64:"1bbe4a1f627f547798b7e2b237943f8dfbff3c86f592f64863e3208d070deafd";}                                                          | 2026-06-29 01:31:28 |
| 1844 | 0e38e67aa68fc3ef66435d0fe4b2b213558534da6aa550438c0f9ae05e65c16f | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"D3+8Kfm4r1NjwMuiuZL8HpdEY942E0VKQ6bOM3DDWZg=";s:11:"qfSessionID";s:64:"0e38e67aa68fc3ef66435d0fe4b2b213558534da6aa550438c0f9ae05e65c16f";}                                                          | 2026-06-29 15:01:00 |
| 1845 | 9f3a586e10855bbcf3920381747e09fae197805c19f844d2bc8682cc6a5f506a | CiviCRM|a:0:{}                                                          | 2026-06-30 03:52:26 |
| 1846 | 553972c9b8876ad5dfbe234efb9df82864b2d39e08f306d75c1bd6760ba80a20 | CiviCRM|a:0:{}                                                          | 2026-06-30 03:52:26 |
| 1847 | 45ddaad2ef0c4d8545bec9326ebbe6f44a48f84a7bb97ec5740a64b4feb7b055 | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"GtkNlceRs7Ihv1QxbfzLpJcId85R4nEJD18e6QjbzLw=";s:11:"qfSessionID";s:64:"45ddaad2ef0c4d8545bec9326ebbe6f44a48f84a7bb97ec5740a64b4feb7b055";}                                                          | 2026-06-30 03:52:27 |
| 1848 | c82abf5d65436408906b86c13a123e11cbe832b6f8792ca184cd0718ebb6c87d | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"SYEi0ZgO2r8M8cmtqAaPFhwrNkHnR6YRcmd7U9rAqLM=";s:11:"qfSessionID";s:64:"c82abf5d65436408906b86c13a123e11cbe832b6f8792ca184cd0718ebb6c87d";}                                                          | 2026-06-30 03:52:27 |
| 1857 | 3833c71df54babe55583cfe54769d9b4835a502c57681d78907433d922e186e1 | CiviCRM|a:0:{}                                                          | 2026-06-30 09:29:45 |
| 1868 | 5bbaa2173fb0e13593abb55d42a3a7e2ec41883dcf4c393b725739adea3e84b2 | CiviCRM|a:0:{}                                                          | 2026-07-01 12:33:59 |
| 1869 | 5569c8138203c8554f97fb903237ea88eae6e62ba4d7e092cc72c5cb45ef236e | CiviCRM|a:0:{}                                                          | 2026-07-01 12:33:59 |
| 1870 | 2af5e0eb51eef2962f6655ad0a831cd23215548083cc295a2ee259f895db5aae | CiviCRM|a:0:{}                                                          | 2026-07-01 12:34:00 |
| 1871 | d5d91d97e5aacb86d6a3ed1492223722596d4959ccc995e3844ea64ad9d02f37 | CiviCRM|a:0:{}                                                          | 2026-07-01 12:34:00 |
| 1882 | 37fcb77e3e83dcf1e52d1d2e76e7d2ce299ce48af091fc0d98c872c3a3ea1d5e | CiviCRM|a:2:{s:12:"qfPrivateKey";s:44:"HtQU/mJG1GoWw3GitpENbFq6hNVRumcCeK1/lhhy5qg=";s:11:"qfSessionID";s:64:"37fcb77e3e83dcf1e52d1d2e76e7d2ce299ce48af091fc0d98c872c3a3ea1d5e";}                                                          | 2026-07-02 17:41:59 |
| 1884 | e5a535879652852063ca83556420a9329661aaf9bddf0fe5969aeca51d5420d6 | CiviCRM|a:0:{}                                                          | 2026-07-02 17:42:04 |
```

## Mosaico

Mosaico adds to tables to CiviCRM

* civicrm_mosaico_template
* civicrm_mosaico_msg_template

### civicrm_mosaico_template

```
$ mysql --defaults-file=/home/ian/.my_civiusa.cnf --execute='SHOW COLUMNS FROM civicrm_mosaico_template';
+-------------+------------------+------+-----+---------+----------------+
| Field       | Type             | Null | Key | Default | Extra          |
+-------------+------------------+------+-----+---------+----------------+
| id          | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| title       | varchar(255)     | YES  |     | NULL    |                |
| base        | varchar(64)      | YES  |     | NULL    |                |
| html        | longtext         | YES  |     | NULL    |                |
| metadata    | longtext         | YES  |     | NULL    |                |
| content     | longtext         | YES  |     | NULL    |                |
| msg_tpl_id  | int(10) unsigned | YES  | MUL | NULL    |                |
| category_id | int(10) unsigned | YES  |     | NULL    |                |
| domain_id   | int(10) unsigned | YES  | MUL | NULL    |                |
+-------------+------------------+------+-----+---------+----------------+

ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civiusa.cnf --execute='SELECT id, title, base FROM civicrm_mosaico_template';
+----+-----------------------------+------------+
| id | title                       | base       |
+----+-----------------------------+------------+
|  1 | CMRT Newsletter Template 1  | versafix-1 |
|  2 | CMRT Newsletter Template 3  | tutorial   |
|  3 | CMRT Newsletter Template 2  | tedc15     |
|  6 | CMRT Newsletter Base (copy) | versafix-1 |
+----+-----------------------------+------------+
```

### civicrm_mosaico_msg_template

```
ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civiusa.cnf --execute='SHOW COLUMNS FROM civicrm_mosaico_msg_template';
+------------+------------------+------+-----+---------+----------------+
| Field      | Type             | Null | Key | Default | Extra          |
+------------+------------------+------+-----+---------+----------------+
| id         | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| msg_tpl_id | int(10) unsigned | NO   | MUL | NULL    |                |
| hash_key   | varchar(32)      | NO   |     | NULL    |                |
| name       | varchar(32)      | NO   |     | NULL    |                |
| html       | longtext         | NO   |     | NULL    |                |
| metadata   | longtext         | NO   |     | NULL    |                |
| template   | longtext         | NO   |     | NULL    |                |
+------------+------------------+------+-----+---------+----------------+

EMPTY...
ian@hp:~/ken8/mysql_data/usa_civi$ mysql --defaults-file=/home/ian/.my_civiusa.cnf --execute='SELECT * FROM civicrm_mosaico_msg_template';
ian@hp:~/ken8/mysql_data/usa_civi$

```
