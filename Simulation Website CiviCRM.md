# Installation of CiviCRM on the Simulation Website

The document [Simulation Website](Simulation%20Website.md) contains information on the preparation and installation of WordPress to simulate the configuration on the *Ventraip - cmrailtrail.org.au* website. This follow on document details the adding of CiviCRM onto this Ubuntu 24.04 based simulation website.

### Reference Documents

[CiviCRM Installation Guide](https://docs.civicrm.org/installation/en/latest/)

### PHP Modules:

The installation of PHP modules for WordPress covered the PHP requirements for CiviCRM. Thus, no further PHP modules need to be installed.

The [PHP Extensions](https://docs.civicrm.org/installation/en/latest/requirements/#php-extensions) section states CiviCRM requires:

* bcmath
* curl
* dom - xml
* mbstring
* zip
* intl
* fileinfo
* soap

These should have already been installed.

### Edit the Apach2 php.ini file.

Some parameters in the file `/etc/php/8.3/apache2/php.ini` need to be increased for CiviCRM. 

These are the parameters that need increasing and line number in the `php.ini` file where they were found:
```
Line 417: max_execution_time = 240
Line 429: max_input_time = 120
Line 445: memory_limit = 256M    
Line 713: post_max_size = 50M
Line 865: upload_max_filesize =  50M 
```

### Using pluma on normal computer to edit php.ini

Copy the php.ini file from the simulation computer to the normal computer
```
ian@hp:~$ scp cmrailtr@192.168.1.101:/etc/php/8.3/apache2/php.ini php.ini
cmrailtr@192.168.1.101's password: 
php.ini                                       100%   72KB 293.4KB/s   00:00    
```
Use *pluma* to edit the file and apply the above changes:
```
ian@hp:~$ pluma php.ini
```
Copy the edited file back to the `home` folder on the simulaton computer: 
```
ian@hp:~$ sudo scp php.ini cmrailtr@192.168.1.101:php.ini
cmrailtr@192.168.1.101's password: 
php.ini                                       100%   72KB 706.7KB/s   00:00    
```

Connect to the simulation computer `home` folder and copy the `php.ini` so it replaces the `/etc/php/8.3/apache/php.ini` file
```
cmrailtr@CMRT-Demo:~$ ls -l /etc/php/8.3/apache2/
total 76
drwxr-xr-x 2 root root  4096 Jun 19 11:48 conf.d
-rw-r--r-- 1 root root 73718 Mar 19 23:08 php.ini

cmrailtr@CMRT-Demo:~$ ls -l php.ini
-rw-r--r-- 1 cmrailtr cmrailtr 74053 Jun 27 11:12 php.ini

cmrailtr@CMRT-Demo:~$ sudo cp php.ini /etc/php/8.3/apache2/php.ini
[sudo] password for cmrailtr: 

cmrailtr@CMRT-Demo:~$ ls -l /etc/php/8.3/apache2/
total 80
drwxr-xr-x 2 root root  4096 Jun 19 11:48 conf.d
-rw-r--r-- 1 root root 74053 Jun 27 11:15 php.ini
cmrailtr@CMRT-Demo:~$ ls -l /etc/php/8.3/apache2/
```

### Connect to Database as root
```
cmrailtr@CMRT-Demo:~$ sudo mysql -u root -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 36
Server version: 10.11.13-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_czhn1     |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.008 sec)
```

### Check if Timezone Data has been installed
```
MariaDB [(none)]> SELECT @@system_time_zone;
+--------------------+
| @@system_time_zone |
+--------------------+
| NZST               |
+--------------------+
1 row in set (0.000 sec)

MariaDB [(none)]> SELECT TIMEDIFF(NOW(), UTC_TIMESTAMP);
+--------------------------------+
| TIMEDIFF(NOW(), UTC_TIMESTAMP) |
+--------------------------------+
| 12:00:00                       |
+--------------------------------+
1 row in set (0.000 sec)

MariaDB [(none)]> SELECT CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland",
"Australia/Melbourne");
+------------------------------------------------------------------------------+
| CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland", "Australia/Melbourne") |
+------------------------------------------------------------------------------+
| NULL                                                                         |
+------------------------------------------------------------------------------+
1 row in set (0.000 sec)
```
NULL so Timezone data is not installed:

### Execute command to install Timezone data

From the command prompt execute:
```
cmrailtr@CMRT-Demo:~$ sudo mysql_tzinfo_to_sql /usr/share/zoneinfo | sudo mysql -u root mysql
```

Check Timezone
```
MariaDB [(none)]> SELECT CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland",
    -> "Australia/Melbourne");
+------------------------------------------------------------------------------+
| CONVERT_TZ("2025-06-03 14:30:00", "Pacific/Auckland", "Australia/Melbourne") |
+------------------------------------------------------------------------------+
| 2025-06-03 12:30:00                                                          |
+------------------------------------------------------------------------------+
```
Not NULL. Know that Melbourne is 2 hours behind Auckland.


### Create the CiviCRM Database
```
MariaDB [(none)]> use mysql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [mysql]> show databases;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_czhn1     |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.001 sec)

MariaDB [mysql]> CREATE DATABASE cmrailtr_civicrm;
Query OK, 1 row affected (0.007 sec)

MariaDB [mysql]> show databases;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civicrm   |
| cmrailtr_czhn1     |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
6 rows in set (0.000 sec)
```

Grant the privileges to the User of CiviCRM, `cmrailtr_czhn1`:
```
MariaDB [mysql]> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES, TRIGGER, CREATE ROUTINE, ALTER ROUTINE, REFERENCES, CREATE VIEW, SHOW VIEW ON cmrailtr_civicrm.* TO 'cmrailtr_czhn1'@'localhost' IDENTIFIED BY 'W---HIDDEN---0';
Query OK, 0 rows affected (0.011 sec)

MariaDB [mysql]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.001 sec)
```

### Check Login by User 

The User `cmrailtr_czhn1` does not need sudo priv to login.
However, they have restricted view of only three of the six databases.
```
cmrailtr@CMRT-Demo:~$ mysql -u cmrailtr_czhn1 -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 41
Server version: 10.11.13-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civicrm   |
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
3 rows in set (0.001 sec)
```

### Review the `cmrailtr_civicrm` Database before CiviCRM install
```
MariaDB [(none)]> use cmrailtr_civicrm
Database changed
MariaDB [cmrailtr_civicrm]> show tables;
Empty set (0.000 sec)
```

### Unzip CiviCRM

The CiviCRM for WordPress zip file has been downloaded to the `home` folder. From the `home` folder the directory is changed to be:
`/home/cmrailtr/public_html/wp-content/plugins`. The zip file is then copied to the `plugins` folder:
```
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ cp ~/civicrm-6.2.0-wordpress.zip civicrm-6.2.0-wordpress.zip

cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ ls -l
total 46360
drwxr-xr-x 4 cmrailtr cmrailtr     4096 Apr 14 23:37 akismet
-rw-rw-r-- 1 cmrailtr cmrailtr 47456829 Jun 27 12:14 civicrm-6.2.0-wordpress.zip
-rw-r--r-- 1 cmrailtr cmrailtr     2646 Mar  6 00:18 hello.php
-rw-r--r-- 1 cmrailtr cmrailtr       28 Jun  5  2014 index.php
```
The unzip command is used with the quiet option.
```
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ unzip -q civicrm-6.2.0-wordpress.zip
```
From the `plugins` folder, the unzipping created a `civicrm` folder. Off the `civicrm` folder:
```
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ tree civicrm
...snip...
2792 directories, 18272 files
```
The top two levels of directories of the plugin folder then looked like this:
```
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ tree -L 2

/home/cmrailtr/public_html/wp-content/plugins
├── akismet
│   ├── LICENSE.txt
│   ├── _inc
│   ├── akismet.php
│   ├── changelog.txt
│   ├── class.akismet-admin.php
│   ├── class.akismet-cli.php
│   ├── class.akismet-rest-api.php
│   ├── class.akismet-widget.php
│   ├── class.akismet.php
│   ├── index.php
│   ├── readme.txt
│   ├── views
│   └── wrapper.php
├── civicrm
│   ├── README.md
│   ├── assets
│   ├── civicrm
│   ├── civicrm.php
│   ├── includes
│   ├── languages
│   ├── phpcs.xml
│   ├── phpunit.xml.dist
│   ├── readme.txt
│   ├── tests
│   ├── uninstall.php
│   ├── wp-cli
│   └── wp-rest
├── civicrm-6.2.0-wordpress.zip
├── hello.php
└── index.php

12 directories, 20 files
```
The zip file is no longer required and was removed.
```
cmrailtr@CMRT-Demo:~/public_html/wp-content/plugins$ rm civicrm-6.2.0-wordpress.zip 
```

### Switch to Wordpress wp-admin to complete the CiviCRM installation:

Open a browser and login to the WordPress Admin account on the simulation computer. E.g. `http://192.168.1.101/wp-admin`

In the WordPress main screen go to --> Plugins --> civicrm --> activate

The CiviCRM Installation will be performed in the browser...

Initial Installation Screen - Errors are due to the link to the CiviCRM Database defaulted to the WordPress database
![civicrm1](/images/simulation_civicrm/civicrm1.png)

Editing the link so that the `cmrailtr_civicrm` database is used via user `cmrailtr_czhn1`
CiviCRMmysql://cmrailtr_czhn1:W----HIDDEN-----0@localhost:3306/cmrailtr_civicrm
![civicrm2](/images/simulation_civicrm/civicrm2.png)

CiviCRM Installer screen with out any errors. Top.
![civicrm3](/images/simulation_civicrm/civicrm3.png)

CiviCRM Installer screen with out any errors. Bottom.  5 Components selected and 3 unselected.
![civicrm4](/images/simulation_civicrm/civicrm4.png)

Change to all 8 components selected. No sample data.
![civicrm5](/images/simulation_civicrm/civicrm5.png)
Environment with CiviCRM Database set to `cmrailtr_civicrm`:

![civicrm6](/images/simulation_civicrm/civicrm6.png)

Installation Success screen
![civicrm7](/images/simulation_civicrm/civicrm7.png)

CiviCRM Home screen - with System Status: Warnings
![civicrm8](/images/simulation_civicrm/civicrm8.png)

CiviCRM System Status Screen - Top.
![civicrm9](/images/simulation_civicrm/civicrm9.png)

CiviCRM System Status Screen - Bottom.
![civicrm10](/images/simulation_civicrm/civicrm10.png)

### Review the `cmrailtr_civicrm` Database after the CiviCRM install
```
cmrailtr@CMRT-Demo:~/public_html$ mysql -u cmrailtr_czhn1 -p
Enter password: 
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 325
Server version: 10.11.13-MariaDB-0ubuntu0.24.04.1 Ubuntu 24.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civicrm   |
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
3 rows in set (0.001 sec)

MariaDB [(none)]> use cmrailtr_civicrm;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [cmrailtr_civicrm]> show tables;
+------------------------------------------+
| Tables_in_cmrailtr_civicrm               |
+------------------------------------------+
| civicrm_acl                              |
| civicrm_acl_cache                        |
| civicrm_acl_contact_cache                |
| civicrm_acl_entity_role                  |
| civicrm_action_log                       |
| civicrm_action_schedule                  |
| civicrm_activity                         |
| civicrm_activity_contact                 |
| civicrm_address                          |
| civicrm_address_format                   |
| civicrm_afform_submission                |
| civicrm_batch                            |
| civicrm_cache                            |
| civicrm_campaign                         |
| civicrm_campaign_group                   |
| civicrm_case                             |
| civicrm_case_activity                    |
| civicrm_case_contact                     |
| civicrm_case_type                        |
| civicrm_component                        |
| civicrm_contact                          |
| civicrm_contact_type                     |
| civicrm_contribution                     |
| civicrm_contribution_page                |
| civicrm_contribution_product             |
| civicrm_contribution_recur               |
| civicrm_contribution_soft                |
| civicrm_contribution_widget              |
| civicrm_country                          |
| civicrm_county                           |
| civicrm_currency                         |
| civicrm_custom_field                     |
| civicrm_custom_group                     |
| civicrm_dashboard                        |
| civicrm_dashboard_contact                |
| civicrm_dedupe_exception                 |
| civicrm_dedupe_rule                      |
| civicrm_dedupe_rule_group                |
| civicrm_discount                         |
| civicrm_domain                           |
| civicrm_email                            |
| civicrm_entity_batch                     |
| civicrm_entity_file                      |
| civicrm_entity_financial_account         |
| civicrm_entity_financial_trxn            |
| civicrm_entity_tag                       |
| civicrm_event                            |
| civicrm_extension                        |
| civicrm_file                             |
| civicrm_financial_account                |
| civicrm_financial_item                   |
| civicrm_financial_trxn                   |
| civicrm_financial_type                   |
| civicrm_group                            |
| civicrm_group_contact                    |
| civicrm_group_contact_cache              |
| civicrm_group_nesting                    |
| civicrm_group_organization               |
| civicrm_im                               |
| civicrm_import_template_field            |
| civicrm_install_canary                   |
| civicrm_job                              |
| civicrm_job_log                          |
| civicrm_line_item                        |
| civicrm_loc_block                        |
| civicrm_location_type                    |
| civicrm_log                              |
| civicrm_mail_settings                    |
| civicrm_mailing                          |
| civicrm_mailing_abtest                   |
| civicrm_mailing_bounce_pattern           |
| civicrm_mailing_bounce_type              |
| civicrm_mailing_component                |
| civicrm_mailing_event_bounce             |
| civicrm_mailing_event_confirm            |
| civicrm_mailing_event_delivered          |
| civicrm_mailing_event_opened             |
| civicrm_mailing_event_queue              |
| civicrm_mailing_event_reply              |
| civicrm_mailing_event_subscribe          |
| civicrm_mailing_event_trackable_url_open |
| civicrm_mailing_event_unsubscribe        |
| civicrm_mailing_group                    |
| civicrm_mailing_job                      |
| civicrm_mailing_recipients               |
| civicrm_mailing_spool                    |
| civicrm_mailing_trackable_url            |
| civicrm_managed                          |
| civicrm_mapping                          |
| civicrm_mapping_field                    |
| civicrm_membership                       |
| civicrm_membership_block                 |
| civicrm_membership_log                   |
| civicrm_membership_payment               |
| civicrm_membership_status                |
| civicrm_membership_type                  |
| civicrm_menu                             |
| civicrm_msg_template                     |
| civicrm_navigation                       |
| civicrm_note                             |
| civicrm_openid                           |
| civicrm_option_group                     |
| civicrm_option_value                     |
| civicrm_participant                      |
| civicrm_participant_payment              |
| civicrm_participant_status_type          |
| civicrm_payment_processor                |
| civicrm_payment_processor_type           |
| civicrm_payment_token                    |
| civicrm_pcp                              |
| civicrm_pcp_block                        |
| civicrm_phone                            |
| civicrm_pledge                           |
| civicrm_pledge_block                     |
| civicrm_pledge_payment                   |
| civicrm_preferences_date                 |
| civicrm_premiums                         |
| civicrm_premiums_product                 |
| civicrm_prevnext_cache                   |
| civicrm_price_field                      |
| civicrm_price_field_value                |
| civicrm_price_set                        |
| civicrm_price_set_entity                 |
| civicrm_print_label                      |
| civicrm_product                          |
| civicrm_queue                            |
| civicrm_queue_item                       |
| civicrm_recurring_entity                 |
| civicrm_relationship                     |
| civicrm_relationship_cache               |
| civicrm_relationship_type                |
| civicrm_report_instance                  |
| civicrm_saved_search                     |
| civicrm_search_display                   |
| civicrm_search_segment                   |
| civicrm_setting                          |
| civicrm_site_email_address               |
| civicrm_site_token                       |
| civicrm_sms_provider                     |
| civicrm_state_province                   |
| civicrm_status_pref                      |
| civicrm_subscription_history             |
| civicrm_survey                           |
| civicrm_system_log                       |
| civicrm_tag                              |
| civicrm_tell_friend                      |
| civicrm_timezone                         |
| civicrm_translation                      |
| civicrm_uf_field                         |
| civicrm_uf_group                         |
| civicrm_uf_join                          |
| civicrm_uf_match                         |
| civicrm_user_job                         |
| civicrm_website                          |
| civicrm_word_replacement                 |
| civicrm_worldregion                      |
+------------------------------------------+
156 rows in set (0.001 sec)
```
Show the columns of the table `civicrm_contact`:
```
MariaDB [cmrailtr_civicrm]> show columns from civicrm_contact;
+--------------------------------+------------------+------+-----+---------------------+-------------------------------+
| Field                          | Type             | Null | Key | Default             | Extra                         |
+--------------------------------+------------------+------+-----+---------------------+-------------------------------+
| id                             | int(10) unsigned | NO   | PRI | NULL                | auto_increment                |
| contact_type                   | varchar(64)      | YES  | MUL | NULL                |                               |
| external_identifier            | varchar(64)      | YES  | UNI | NULL                |                               |
| display_name                   | varchar(128)     | YES  |     | NULL                |                               |
| organization_name              | varchar(128)     | YES  | MUL | NULL                |                               |
| contact_sub_type               | varchar(255)     | YES  | MUL | NULL                |                               |
| first_name                     | varchar(64)      | YES  | MUL | NULL                |                               |
| middle_name                    | varchar(64)      | YES  |     | NULL                |                               |
| last_name                      | varchar(64)      | YES  | MUL | NULL                |                               |
| do_not_email                   | tinyint(1)       | NO   |     | 0                   |                               |
| do_not_phone                   | tinyint(1)       | NO   |     | 0                   |                               |
| do_not_mail                    | tinyint(1)       | NO   |     | 0                   |                               |
| do_not_sms                     | tinyint(1)       | NO   |     | 0                   |                               |
| do_not_trade                   | tinyint(1)       | NO   |     | 0                   |                               |
| is_opt_out                     | tinyint(1)       | NO   |     | 0                   |                               |
| legal_identifier               | varchar(32)      | YES  |     | NULL                |                               |
| sort_name                      | varchar(128)     | YES  | MUL | NULL                |                               |
| nick_name                      | varchar(128)     | YES  |     | NULL                |                               |
| legal_name                     | varchar(128)     | YES  |     | NULL                |                               |
| image_URL                      | text             | YES  |     | NULL                |                               |
| preferred_communication_method | varchar(255)     | YES  | MUL | NULL                |                               |
| preferred_language             | varchar(5)       | YES  |     | NULL                |                               |
| hash                           | varchar(32)      | YES  | MUL | NULL                |                               |
| api_key                        | varchar(32)      | YES  | MUL | NULL                |                               |
| source                         | varchar(255)     | YES  |     | NULL                |                               |
| prefix_id                      | int(10) unsigned | YES  | MUL | NULL                |                               |
| suffix_id                      | int(10) unsigned | YES  | MUL | NULL                |                               |
| formal_title                   | varchar(64)      | YES  |     | NULL                |                               |
| communication_style_id         | int(10) unsigned | YES  | MUL | NULL                |                               |
| email_greeting_id              | int(10) unsigned | YES  |     | NULL                |                               |
| email_greeting_custom          | varchar(128)     | YES  |     | NULL                |                               |
| email_greeting_display         | varchar(255)     | YES  |     | NULL                |                               |
| postal_greeting_id             | int(10) unsigned | YES  |     | NULL                |                               |
| postal_greeting_custom         | varchar(128)     | YES  |     | NULL                |                               |
| postal_greeting_display        | varchar(255)     | YES  |     | NULL                |                               |
| addressee_id                   | int(10) unsigned | YES  |     | NULL                |                               |
| addressee_custom               | varchar(128)     | YES  |     | NULL                |                               |
| addressee_display              | varchar(255)     | YES  |     | NULL                |                               |
| job_title                      | varchar(255)     | YES  |     | NULL                |                               |
| gender_id                      | int(10) unsigned | YES  | MUL | NULL                |                               |
| birth_date                     | date             | YES  |     | NULL                |                               |
| is_deceased                    | tinyint(1)       | NO   | MUL | 0                   |                               |
| deceased_date                  | date             | YES  |     | NULL                |                               |
| household_name                 | varchar(128)     | YES  | MUL | NULL                |                               |
| primary_contact_id             | int(10) unsigned | YES  | MUL | NULL                |                               |
| sic_code                       | varchar(8)       | YES  |     | NULL                |                               |
| user_unique_id                 | varchar(255)     | YES  |     | NULL                |                               |
| employer_id                    | int(10) unsigned | YES  | MUL | NULL                |                               |
| is_deleted                     | tinyint(1)       | NO   | MUL | 0                   |                               |
| created_date                   | timestamp        | YES  | MUL | NULL                |                               |
| modified_date                  | timestamp        | YES  | MUL | current_timestamp() | on update current_timestamp() |
| preferred_mail_format          | varchar(8)       | YES  |     | Both                |                               |
+--------------------------------+------------------+------+-----+---------------------+-------------------------------+
52 rows in set (0.001 sec)
```
Show some of the fields in the `civicrm_contacts` table.
At this stage only a *Default Organization* and a `NULL` exist in the contacts database.
```
MariaDB [cmrailtr_civicrm]> select ID, organization_name, first_name, last_name FROM civicrm_contact;
+----+----------------------+------------+-----------+
| ID | organization_name    | first_name | last_name |
+----+----------------------+------------+-----------+
|  1 | Default Organization | NULL       | NULL      |
|  2 | NULL                 | NULL       | NULL      |
+----+----------------------+------------+-----------+
2 rows in set (0.000 sec)
```
