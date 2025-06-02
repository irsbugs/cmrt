## Tables in CiviCRM:

Information collected after a new installation with all 8 x components selected.

### 8 x Components of CiviCRM

* CiviContribute
* CiviEvent
* CiviMail
* CiviMember
* CiviCase
* CiviPledge
* CiviReport
* CiviCampaign


### Tables in CiviCRM - 156:

SQL command: SHOW TABLES;

* civicrm_acl
* civicrm_acl_cache
* civicrm_acl_contact_cache
* civicrm_acl_entity_role
* civicrm_action_log
* civicrm_action_schedule
* civicrm_activity
* civicrm_activity_contact
* civicrm_address
* civicrm_address_format
* civicrm_afform_submission
* civicrm_batch
* civicrm_cache
* civicrm_campaign
* civicrm_campaign_group
* civicrm_case
* civicrm_case_activity
* civicrm_case_contact
* civicrm_case_type
* civicrm_component
* civicrm_contact
* civicrm_contact_type
* civicrm_contribution
* civicrm_contribution_page
* civicrm_contribution_product
* civicrm_contribution_recur
* civicrm_contribution_soft
* civicrm_contribution_widget
* civicrm_country
* civicrm_county
* civicrm_currency
* civicrm_custom_field
* civicrm_custom_group
* civicrm_dashboard
* civicrm_dashboard_contact
* civicrm_dedupe_exception
* civicrm_dedupe_rule
* civicrm_dedupe_rule_group
* civicrm_discount
* civicrm_domain
* civicrm_email
* civicrm_entity_batch
* civicrm_entity_file
* civicrm_entity_financial_account
* civicrm_entity_financial_trxn
* civicrm_entity_tag
* civicrm_event
* civicrm_extension
* civicrm_file
* civicrm_financial_account
* civicrm_financial_item
* civicrm_financial_trxn
* civicrm_financial_type
* civicrm_group
* civicrm_group_contact
* civicrm_group_contact_cache
* civicrm_group_nesting
* civicrm_group_organization
* civicrm_im
* civicrm_import_template_field
* civicrm_install_canary
* civicrm_job
* civicrm_job_log
* civicrm_line_item
* civicrm_loc_block
* civicrm_location_type
* civicrm_log
* civicrm_mail_settings
* civicrm_mailing
* civicrm_mailing_abtest
* civicrm_mailing_bounce_pattern
* civicrm_mailing_bounce_type
* civicrm_mailing_component
* civicrm_mailing_event_bounce
* civicrm_mailing_event_confirm
* civicrm_mailing_event_delivered
* civicrm_mailing_event_opened
* civicrm_mailing_event_queue
* civicrm_mailing_event_reply
* civicrm_mailing_event_subscribe
* civicrm_mailing_event_trackable_url_open
* civicrm_mailing_event_unsubscribe
* civicrm_mailing_group
* civicrm_mailing_job
* civicrm_mailing_recipients
* civicrm_mailing_spool
* civicrm_mailing_trackable_url
* civicrm_managed
* civicrm_mapping
* civicrm_mapping_field
* civicrm_membership
* civicrm_membership_block
* civicrm_membership_log
* civicrm_membership_payment
* civicrm_membership_status
* civicrm_membership_type
* civicrm_menu
* civicrm_msg_template
* civicrm_navigation
* civicrm_note
* civicrm_openid
* civicrm_option_group
* civicrm_option_value
* civicrm_participant
* civicrm_participant_payment
* civicrm_participant_status_type
* civicrm_payment_processor
* civicrm_payment_processor_type
* civicrm_payment_token
* civicrm_pcp
* civicrm_pcp_block
* civicrm_phone
* civicrm_pledge
* civicrm_pledge_block
* civicrm_pledge_payment
* civicrm_preferences_date
* civicrm_premiums
* civicrm_premiums_product
* civicrm_prevnext_cache
* civicrm_price_field
* civicrm_price_field_value
* civicrm_price_set
* civicrm_price_set_entity
* civicrm_print_label
* civicrm_product
* civicrm_queue
* civicrm_queue_item
* civicrm_recurring_entity
* civicrm_relationship
* civicrm_relationship_cache
* civicrm_relationship_type
* civicrm_report_instance
* civicrm_saved_search
* civicrm_search_display
* civicrm_search_segment
* civicrm_setting
* civicrm_site_email_address
* civicrm_site_token
* civicrm_sms_provider
* civicrm_state_province
* civicrm_status_pref
* civicrm_subscription_history
* civicrm_survey
* civicrm_system_log
* civicrm_tag
* civicrm_tell_friend
* civicrm_timezone
* civicrm_translation
* civicrm_uf_field
* civicrm_uf_group
* civicrm_uf_join
* civicrm_uf_match
* civicrm_user_job
* civicrm_website
* civicrm_word_replacement
* civicrm_worldregion

156 rows

### Show Columns from all 156 x CiviCRM Tables

SQL command: cur.execute("SHOW COLUMNS FROM {}".format(table))

Total rows/fields: 1786

```
civicrm_acl
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES |     | NULL                     |                               |
| deny                                     | tinyint(1)       | NO  |     | 0                        |                               |
| entity_table                             | varchar(64)      | NO  |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | YES |     | NULL                     |                               |
| operation                                | varchar(8)       | NO  |     | NULL                     |                               |
| object_table                             | varchar(64)      | YES |     | NULL                     |                               |
| object_id                                | int(10) unsigned | YES |     | NULL                     |                               |
| acl_table                                | varchar(64)      | YES |     | NULL                     |                               |
| acl_id                                   | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| priority                                 | int(11)          | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
12 rows

civicrm_acl_cache
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| acl_id                                   | int(10) unsigned | NO  | MUL | NULL                     |                               |
| modified_date                            | timestamp        | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_acl_contact_cache
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| user_id                                  | int(10) unsigned | YES |     | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  |     | NULL                     |                               |
| operation                                | varchar(8)       | NO  |     | NULL                     |                               |
| domain_id                                | int(10) unsigned | NO  | MUL | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_acl_entity_role
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| acl_role_id                              | int(10) unsigned | NO  | MUL | NULL                     |                               |
| entity_table                             | varchar(64)      | NO  | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_action_log
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| entity_table                             | varchar(255)     | YES |     | NULL                     |                               |
| action_schedule_id                       | int(10) unsigned | NO  | MUL | NULL                     |                               |
| action_date_time                         | datetime         | YES |     | NULL                     |                               |
| is_error                                 | tinyint(1)       | NO  |     | 0                        |                               |
| message                                  | text             | YES |     | NULL                     |                               |
| repetition_number                        | int(10) unsigned | YES |     | NULL                     |                               |
| reference_date                           | datetime         | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
10 rows

civicrm_action_schedule
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(128)     | NO  | UNI | NULL                     |                               |
| title                                    | varchar(64)      | YES |     | NULL                     |                               |
| recipient                                | varchar(64)      | YES |     | NULL                     |                               |
| limit_to                                 | int(11)          | YES |     | NULL                     |                               |
| entity_value                             | varchar(255)     | YES |     | NULL                     |                               |
| entity_status                            | varchar(255)     | YES |     | NULL                     |                               |
| start_action_offset                      | int(10) unsigned | YES |     | 0                        |                               |
| start_action_unit                        | varchar(8)       | YES |     | NULL                     |                               |
| start_action_condition                   | varchar(64)      | YES |     | NULL                     |                               |
| start_action_date                        | varchar(2048)    | YES |     | NULL                     |                               |
| is_repeat                                | tinyint(1)       | NO  |     | 0                        |                               |
| repetition_frequency_unit                | varchar(8)       | YES |     | NULL                     |                               |
| repetition_frequency_interval            | int(10) unsigned | YES |     | 0                        |                               |
| end_frequency_unit                       | varchar(8)       | YES |     | NULL                     |                               |
| end_frequency_interval                   | int(10) unsigned | YES |     | 0                        |                               |
| end_action                               | varchar(32)      | YES |     | NULL                     |                               |
| end_date                                 | varchar(64)      | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| recipient_manual                         | varchar(128)     | YES |     | NULL                     |                               |
| recipient_listing                        | varchar(128)     | YES |     | NULL                     |                               |
| body_text                                | longtext         | YES |     | NULL                     |                               |
| body_html                                | longtext         | YES |     | NULL                     |                               |
| sms_body_text                            | longtext         | YES |     | NULL                     |                               |
| subject                                  | varchar(128)     | YES |     | NULL                     |                               |
| record_activity                          | tinyint(1)       | NO  |     | 0                        |                               |
| mapping_id                               | varchar(64)      | YES |     | NULL                     |                               |
| group_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
| msg_template_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| sms_template_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| absolute_date                            | date             | YES |     | NULL                     |                               |
| from_name                                | varchar(255)     | YES |     | NULL                     |                               |
| from_email                               | varchar(255)     | YES |     | NULL                     |                               |
| mode                                     | varchar(128)     | YES |     | Email                    |                               |
| sms_provider_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| used_for                                 | varchar(64)      | YES |     | NULL                     |                               |
| filter_contact_language                  | varchar(128)     | YES |     | NULL                     |                               |
| communication_language                   | varchar(8)       | YES |     | NULL                     |                               |
| created_date                             | timestamp        | YES |     | current_timestamp()      |                               |
| modified_date                            | timestamp        | YES |     | current_timestamp()      | on update current_timestamp() |
| effective_start_date                     | timestamp        | YES |     | NULL                     |                               |
| effective_end_date                       | timestamp        | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
42 rows

civicrm_activity
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| source_record_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| activity_type_id                         | int(10) unsigned | NO  | MUL | 1                        |                               |
| subject                                  | varchar(255)     | YES |     | NULL                     |                               |
| activity_date_time                       | datetime         | YES | MUL | current_timestamp()      |                               |
| duration                                 | int(10) unsigned | YES |     | NULL                     |                               |
| location                                 | varchar(2048)    | YES |     | NULL                     |                               |
| phone_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
| phone_number                             | varchar(64)      | YES |     | NULL                     |                               |
| details                                  | longtext         | YES |     | NULL                     |                               |
| status_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| priority_id                              | int(10) unsigned | YES |     | NULL                     |                               |
| parent_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_test                                  | tinyint(1)       | NO  |     | 0                        |                               |
| medium_id                                | int(10) unsigned | YES |     | NULL                     |                               |
| is_auto                                  | tinyint(1)       | NO  |     | 0                        |                               |
| relationship_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_current_revision                      | tinyint(1)       | NO  | MUL | 1                        |                               |
| original_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| result                                   | varchar(255)     | YES |     | NULL                     |                               |
| is_deleted                               | tinyint(1)       | NO  | MUL | 0                        |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| engagement_level                         | int(10) unsigned | YES |     | NULL                     |                               |
| weight                                   | int(11)          | YES |     | NULL                     |                               |
| is_star                                  | tinyint(1)       | NO  |     | 0                        |                               |
| created_date                             | timestamp        | YES |     | current_timestamp()      |                               |
| modified_date                            | timestamp        | YES |     | current_timestamp()      | on update current_timestamp() |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
27 rows

civicrm_activity_contact
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| activity_id                              | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| record_type_id                           | int(10) unsigned | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_address
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| location_type_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_primary                               | tinyint(1)       | NO  | MUL | 0                        |                               |
| is_billing                               | tinyint(1)       | NO  | MUL | 0                        |                               |
| street_address                           | varchar(96)      | YES |     | NULL                     |                               |
| street_number                            | int(11)          | YES |     | NULL                     |                               |
| street_number_suffix                     | varchar(8)       | YES |     | NULL                     |                               |
| street_number_predirectional             | varchar(8)       | YES |     | NULL                     |                               |
| street_name                              | varchar(64)      | YES | MUL | NULL                     |                               |
| street_type                              | varchar(8)       | YES |     | NULL                     |                               |
| street_number_postdirectional            | varchar(8)       | YES |     | NULL                     |                               |
| street_unit                              | varchar(16)      | YES |     | NULL                     |                               |
| supplemental_address_1                   | varchar(96)      | YES |     | NULL                     |                               |
| supplemental_address_2                   | varchar(96)      | YES |     | NULL                     |                               |
| supplemental_address_3                   | varchar(96)      | YES |     | NULL                     |                               |
| city                                     | varchar(64)      | YES | MUL | NULL                     |                               |
| county_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| state_province_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| postal_code_suffix                       | varchar(12)      | YES |     | NULL                     |                               |
| postal_code                              | varchar(64)      | YES |     | NULL                     |                               |
| usps_adc                                 | varchar(32)      | YES |     | NULL                     |                               |
| country_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| geo_code_1                               | double           | YES | MUL | NULL                     |                               |
| geo_code_2                               | double           | YES |     | NULL                     |                               |
| manual_geo_code                          | tinyint(1)       | NO  |     | 0                        |                               |
| timezone                                 | varchar(8)       | YES |     | NULL                     |                               |
| name                                     | varchar(255)     | YES |     | NULL                     |                               |
| master_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
29 rows

civicrm_address_format
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| format                                   | text             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
2 rows

civicrm_afform_submission
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| afform_name                              | varchar(255)     | YES |     | NULL                     |                               |
| data                                     | text             | YES |     | NULL                     |                               |
| submission_date                          | timestamp        | YES |     | current_timestamp()      |                               |
| status_id                                | int(10) unsigned | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_batch
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES | UNI | NULL                     |                               |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | datetime         | NO  |     | current_timestamp()      |                               |
| modified_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| modified_date                            | datetime         | NO  |     | current_timestamp()      | on update current_timestamp() |
| saved_search_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| status_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| type_id                                  | int(10) unsigned | YES |     | NULL                     |                               |
| mode_id                                  | int(10) unsigned | YES |     | NULL                     |                               |
| total                                    | decimal(20,2)    | YES |     | NULL                     |                               |
| item_count                               | int(10) unsigned | YES |     | NULL                     |                               |
| payment_instrument_id                    | int(10) unsigned | YES |     | NULL                     |                               |
| exported_date                            | datetime         | YES |     | NULL                     |                               |
| data                                     | longtext         | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
17 rows

civicrm_cache
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| group_name                               | varchar(32)      | NO  | MUL | NULL                     |                               |
| path                                     | varchar(255)     | YES |     | NULL                     |                               |
| data                                     | longtext         | YES |     | NULL                     |                               |
| component_id                             | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | timestamp        | NO  |     | current_timestamp()      |                               |
| expired_date                             | timestamp        | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_campaign
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(255)     | NO  | UNI | NULL                     |                               |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| start_date                               | datetime         | YES |     | NULL                     |                               |
| end_date                                 | datetime         | YES |     | NULL                     |                               |
| campaign_type_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| status_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| external_identifier                      | varchar(32)      | YES | UNI | NULL                     |                               |
| parent_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | datetime         | NO  |     | current_timestamp()      |                               |
| last_modified_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| last_modified_date                       | datetime         | NO  |     | current_timestamp()      | on update current_timestamp() |
| goal_general                             | text             | YES |     | NULL                     |                               |
| goal_revenue                             | decimal(20,2)    | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
17 rows

civicrm_campaign_group
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| campaign_id                              | int(10) unsigned | NO  | MUL | NULL                     |                               |
| group_type                               | varchar(8)       | YES |     | NULL                     |                               |
| entity_table                             | varchar(64)      | YES |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_case
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| case_type_id                             | int(10) unsigned | NO  | MUL | NULL                     |                               |
| subject                                  | varchar(128)     | YES |     | NULL                     |                               |
| start_date                               | date             | YES |     | NULL                     |                               |
| end_date                                 | date             | YES |     | NULL                     |                               |
| details                                  | text             | YES |     | NULL                     |                               |
| status_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| is_deleted                               | tinyint(1)       | NO  | MUL | 0                        |                               |
| created_date                             | timestamp        | YES |     | NULL                     |                               |
| modified_date                            | timestamp        | YES |     | current_timestamp()      | on update current_timestamp() |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
10 rows

civicrm_case_activity
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| case_id                                  | int(10) unsigned | NO  | MUL | NULL                     |                               |
| activity_id                              | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_case_contact
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| case_id                                  | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_case_type
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | UNI | NULL                     |                               |
| title                                    | varchar(64)      | NO  |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| weight                                   | int(11)          | NO  |     | 1                        |                               |
| definition                               | blob             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
8 rows

civicrm_component
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  |     | NULL                     |                               |
| namespace                                | varchar(128)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_contact
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_type                             | varchar(64)      | YES | MUL | NULL                     |                               |
| external_identifier                      | varchar(64)      | YES | UNI | NULL                     |                               |
| display_name                             | varchar(128)     | YES |     | NULL                     |                               |
| organization_name                        | varchar(128)     | YES | MUL | NULL                     |                               |
| contact_sub_type                         | varchar(255)     | YES | MUL | NULL                     |                               |
| first_name                               | varchar(64)      | YES | MUL | NULL                     |                               |
| middle_name                              | varchar(64)      | YES |     | NULL                     |                               |
| last_name                                | varchar(64)      | YES | MUL | NULL                     |                               |
| do_not_email                             | tinyint(1)       | NO  |     | 0                        |                               |
| do_not_phone                             | tinyint(1)       | NO  |     | 0                        |                               |
| do_not_mail                              | tinyint(1)       | NO  |     | 0                        |                               |
| do_not_sms                               | tinyint(1)       | NO  |     | 0                        |                               |
| do_not_trade                             | tinyint(1)       | NO  |     | 0                        |                               |
| is_opt_out                               | tinyint(1)       | NO  |     | 0                        |                               |
| legal_identifier                         | varchar(32)      | YES |     | NULL                     |                               |
| sort_name                                | varchar(128)     | YES | MUL | NULL                     |                               |
| nick_name                                | varchar(128)     | YES |     | NULL                     |                               |
| legal_name                               | varchar(128)     | YES |     | NULL                     |                               |
| image_URL                                | text             | YES |     | NULL                     |                               |
| preferred_communication_method           | varchar(255)     | YES | MUL | NULL                     |                               |
| preferred_language                       | varchar(5)       | YES |     | NULL                     |                               |
| hash                                     | varchar(32)      | YES | MUL | NULL                     |                               |
| api_key                                  | varchar(32)      | YES | MUL | NULL                     |                               |
| source                                   | varchar(255)     | YES |     | NULL                     |                               |
| prefix_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| suffix_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| formal_title                             | varchar(64)      | YES |     | NULL                     |                               |
| communication_style_id                   | int(10) unsigned | YES | MUL | NULL                     |                               |
| email_greeting_id                        | int(10) unsigned | YES |     | NULL                     |                               |
| email_greeting_custom                    | varchar(128)     | YES |     | NULL                     |                               |
| email_greeting_display                   | varchar(255)     | YES |     | NULL                     |                               |
| postal_greeting_id                       | int(10) unsigned | YES |     | NULL                     |                               |
| postal_greeting_custom                   | varchar(128)     | YES |     | NULL                     |                               |
| postal_greeting_display                  | varchar(255)     | YES |     | NULL                     |                               |
| addressee_id                             | int(10) unsigned | YES |     | NULL                     |                               |
| addressee_custom                         | varchar(128)     | YES |     | NULL                     |                               |
| addressee_display                        | varchar(255)     | YES |     | NULL                     |                               |
| job_title                                | varchar(255)     | YES |     | NULL                     |                               |
| gender_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| birth_date                               | date             | YES |     | NULL                     |                               |
| is_deceased                              | tinyint(1)       | NO  | MUL | 0                        |                               |
| deceased_date                            | date             | YES |     | NULL                     |                               |
| household_name                           | varchar(128)     | YES | MUL | NULL                     |                               |
| primary_contact_id                       | int(10) unsigned | YES | MUL | NULL                     |                               |
| sic_code                                 | varchar(8)       | YES |     | NULL                     |                               |
| user_unique_id                           | varchar(255)     | YES |     | NULL                     |                               |
| employer_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_deleted                               | tinyint(1)       | NO  | MUL | 0                        |                               |
| created_date                             | timestamp        | YES | MUL | NULL                     |                               |
| modified_date                            | timestamp        | YES | MUL | current_timestamp()      | on update current_timestamp() |
| preferred_mail_format                    | varchar(8)       | YES |     | Both                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
52 rows

civicrm_contact_type
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | UNI | NULL                     |                               |
| label                                    | varchar(64)      | YES |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| image_URL                                | varchar(255)     | YES |     | NULL                     |                               |
| icon                                     | varchar(255)     | YES |     | NULL                     |                               |
| parent_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
9 rows

civicrm_contribution
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| financial_type_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| contribution_page_id                     | int(10) unsigned | YES | MUL | NULL                     |                               |
| payment_instrument_id                    | int(10) unsigned | YES | MUL | NULL                     |                               |
| receive_date                             | datetime         | YES | MUL | NULL                     |                               |
| non_deductible_amount                    | decimal(20,2)    | YES |     | 0.00                     |                               |
| total_amount                             | decimal(20,2)    | NO  | MUL | NULL                     |                               |
| fee_amount                               | decimal(20,2)    | YES |     | NULL                     |                               |
| net_amount                               | decimal(20,2)    | YES |     | NULL                     |                               |
| trxn_id                                  | varchar(255)     | YES | UNI | NULL                     |                               |
| invoice_id                               | varchar(255)     | YES | UNI | NULL                     |                               |
| invoice_number                           | varchar(255)     | YES |     | NULL                     |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| cancel_date                              | datetime         | YES |     | NULL                     |                               |
| cancel_reason                            | text             | YES |     | NULL                     |                               |
| receipt_date                             | datetime         | YES |     | NULL                     |                               |
| thankyou_date                            | datetime         | YES |     | NULL                     |                               |
| source                                   | varchar(255)     | YES | MUL | NULL                     |                               |
| amount_level                             | text             | YES |     | NULL                     |                               |
| contribution_recur_id                    | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_test                                  | tinyint(1)       | NO  |     | 0                        |                               |
| is_pay_later                             | tinyint(1)       | NO  |     | 0                        |                               |
| contribution_status_id                   | int(10) unsigned | YES | MUL | 1                        |                               |
| address_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| check_number                             | varchar(255)     | YES | MUL | NULL                     |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| creditnote_id                            | varchar(255)     | YES | MUL | NULL                     |                               |
| tax_amount                               | decimal(20,2)    | NO  |     | 0.00                     |                               |
| revenue_recognition_date                 | datetime         | YES |     | NULL                     |                               |
| is_template                              | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
31 rows

civicrm_contribution_page
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| title                                    | varchar(255)     | NO  |     | NULL                     |                               |
| frontend_title                           | varchar(255)     | NO  |     | NULL                     |                               |
| name                                     | varchar(255)     | NO  | UNI | NULL                     |                               |
| intro_text                               | text             | YES |     | NULL                     |                               |
| financial_type_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| payment_processor                        | varchar(128)     | YES |     | NULL                     |                               |
| is_credit_card_only                      | tinyint(1)       | NO  |     | 0                        |                               |
| is_monetary                              | tinyint(1)       | NO  |     | 1                        |                               |
| is_recur                                 | tinyint(1)       | NO  |     | 0                        |                               |
| is_confirm_enabled                       | tinyint(1)       | NO  |     | 1                        |                               |
| recur_frequency_unit                     | varchar(128)     | YES |     | NULL                     |                               |
| is_recur_interval                        | tinyint(1)       | NO  |     | 0                        |                               |
| is_recur_installments                    | tinyint(1)       | NO  |     | 0                        |                               |
| adjust_recur_start_date                  | tinyint(1)       | NO  |     | 0                        |                               |
| is_pay_later                             | tinyint(1)       | NO  |     | 0                        |                               |
| pay_later_text                           | text             | YES |     | NULL                     |                               |
| pay_later_receipt                        | text             | YES |     | NULL                     |                               |
| is_partial_payment                       | tinyint(1)       | YES |     | 0                        |                               |
| initial_amount_label                     | varchar(255)     | YES |     | NULL                     |                               |
| initial_amount_help_text                 | text             | YES |     | NULL                     |                               |
| min_initial_amount                       | decimal(20,2)    | YES |     | NULL                     |                               |
| is_allow_other_amount                    | tinyint(1)       | NO  |     | 0                        |                               |
| default_amount_id                        | int(10) unsigned | YES |     | NULL                     |                               |
| min_amount                               | decimal(20,2)    | YES |     | NULL                     |                               |
| max_amount                               | decimal(20,2)    | YES |     | NULL                     |                               |
| goal_amount                              | decimal(20,2)    | YES |     | NULL                     |                               |
| thankyou_title                           | varchar(255)     | YES |     | NULL                     |                               |
| thankyou_text                            | text             | YES |     | NULL                     |                               |
| thankyou_footer                          | text             | YES |     | NULL                     |                               |
| is_email_receipt                         | tinyint(1)       | NO  |     | 0                        |                               |
| receipt_from_name                        | varchar(255)     | YES |     | NULL                     |                               |
| receipt_from_email                       | varchar(255)     | YES |     | NULL                     |                               |
| cc_receipt                               | varchar(255)     | YES |     | NULL                     |                               |
| bcc_receipt                              | varchar(255)     | YES |     | NULL                     |                               |
| receipt_text                             | text             | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| footer_text                              | text             | YES |     | NULL                     |                               |
| amount_block_is_active                   | tinyint(1)       | NO  |     | 1                        |                               |
| start_date                               | datetime         | YES |     | NULL                     |                               |
| end_date                                 | datetime         | YES |     | NULL                     |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | datetime         | NO  |     | current_timestamp()      |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_share                                 | tinyint(1)       | NO  |     | 1                        |                               |
| is_billing_required                      | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
47 rows

civicrm_contribution_product
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| product_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contribution_id                          | int(10) unsigned | NO  | MUL | NULL                     |                               |
| product_option                           | varchar(255)     | YES |     | NULL                     |                               |
| quantity                                 | int(11)          | YES |     | NULL                     |                               |
| fulfilled_date                           | date             | YES |     | NULL                     |                               |
| start_date                               | date             | YES |     | NULL                     |                               |
| end_date                                 | date             | YES |     | NULL                     |                               |
| comment                                  | text             | YES |     | NULL                     |                               |
| financial_type_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
10 rows

civicrm_contribution_recur
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| amount                                   | decimal(20,2)    | NO  |     | NULL                     |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| frequency_unit                           | varchar(8)       | YES |     | month                    |                               |
| frequency_interval                       | int(10) unsigned | NO  |     | 1                        |                               |
| installments                             | int(10) unsigned | YES |     | NULL                     |                               |
| start_date                               | datetime         | NO  |     | current_timestamp()      |                               |
| create_date                              | datetime         | NO  |     | current_timestamp()      |                               |
| modified_date                            | timestamp        | NO  |     | current_timestamp()      | on update current_timestamp() |
| cancel_date                              | datetime         | YES |     | NULL                     |                               |
| cancel_reason                            | text             | YES |     | NULL                     |                               |
| end_date                                 | datetime         | YES |     | NULL                     |                               |
| processor_id                             | varchar(255)     | YES |     | NULL                     |                               |
| payment_token_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| trxn_id                                  | varchar(255)     | YES | UNI | NULL                     |                               |
| invoice_id                               | varchar(255)     | YES | UNI | NULL                     |                               |
| contribution_status_id                   | int(10) unsigned | YES | MUL | 2                        |                               |
| is_test                                  | tinyint(1)       | NO  |     | 0                        |                               |
| cycle_day                                | int(10) unsigned | NO  |     | 1                        |                               |
| next_sched_contribution_date             | datetime         | YES |     | NULL                     |                               |
| failure_count                            | int(10) unsigned | YES |     | 0                        |                               |
| failure_retry_date                       | datetime         | YES |     | NULL                     |                               |
| auto_renew                               | tinyint(1)       | NO  |     | 0                        |                               |
| payment_processor_id                     | int(10) unsigned | YES | MUL | NULL                     |                               |
| financial_type_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| payment_instrument_id                    | int(10) unsigned | YES | MUL | NULL                     |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_email_receipt                         | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
29 rows

civicrm_contribution_soft
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contribution_id                          | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| amount                                   | decimal(20,2)    | NO  |     | NULL                     |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| pcp_id                                   | int(10) unsigned | YES | MUL | NULL                     |                               |
| pcp_display_in_roll                      | tinyint(1)       | NO  |     | 0                        |                               |
| pcp_roll_nickname                        | varchar(255)     | YES |     | NULL                     |                               |
| pcp_personal_note                        | varchar(255)     | YES |     | NULL                     |                               |
| soft_credit_type_id                      | int(10) unsigned | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
10 rows

civicrm_contribution_widget
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contribution_page_id                     | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| url_logo                                 | varchar(255)     | YES |     | NULL                     |                               |
| button_title                             | varchar(255)     | YES |     | NULL                     |                               |
| about                                    | text             | YES |     | NULL                     |                               |
| url_homepage                             | varchar(255)     | YES |     | NULL                     |                               |
| color_title                              | varchar(10)      | YES |     | NULL                     |                               |
| color_button                             | varchar(10)      | YES |     | NULL                     |                               |
| color_bar                                | varchar(10)      | YES |     | NULL                     |                               |
| color_main_text                          | varchar(10)      | YES |     | NULL                     |                               |
| color_main                               | varchar(10)      | YES |     | NULL                     |                               |
| color_main_bg                            | varchar(10)      | YES |     | NULL                     |                               |
| color_bg                                 | varchar(10)      | YES |     | NULL                     |                               |
| color_about_link                         | varchar(10)      | YES |     | NULL                     |                               |
| color_homepage_link                      | varchar(10)      | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
17 rows

civicrm_country
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES | MUL | NULL                     |                               |
| iso_code                                 | char(2)          | YES |     | NULL                     |                               |
| country_code                             | varchar(4)       | YES |     | NULL                     |                               |
| address_format_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| idd_prefix                               | varchar(4)       | YES |     | NULL                     |                               |
| ndd_prefix                               | varchar(4)       | YES |     | NULL                     |                               |
| region_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| is_province_abbreviated                  | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
10 rows

civicrm_county
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES | MUL | NULL                     |                               |
| abbreviation                             | varchar(4)       | YES |     | NULL                     |                               |
| state_province_id                        | int(10) unsigned | NO  | MUL | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_currency
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES |     | NULL                     |                               |
| symbol                                   | varchar(8)       | YES |     | NULL                     |                               |
| numeric_code                             | varchar(3)       | YES |     | NULL                     |                               |
| full_name                                | varchar(64)      | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_custom_field
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| custom_group_id                          | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(64)      | YES | MUL | NULL                     |                               |
| label                                    | varchar(255)     | NO  | MUL | NULL                     |                               |
| data_type                                | varchar(16)      | NO  |     | NULL                     |                               |
| html_type                                | varchar(32)      | NO  |     | NULL                     |                               |
| default_value                            | varchar(255)     | YES |     | NULL                     |                               |
| is_required                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_searchable                            | tinyint(1)       | NO  |     | 0                        |                               |
| is_search_range                          | tinyint(1)       | NO  |     | 0                        |                               |
| weight                                   | int(11)          | NO  |     | 1                        |                               |
| help_pre                                 | text             | YES |     | NULL                     |                               |
| help_post                                | text             | YES |     | NULL                     |                               |
| attributes                               | varchar(255)     | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | YES |     | 1                        |                               |
| is_view                                  | tinyint(1)       | NO  |     | 0                        |                               |
| options_per_line                         | int(10) unsigned | YES |     | NULL                     |                               |
| text_length                              | int(10) unsigned | YES |     | NULL                     |                               |
| start_date_years                         | int(11)          | YES |     | NULL                     |                               |
| end_date_years                           | int(11)          | YES |     | NULL                     |                               |
| date_format                              | varchar(64)      | YES |     | NULL                     |                               |
| time_format                              | int(10) unsigned | YES |     | NULL                     |                               |
| note_columns                             | int(10) unsigned | YES |     | NULL                     |                               |
| note_rows                                | int(10) unsigned | YES |     | NULL                     |                               |
| column_name                              | varchar(255)     | YES |     | NULL                     |                               |
| option_group_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| serialize                                | int(10) unsigned | NO  |     | 0                        |                               |
| filter                                   | varchar(255)     | YES |     | NULL                     |                               |
| in_selector                              | tinyint(1)       | NO  |     | 0                        |                               |
| fk_entity                                | varchar(255)     | YES |     | NULL                     |                               |
| fk_entity_on_delete                      | varchar(255)     | NO  |     | set_null                 |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
31 rows

civicrm_custom_group
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | UNI | NULL                     |                               |
| title                                    | varchar(64)      | NO  | MUL | NULL                     |                               |
| extends                                  | varchar(255)     | NO  |     | Contact                  |                               |
| extends_entity_column_id                 | int(10) unsigned | YES |     | NULL                     |                               |
| extends_entity_column_value              | varchar(255)     | YES |     | NULL                     |                               |
| style                                    | varchar(15)      | NO  |     | Inline                   |                               |
| collapse_display                         | tinyint(1)       | NO  |     | 0                        |                               |
| help_pre                                 | text             | YES |     | NULL                     |                               |
| help_post                                | text             | YES |     | NULL                     |                               |
| weight                                   | int(11)          | NO  |     | 1                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| table_name                               | varchar(255)     | YES |     | NULL                     |                               |
| is_multiple                              | tinyint(1)       | NO  |     | 0                        |                               |
| min_multiple                             | int(10) unsigned | YES |     | NULL                     |                               |
| max_multiple                             | int(10) unsigned | YES |     | NULL                     |                               |
| collapse_adv_display                     | tinyint(1)       | NO  |     | 0                        |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | datetime         | YES |     | NULL                     |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_public                                | tinyint(1)       | NO  |     | 1                        |                               |
| icon                                     | varchar(255)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
22 rows

civicrm_dashboard
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(64)      | YES |     | NULL                     |                               |
| label                                    | varchar(255)     | YES |     | NULL                     |                               |
| url                                      | varchar(255)     | YES |     | NULL                     |                               |
| permission                               | varchar(255)     | YES |     | NULL                     |                               |
| permission_operator                      | varchar(3)       | YES |     | NULL                     |                               |
| fullscreen_url                           | varchar(255)     | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 0                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| cache_minutes                            | int(10) unsigned | NO  |     | 60                       |                               |
| directive                                | varchar(255)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
12 rows

civicrm_dashboard_contact
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| dashboard_id                             | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| column_no                                | int(11)          | YES |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 0                        |                               |
| weight                                   | int(11)          | YES |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_dedupe_exception
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id1                              | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contact_id2                              | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_dedupe_rule
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| dedupe_rule_group_id                     | int(10) unsigned | NO  | MUL | NULL                     |                               |
| rule_table                               | varchar(64)      | NO  |     | NULL                     |                               |
| rule_field                               | varchar(64)      | NO  |     | NULL                     |                               |
| rule_length                              | int(10) unsigned | YES |     | NULL                     |                               |
| rule_weight                              | int(11)          | NO  |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_dedupe_rule_group
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_type                             | varchar(12)      | YES |     | NULL                     |                               |
| threshold                                | int(11)          | NO  |     | NULL                     |                               |
| used                                     | varchar(12)      | NO  |     | NULL                     |                               |
| name                                     | varchar(255)     | YES | UNI | NULL                     |                               |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_discount
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| price_set_id                             | int(10) unsigned | NO  | MUL | NULL                     |                               |
| start_date                               | date             | YES |     | NULL                     |                               |
| end_date                                 | date             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_domain
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES | UNI | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| version                                  | varchar(32)      | YES |     | NULL                     |                               |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| locales                                  | text             | YES |     | NULL                     |                               |
| locale_custom_strings                    | text             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_email
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| location_type_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| email                                    | varchar(254)     | YES | MUL | NULL                     |                               |
| is_primary                               | tinyint(1)       | NO  | MUL | 0                        |                               |
| is_billing                               | tinyint(1)       | NO  | MUL | 0                        |                               |
| on_hold                                  | int(10) unsigned | NO  |     | 0                        |                               |
| is_bulkmail                              | tinyint(1)       | NO  |     | 0                        |                               |
| hold_date                                | datetime         | YES |     | NULL                     |                               |
| reset_date                               | datetime         | YES |     | NULL                     |                               |
| signature_text                           | text             | YES |     | NULL                     |                               |
| signature_html                           | text             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
12 rows

civicrm_entity_batch
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | YES | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| batch_id                                 | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_entity_file
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| file_id                                  | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_entity_financial_account
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| account_relationship                     | int(10) unsigned | NO  |     | NULL                     |                               |
| financial_account_id                     | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_entity_financial_trxn
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| financial_trxn_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| amount                                   | decimal(20,2)    | NO  |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_entity_tag
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | YES |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| tag_id                                   | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_event
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| summary                                  | text             | YES |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| event_type_id                            | int(10) unsigned | YES | MUL | 0                        |                               |
| participant_listing_id                   | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_public                                | tinyint(1)       | NO  |     | 1                        |                               |
| start_date                               | datetime         | YES |     | NULL                     |                               |
| end_date                                 | datetime         | YES |     | NULL                     |                               |
| is_online_registration                   | tinyint(1)       | NO  |     | 0                        |                               |
| registration_link_text                   | varchar(255)     | YES |     | NULL                     |                               |
| registration_start_date                  | datetime         | YES |     | NULL                     |                               |
| registration_end_date                    | datetime         | YES |     | NULL                     |                               |
| max_participants                         | int(10) unsigned | YES |     | NULL                     |                               |
| event_full_text                          | text             | YES |     | NULL                     |                               |
| is_monetary                              | tinyint(1)       | NO  |     | 0                        |                               |
| financial_type_id                        | int(10) unsigned | YES |     | NULL                     |                               |
| payment_processor                        | varchar(128)     | YES |     | NULL                     |                               |
| is_map                                   | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 0                        |                               |
| fee_label                                | varchar(255)     | YES |     | NULL                     |                               |
| is_show_location                         | tinyint(1)       | NO  |     | 1                        |                               |
| loc_block_id                             | int(10) unsigned | YES | MUL | NULL                     |                               |
| default_role_id                          | int(10) unsigned | YES |     | 1                        |                               |
| intro_text                               | text             | YES |     | NULL                     |                               |
| footer_text                              | text             | YES |     | NULL                     |                               |
| confirm_title                            | varchar(255)     | YES |     | NULL                     |                               |
| confirm_text                             | text             | YES |     | NULL                     |                               |
| confirm_footer_text                      | text             | YES |     | NULL                     |                               |
| is_email_confirm                         | tinyint(1)       | NO  |     | 0                        |                               |
| confirm_email_text                       | text             | YES |     | NULL                     |                               |
| confirm_from_name                        | varchar(255)     | YES |     | NULL                     |                               |
| confirm_from_email                       | varchar(255)     | YES |     | NULL                     |                               |
| cc_confirm                               | varchar(255)     | YES |     | NULL                     |                               |
| bcc_confirm                              | varchar(255)     | YES |     | NULL                     |                               |
| default_fee_id                           | int(10) unsigned | YES |     | NULL                     |                               |
| default_discount_fee_id                  | int(10) unsigned | YES |     | NULL                     |                               |
| thankyou_title                           | varchar(255)     | YES |     | NULL                     |                               |
| thankyou_text                            | text             | YES |     | NULL                     |                               |
| thankyou_footer_text                     | text             | YES |     | NULL                     |                               |
| is_pay_later                             | tinyint(1)       | NO  |     | 0                        |                               |
| pay_later_text                           | text             | YES |     | NULL                     |                               |
| pay_later_receipt                        | text             | YES |     | NULL                     |                               |
| is_partial_payment                       | tinyint(1)       | NO  |     | 0                        |                               |
| initial_amount_label                     | varchar(255)     | YES |     | NULL                     |                               |
| initial_amount_help_text                 | text             | YES |     | NULL                     |                               |
| min_initial_amount                       | decimal(20,2)    | YES |     | NULL                     |                               |
| is_multiple_registrations                | tinyint(1)       | NO  |     | 0                        |                               |
| max_additional_participants              | int(10) unsigned | YES |     | 0                        |                               |
| allow_same_participant_emails            | tinyint(1)       | NO  |     | 0                        |                               |
| has_waitlist                             | tinyint(1)       | NO  |     | 0                        |                               |
| requires_approval                        | tinyint(1)       | NO  |     | 0                        |                               |
| expiration_time                          | int(10) unsigned | YES |     | NULL                     |                               |
| allow_selfcancelxfer                     | tinyint(1)       | NO  |     | 0                        |                               |
| selfcancelxfer_time                      | int(11)          | NO  |     | 0                        |                               |
| waitlist_text                            | text             | YES |     | NULL                     |                               |
| approval_req_text                        | text             | YES |     | NULL                     |                               |
| is_template                              | tinyint(1)       | NO  |     | 0                        |                               |
| template_title                           | varchar(255)     | YES |     | NULL                     |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | datetime         | YES |     | NULL                     |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_share                                 | tinyint(1)       | NO  |     | 1                        |                               |
| is_confirm_enabled                       | tinyint(1)       | NO  |     | 1                        |                               |
| parent_event_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| slot_label_id                            | int(10) unsigned | YES |     | NULL                     |                               |
| dedupe_rule_group_id                     | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_billing_required                      | tinyint(1)       | NO  |     | 0                        |                               |
| is_show_calendar_links                   | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
70 rows

civicrm_extension
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| type                                     | varchar(8)       | NO  |     | NULL                     |                               |
| full_name                                | varchar(255)     | NO  | UNI | NULL                     |                               |
| name                                     | varchar(255)     | YES | MUL | NULL                     |                               |
| label                                    | varchar(255)     | YES |     | NULL                     |                               |
| file                                     | varchar(255)     | YES |     | NULL                     |                               |
| schema_version                           | varchar(63)      | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | YES |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
8 rows

civicrm_file
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| file_type_id                             | int(10) unsigned | YES |     | NULL                     |                               |
| mime_type                                | varchar(255)     | YES |     | NULL                     |                               |
| uri                                      | varchar(255)     | YES |     | NULL                     |                               |
| document                                 | mediumblob       | YES |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| upload_date                              | datetime         | NO  |     | current_timestamp()      |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
8 rows

civicrm_financial_account
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(255)     | NO  | UNI | NULL                     |                               |
| label                                    | varchar(64)      | NO  |     | NULL                     |                               |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| financial_account_type_id                | int(10) unsigned | NO  |     | 3                        |                               |
| accounting_code                          | varchar(64)      | YES |     | NULL                     |                               |
| account_type_code                        | varchar(64)      | YES |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| parent_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_header_account                        | tinyint(1)       | NO  |     | 0                        |                               |
| is_deductible                            | tinyint(1)       | NO  |     | 0                        |                               |
| is_tax                                   | tinyint(1)       | NO  |     | 0                        |                               |
| tax_rate                                 | decimal(10,8)    | YES |     | NULL                     |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
16 rows

civicrm_financial_item
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| created_date                             | timestamp        | NO  | MUL | current_timestamp()      |                               |
| transaction_date                         | datetime         | NO  | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| amount                                   | decimal(20,2)    | NO  |     | 0.00                     |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| financial_account_id                     | int(10) unsigned | YES | MUL | NULL                     |                               |
| status_id                                | int(10) unsigned | YES |     | NULL                     |                               |
| entity_table                             | varchar(64)      | YES |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
11 rows

civicrm_financial_trxn
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| from_financial_account_id                | int(10) unsigned | YES | MUL | NULL                     |                               |
| to_financial_account_id                  | int(10) unsigned | YES | MUL | NULL                     |                               |
| trxn_date                                | datetime         | YES |     | NULL                     |                               |
| total_amount                             | decimal(20,2)    | NO  |     | NULL                     |                               |
| fee_amount                               | decimal(20,2)    | YES |     | NULL                     |                               |
| net_amount                               | decimal(20,2)    | YES |     | NULL                     |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| is_payment                               | tinyint(1)       | NO  |     | 0                        |                               |
| trxn_id                                  | varchar(255)     | YES | MUL | NULL                     |                               |
| trxn_result_code                         | varchar(255)     | YES |     | NULL                     |                               |
| status_id                                | int(10) unsigned | YES |     | NULL                     |                               |
| payment_processor_id                     | int(10) unsigned | YES | MUL | NULL                     |                               |
| payment_instrument_id                    | int(10) unsigned | YES | MUL | NULL                     |                               |
| card_type_id                             | int(10) unsigned | YES |     | NULL                     |                               |
| check_number                             | varchar(255)     | YES | MUL | NULL                     |                               |
| pan_truncation                           | varchar(4)       | YES |     | NULL                     |                               |
| order_reference                          | varchar(255)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
18 rows

civicrm_financial_type
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  |     | NULL                     |                               |
| label                                    | varchar(64)      | NO  |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| is_deductible                            | tinyint(1)       | NO  |     | 0                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_group
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | UNI | NULL                     |                               |
| title                                    | varchar(255)     | NO  | UNI | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| source                                   | varchar(64)      | YES |     | NULL                     |                               |
| saved_search_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| visibility                               | varchar(24)      | YES |     | User and User Admin Only |                               |
| where_clause                             | text             | YES |     | NULL                     |                               |
| select_tables                            | text             | YES |     | NULL                     |                               |
| where_tables                             | text             | YES |     | NULL                     |                               |
| group_type                               | varchar(128)     | YES | MUL | NULL                     |                               |
| cache_date                               | timestamp        | YES | MUL | NULL                     |                               |
| cache_fill_took                          | double           | YES |     | NULL                     |                               |
| refresh_date                             | timestamp        | YES |     | NULL                     |                               |
| parents                                  | text             | YES |     | NULL                     |                               |
| children                                 | text             | YES |     | NULL                     |                               |
| is_hidden                                | tinyint(1)       | NO  |     | 0                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| modified_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| frontend_title                           | varchar(255)     | NO  |     | NULL                     |                               |
| frontend_description                     | text             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
23 rows

civicrm_group_contact
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| group_id                                 | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| status                                   | varchar(8)       | YES |     | NULL                     |                               |
| location_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| email_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_group_contact_cache
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| group_id                                 | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_group_nesting
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| child_group_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| parent_group_id                          | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_group_organization
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| group_id                                 | int(10) unsigned | NO  | MUL | NULL                     |                               |
| organization_id                          | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_im
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| location_type_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| name                                     | varchar(64)      | YES |     | NULL                     |                               |
| provider_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_primary                               | tinyint(1)       | NO  | MUL | 0                        |                               |
| is_billing                               | tinyint(1)       | NO  | MUL | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_import_template_field
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| user_job_id                              | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(1024)    | NO  |     | NULL                     |                               |
| column_number                            | int(10) unsigned | NO  |     | NULL                     |                               |
| entity                                   | varchar(255)     | NO  |     | NULL                     |                               |
| default_value                            | varchar(1024)    | YES |     | NULL                     |                               |
| data                                     | text             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_install_canary
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
1 rows

civicrm_job
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| run_frequency                            | varchar(8)       | YES |     | Daily                    |                               |
| last_run                                 | timestamp        | YES |     | NULL                     |                               |
| last_run_end                             | timestamp        | YES |     | NULL                     |                               |
| scheduled_run_date                       | timestamp        | YES |     | NULL                     |                               |
| name                                     | varchar(255)     | YES |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| api_entity                               | varchar(255)     | YES |     | NULL                     |                               |
| api_action                               | varchar(255)     | YES |     | NULL                     |                               |
| parameters                               | text             | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
12 rows

civicrm_job_log
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| run_time                                 | timestamp        | NO  |     | current_timestamp()      | on update current_timestamp() |
| job_id                                   | int(10) unsigned | YES | MUL | NULL                     |                               |
| name                                     | varchar(255)     | YES |     | NULL                     |                               |
| command                                  | varchar(255)     | YES |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| data                                     | longtext         | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
8 rows

civicrm_line_item
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| contribution_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| price_field_id                           | int(10) unsigned | YES | MUL | NULL                     |                               |
| label                                    | varchar(255)     | YES |     | NULL                     |                               |
| qty                                      | decimal(20,2)    | NO  |     | NULL                     |                               |
| unit_price                               | decimal(20,2)    | NO  |     | NULL                     |                               |
| line_total                               | decimal(20,2)    | NO  |     | NULL                     |                               |
| participant_count                        | int(10) unsigned | YES |     | NULL                     |                               |
| price_field_value_id                     | int(10) unsigned | YES | MUL | NULL                     |                               |
| financial_type_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| non_deductible_amount                    | decimal(20,2)    | NO  |     | 0.00                     |                               |
| tax_amount                               | decimal(20,2)    | NO  |     | 0.00                     |                               |
| membership_num_terms                     | int(10) unsigned | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
15 rows

civicrm_loc_block
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| address_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| email_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
| phone_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
| im_id                                    | int(10) unsigned | YES | MUL | NULL                     |                               |
| address_2_id                             | int(10) unsigned | YES | MUL | NULL                     |                               |
| email_2_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| phone_2_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| im_2_id                                  | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
9 rows

civicrm_location_type
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | UNI | NULL                     |                               |
| display_name                             | varchar(64)      | NO  |     | NULL                     |                               |
| vcard_name                               | varchar(64)      | YES |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
8 rows

civicrm_log
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| data                                     | text             | YES |     | NULL                     |                               |
| modified_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| modified_date                            | datetime         | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_mail_settings
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(255)     | YES |     | NULL                     |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
| domain                                   | varchar(255)     | YES |     | NULL                     |                               |
| localpart                                | varchar(255)     | YES |     | NULL                     |                               |
| return_path                              | varchar(255)     | YES |     | NULL                     |                               |
| protocol                                 | varchar(255)     | YES |     | NULL                     |                               |
| server                                   | varchar(255)     | YES |     | NULL                     |                               |
| port                                     | int(10) unsigned | YES |     | NULL                     |                               |
| username                                 | varchar(255)     | YES |     | NULL                     |                               |
| password                                 | varchar(255)     | YES |     | NULL                     |                               |
| is_ssl                                   | tinyint(1)       | NO  |     | 0                        |                               |
| source                                   | varchar(255)     | YES |     | NULL                     |                               |
| activity_status                          | varchar(255)     | YES |     | NULL                     |                               |
| is_non_case_email_skipped                | tinyint(1)       | NO  |     | 0                        |                               |
| is_contact_creation_disabled_if_no_match | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| activity_type_id                         | int(10) unsigned | YES |     | NULL                     |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| activity_source                          | varchar(4)       | YES |     | NULL                     |                               |
| activity_targets                         | varchar(16)      | YES |     | NULL                     |                               |
| activity_assignees                       | varchar(16)      | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
23 rows

civicrm_mailing
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| header_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| footer_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| reply_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
| unsubscribe_id                           | int(10) unsigned | YES | MUL | NULL                     |                               |
| resubscribe_id                           | int(10) unsigned | YES |     | NULL                     |                               |
| optout_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| name                                     | varchar(128)     | YES |     | NULL                     |                               |
| mailing_type                             | varchar(32)      | YES |     | NULL                     |                               |
| from_name                                | varchar(128)     | YES |     | NULL                     |                               |
| from_email                               | varchar(128)     | YES |     | NULL                     |                               |
| replyto_email                            | varchar(128)     | YES |     | NULL                     |                               |
| template_type                            | varchar(64)      | NO  |     | traditional              |                               |
| template_options                         | longtext         | YES |     | NULL                     |                               |
| subject                                  | varchar(128)     | YES |     | NULL                     |                               |
| body_text                                | longtext         | YES |     | NULL                     |                               |
| body_html                                | longtext         | YES |     | NULL                     |                               |
| url_tracking                             | tinyint(1)       | NO  |     | 0                        |                               |
| forward_replies                          | tinyint(1)       | NO  |     | 0                        |                               |
| auto_responder                           | tinyint(1)       | NO  |     | 0                        |                               |
| open_tracking                            | tinyint(1)       | NO  |     | 0                        |                               |
| is_completed                             | tinyint(1)       | NO  |     | 0                        |                               |
| msg_template_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| override_verp                            | tinyint(1)       | NO  |     | 0                        |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | timestamp        | YES |     | current_timestamp()      |                               |
| modified_date                            | timestamp        | YES |     | current_timestamp()      | on update current_timestamp() |
| scheduled_id                             | int(10) unsigned | YES | MUL | NULL                     |                               |
| scheduled_date                           | timestamp        | YES |     | NULL                     |                               |
| start_date                               | timestamp        | YES |     | NULL                     |                               |
| end_date                                 | timestamp        | YES |     | NULL                     |                               |
| status                                   | varchar(32)      | YES |     | Draft                    |                               |
| approver_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| approval_date                            | timestamp        | YES |     | NULL                     |                               |
| approval_status_id                       | int(10) unsigned | YES |     | NULL                     |                               |
| approval_note                            | longtext         | YES |     | NULL                     |                               |
| is_archived                              | tinyint(1)       | NO  |     | 0                        |                               |
| visibility                               | varchar(40)      | YES |     | Public Pages             |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| dedupe_email                             | tinyint(1)       | NO  |     | 0                        |                               |
| sms_provider_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| hash                                     | varchar(16)      | YES | MUL | NULL                     |                               |
| location_type_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| email_selection_method                   | varchar(20)      | YES |     | automatic                |                               |
| language                                 | varchar(5)       | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
46 rows

civicrm_mailing_abtest
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(128)     | YES |     | NULL                     |                               |
| status                                   | varchar(32)      | YES |     | NULL                     |                               |
| mailing_id_a                             | int(10) unsigned | YES |     | NULL                     |                               |
| mailing_id_b                             | int(10) unsigned | YES |     | NULL                     |                               |
| mailing_id_c                             | int(10) unsigned | YES |     | NULL                     |                               |
| domain_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| testing_criteria                         | varchar(32)      | YES |     | NULL                     |                               |
| winner_criteria                          | varchar(32)      | YES |     | NULL                     |                               |
| specific_url                             | varchar(255)     | YES |     | NULL                     |                               |
| declare_winning_time                     | datetime         | YES |     | NULL                     |                               |
| group_percentage                         | int(10) unsigned | YES |     | NULL                     |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | timestamp        | YES |     | current_timestamp()      |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
14 rows

civicrm_mailing_bounce_pattern
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| bounce_type_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| pattern                                  | varchar(255)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_mailing_bounce_type
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(255)     | NO  |     | NULL                     |                               |
| description                              | varchar(2048)    | YES |     | NULL                     |                               |
| hold_threshold                           | int(10) unsigned | NO  |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_mailing_component
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES |     | NULL                     |                               |
| component_type                           | varchar(12)      | YES |     | NULL                     |                               |
| subject                                  | varchar(255)     | YES |     | NULL                     |                               |
| body_html                                | text             | YES |     | NULL                     |                               |
| body_text                                | text             | YES |     | NULL                     |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
8 rows

civicrm_mailing_event_bounce
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| event_queue_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| bounce_type_id                           | int(10) unsigned | YES |     | NULL                     |                               |
| bounce_reason                            | varchar(255)     | YES |     | NULL                     |                               |
| time_stamp                               | timestamp        | NO  |     | current_timestamp()      |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_mailing_event_confirm
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| event_subscribe_id                       | int(10) unsigned | NO  | MUL | NULL                     |                               |
| time_stamp                               | timestamp        | NO  |     | current_timestamp()      |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_mailing_event_delivered
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| event_queue_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| time_stamp                               | timestamp        | NO  |     | current_timestamp()      |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_mailing_event_opened
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| event_queue_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| time_stamp                               | timestamp        | NO  |     | current_timestamp()      |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_mailing_event_queue
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| job_id                                   | int(10) unsigned | YES | MUL | NULL                     |                               |
| mailing_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_test                                  | tinyint(1)       | NO  |     | 0                        |                               |
| email_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| hash                                     | varchar(255)     | NO  | MUL | NULL                     |                               |
| phone_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
8 rows

civicrm_mailing_event_reply
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| event_queue_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| time_stamp                               | timestamp        | NO  |     | current_timestamp()      |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_mailing_event_subscribe
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| group_id                                 | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| hash                                     | varchar(255)     | NO  |     | NULL                     |                               |
| time_stamp                               | timestamp        | NO  |     | current_timestamp()      |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_mailing_event_trackable_url_open
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| event_queue_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| trackable_url_id                         | int(10) unsigned | NO  | MUL | NULL                     |                               |
| time_stamp                               | timestamp        | NO  |     | current_timestamp()      |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_mailing_event_unsubscribe
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| event_queue_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| org_unsubscribe                          | tinyint(1)       | NO  |     | 0                        |                               |
| time_stamp                               | timestamp        | NO  |     | current_timestamp()      |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_mailing_group
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| mailing_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| group_type                               | varchar(8)       | YES |     | NULL                     |                               |
| entity_table                             | varchar(64)      | NO  |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| search_id                                | int(11)          | YES |     | NULL                     |                               |
| search_args                              | text             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_mailing_job
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| mailing_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| scheduled_date                           | timestamp        | YES |     | NULL                     |                               |
| start_date                               | timestamp        | YES |     | NULL                     |                               |
| end_date                                 | timestamp        | YES |     | NULL                     |                               |
| status                                   | varchar(12)      | YES |     | NULL                     |                               |
| is_test                                  | tinyint(1)       | NO  |     | 0                        |                               |
| job_type                                 | varchar(255)     | YES |     | NULL                     |                               |
| parent_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| job_offset                               | int(11)          | YES |     | 0                        |                               |
| job_limit                                | int(11)          | YES |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
11 rows

civicrm_mailing_recipients
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| mailing_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| email_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
| phone_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_mailing_spool
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| job_id                                   | int(10) unsigned | NO  | MUL | NULL                     |                               |
| recipient_email                          | text             | YES |     | NULL                     |                               |
| headers                                  | text             | YES |     | NULL                     |                               |
| body                                     | text             | YES |     | NULL                     |                               |
| added_at                                 | timestamp        | YES |     | NULL                     |                               |
| removed_at                               | timestamp        | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_mailing_trackable_url
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| url                                      | text             | NO  |     | NULL                     |                               |
| mailing_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_managed
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| module                                   | varchar(255)     | NO  | MUL | NULL                     |                               |
| name                                     | varchar(255)     | NO  |     | NULL                     |                               |
| entity_type                              | varchar(64)      | NO  | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | YES |     | NULL                     |                               |
| checksum                                 | varchar(45)      | YES |     | NULL                     |                               |
| cleanup                                  | varchar(16)      | NO  |     | always                   |                               |
| entity_modified_date                     | timestamp        | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
8 rows

civicrm_mapping
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | UNI | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| mapping_type_id                          | int(10) unsigned | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_mapping_field
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| mapping_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(255)     | YES |     | NULL                     |                               |
| contact_type                             | varchar(64)      | YES |     | NULL                     |                               |
| column_number                            | int(10) unsigned | NO  |     | NULL                     |                               |
| location_type_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| phone_type_id                            | int(10) unsigned | YES |     | NULL                     |                               |
| im_provider_id                           | int(10) unsigned | YES |     | NULL                     |                               |
| website_type_id                          | int(10) unsigned | YES |     | NULL                     |                               |
| relationship_type_id                     | int(10) unsigned | YES | MUL | NULL                     |                               |
| relationship_direction                   | varchar(6)       | YES |     | NULL                     |                               |
| grouping                                 | int(10) unsigned | YES |     | 1                        |                               |
| operator                                 | varchar(16)      | YES |     | NULL                     |                               |
| value                                    | varchar(255)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
14 rows

civicrm_membership
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| membership_type_id                       | int(10) unsigned | NO  | MUL | NULL                     |                               |
| join_date                                | date             | YES |     | NULL                     |                               |
| start_date                               | date             | YES |     | NULL                     |                               |
| end_date                                 | date             | YES |     | NULL                     |                               |
| source                                   | varchar(128)     | YES |     | NULL                     |                               |
| status_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| is_override                              | tinyint(1)       | NO  |     | 0                        |                               |
| status_override_end_date                 | date             | YES |     | NULL                     |                               |
| owner_membership_id                      | int(10) unsigned | YES | MUL | NULL                     |                               |
| max_related                              | int(11)          | YES |     | NULL                     |                               |
| is_test                                  | tinyint(1)       | NO  |     | 0                        |                               |
| is_pay_later                             | tinyint(1)       | NO  |     | 0                        |                               |
| contribution_recur_id                    | int(10) unsigned | YES | MUL | NULL                     |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
16 rows

civicrm_membership_block
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | YES |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| membership_types                         | varchar(1024)    | YES |     | NULL                     |                               |
| membership_type_default                  | int(10) unsigned | YES | MUL | NULL                     |                               |
| display_min_fee                          | tinyint(1)       | NO  |     | 1                        |                               |
| is_separate_payment                      | tinyint(1)       | NO  |     | 1                        |                               |
| new_title                                | varchar(255)     | YES |     | NULL                     |                               |
| new_text                                 | text             | YES |     | NULL                     |                               |
| renewal_title                            | varchar(255)     | YES |     | NULL                     |                               |
| renewal_text                             | text             | YES |     | NULL                     |                               |
| is_required                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
13 rows

civicrm_membership_log
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| membership_id                            | int(10) unsigned | NO  | MUL | NULL                     |                               |
| status_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| start_date                               | date             | YES |     | NULL                     |                               |
| end_date                                 | date             | YES |     | NULL                     |                               |
| modified_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| modified_date                            | timestamp        | YES |     | NULL                     |                               |
| membership_type_id                       | int(10) unsigned | YES | MUL | NULL                     |                               |
| max_related                              | int(11)          | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
9 rows

civicrm_membership_payment
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| membership_id                            | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contribution_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_membership_status
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(128)     | NO  |     | NULL                     |                               |
| label                                    | varchar(128)     | YES |     | NULL                     |                               |
| start_event                              | varchar(12)      | YES |     | NULL                     |                               |
| start_event_adjust_unit                  | varchar(8)       | YES |     | NULL                     |                               |
| start_event_adjust_interval              | int(11)          | YES |     | NULL                     |                               |
| end_event                                | varchar(12)      | YES |     | NULL                     |                               |
| end_event_adjust_unit                    | varchar(8)       | YES |     | NULL                     |                               |
| end_event_adjust_interval                | int(11)          | YES |     | NULL                     |                               |
| is_current_member                        | tinyint(1)       | NO  |     | 0                        |                               |
| is_admin                                 | tinyint(1)       | NO  |     | 0                        |                               |
| weight                                   | int(11)          | YES |     | NULL                     |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
15 rows

civicrm_membership_type
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(128)     | NO  |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| member_of_contact_id                     | int(10) unsigned | NO  | MUL | NULL                     |                               |
| financial_type_id                        | int(10) unsigned | NO  | MUL | NULL                     |                               |
| minimum_fee                              | decimal(18,9)    | YES |     | 0.000000000              |                               |
| duration_unit                            | varchar(8)       | NO  |     | NULL                     |                               |
| duration_interval                        | int(11)          | YES |     | NULL                     |                               |
| period_type                              | varchar(8)       | NO  |     | NULL                     |                               |
| fixed_period_start_day                   | int(11)          | YES |     | NULL                     |                               |
| fixed_period_rollover_day                | int(11)          | YES |     | NULL                     |                               |
| relationship_type_id                     | varchar(64)      | YES | MUL | NULL                     |                               |
| relationship_direction                   | varchar(128)     | YES |     | NULL                     |                               |
| max_related                              | int(11)          | YES |     | NULL                     |                               |
| visibility                               | varchar(64)      | YES |     | NULL                     |                               |
| weight                                   | int(11)          | YES |     | NULL                     |                               |
| receipt_text_signup                      | varchar(255)     | YES |     | NULL                     |                               |
| receipt_text_renewal                     | varchar(255)     | YES |     | NULL                     |                               |
| auto_renew                               | tinyint(4)       | YES |     | 0                        |                               |
| is_active                                | tinyint(1)       | YES |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
21 rows

civicrm_menu
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| path                                     | varchar(255)     | YES | MUL | NULL                     |                               |
| path_arguments                           | text             | YES |     | NULL                     |                               |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| access_callback                          | varchar(255)     | YES |     | NULL                     |                               |
| access_arguments                         | text             | YES |     | NULL                     |                               |
| page_callback                            | varchar(255)     | YES |     | NULL                     |                               |
| page_arguments                           | text             | YES |     | NULL                     |                               |
| breadcrumb                               | text             | YES |     | NULL                     |                               |
| return_url                               | varchar(255)     | YES |     | NULL                     |                               |
| return_url_args                          | varchar(255)     | YES |     | NULL                     |                               |
| component_id                             | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_public                                | tinyint(1)       | NO  |     | 0                        |                               |
| is_exposed                               | tinyint(1)       | NO  |     | 1                        |                               |
| is_ssl                                   | tinyint(1)       | NO  |     | 1                        |                               |
| weight                                   | int(11)          | NO  |     | 1                        |                               |
| type                                     | int(11)          | NO  |     | 1                        |                               |
| page_type                                | int(11)          | NO  |     | 1                        |                               |
| skipBreadcrumb                           | tinyint(1)       | NO  |     | 0                        |                               |
| module_data                              | text             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
22 rows

civicrm_msg_template
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| msg_title                                | varchar(255)     | YES |     | NULL                     |                               |
| msg_subject                              | text             | YES |     | NULL                     |                               |
| msg_text                                 | longtext         | YES |     | NULL                     |                               |
| msg_html                                 | longtext         | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| workflow_id                              | int(10) unsigned | YES |     | NULL                     |                               |
| workflow_name                            | varchar(255)     | YES |     | NULL                     |                               |
| is_default                               | tinyint(1)       | NO  |     | 1                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_sms                                   | tinyint(1)       | NO  |     | 0                        |                               |
| pdf_format_id                            | int(10) unsigned | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
12 rows

civicrm_navigation
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| label                                    | varchar(255)     | YES |     | NULL                     |                               |
| name                                     | varchar(255)     | YES |     | NULL                     |                               |
| url                                      | varchar(255)     | YES |     | NULL                     |                               |
| icon                                     | varchar(255)     | YES |     | NULL                     |                               |
| permission                               | varchar(255)     | YES |     | NULL                     |                               |
| permission_operator                      | varchar(3)       | YES |     | NULL                     |                               |
| parent_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| has_separator                            | tinyint(4)       | YES |     | 0                        |                               |
| weight                                   | int(11)          | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
12 rows

civicrm_note
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| note                                     | text             | YES |     | NULL                     |                               |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| note_date                                | timestamp        | NO  |     | current_timestamp()      |                               |
| created_date                             | timestamp        | NO  |     | current_timestamp()      |                               |
| modified_date                            | timestamp        | NO  |     | current_timestamp()      | on update current_timestamp() |
| subject                                  | varchar(255)     | YES |     | NULL                     |                               |
| privacy                                  | varchar(255)     | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
10 rows

civicrm_openid
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| location_type_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| openid                                   | varchar(255)     | YES | UNI | NULL                     |                               |
| allowed_to_login                         | tinyint(1)       | NO  |     | 0                        |                               |
| is_primary                               | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_option_group
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | UNI | NULL                     |                               |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| data_type                                | varchar(128)     | YES |     | NULL                     |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 1                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_locked                                | tinyint(1)       | NO  |     | 0                        |                               |
| option_value_fields                      | varchar(128)     | YES |     | name,label,description   |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
9 rows

civicrm_option_value
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| option_group_id                          | int(10) unsigned | NO  | MUL | NULL                     |                               |
| label                                    | varchar(512)     | NO  |     | NULL                     |                               |
| value                                    | varchar(512)     | NO  | MUL | NULL                     |                               |
| name                                     | varchar(255)     | YES | MUL | NULL                     |                               |
| grouping                                 | varchar(255)     | YES |     | NULL                     |                               |
| filter                                   | int(10) unsigned | YES |     | 0                        |                               |
| is_default                               | tinyint(1)       | YES |     | 0                        |                               |
| weight                                   | int(10) unsigned | NO  |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| is_optgroup                              | tinyint(1)       | YES |     | 0                        |                               |
| is_reserved                              | tinyint(1)       | YES |     | 0                        |                               |
| is_active                                | tinyint(1)       | YES |     | 1                        |                               |
| component_id                             | int(10) unsigned | YES | MUL | NULL                     |                               |
| domain_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| visibility_id                            | int(10) unsigned | YES |     | NULL                     |                               |
| icon                                     | varchar(255)     | YES |     | NULL                     |                               |
| color                                    | varchar(255)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
18 rows

civicrm_participant
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| event_id                                 | int(10) unsigned | NO  | MUL | NULL                     |                               |
| status_id                                | int(10) unsigned | NO  | MUL | 1                        |                               |
| role_id                                  | varchar(128)     | YES | MUL | NULL                     |                               |
| register_date                            | datetime         | YES |     | NULL                     |                               |
| source                                   | varchar(128)     | YES |     | NULL                     |                               |
| fee_level                                | text             | YES |     | NULL                     |                               |
| is_test                                  | tinyint(1)       | NO  |     | 0                        |                               |
| is_pay_later                             | tinyint(1)       | NO  |     | 0                        |                               |
| fee_amount                               | decimal(20,2)    | YES |     | NULL                     |                               |
| registered_by_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| discount_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| fee_currency                             | varchar(3)       | YES |     | NULL                     |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| discount_amount                          | int(10) unsigned | YES |     | NULL                     |                               |
| must_wait                                | int(11)          | YES |     | NULL                     |                               |
| transferred_to_contact_id                | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
19 rows

civicrm_participant_payment
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| participant_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contribution_id                          | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
3 rows

civicrm_participant_status_type
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES |     | NULL                     |                               |
| label                                    | varchar(255)     | YES |     | NULL                     |                               |
| class                                    | varchar(8)       | YES |     | NULL                     |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_counted                               | tinyint(1)       | NO  |     | 0                        |                               |
| weight                                   | int(10) unsigned | NO  |     | NULL                     |                               |
| visibility_id                            | int(10) unsigned | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
9 rows

civicrm_payment_processor
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(64)      | NO  | MUL | NULL                     |                               |
| title                                    | varchar(255)     | NO  |     | NULL                     |                               |
| frontend_title                           | varchar(255)     | NO  |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| payment_processor_type_id                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
| is_test                                  | tinyint(1)       | NO  |     | 0                        |                               |
| user_name                                | varchar(255)     | YES |     | NULL                     |                               |
| password                                 | varchar(255)     | YES |     | NULL                     |                               |
| signature                                | text             | YES |     | NULL                     |                               |
| url_site                                 | varchar(255)     | YES |     | NULL                     |                               |
| url_api                                  | varchar(255)     | YES |     | NULL                     |                               |
| url_recur                                | varchar(255)     | YES |     | NULL                     |                               |
| url_button                               | varchar(255)     | YES |     | NULL                     |                               |
| subject                                  | varchar(255)     | YES |     | NULL                     |                               |
| class_name                               | varchar(255)     | YES |     | NULL                     |                               |
| billing_mode                             | int(10) unsigned | NO  |     | NULL                     |                               |
| is_recur                                 | tinyint(1)       | NO  |     | 0                        |                               |
| payment_type                             | int(10) unsigned | YES |     | 1                        |                               |
| payment_instrument_id                    | int(10) unsigned | YES |     | 1                        |                               |
| accepted_credit_cards                    | text             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
24 rows

civicrm_payment_processor_type
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | UNI | NULL                     |                               |
| title                                    | varchar(127)     | NO  |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
| user_name_label                          | varchar(255)     | YES |     | NULL                     |                               |
| password_label                           | varchar(255)     | YES |     | NULL                     |                               |
| signature_label                          | varchar(255)     | YES |     | NULL                     |                               |
| subject_label                            | varchar(255)     | YES |     | NULL                     |                               |
| class_name                               | varchar(255)     | NO  |     | NULL                     |                               |
| url_site_default                         | varchar(255)     | YES |     | NULL                     |                               |
| url_api_default                          | varchar(255)     | YES |     | NULL                     |                               |
| url_recur_default                        | varchar(255)     | YES |     | NULL                     |                               |
| url_button_default                       | varchar(255)     | YES |     | NULL                     |                               |
| url_site_test_default                    | varchar(255)     | YES |     | NULL                     |                               |
| url_api_test_default                     | varchar(255)     | YES |     | NULL                     |                               |
| url_recur_test_default                   | varchar(255)     | YES |     | NULL                     |                               |
| url_button_test_default                  | varchar(255)     | YES |     | NULL                     |                               |
| billing_mode                             | int(10) unsigned | NO  |     | NULL                     |                               |
| is_recur                                 | tinyint(1)       | NO  |     | 0                        |                               |
| payment_type                             | int(10) unsigned | YES |     | 1                        |                               |
| payment_instrument_id                    | int(10) unsigned | YES |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
23 rows

civicrm_payment_token
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| payment_processor_id                     | int(10) unsigned | NO  | MUL | NULL                     |                               |
| token                                    | varchar(255)     | NO  |     | NULL                     |                               |
| created_date                             | timestamp        | NO  |     | current_timestamp()      |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| expiry_date                              | datetime         | YES |     | NULL                     |                               |
| email                                    | varchar(255)     | YES |     | NULL                     |                               |
| billing_first_name                       | varchar(255)     | YES |     | NULL                     |                               |
| billing_middle_name                      | varchar(255)     | YES |     | NULL                     |                               |
| billing_last_name                        | varchar(255)     | YES |     | NULL                     |                               |
| masked_account_number                    | varchar(255)     | YES |     | NULL                     |                               |
| ip_address                               | varchar(255)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
13 rows

civicrm_pcp
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| status_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| intro_text                               | text             | YES |     | NULL                     |                               |
| page_text                                | text             | YES |     | NULL                     |                               |
| donate_link_text                         | varchar(255)     | YES |     | NULL                     |                               |
| page_id                                  | int(10) unsigned | NO  |     | NULL                     |                               |
| page_type                                | varchar(64)      | YES |     | contribute               |                               |
| pcp_block_id                             | int(10) unsigned | NO  |     | NULL                     |                               |
| is_thermometer                           | int(10) unsigned | YES |     | 0                        |                               |
| is_honor_roll                            | int(10) unsigned | YES |     | 0                        |                               |
| goal_amount                              | decimal(20,2)    | YES |     | NULL                     |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_notify                                | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
16 rows

civicrm_pcp_block
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | YES |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| target_entity_type                       | varchar(255)     | NO  |     | contribute               |                               |
| target_entity_id                         | int(10) unsigned | NO  |     | NULL                     |                               |
| supporter_profile_id                     | int(10) unsigned | YES | MUL | NULL                     |                               |
| owner_notify_id                          | int(10) unsigned | YES |     | 0                        |                               |
| is_approval_needed                       | tinyint(1)       | NO  |     | 0                        |                               |
| is_tellfriend_enabled                    | tinyint(1)       | NO  |     | 0                        |                               |
| tellfriend_limit                         | int(10) unsigned | YES |     | NULL                     |                               |
| link_text                                | varchar(255)     | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| notify_email                             | varchar(255)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
13 rows

civicrm_phone
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| location_type_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_primary                               | tinyint(1)       | NO  | MUL | 0                        |                               |
| is_billing                               | tinyint(1)       | NO  | MUL | 0                        |                               |
| mobile_provider_id                       | int(10) unsigned | YES | MUL | NULL                     |                               |
| phone                                    | varchar(32)      | YES |     | NULL                     |                               |
| phone_ext                                | varchar(16)      | YES |     | NULL                     |                               |
| phone_numeric                            | varchar(32)      | YES | MUL | NULL                     |                               |
| phone_type_id                            | int(10) unsigned | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
10 rows

civicrm_pledge
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| financial_type_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| contribution_page_id                     | int(10) unsigned | YES | MUL | NULL                     |                               |
| amount                                   | decimal(20,2)    | NO  |     | NULL                     |                               |
| original_installment_amount              | decimal(20,2)    | NO  |     | NULL                     |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| frequency_unit                           | varchar(8)       | NO  |     | month                    |                               |
| frequency_interval                       | int(10) unsigned | NO  |     | 1                        |                               |
| frequency_day                            | int(10) unsigned | NO  |     | 3                        |                               |
| installments                             | int(10) unsigned | NO  |     | 1                        |                               |
| start_date                               | datetime         | NO  |     | NULL                     |                               |
| create_date                              | datetime         | NO  |     | NULL                     |                               |
| acknowledge_date                         | datetime         | YES |     | NULL                     |                               |
| modified_date                            | datetime         | YES |     | NULL                     |                               |
| cancel_date                              | datetime         | YES |     | NULL                     |                               |
| end_date                                 | datetime         | YES |     | NULL                     |                               |
| max_reminders                            | int(10) unsigned | YES |     | 1                        |                               |
| initial_reminder_day                     | int(10) unsigned | YES |     | 5                        |                               |
| additional_reminder_day                  | int(10) unsigned | YES |     | 5                        |                               |
| status_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| is_test                                  | tinyint(1)       | NO  |     | 0                        |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
23 rows

civicrm_pledge_block
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | YES | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| pledge_frequency_unit                    | varchar(128)     | YES |     | NULL                     |                               |
| is_pledge_interval                       | tinyint(1)       | NO  |     | 0                        |                               |
| max_reminders                            | int(10) unsigned | YES |     | 1                        |                               |
| initial_reminder_day                     | int(10) unsigned | YES |     | 5                        |                               |
| additional_reminder_day                  | int(10) unsigned | YES |     | 5                        |                               |
| pledge_start_date                        | varchar(64)      | YES |     | NULL                     |                               |
| is_pledge_start_date_visible             | tinyint(1)       | NO  |     | 0                        |                               |
| is_pledge_start_date_editable            | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
11 rows

civicrm_pledge_payment
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| pledge_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contribution_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| scheduled_amount                         | decimal(20,2)    | NO  |     | NULL                     |                               |
| actual_amount                            | decimal(20,2)    | YES |     | NULL                     |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| scheduled_date                           | datetime         | NO  |     | NULL                     |                               |
| reminder_date                            | datetime         | YES |     | NULL                     |                               |
| reminder_count                           | int(10) unsigned | YES |     | 0                        |                               |
| status_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
10 rows

civicrm_preferences_date
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | MUL | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| start                                    | int(11)          | NO  |     | NULL                     |                               |
| end                                      | int(11)          | NO  |     | NULL                     |                               |
| date_format                              | varchar(64)      | YES |     | NULL                     |                               |
| time_format                              | varchar(64)      | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_premiums
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| premiums_active                          | tinyint(1)       | NO  |     | 0                        |                               |
| premiums_intro_title                     | varchar(255)     | YES |     | NULL                     |                               |
| premiums_intro_text                      | text             | YES |     | NULL                     |                               |
| premiums_contact_email                   | varchar(100)     | YES |     | NULL                     |                               |
| premiums_contact_phone                   | varchar(50)      | YES |     | NULL                     |                               |
| premiums_display_min_contribution        | tinyint(1)       | NO  |     | 0                        |                               |
| premiums_nothankyou_label                | varchar(255)     | YES |     | NULL                     |                               |
| premiums_nothankyou_position             | int(10) unsigned | YES |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
11 rows

civicrm_premiums_product
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| premiums_id                              | int(10) unsigned | NO  | MUL | NULL                     |                               |
| product_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| weight                                   | int(10) unsigned | NO  |     | NULL                     |                               |
| financial_type_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_prevnext_cache
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | YES |     | NULL                     |                               |
| entity_id1                               | int(10) unsigned | NO  |     | NULL                     |                               |
| entity_id2                               | int(10) unsigned | YES |     | NULL                     |                               |
| cachekey                                 | varchar(255)     | YES | MUL | NULL                     |                               |
| data                                     | longtext         | YES |     | NULL                     |                               |
| is_selected                              | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_price_field
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| price_set_id                             | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(255)     | NO  | MUL | NULL                     |                               |
| label                                    | varchar(255)     | NO  |     | NULL                     |                               |
| html_type                                | varchar(12)      | NO  |     | NULL                     |                               |
| is_enter_qty                             | tinyint(1)       | NO  |     | 0                        |                               |
| help_pre                                 | text             | YES |     | NULL                     |                               |
| help_post                                | text             | YES |     | NULL                     |                               |
| weight                                   | int(11)          | YES |     | 1                        |                               |
| is_display_amounts                       | tinyint(1)       | NO  |     | 1                        |                               |
| options_per_line                         | int(10) unsigned | YES |     | 1                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_required                              | tinyint(1)       | NO  |     | 1                        |                               |
| active_on                                | datetime         | YES |     | NULL                     |                               |
| expire_on                                | datetime         | YES |     | NULL                     |                               |
| javascript                               | varchar(255)     | YES |     | NULL                     |                               |
| visibility_id                            | int(10) unsigned | YES |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
17 rows

civicrm_price_field_value
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| price_field_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(255)     | YES |     | NULL                     |                               |
| label                                    | varchar(255)     | YES |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| help_pre                                 | text             | YES |     | NULL                     |                               |
| help_post                                | text             | YES |     | NULL                     |                               |
| amount                                   | decimal(18,9)    | NO  |     | NULL                     |                               |
| count                                    | int(10) unsigned | YES |     | NULL                     |                               |
| max_value                                | int(10) unsigned | YES |     | NULL                     |                               |
| weight                                   | int(11)          | YES |     | 1                        |                               |
| membership_type_id                       | int(10) unsigned | YES | MUL | NULL                     |                               |
| membership_num_terms                     | int(10) unsigned | YES |     | NULL                     |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| financial_type_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| non_deductible_amount                    | decimal(20,2)    | NO  |     | 0.00                     |                               |
| visibility_id                            | int(10) unsigned | YES |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
18 rows

civicrm_price_set
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| name                                     | varchar(255)     | NO  | UNI | NULL                     |                               |
| title                                    | varchar(255)     | NO  |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| help_pre                                 | text             | YES |     | NULL                     |                               |
| help_post                                | text             | YES |     | NULL                     |                               |
| javascript                               | varchar(64)      | YES |     | NULL                     |                               |
| extends                                  | varchar(255)     | NO  |     | NULL                     |                               |
| financial_type_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_quick_config                          | tinyint(1)       | NO  |     | 0                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| min_amount                               | decimal(20,2)    | YES |     | 0.00                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
13 rows

civicrm_price_set_entity
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| price_set_id                             | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_print_label
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| name                                     | varchar(255)     | YES |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| label_format_name                        | varchar(255)     | YES |     | NULL                     |                               |
| label_type_id                            | int(10) unsigned | YES |     | NULL                     |                               |
| data                                     | longtext         | YES |     | NULL                     |                               |
| is_default                               | tinyint(1)       | NO  |     | 1                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 1                        |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
11 rows

civicrm_product
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(255)     | NO  |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| sku                                      | varchar(50)      | YES |     | NULL                     |                               |
| options                                  | text             | YES |     | NULL                     |                               |
| image                                    | varchar(255)     | YES |     | NULL                     |                               |
| thumbnail                                | varchar(255)     | YES |     | NULL                     |                               |
| price                                    | decimal(20,2)    | YES |     | NULL                     |                               |
| currency                                 | varchar(3)       | YES |     | NULL                     |                               |
| financial_type_id                        | int(10) unsigned | YES | MUL | NULL                     |                               |
| min_contribution                         | decimal(20,2)    | YES |     | NULL                     |                               |
| cost                                     | decimal(20,2)    | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| period_type                              | varchar(8)       | YES |     | rolling                  |                               |
| fixed_period_start_day                   | int(11)          | YES |     | 101                      |                               |
| duration_unit                            | varchar(8)       | YES |     | year                     |                               |
| duration_interval                        | int(11)          | YES |     | NULL                     |                               |
| frequency_unit                           | varchar(8)       | YES |     | month                    |                               |
| frequency_interval                       | int(11)          | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
19 rows

civicrm_queue
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(128)     | NO  | UNI | NULL                     |                               |
| type                                     | varchar(64)      | NO  |     | NULL                     |                               |
| runner                                   | varchar(64)      | YES |     | NULL                     |                               |
| batch_limit                              | int(10) unsigned | NO  |     | 1                        |                               |
| lease_time                               | int(10) unsigned | NO  |     | 3600                     |                               |
| retry_limit                              | int(11)          | NO  |     | 0                        |                               |
| retry_interval                           | int(11)          | YES |     | NULL                     |                               |
| status                                   | varchar(16)      | YES |     | active                   |                               |
| error                                    | varchar(16)      | YES |     | NULL                     |                               |
| is_template                              | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
11 rows

civicrm_queue_item
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| queue_name                               | varchar(128)     | NO  | MUL | NULL                     |                               |
| weight                                   | int(11)          | NO  |     | NULL                     |                               |
| submit_time                              | timestamp        | NO  |     | NULL                     |                               |
| release_time                             | timestamp        | YES |     | NULL                     |                               |
| run_count                                | int(11)          | NO  |     | 0                        |                               |
| data                                     | longtext         | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_recurring_entity
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| parent_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | YES |     | NULL                     |                               |
| entity_table                             | varchar(64)      | NO  |     | NULL                     |                               |
| mode                                     | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_relationship
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id_a                             | int(10) unsigned | NO  | MUL | NULL                     |                               |
| contact_id_b                             | int(10) unsigned | NO  | MUL | NULL                     |                               |
| relationship_type_id                     | int(10) unsigned | NO  | MUL | NULL                     |                               |
| start_date                               | date             | YES |     | NULL                     |                               |
| end_date                                 | date             | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| is_permission_a_b                        | int(10) unsigned | NO  |     | 0                        |                               |
| is_permission_b_a                        | int(10) unsigned | NO  |     | 0                        |                               |
| case_id                                  | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | timestamp        | NO  |     | current_timestamp()      |                               |
| modified_date                            | timestamp        | NO  |     | current_timestamp()      | on update current_timestamp() |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
13 rows

civicrm_relationship_cache
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| relationship_id                          | int(10) unsigned | NO  | MUL | NULL                     |                               |
| relationship_type_id                     | int(10) unsigned | NO  | MUL | NULL                     |                               |
| orientation                              | char(3)          | NO  |     | NULL                     |                               |
| near_contact_id                          | int(10) unsigned | NO  | MUL | NULL                     |                               |
| near_relation                            | varchar(64)      | YES | MUL | NULL                     |                               |
| far_contact_id                           | int(10) unsigned | NO  | MUL | NULL                     |                               |
| far_relation                             | varchar(64)      | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| start_date                               | date             | YES |     | NULL                     |                               |
| end_date                                 | date             | YES |     | NULL                     |                               |
| case_id                                  | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
12 rows

civicrm_relationship_type
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name_a_b                                 | varchar(64)      | YES | UNI | NULL                     |                               |
| label_a_b                                | varchar(64)      | YES |     | NULL                     |                               |
| name_b_a                                 | varchar(64)      | YES | UNI | NULL                     |                               |
| label_b_a                                | varchar(64)      | YES |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| contact_type_a                           | varchar(12)      | YES |     | NULL                     |                               |
| contact_type_b                           | varchar(12)      | YES |     | NULL                     |                               |
| contact_sub_type_a                       | varchar(64)      | YES |     | NULL                     |                               |
| contact_sub_type_b                       | varchar(64)      | YES |     | NULL                     |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
12 rows

civicrm_report_instance
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| report_id                                | varchar(512)     | NO  |     | NULL                     |                               |
| name                                     | varchar(255)     | YES |     | NULL                     |                               |
| args                                     | varchar(255)     | YES |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| permission                               | varchar(255)     | YES |     | NULL                     |                               |
| grouprole                                | varchar(1024)    | YES |     | NULL                     |                               |
| form_values                              | longtext         | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| owner_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
| email_subject                            | varchar(255)     | YES |     | NULL                     |                               |
| email_to                                 | text             | YES |     | NULL                     |                               |
| email_cc                                 | text             | YES |     | NULL                     |                               |
| header                                   | text             | YES |     | NULL                     |                               |
| footer                                   | text             | YES |     | NULL                     |                               |
| navigation_id                            | int(10) unsigned | YES | MUL | NULL                     |                               |
| drilldown_id                             | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
21 rows

civicrm_saved_search
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(255)     | YES | UNI | NULL                     |                               |
| label                                    | varchar(255)     | YES |     | NULL                     |                               |
| form_values                              | text             | YES |     | NULL                     |                               |
| mapping_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| search_custom_id                         | int(10) unsigned | YES |     | NULL                     |                               |
| api_entity                               | varchar(255)     | YES |     | NULL                     |                               |
| api_params                               | text             | YES |     | NULL                     |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| modified_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| expires_date                             | timestamp        | YES |     | NULL                     |                               |
| created_date                             | timestamp        | NO  |     | current_timestamp()      |                               |
| modified_date                            | timestamp        | NO  |     | current_timestamp()      | on update current_timestamp() |
| description                              | text             | YES |     | NULL                     |                               |
| is_template                              | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
15 rows

civicrm_search_display
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(255)     | NO  |     | NULL                     |                               |
| label                                    | varchar(255)     | NO  |     | NULL                     |                               |
| saved_search_id                          | int(10) unsigned | NO  | MUL | NULL                     |                               |
| type                                     | varchar(128)     | NO  |     | NULL                     |                               |
| settings                                 | text             | YES |     | NULL                     |                               |
| acl_bypass                               | tinyint(1)       | YES |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_search_segment
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(255)     | NO  | UNI | NULL                     |                               |
| label                                    | varchar(255)     | NO  |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| entity_name                              | varchar(255)     | NO  |     | NULL                     |                               |
| items                                    | text             | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_setting
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(255)     | YES |     | NULL                     |                               |
| value                                    | text             | YES |     | NULL                     |                               |
| domain_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_domain                                | tinyint(1)       | NO  |     | 0                        |                               |
| component_id                             | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | datetime         | YES |     | NULL                     |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
9 rows

civicrm_site_email_address
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| display_name                             | varchar(254)     | NO  |     | NULL                     |                               |
| email                                    | varchar(254)     | NO  |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_site_token
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(64)      | NO  | MUL | NULL                     |                               |
| label                                    | varchar(255)     | NO  | MUL | NULL                     |                               |
| body_html                                | text             | YES |     | NULL                     |                               |
| body_text                                | text             | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| modified_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| modified_date                            | timestamp        | YES |     | current_timestamp()      | on update current_timestamp() |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
11 rows

civicrm_sms_provider
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES |     | NULL                     |                               |
| title                                    | varchar(64)      | YES |     | NULL                     |                               |
| username                                 | varchar(255)     | YES |     | NULL                     |                               |
| password                                 | varchar(255)     | YES |     | NULL                     |                               |
| api_type                                 | int(10) unsigned | NO  |     | NULL                     |                               |
| api_url                                  | varchar(128)     | YES |     | NULL                     |                               |
| api_params                               | text             | YES |     | NULL                     |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| domain_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
11 rows

civicrm_state_province
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES | MUL | NULL                     |                               |
| abbreviation                             | varchar(4)       | YES |     | NULL                     |                               |
| country_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
5 rows

civicrm_status_pref
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| name                                     | varchar(255)     | NO  | MUL | NULL                     |                               |
| hush_until                               | date             | YES |     | NULL                     |                               |
| ignore_severity                          | int(10) unsigned | YES |     | 1                        |                               |
| prefs                                    | varchar(255)     | YES |     | NULL                     |                               |
| check_info                               | varchar(255)     | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
8 rows

civicrm_subscription_history
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
| group_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
| date                                     | timestamp        | NO  |     | current_timestamp()      |                               |
| method                                   | varchar(8)       | YES |     | NULL                     |                               |
| status                                   | varchar(8)       | YES |     | NULL                     |                               |
| tracking                                 | varchar(255)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_survey
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| title                                    | varchar(255)     | NO  |     | NULL                     |                               |
| campaign_id                              | int(10) unsigned | YES | MUL | NULL                     |                               |
| activity_type_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| instructions                             | text             | YES |     | NULL                     |                               |
| release_frequency                        | int(10) unsigned | YES |     | NULL                     |                               |
| max_number_of_contacts                   | int(10) unsigned | YES |     | NULL                     |                               |
| default_number_of_contacts               | int(10) unsigned | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_default                               | tinyint(1)       | NO  |     | 0                        |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | datetime         | NO  |     | current_timestamp()      |                               |
| last_modified_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| last_modified_date                       | datetime         | NO  |     | current_timestamp()      | on update current_timestamp() |
| result_id                                | int(10) unsigned | YES |     | NULL                     |                               |
| bypass_confirm                           | tinyint(1)       | NO  |     | 0                        |                               |
| thankyou_title                           | varchar(255)     | YES |     | NULL                     |                               |
| thankyou_text                            | text             | YES |     | NULL                     |                               |
| is_share                                 | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
19 rows

civicrm_system_log
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| message                                  | varchar(128)     | NO  |     | NULL                     |                               |
| context                                  | longtext         | YES |     | NULL                     |                               |
| level                                    | varchar(9)       | YES |     | info                     |                               |
| timestamp                                | timestamp        | NO  |     | current_timestamp()      |                               |
| contact_id                               | int(10) unsigned | YES |     | NULL                     |                               |
| hostname                                 | varchar(128)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_tag
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | UNI | NULL                     |                               |
| label                                    | varchar(64)      | NO  |     | NULL                     |                               |
| description                              | varchar(255)     | YES |     | NULL                     |                               |
| parent_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
| is_selectable                            | tinyint(1)       | NO  |     | 1                        |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_tagset                                | tinyint(1)       | NO  |     | 0                        |                               |
| used_for                                 | varchar(64)      | YES |     | NULL                     |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| color                                    | varchar(255)     | YES |     | NULL                     |                               |
| created_date                             | datetime         | YES |     | current_timestamp()      |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
12 rows

civicrm_tell_friend
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  |     | NULL                     |                               |
| entity_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| title                                    | varchar(255)     | YES |     | NULL                     |                               |
| intro                                    | text             | YES |     | NULL                     |                               |
| suggested_message                        | text             | YES |     | NULL                     |                               |
| general_link                             | varchar(255)     | YES |     | NULL                     |                               |
| thankyou_title                           | varchar(255)     | YES |     | NULL                     |                               |
| thankyou_text                            | text             | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
10 rows

civicrm_timezone
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES |     | NULL                     |                               |
| abbreviation                             | char(3)          | YES |     | NULL                     |                               |
| gmt                                      | varchar(64)      | YES |     | NULL                     |                               |
| offset                                   | int(11)          | YES |     | NULL                     |                               |
| country_id                               | int(10) unsigned | NO  | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_translation
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| entity_table                             | varchar(64)      | NO  |     | NULL                     |                               |
| entity_field                             | varchar(64)      | NO  |     | NULL                     |                               |
| entity_id                                | int(11)          | NO  | MUL | NULL                     |                               |
| language                                 | varchar(5)       | NO  |     | NULL                     |                               |
| status_id                                | tinyint(4)       | NO  |     | 1                        |                               |
| string                                   | longtext         | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
7 rows

civicrm_uf_field
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| uf_group_id                              | int(10) unsigned | NO  | MUL | NULL                     |                               |
| field_name                               | varchar(64)      | NO  |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| is_view                                  | tinyint(1)       | NO  |     | 0                        |                               |
| is_required                              | tinyint(1)       | NO  |     | 0                        |                               |
| weight                                   | int(11)          | NO  |     | 1                        |                               |
| help_post                                | text             | YES |     | NULL                     |                               |
| help_pre                                 | text             | YES |     | NULL                     |                               |
| visibility                               | varchar(32)      | YES |     | User and User Admin Only |                               |
| in_selector                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_searchable                            | tinyint(1)       | NO  |     | 0                        |                               |
| location_type_id                         | int(10) unsigned | YES | MUL | NULL                     |                               |
| phone_type_id                            | int(10) unsigned | YES |     | NULL                     |                               |
| website_type_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| label                                    | varchar(255)     | NO  |     | NULL                     |                               |
| field_type                               | varchar(255)     | YES |     | NULL                     |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_multi_summary                         | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
19 rows

civicrm_uf_group
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | NO  | UNI | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| group_type                               | varchar(255)     | YES |     | NULL                     |                               |
| title                                    | varchar(64)      | NO  |     | NULL                     |                               |
| frontend_title                           | varchar(64)      | NO  |     | NULL                     |                               |
| description                              | text             | YES |     | NULL                     |                               |
| help_pre                                 | text             | YES |     | NULL                     |                               |
| help_post                                | text             | YES |     | NULL                     |                               |
| limit_listings_group_id                  | int(10) unsigned | YES | MUL | NULL                     |                               |
| post_url                                 | varchar(255)     | YES |     | NULL                     |                               |
| add_to_group_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
| add_captcha                              | tinyint(1)       | NO  |     | 0                        |                               |
| is_map                                   | tinyint(1)       | NO  |     | 0                        |                               |
| is_edit_link                             | tinyint(1)       | NO  |     | 0                        |                               |
| is_uf_link                               | tinyint(1)       | NO  |     | 0                        |                               |
| is_update_dupe                           | tinyint(1)       | NO  |     | 0                        |                               |
| cancel_url                               | varchar(255)     | YES |     | NULL                     |                               |
| is_cms_user                              | tinyint(1)       | NO  |     | 0                        |                               |
| notify                                   | text             | YES |     | NULL                     |                               |
| is_reserved                              | tinyint(1)       | NO  |     | 0                        |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | datetime         | YES |     | NULL                     |                               |
| is_proximity_search                      | tinyint(1)       | NO  |     | 0                        |                               |
| cancel_button_text                       | varchar(64)      | YES |     | NULL                     |                               |
| submit_button_text                       | varchar(64)      | YES |     | NULL                     |                               |
| add_cancel_button                        | tinyint(1)       | NO  |     | 1                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
27 rows

civicrm_uf_join
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| module                                   | varchar(64)      | NO  |     | NULL                     |                               |
| entity_table                             | varchar(64)      | YES | MUL | NULL                     |                               |
| entity_id                                | int(10) unsigned | YES |     | NULL                     |                               |
| weight                                   | int(11)          | NO  |     | 1                        |                               |
| uf_group_id                              | int(10) unsigned | NO  | MUL | NULL                     |                               |
| module_data                              | longtext         | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
8 rows

civicrm_uf_match
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| domain_id                                | int(10) unsigned | NO  | MUL | NULL                     |                               |
| uf_id                                    | int(10) unsigned | NO  | MUL | NULL                     |                               |
| uf_name                                  | varchar(128)     | YES | MUL | NULL                     |                               |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| language                                 | varchar(5)       | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_user_job
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(64)      | YES | UNI | NULL                     |                               |
| created_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| created_date                             | timestamp        | NO  |     | current_timestamp()      |                               |
| start_date                               | timestamp        | YES |     | NULL                     |                               |
| end_date                                 | timestamp        | YES |     | NULL                     |                               |
| expires_date                             | timestamp        | YES |     | NULL                     |                               |
| status_id                                | int(10) unsigned | NO  |     | NULL                     |                               |
| job_type                                 | varchar(64)      | NO  |     | NULL                     |                               |
| queue_id                                 | int(10) unsigned | YES | MUL | NULL                     |                               |
| metadata                                 | text             | YES |     | NULL                     |                               |
| is_template                              | tinyint(1)       | NO  |     | 0                        |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
12 rows

civicrm_website
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| contact_id                               | int(10) unsigned | YES | MUL | NULL                     |                               |
| url                                      | varchar(2048)    | YES |     | NULL                     |                               |
| website_type_id                          | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
4 rows

civicrm_word_replacement
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| find_word                                | varchar(255)     | YES |     | NULL                     |                               |
| replace_word                             | varchar(255)     | YES |     | NULL                     |                               |
| is_active                                | tinyint(1)       | NO  |     | 1                        |                               |
| match_type                               | varchar(16)      | YES |     | wildcardMatch            |                               |
| domain_id                                | int(10) unsigned | YES | MUL | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
6 rows

civicrm_worldregion
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| Field                                    | Type             | Null| Key | Default                  | Extra                         |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
| id                                       | int(10) unsigned | NO  | PRI | NULL                     | auto_increment                |
| name                                     | varchar(128)     | YES |     | NULL                     |                               |
+------------------------------------------+------------------+-----+-----+--------------------------+-------------------------------+
2 rows
```

### Data Types used by CiviCRM Fields

* blob
* char(2), char(3)
* date
* datetime
* decimal(10,8), decimal(18,9), decimal(20,2)
* double
* int(10) unsigned
* int(11)
* longtext
* mediumblob
* text
* timestamp
* tinyint(1), tinyint(4)
* varchar(10)
* other varchar's: 3, 4, 5, 6, 8, 9, 12, 15, 16, 20, 24, 32, 40, 45, 50, 63, 64, 96, 100, 127, 128, 254, 255, 512, 1024, 2048.
