# Status of User Accounts on CiviCRM crm.cmrailtrail.org.au

2026-10-10

## Introduction 

In migrating the database from Spark Essentials to crm.cmrailtrail.org.au CiviCRM Standalone, the User accounts were preserved, however the passwords may have changed.

This document details the status of the User Accounts.


## Information about the User accounts on crm.cmrailtrail.org.au

The *maintenance* account on CiviCRM, used by Spark Essentials staff, was last accessed on September 15th, 2026 3:00 AM. This would be the Spark development team converting the CiviCRM from Drupal to Standalone.

This *maintenance* account on crm.cmrailtrail.org.au has now been set to is_active = false.  Later, *maintenance* will be deleted as a User of crm.cmrailtrail.org.au CiviCRM, and also delete its CiviCRM database Individual Contact record.

Using API4 to look at the Users of CiviCRM on crm.cmrailtrail.org.au the passwords were updated at: 2026-09-15 02:54 to 02:56. This would have been Spark developers performing the Drupal to Standalone conversion.

This is the current list of User accounts on crm.cmrailtrail.org.au CiviCRM. Note that on logging into CiviCRM for the Username either the *username* or the *uf_name* can be used.

```
$ cv api4 User.get +s id,username,uf_name,contact_id.first_name,contact_id.last_name,is_active,when_updated -T
+-----+----------------------------+----------------------------------+-----------------------+----------------------+-----------+---------------------+
| id  | username                   | uf_name                          | contact_id.first_name | contact_id.last_name | is_active | when_updated        |
+-----+----------------------------+----------------------------------+-----------------------+----------------------+-----------+---------------------+
| 117 | maintenance                | spark@civicrm.org                | CiviCRM               | Maintenance          |           | 2026-10-06 14:55:36 |
| 118 | admin                      | admin@cmrailtrail.org.au         | KenTest               | Stewart              | 1         | 2026-09-15 09:11:26 |
| 123 | ken@cmrailtrail.org.au     | kjstewart52@gmail.com            | Ken                   | Stewart              | 1         | 2026-10-11 09:13:00 |
| 124 | des@cmrailtrail.org.au     | desboucher1@gmail.com            | Des                   | Boucher              | 1         | 2026-09-15 02:54:55 |
| 125 | kate@cmrailtrail.org.au    | kate.couttie@gmail.com           | Kate                  | Couttie              | 1         | 2026-09-15 02:55:58 |
| 126 | carolyn@cmrailtrail.org.au | carolyn@carolyndennis.com        | Carolyn               | Dennis               | 1         | 2026-09-15 02:56:26 |
| 127 | steve@cmrailtrail.org.au   | stevefoskey@hotmail.com          | Steve                 | Foskey               | 1         | 2026-09-15 02:57:13 |
| 128 | steveh@cmrailtrail.org.au  | steveh@cmrailtrail.org.au        | Steve                 | Harrison             | 1         | 2026-09-15 02:57:27 |
| 129 | geoff@cmrailtrail.org.au   | geoffreyhooke52@gmail.com        | Geoff                 | Hooke                | 1         | 2026-09-15 02:56:44 |
| 130 | greg@cmrailtrail.org.au    | james.grsl@bigpond.com           | Greg                  | James                | 1         | 2026-09-15 02:56:58 |
| 131 | janice@cmrailtrail.org.au  | janicesimpson@hotmail.com        | Janice                | Simpson              | 1         | 2026-09-15 02:55:12 |
| 132 | maureen@cmrailtrail.org.au | maureenwelch56@gmail.com         | Maureen               | Welch                | 1         | 2026-09-15 02:55:26 |
| 134 | civicrm_cron               | cron@cmrailtrail.org.au          | CMRT                  | Cron                 | 1         | 2026-10-07 08:24:54 |
| 135 | noreply@cmrailtrail.org.au | noreply@cmrailtrail.org.au       | CMRT                  | Noreply              | 1         | 2026-10-07 08:34:41 |
| 136 | civicrm_irs                | irsbugs@hotmail.com              | Check                 | Stewart              | 1         | 2026-10-06 19:05:50 |
| 137 | cmrt_campaign              | cmrt_campaign@cmrailtrail.org.au | CMRT                  | Campaign             | 1         | 2026-10-13 14:21:57 |
+-----+----------------------------+----------------------------------+-----------------------+----------------------+-----------+---------------------+

```
These following Users I setup and had to give them a new password in order to log in. They all have the same password: Rxxxxxx432x. However when I look at the "password hash" fields they are all different. So I suspect CiviCRM Standalone is now using a new password program / algorithm...

```
$ cv api4 User.get +s id,username,uf_name,hashed_password -T

| 134 | civicrm_cron               | cron@cmrailtrail.org.au          | $S$GqmlMKhHCcMyQEo3yx86Yhh22tBNV3zl4Ir.D.60Wm09ihZhvB06 |
| 135 | noreply@cmrailtrail.org.au | noreply@cmrailtrail.org.au       | $S$GBlyU1pF0hogb3rYWRLMQtR.HRYR5Fj1xX8zYbzxjlSKdvKirlCU |
| 136 | civicrm_irs                | irsbugs@hotmail.com              | $S$GuhnV3nzujJtcObxGfJCEufqjSI4h40dyYhddeOBNfBBqBBpwFPA |
```



If they can log in with their old password, then all good. Otherwise they have to click on "Forgotten password?" and request a password reset. They need to go back to the Webmail tab to get the email from CiviCRM and click on the link in the email to bring up the screen that allows them to reset their CiviCRM User account.

The list of the committee members with CiviCRM accounts is as follows. This email address is what they use for logging into both Webmail/RoundCube and the CiviCRM account. These accounts were initi9ally created on 2026-02-08:

* des@cmrailtrail.org.au    
* kate@cmrailtrail.org.au    
* carolyn@cmrailtrail.org.au    
* steve@cmrailtrail.org.au    
* steveh@cmrailtrail.org.au    
* geoff@cmrailtrail.org.au    
* greg@cmrailtrail.org.au    
* janice@cmrailtrail.org.au    
* maureen@cmrailtrail.org.au

Most of the committee last accessed the CiviCRM account on 2026-02-09. The exceptions are: Greg last accessed it on 2026-06-14 and Geoff last accessed it on 2026-08-31.

## Information about the special User accounts on crm.cmrailtrail.org.au

The status of the other CiviCRM / Webmail accounts is:
 
* maintenance <-- Disabled. Was used by Spark. To be deleted.
* admin <-- Ken reset this password a couple of weeks ago.
* ken@cmrailtrail.org.au <-- Ken reset password on this account on Sunday
* civicrm_cron <-- Ian runs the Scheduled Jobs
* noreply@cmrailtrail.org.au <--Ian - For email bounces
* civicrm_irs <-- Ian. - For testing. Will be deleted later.
* cmrt_campaign <-- Ian set this up 2926-10-11. Account to be passed to Campaign Manager. For Webmail/Roundcube: Username: cmrt_campaign@cmrailtrail.org.au Password: Cxxxxxxxmxx@x. For CiviCRM Account: Username: cmrt_campaign or cmrt_campaign@cmrailtrail.org.au Password: Cxxxxxxxmxx@x
 
