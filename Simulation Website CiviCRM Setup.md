# Simulation Website CiviCRM Setup

## Review the `cmrailtr_civicrm` Database after the CiviCRM install
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
At this stage only a *Default Organization* and a `NULL` entry exist in the contacts database.
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
Another table is the civicrm_email:
```
MariaDB [cmrailtr_civicrm]> show columns from civicrm_email;
+------------------+------------------+------+-----+---------+----------------+
| Field            | Type             | Null | Key | Default | Extra          |
+------------------+------------------+------+-----+---------+----------------+
| id               | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| contact_id       | int(10) unsigned | YES  | MUL | NULL    |                |
| location_type_id | int(10) unsigned | YES  | MUL | NULL    |                |
| email            | varchar(254)     | YES  | MUL | NULL    |                |
| is_primary       | tinyint(1)       | NO   | MUL | 0       |                |
| is_billing       | tinyint(1)       | NO   | MUL | 0       |                |
| on_hold          | int(10) unsigned | NO   |     | 0       |                |
| is_bulkmail      | tinyint(1)       | NO   |     | 0       |                |
| hold_date        | datetime         | YES  |     | NULL    |                |
| reset_date       | datetime         | YES  |     | NULL    |                |
| signature_text   | text             | YES  |     | NULL    |                |
| signature_html   | text             | YES  |     | NULL    |                |
+------------------+------------------+------+-----+---------+----------------+
12 rows in set (0.001 sec
```
Selecting fields from the civicrm_email table we see the `organization` contact email address, and the `individual` contact email address:
```
MariaDB [cmrailtr_civicrm]> SELECT id, contact_id, email FROM civicrm_email;
+----+------------+-------------------------------+
| id | contact_id | email                         |
+----+------------+-------------------------------+
|  1 |          1 | fixme.domainemail@example.org |
|  2 |          2 | ianstewart56@hotmail.com      |
+----+------------+-------------------------------+
```
The `contact_id`'s above match the `ID` fields in the `civicrm_contact` table.

Thus, in CiviCRM a search of all contacts in this fresh installation is as shown in the screen shot below:
![civicrm_setup1](/images/civicrm_setup/civicrm_setup1.png)

As the *Default Organization* has a *Contact ID* of 1, this will be edited manually to add the *Contact Details* of *CMRT*.
![civicrm_setup2](/images/civicrm_setup/civicrm_setup2.png)

CMRT Organization - Address Details
![civicrm_setup3](/images/civicrm_setup/civicrm_setup3.png)

CMRT Organization - Communication Details. Then click on *Save*.
![civicrm_setup4](/images/civicrm_setup/civicrm_setup4.png)

CMRT Organi
![civicrm_setup5](/images/civicrm_setup/civicrm_setup5.png)
![civicrm_setup6](/images/civicrm_setup/civicrm_setup6.png)
![civicrm_setup7](/images/civicrm_setup/civicrm_setup7.png)


