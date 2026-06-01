# User Accounts on CiviCRM Standalone

## Introduction

When CiviCRM is a plugin to a CMS, E.g. Wordpress, then User accounts that login and access the CiviCRM and Wordpress dashboard are managed by the CMS.


With CiviCRM Standalone, the User accounts are managed by CiviCRM. A User account has a set of priviledges and a password, is linked to an Individual Contact who has an email address. The email address is likely to that of the mail system provided by the ISP and it will also have a password. In summary:

* CiviCRM User account requires:
  * Username
  * Password
* CiviCRM Individual Contact requires a minimum of:
  * First Name
  * Last Name
  * Email
* Email account requires:
  * Email username
  * Email password  
  * Display Name
 
As an example of the above:

* CiviCRM User account. In this case for the User account to manage Cron job:
  * Username: civicrm_cron
  * Password: Cronpassword#1 <--- If desired to have the same password for the email, then meet the Email password requirements specs.
  
Connection to login page from Web-browser: https://crm.cmrailtrail.org.au/civicrm/login Note: Ensure you are not already logged in with another account.
    
* CiviCRM Individual Contact requires a minimum of:
  * First Name: Cron
  * Last Name:  Admin
  * Email: cron@cmrailtrail.org.au

* Email account using VentraIP Webmail:
  * Email username: cron
  * Email password:  Cronpassword#1
  * Display Name: Cron Admin

Connection to VentraIP Webmail login from a web-browser: https://s03dd.syd6.hostingplatform.net.au:2096/

Note: During the Installation of CiviCRM Standalone the installation process requests and Administration User account, password and email address. 


## Example of adding password for Cron after creating the civicrm_cron user account. 

Performed by copying and pasting the Admin password.

```

MariaDB [cmrailtr_civi]> SELECT id, uf_id, uf_name, username, hashed_password FROM civicrm_uf_match;
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+
| id | uf_id | uf_name                        | username            | hashed_password                                         |
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+
|  1 |     1 | hello@cmrailtrail.org.au       | civicrm_admin       | $$1234------secure Bcrypt hashing algorithm------4321$$ |
|  2 |     2 | cron@cmrailtrail.org.au        | civicrm_cron        |                                                         |
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+

```
Use SQL to add the password for the Cron account with uf_id = 2.
```
MariaDB [cmrailtr_civi]> UPDATE civicrm_uf_match SET hashed_password = '$$1234------secure Bcrypt hashing algorithm-----4321$$' WHERE id = 2;

MariaDB [cmrailtr_civi]> SELECT id, uf_id, uf_name, username, hashed_password FROM civicrm_uf_match;
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+
| id | uf_id | uf_name                        | username            | hashed_password                                         |
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+
|  1 |     1 | hello@cmrailtrail.org.au       | civicrm_admin       | $$1234------secure Bcrypt hashing algorithm------4321$$ |
|  2 |     2 | cron@cmrailtrail.org.au        | civicrm_cron        | $$1234------secure Bcrypt hashing algorithm------4321$$ |
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+

```

On a web-browser go to: https://crm.cmrailtrail.org.au/civicrm/login

Log into civicrm_cron with password the same as civicrm_admin



## Gemini response to query on setting password in CiviCRM Standalone

Question to Gemini:  

Can the password be setup by using mysql and going to the CiviCRM uf_match table and inserting a hashed_password for the desired uf_id?

Yes, absolutely. You can set a password directly in the MySQL database for CiviCRM Standalone.

As you noted, CiviCRM Standalone repurposes the civicrm_uf_match table (which traditionally maps external CMS users to CiviCRM contacts) to store actual native user accounts.

### 1. The Table Structure

In a Standalone installation, the civicrm_uf_match table has added columns specifically for managing credentials, including username and password.

To update or set a password directly via MySQL, you will target the password column (not hashed_password) for the row corresponding to your target user ID.

### 2. The Hashing Mechanism

CiviCRM Standalone relies on PHP's native password_hash() function, which defaults to the secure Bcrypt hashing algorithm.

Because of this, you cannot use MySQL's legacy, built-in MD5() or SHA2() functions to generate the string. Doing so will break the login mechanism, as CiviCRM won't be able to verify it. You must generate a proper Bcrypt hash first.


## Step-by-Step Direct Database Update

### Step 1: Generate the Bcrypt Hash

You can use the command line via PHP to quickly spit out a properly formatted string:

```Bash

php -r "echo password_hash('YourNewSecurePassword', PASSWORD_BCRYPT) . PHP_EOL;"
```

*This will output a string resembling something like: $2y$10$abcdefghijklmnopqrstuv...*

### Step 2: Run the MySQL Update Statement

Log into your MySQL/MariaDB terminal and execute the update query against your target id:

```SQL
UPDATE civicrm_uf_match 
SET hashed_password = '$2y$10$YourGeneratedHashStringGoesHere...' 
WHERE id = 12;
```

⚠️ **Note on IDs:** Make sure you are filtering by the primary key id of the user account row in the civicrm_uf_match table, or by its uf_id (which matches the corresponding internal record), depending on how your specific accounts are indexed.

Once the query executes successfully, the user can immediately log in using their username and the plain-text password you just hashed. No cache clearing or system reboot is required!

# Gemini on permissions

 With CiviCRM Standalone which table and column in the database has the Admin and Staff permissions

In CiviCRM Standalone, user authentication, roles, and basic system permissions are managed by a core extension called standaloneusers. Because it operates without a traditional CMS (like Drupal or WordPress) handling user roles, it maintains its own distinct schema tables.  

The administration ("Admin") and staff-level permissions are split across two core tables in the database:
1. The Roles Table

To see the definition of the actual Admin and Staff roles, look at:

    Table: civicrm_user_role

    Column: name

In this column, you will find the distinct system string representations for your tiers, typically defined by default as admin (or administrator) and staff.
2. The Role-to-Permission Mapping Table

To see which specific fine-grained granular permissions (e.g., access CiviCRM, administer CiviCRM) are mapped to those Admin and Staff roles, you query:

    Table: civicrm_user_role_permission

    Columns: * role_id: Joins back to the civicrm_user_role table to identify if it is Admin or Staff.

        permission: A text string column containing the specific permission key assigned to that role.

Looking to check User Assignments?

If you are trying to figure out which individual human users belong to the Admin or Staff groups, you will want to look at:

    Table: civicrm_user_to_role

    Columns: user_id (the ID of the Standalone account) and role_id (the ID corresponding to the Admin/Staff record).


```

MariaDB [cmrailtr_civi]> show tables;
+------------------------------------------+
| Tables_in_cmrailtr_civi                  |
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
| civicrm_grant                            |
| civicrm_group                            |
| civicrm_group_contact                    |
| civicrm_group_contact_cache              |
| civicrm_group_nesting                    |
| civicrm_group_organization               |
| civicrm_im                               |
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
| civicrm_mosaico_template                 |
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
| civicrm_riverlea_stream                  |
| civicrm_role                             |
| civicrm_saved_search                     |
| civicrm_search_display                   |
| civicrm_search_param_set                 |
| civicrm_search_segment                   |
| civicrm_session                          |
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
| civicrm_totp                             |
| civicrm_translation                      |
| civicrm_translation_source               |
| civicrm_uf_field                         |
| civicrm_uf_group                         |
| civicrm_uf_join                          |
| civicrm_uf_match                         |
| civicrm_user_job                         |
| civicrm_user_role                        |
| civicrm_website                          |
| civicrm_word_replacement                 |
| civicrm_worldregion                      |
+------------------------------------------+
164 rows in set (0.001 sec)

```

```
MariaDB [cmrailtr_civi]> SHOW COLUMNS FROM civicrm_user_role;
+---------+------------------+------+-----+---------+----------------+
| Field   | Type             | Null | Key | Default | Extra          |
+---------+------------------+------+-----+---------+----------------+
| id      | int(10) unsigned | NO   | PRI | NULL    | auto_increment |
| user_id | int(10) unsigned | YES  | MUL | NULL    |                |
| role_id | int(10) unsigned | YES  | MUL | NULL    |                |
+---------+------------------+------+-----+---------+----------------+


MariaDB [cmrailtr_civi]> SELECT id, user_id, role_id FROM civicrm_user_role;
+----+---------+---------+
| id | user_id | role_id |
+----+---------+---------+
|  3 |       2 |       2 |
|  4 |       1 |       2 |
|  7 |       3 |       3 |
|  8 |       4 |       2 |
+----+---------+---------+
4 rows in set (0.000 sec)



```

All Permissions
* Afform: Inherit permission of afformQuickAddIndividual
* Afform: Inherit permission of afformQuickAddOrganization
* Afform: Inherit permission of afformQuickEditHousehold
* Afform: Inherit permission of afformQuickEditIndividual
* Afform: Inherit permission of afformQuickEditOrganization
* Afform: Inherit permission of afformSiteEmailAddress
* Afform: Inherit permission of afformSiteToken
* Afform: Inherit permission of afsearchAdminCustomFields
* Afform: Inherit permission of afsearchAdminCustomGroups
* Afform: Inherit permission of afsearchCustomFieldOptions
* Afform: Inherit permission of afsearchSiteEmailAddresses
* Afform: Inherit permission of afsearchSiteTokens
* Afform: Inherit permission of afsearchTabNote
* Afform: Inherit permission of afsearchTabRel
* Afform: Inherit permission of afsearchMosaicoTemplateList
* Afform: Inherit permission of afformEditMyAccount
* Afform: Inherit permission of afformEditRole
* Afform: Inherit permission of afformEditUserAccount
* Afform: Inherit permission of afsearchAdministerRoles
* Afform: Inherit permission of afsearchAdministerUserAccounts
* Afform: Inherit permission of afsearchMyAccount
* Afform: Inherit permission of afsearchPermissions
* Afform: Inherit permission of afAdminFormSubmissionList
* Afform: Inherit permission of afblockContactAddress
* Afform: Inherit permission of afblockContactEmail
* Afform: Inheritpermission of afblockContactIM
* Afform: Inherit permission of afblockContactNote
* Afform: Inherit permission of afblockContactPhone
* Afform: Inherit permission of afblockContactWebsite
* Afform: Inherit permission of afblockEventLocBlock
* Afform: Inherit permission of afblockNameHousehold
* Afform: Inherit permission of afblockNameIndividual
* Afform: Inherit permission of afblockNameOrganization
* Afform: Inherit permission of afblockParticipantNote
* Afform: Inherit permission of crmMsgadmMonaco
* Afform: Inherit permission of afsearchAllImports
* Afform: Inherit permission of afsearchMyImports
* Afform: Inherit permission of afsearchTemplates
* Afform: Inherit permission of afsearchCiviGrantDashboard
* Afform: Inherit permission of afsearchTabGrant
* Afform: Inherit permission of afformTabMember
* Afform: Inherit permission of afsearchAdminBadgelayout
* Afform: Inherit permission of afsearchAdminContactTypes
* Afform: Inherit permission of afsearchAdminFinancialTypes
* Afform: Inherit permission of afsearchAdminScheduledReminders
* Afform: Inherit permission of afsearchAdministerLocationTypes
* Afform: Inherit permission of afsearchAdministerMembershipStatusRules
* Afform: Inherit permission of afsearchAdministerNavigationMenu
* Afform: Inherit permission of afsearchAdministerPaymentProcessors
* Afform: Inherit permission of afsearchAdministerPriceFieldValues
* Afform: Inherit permission of afsearchAdministerPriceFields
* Afform: Inherit permission of afsearchAdministerPriceSets
* Afform: Inherit permission of afsearchAssignUsersToRoles
* Afform: Inherit permission of afsearchAssignedFinancialAccounts
* Afform: Inherit permission of afsearchCiviCRMQueues
* Afform: Inherit permission of afsearchFinancialAccounts
* Afform: Inherit permission of afsearchHeadersFootersAndAutomatedMessages
* Afform: Inherit permission of afsearchImportExportMappings
* Afform: Inherit permission of afsearchLabelFormats
* Afform: Inherit permission of afsearchMailAccounts
* Afform: Inherit permission of afsearchMailingBrowseScheduled
* Afform: Inherit permission of afsearchMailingClickThroughsResults
* Afform: Inherit permission of afsearchManageACLs
* Afform: Inherit permission of afsearchManageContributionPages
* Afform: Inherit permission of afsearchManageGroups
* Afform: Inherit permission of afsearchManageScheduledJobs
* Afform: Inherit permission of afsearchPersonalCampaignPages
* Afform: Inherit permission of afsearchPremiumProducts
* Afform: Inherit permission of afsearchPrintPagePDFFormats
* Afform: Inherit permission of afsearchProfileFields
* Afform: Inherit permission of afsearchProfiles
* Afform: Inherit permission of afsearchRelationshipTypes
* Afform: Inherit permission of afsearchSMSProvider
* Afform: Inherit permission of afsearchScheduledJobsLog
* Afform: Inherit permission of afsearchSettingsDatePreferences
* Afform: Inherit permission of afsearchTabActivity
* Afform: Inherit permission of afsearchTabCase
* Afform: Inherit permission of afsearchTabMember
* Afform: Inherit permission of afsearchTabParticipant
* Afform: Inherit permission of afsearchTabPledge
* Afform: Inherit permission of afsearchEmailBounceHistory
* Afform: Inherit permission of afformNewDonation
* Afform: Inherit permission of afsearchCampaignDashboard
* Afform: Inherit permission of afsearchSurveyOptionGroup
* AuthX: Authenticate to services with password
* AuthX: Authenticate to services with API key
* AuthX: Generate new JWT credentials for other users via the API
* AuthX: Validate credentials for other users via the API
* AuthX: Administer settings
* CiviCampaign: administer CiviCampaign
* CiviCampaign: manage campaign
* CiviCampaign: reserve campaign contacts
* CiviCampaign: release campaign contacts
* CiviCampaign: interview campaign contacts
* CiviCampaign: GOTV campaign contacts
* CiviCampaign: sign CiviCRM Petition
* CiviCase: delete in CiviCase
* CiviCase: administer CiviCase
* CiviCase: access my cases and activities
* CiviCase: access all cases and activities
* CiviCase: add cases
* CiviContribute: access CiviContribute
* CiviContribute: edit contributions
* CiviContribute: Refund contributions
* CiviContribute: make online contributions
* CiviContribute: delete in CiviContribute
* CiviCRM: add contacts
* CiviCRM: view all contacts
* CiviCRM: edit all contacts
* CiviCRM: view my contact
* CiviCRM: edit my contact
* CiviCRM: delete contacts
* CiviCRM: access deleted contacts
* CiviCRM: import contacts
* CiviCRM: import SQL datasource
* CiviCRM: edit groups
* CiviCRM: administer CiviCRM
* CiviCRM: skip IDS check
* CiviCRM: access uploaded files
* CiviCRM: profile listings and forms
* CiviCRM: profile listings
* CiviCRM: profile create
* CiviCRM: profile edit
* CiviCRM: profile view
* CiviCRM: access all custom data
* CiviCRM: view all activities
* CiviCRM: Delete activities
* CiviCRM: edit inbound email basic information
* CiviCRM: edit inbound email basic information and content
* CiviCRM: access CiviCRM backend and API
* CiviCRM: access Contact Dashboard
* CiviCRM: translate CiviCRM
* CiviCRM: manage tags
* CiviCRM: administer reserved groups
* CiviCRM: administer Tagsets
* CiviCRM: administer reserved tags
* CiviCRM: administer queues
* CiviCRM: administer dedupe rules
* CiviCRM: merge duplicate contacts
* CiviCRM: force merge duplicate contacts
* CiviCRM: view debug output
* CiviCRM: view all notes
* CiviCRM: add contact notes
* CiviCRM: access AJAX API
* CiviCRM: access contact reference fields
* CiviCRM: create manual batch
* CiviCRM: edit own manual batches
* CiviCRM: edit all manual batches
* CiviCRM: close own manual batches
* CiviCRM: close all manual batches
* CiviCRM: reopen own manual batches
* CiviCRM: reopen all manual batches
* CiviCRM: view own manual batches
* CiviCRM: view all manual batches
* CiviCRM: delete own manual batches
* CiviCRM: delete all manual batches
* CiviCRM: export own manual batches
* CiviCRM: export all manual batches
* CiviCRM: administer payment processors
* CiviCRM: render templates
* CiviCRM: edit message templates
* CiviCRM: edit system workflow message templates
* CiviCRM: edit user-driven message templates
* CiviCRM: view my invoices
* CiviCRM: edit api keys
* CiviCRM: edit own api keys
* CiviCRM: send SMS
* CiviCRM: administer CiviCRM System
* CiviCRM: administer CiviCRM Data
* CiviCRM: all CiviCRM permissions and ACLs
* CiviCRM Standalone Users: Allow users to access the reset password system
* CiviCRM Standalone Users: Administer user accounts
* CiviCRM Standalone Users: Bypass maintenance mode
* CiviCRM Standalone Users: Administer settings
* CiviCRM StandaloneUsers: View user accounts
* CiviEvent: access CiviEvent
* CiviEvent: edit event participants
* CiviEvent: edit all events
* CiviEvent: register for events
* CiviEvent: view event info
* CiviEvent: view event participants
* CiviEvent: delete in CiviEvent
* CiviEvent: manage event profiles
* CiviGrant: access CiviGrant
* CiviGrant: edit grants
* CiviGrant: delete in CiviGrant
* CiviMail: access CiviMail
* CiviMail: access CiviMail subscribe/unsubscribe pages
* CiviMail: delete in CiviMail
* CiviMail: view public CiviMail content
* CiviMail: create mailings
* CiviMail: schedule mailings
* CiviMail: approve mailings
* CiviMember: access CiviMember
* CiviMember: edit memberships
* CiviMember: delete in CiviMember
* CiviPledge: access CiviPledge
* CiviPledge: edit pledges
* CiviPledge: delete in CiviPledge
* CiviReport: access CiviReport
* CiviReport: access Report Criteria
* CiviReport: save Report Criteria
* CiviReport: administer private reports
* CiviReport: administer reserved reports
* CiviReport: administer Reports
* CiviReport: view report sql
* cms: administer users
* cms: view user account
* cms: bypass maintenance mode
* FormBuilder: edit and delete forms
* FormBuilder: edit and delete own forms
* Generic: Deny all users
* Generic: Allow all users (including anonymous)
* Generic: Allow any authenticated contact
* Generic: Anyone with secret link
* reCAPTCHA: Administer settings
* SearchKit: edit and delete all searches
* SearchKit: edit and delete own searches
* User Role: Administrator
* User Role: Staff

