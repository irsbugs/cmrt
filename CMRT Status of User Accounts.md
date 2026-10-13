# Status of User Accounts on CiviCRM crm.cmrailtrail.org.au

2026-10-10

## Introduction 

In migrating the database from Spark Essentials to crm.cmrailtrail.org.au CiviCRM Standalone, the User accounts were preserved, however the passwords may have changed.

This document details the status of the User Accounts.


## Information about the User accounts on crm.cmrailtrail.org.au

The *maintenance* account on CiviCRM was last accessed on September 15th, 2026 3:00 AM. This would be the Spark development team converting the CiviCRM from Drupal to Standalone. 

This *maintenance* account on crm.cmrailtrail.org.au has now been set to is_active == false.



Using API4 to look at the Users of CiviCRM on the civi-AUST system (crm.cmrailtrail.org.au) the passwords were updated at: 2026-09-15 02:54:31. So this must have been Spark developers performing the Drupal to Standalone conversion.

I can see the following for the CiviCRM Users as well as their CiviCRM database Individual Contact details...

[cmrailtr@s03dd civicrm-standalone]$ cv api4 User.get +s id,username,uf_name,contact_id.first_name,contact_id.last_name,is_active -T
+-----+----------------------------+----------------------------+-----------------------+----------------------+-----------+
| id  | username                   | uf_name                    | contact_id.first_name | contact_id.last_name | is_active |
+-----+----------------------------+----------------------------+-----------------------+----------------------+-----------+
| 117 | maintenance                | spark@civicrm.org          | CiviCRM               | Maintenance          |           |
| 118 | admin                      | admin@cmrailtrail.org.au   | KenTest               | Stewart              | 1         |
| 123 | ken@cmrailtrail.org.au     | kjstewart52@gmail.com      | Ken                   | Stewart              | 1         |
| 124 | des@cmrailtrail.org.au     | desboucher1@gmail.com      | Des                   | Boucher              | 1         |
| 125 | kate@cmrailtrail.org.au    | kate.couttie@gmail.com     | Kate                  | Couttie              | 1         |
| 126 | carolyn@cmrailtrail.org.au | carolyn@carolyndennis.com  | Carolyn               | Dennis               | 1         |
| 127 | steve@cmrailtrail.org.au   | stevefoskey@hotmail.com    | Steve                 | Foskey               | 1         |
| 128 | steveh@cmrailtrail.org.au  | steveh@cmrailtrail.org.au  | Steve                 | Harrison             | 1         |
| 129 | geoff@cmrailtrail.org.au   | geoffreyhooke52@gmail.com  | Geoff                 | Hooke                | 1         |
| 130 | greg@cmrailtrail.org.au    | james.grsl@bigpond.com     | Greg                  | James                | 1         |
| 131 | janice@cmrailtrail.org.au  | janicesimpson@hotmail.com  | Janice                | Simpson              | 1         |
| 132 | maureen@cmrailtrail.org.au | maureenwelch56@gmail.com   | Maureen               | Welch                | 1         |
| 134 | civicrm_cron               | cron@cmrailtrail.org.au    | CMRT                  | Cron                 | 1         |
| 135 | noreply@cmrailtrail.org.au | noreply@cmrailtrail.org.au | CMRT                  | Noreply              | 1         |
| 136 | civicrm_irs                | irsbugs@hotmail.com        | Check                 | Stewart              | 1         |
+-----+----------------------------+----------------------------+-----------------------+----------------------+-----------+
[cmrailtr@s03dd civicrm-standalone]

For the Spark User "maintenance" I set it to in-active. Later I will delete it as a User of CiviCRM, and also delete its CiviCRM database Individual Contact record.

These following Users I setup and had to give them a new password in order to log in. They all have the same password: Redfxxx432@. However when I look at the "password hash" fields they are not the same. So I suspect we are now using a new password program / algorithm...

| 134 | civicrm_cron               | cron@cmrailtrail.org.au    | CMRT                  | Cron                 | 1         |
| 135 | noreply@cmrailtrail.org.au | noreply@cmrailtrail.org.au | CMRT                  | Noreply              | 1         |
| 136 | civicrm_irs                | irsbugs@hotmail.com        | Check                 | Stewart              | 1         |

The way i9t works is that I can log in by using either of two Usernames: E.g. "civicrm_cron" or "cron@cmrailtrail.org.au"

There is also the account:

| 118 | admin                      | admin@cmrailtrail.org.au   | KenTest               | Stewart              | 1         |

...which I can log into with Sparkxxxxk. Which you set after Spark had done the migration.

=====




Ian <stwrtn@gmail.com>
	
Sun, Oct 11, 10:05 PM (2 days ago)
	
	
to Ken
Hi Ken,

>I  tried again with kjstewart52@gmail.com and reset p/w and it worked

The fact that you had to reset your password suggests to me that when Spark did their migration the passwords got corrupted. Thus all the committee's passwords won't work to log into crm.cmrailtrail.org.au. However the password they use for the email login on Webmail/RoundCube should still work OK.

They need to initially log into Webmail/Roundcube using their email address and password. The Webmail link is:

https://s03dd.syd6.hostingplatform.net.au:2096/

If they have forgotten their password for the email then they (or you as admin) need to reset it. I think the password needs to be about 11 characters and have upper and lower-case and symbols, etc.

Using another Web-browser tab, they can then connect to the link to the Civi-AUST system:

https://crm.cmrailtrail.org.au/

If they can log in with their old password, then all good. Otherwise they have to click on "Forgotten password?" and request a password reset. They need to go back to the Webmail tab to get the email from CiviCRM and click on the link in the email to bring up the screen that allows them to reset their CiviCRM User account.

The list of the committee members with CiviCRM accounts is as follows. This email address is what they use for logging into both Webmail/RoundCube and the CiviCRM account....

des@cmrailtrail.org.au    
kate@cmrailtrail.org.au    
carolyn@cmrailtrail.org.au    
steve@cmrailtrail.org.au    
steveh@cmrailtrail.org.au    
geoff@cmrailtrail.org.au    
greg@cmrailtrail.org.au    
janice@cmrailtrail.org.au    
maureen@cmrailtrail.org.au

Maybe take your laptop to the meeting this week and they can use it to reset their passwords.

=====

FYI: The status of the other CIviCRM / Webmail accounts is:
 
maintenance <-- Disabled. Was used by Spark. To be deleted.
 
 admin <-- Ken reset this password a couple of weeks ago.
 ken@cmrailtrail.org.au <-- Ken reset password on this account on Sunday
 
 civicrm_cron <-- Ian runs the Scheduled Jobs
 noreply@cmrailtrail.org.au <--Ian - For email bounces
 civicrm_irs <-- Ian. - For testing. Will be deleted later.
 
 cmrt_campaign <-- Ian set this up 2926-10-11. Account to be passed to Campaign Manager.
 For Webmail/Roundcube: Username: cmrt_campaign@cmrailtrail.org.au Password: Campaignmgr@1
 For CiviCRM Account: Username: cmrt_campaign or cmrt_campaign@cmrailtrail.org.au Password: Campaignmgr@1
 
cheers, Ian
