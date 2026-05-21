# Mail setup for CiviCRM Standalone

## Introduction

CiviCRM defaults to using PHP mailer, mail(). Which VentraIP supports. However VentraIP, and other documentation, suggest that SMTP mailing is a better choice. This document includes the setting up of SMTP as the mechanism for outgoing mail.

### Prerequisites

Notes and prerequisites for setting up CiviCMR mail:

* VentraIP provide the email service *mail.cmrailtrail.org.au* for CMRT.
* An email account is created using C-Panel --> Email --> Email Accounts
* At least two email accounts need to be created for CiviCRM mailing opeerations:
  	* An account that is the default that CiviCRM uses as: *Site from Email Address*
  	* The account called *bounce*, the allows SMTP outgoing email, and a return address for email bounce errors.
* When installing CiviCRM the administration login account that was created and given a temporary external personal email address. E.g. A gmail address. Having CiviCRM successfully send emails to this external gmail address will be used in testing. 
 
### Site from Email Address Account

Using C-Panel --> Email --> Email Accounts. Create a default outgoing mail sender address. For example: **hello** so that, by default, all bulk emails appear to have been sent by *hello@cmrailtrail.org.au*. If a recipient replies to one of these mails then their reply mail goes into the inbox of the *hello* email account. It is envisaged that the CMRT secretary monitors the inbox of this email account, and responds to any queries raised in these reply emails.

On CiviCRM go to *Site from Email Address* options with either of these links:
* Administer --> CiviMail --> Site from Email Address
* Mailings --> Site from Email Address

Click on *Add Email Address* and enter:
* Display Name: Castlemaine Maryborough Rail Trail
* Email: hello@cmrailtrail.org.au
* Description: Default domain email address and from name.
* Default: Check

When a bulk email is sent from CiviCRM, then, by default, the recipient sees in their inbox an email from *Castlemaine Maryborough Rail Trail* which has an email address that they can respond to of *hello@cmrailtrail.org.au*

Note that other *from email* addresses may be added. E.g. President or The Committee, etc.  

### The Bounce Email Account

This email account may be given any name, but *bounce* is probably the most appropriate. So its email address is *bounce@cmrailtrail.org.au*. The e-mail account serves two purposes:

* It allows CiviCRM bulk e-mails to have a path to get to the VentraIP SMTP server and then onto the internet to be delivered to the recipient.
* If a recipients email address is incorrect, then then *bounce* error information will be delivered to the inbox of *bounce@cmrailrailt.org.au*. CiviCRM reads the inbox of the bounce email account and generates bulk email reports on sucessful email deliveries and failed / bounced email deliveries.


## CiviCRM Settings - Outbound Mail.

CiviCRM, in conjuction with bounce@cmrailtrail.org.au, needs to be setup to use SMTP as its outbound mail.

In CiviCRM-Standalone go to: *Administer --> System Settings --> Outbound Email (SMTP/Sendmail)*. 

The CiviCRM Outbound Mailer Configuration will be defaulted to using *mail()*. i.e. The PHP mailer. This radio button needs to be changed to using the superior *SMTP* mailer method.

Aside: Regarding using *mail()*, it should be noted that: 
* Logged into *Admin Standalone* account of CiviCRM this account email is currently set to stwrtn@gmail.com
* With the selected mailer set to *mail()* then the *Save and Send Test* would sucessfully send an email to stwrtn@gmail.com with the subject: *Test for PHP mail setting*.

  
### SMTP Settings

For CiviCRM to send out SMTP emails, it needs to make use of the VentraIP email account *bounce@cmrailtrail.org.au*. CiviCRM bulk emails pass through the *bounce* account in order to get permission to use the VentraIP SMTP server and out on to the internet for delivery.

In the prerequisites section, the VentraIP email account *bounce@cmrailtrail.org.au* was created.

In CiviCRM, upon selecting the radio buttron for the mailer to be *SMTP* the *SMTP Configuration* panel apears and requires the following details to be entered.

* **SMTP Server:** ssl://mail.cmrailtrail.org.au
* **SMTP Port:** 465
* **Authentication:** Yes (checked)
* **SMTP Username:** bounce@cmrailtrail.org.au
* **SMTP Password:** r-8-@

When *Save & Send Test Email* is clicked, then an email is sent to the email address of the administrator with the emails subject: *Test for SMTP settings*. In this case it went to a personal gmail account as proof it was transmitted through the internet.

## CiviCRM Settings - for Bounced Mail.

If a CiviCRM originated email is undeliverable, a *bounce* message is sent back from the internet mail delivery systems to the *bounce@cmrailtrail.org.au* inbox. CiviCRM reads this inbox and generates report on the emails that bounced.

In CiviCRM go to: Administer --> CiviMail --> Mail Accounts

* Where I setup the "default" mail account to be bounce@mail.cmrailtrail.org.au. i.e.
* 
* Name: default - Name of this group of settings.
* Server: mail.cmrailtrail.org.au - Name or IP address of mail server machine.
* Username: bounce@mail.cmrailtrail.org.au - Username to use when polling (for IMAP and POP3).
* Password: redfred4 - Password to use when polling (for IMAP and POP3).
* Localpart bounce - Optional local part (e.g., 'civimail+' for addresses like civimail+s.1.2@example.com).
* Email Domain: mail.cmrailtrail.org.au - Email address domain (the part after @).
* Return-Path:   - Contents of the Return-Path header. Consult with your SMTP provider what address to put in here so that the SMTP server accepts outgoing mail from CiviMail. If this field is left blank, the From email address will be used as the Return-Path.
* Protocol IMAP - Name of the protocol to use for polling.
* Mail Folder - Folder to poll from when using IMAP (will default to INBOX when empty), path to poll from when using Maildir, etc..
* Use SSL?: Checked - Secure Socket Layer is probablyt best. Whether to use SSL for IMAP and POP3 or not.
* Used For?: Bounce Processing - How this mail account will be used. Only one box may be used for bounce processing. It will also be used as the envelope email when sending mass mailings.



=====


, so its address for incoming emails from the internet is: *bounces@mail.cmrailtrail.org.au*


Is this true?

* All bulk e-mails out of CiviCRM will go through this *bounce* account and go through *mail.cmrialtrail.org.au* to find the VentraIP SNMP server and be delivered to the recipient.
* CiviCRM has outgoing *throttle* settings to control the flow-rate of the bulk emails bering sent.
* In the event that a recipient does not exist, the internet mail system will return a bounce message to *bounces@mail.cmrailtrail.org.au* 

* CiviCRM run a cron job that monitors the bounce@mail.cmrailtrail.org.au account

The account could be 

must exist

```
Ken Stewart
	
	5:27 PM (2 hours ago)
Hi Ian, Hey Ian, Thank you for your reply! PHPmail is enabled on our shared hosting services, although we don't recommend using it when sending mail from it bec
Ian <stwrtn@gmail.com>
	
7:53 PM (6 minutes ago)
	


In the General Section I leave unchanged. Not that I understand what they are all about i.e.:
Allow mail from logged in contact  Enabled
Simple mail limit: 50
Use Smarty in schedule reminders: Disabled
VERP Separator: .
Treat SMRP Error 450.4.1.2 as permanent: No



Administer --> CiviMail --> Mail Accounts

Where I setup the "default" mail account to be bounce@mail.cmrailtrail.org.au. i.e.

Name: default - Name of this group of settings.
Server: mail.cmrailtrail.org.au - Name or IP address of mail server machine.
Username: bounce@mail.cmrailtrail.org.au - Username to use when polling (for IMAP and POP3).
Password: redfred4 - Password to use when polling (for IMAP and POP3).
Localpart bounce - Optional local part (e.g., 'civimail+' for addresses like civimail+s.1.2@example.com).
Email Domain: mail.cmrailtrail.org.au - Email address domain (the part after @).
Return-Path:   - Contents of the Return-Path header. Consult with your SMTP provider what address to put in here so that the SMTP server accepts outgoing mail from CiviMail. If this field is left blank, the From email address will be used as the Return-Path.
Protocol IMAP - Name of the protocol to use for polling.
Mail Folder - Folder to poll from when using IMAP (will default to INBOX when empty), path to poll from when using Maildir, etc..
Use SSL?: Checked - Secure Socket Layer is probablyt best. Whether to use SSL for IMAP and POP3 or not.
Used For?: Bounce Processing - How this mail account will be used. Only one box may be used for bounce processing. It will also be used as the envelope email when sending mass mailings.

There is also the Mailer Settings, but I won't change that at the moment...
Administer --> CiviMail --> Mailer Settings 
Outbound Mailing
Mailer Batch Limit  
Mailer Throttle Time  
Mailer Job Size  
Mailer Cron Job Limit  
Database Update Frequency

Reply and Unsubscribe
Enable Custom Reply-To: Disabled
Unsubscribe Methods  
Default One Click Unsubscribe Mode:L Unsubscribe
```
So, does the above sound OK with you? 
cheers, Ian.


From [cmrailtrail.org.au] Client configuration settings for “bounce@cmrailtrail.org.au”. 
```
Client Configuration settings for "bounce@cmrailtrail.org.au".
	
Mail Client Manual Settings
Secure SSL/TLS Settings (Recommended)
Username: 	bounce@cmrailtrail.org.au
Password: 	Use the email account's password.
Incoming Server: 	mail.cmrailtrail.org.au

    IMAP Port: 993 POP3 Port: 995 

Outgoing Server: 	mail.cmrailtrail.org.au

    SMTP Port: 465 

IMAP, POP3, and SMTP require authentication.


Calendar & Contacts Manual Settings
Secure SSL/TLS Settings (Recommended).
Username: 	bounce@cmrailtrail.org.au
Password: 	Use the email account's password.
Server: 	https://mail.cmrailtrail.org.au:2080

    Port: 2080 

Full Calendar URL(s): 	

    Calendar: https://mail.cmrailtrail.org.au:2080/calendars/__uids__//calendar Task List: https://mail.cmrailtrail.org.au:2080/calendars/__uids__//tasks 

Full Contact List URL(s): 	

    Address Book: https://mail.cmrailtrail.org.au:2080/addressbooks/__uids__//addressbook 

Non-SSL Settings (NOT Recommended).
Username: 	bounce@cmrailtrail.org.au
Password: 	Use the email account's password.
Server: 	http://mail.cmrailtrail.org.au:2079

    Port: 2079 

Full Calendar URL(s): 	

    Calendar: http://mail.cmrailtrail.org.au:2079/calendars/__uids__//calendar Task List: http://mail.cmrailtrail.org.au:2079/calendars/__uids__//tasks 

Full Contact List URL(s): 	

    Address Book: http://mail.cmrailtrail.org.au:2079/addressbooks/__uids__//addressbook 

```

Mail not sent  timeout...
```
Mail Not Sent
Sending test email.:
From: hello@cmrailtrail.org.au
To: stwrtn@gmail.com
Oops. Your SMTP settings are incorrect. No test mail has been sent.

An error occurred when CiviCRM attempted to send an email (via SMTP). If you received this error after submitting on online contribution or event registration - the transaction was completed, but we were unable to send the email receipt.

The mail library returned the following error message:
Failed to connect to mail.cmrailtrail.org.au:465 [SMTP: Invalid response code received from SMTP server while sending email. This is often caused by a misconfiguration in Outbound Email settings. Please verify the settings at Administer CiviCRM >> Global Settings >> Outbound Email (SMTP). (code: -1, response: )]

This is probably related to a problem in your Outbound Email Settings (Administer CiviCRM » System Settings » Outbound Email), OR the FROM email address specifically configured for your contribution page or event. Possible causes are:

    Your Sendmail path is incorrect.
    Your Sendmail argument is incorrect.
    The Site From Email Address configured for this feature may not be a valid sender based on your email service provider rules.

Check this page for more information.

```

Try again, Save and Test Email, without authentication: 
```
Mail Not Sent
Sending test email.:
From: hello@cmrailtrail.org.au
To: stwrtn@gmail.com
Oops. Your SMTP settings are incorrect. No test mail has been sent.

An error occurred when CiviCRM attempted to send an email (via SMTP). If you received this error after submitting on online contribution or event registration - the transaction was completed, but we were unable to send the email receipt.

The mail library returned the following error message:
Failed to connect to mail.cmrailtrail.org.au:465 [SMTP: Invalid response code received from SMTP server while sending email. This is often caused by a misconfiguration in Outbound Email settings. Please verify the settings at Administer CiviCRM >> Global Settings >> Outbound Email (SMTP). (code: -1, response: )]

This is probably related to a problem in your Outbound Email Settings (Administer CiviCRM » System Settings » Outbound Email), OR the FROM email address specifically configured for your contribution page or event. Possible causes are:

    Your Sendmail path is incorrect.
    Your Sendmail argument is incorrect.
    The Site From Email Address configured for this feature may not be a valid sender based on your email service provider rules.

Check this page for more information.

https://docs.civicrm.org/user/en/latest/advanced-configuration/email-system-configuration
```

Try adding ssl://mail.cmrailtraial.org.au

SAame mail-not dent message.

The mail library returned the following error message:
authentication failure 

SMTP: Invalid response code received from SMTP server while sending email. This is often caused by a misconfiguration in Outbound Email settings. Please verify the settings at Administer CiviCRM >> Global Settings >> Outbound Email (SMTP). (code: 535, response: Incorrect authentication data)
ssl error code 535
Tried Username of just "bounce" with ssl:// 

Tried

https://mail.cmrailtrail.org.au

The mail library returned the following error message:
Unable to find the socket transport "https" - did you forget to enable it when you configured PHP?

=====

Failed to connect to mail.cmrailtrail.org.au:465 
SMTP: Invalid response code received from SMTP server while sending email. This is often caused by a misconfiguration in Outbound Email settings. Please verify the settings at Administer CiviCRM >> Global Settings >> Outbound Email (SMTP). (code: -1, response: )

SMTP USername off bounce@cmrailtrail.org.au

Above but with ssl://

Worked.


redfred4@@


