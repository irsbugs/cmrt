# Mail setup for CiviCRM Stanalone

## Introduction

CiviCRM defaults to using PHP mailer, mail(). Which VentraIP supports. However VentraIP, and othjer documentation, suggest that SNMP mailing is superior.

* VentraIP provide the e-mail service *mail.cmrailtrail.org.au*
* An e-mail account is created Using C-Panel -> Email -> Email Accounts
* The account may be named *bounces*, so its address for incoming emails from the internet is: *bounces@mail.cmrailtrail.org.au*


Is this true?

* All bulk e-mails out of CiviCRM will go through this *bounce* account and go through *mail.cmrialtrail.org.au* to find the VentraIP SNMP server and be delivered to the recipient.
* CiviCRM has outgoing *throttle* settings to control the flow-rate of the bulk emails bering sent.
* In the event that a recipient does not exist, the internet mail system will return a bounce message to *bounces@mail.cmrailtrail.org.au* 

* CiviCRM run a cron job that monitors the bounce@mail.cmrailtrail.org.au account

The account could be 

must exist

##  Setup of Settings - Outbound Mail.

With CiviCRM-Standalone, *Administer --> System Settings --> Outbound Email (SMTP/Sendmail)*, the CiviCRM default Outbound Mail of PHP mailer i.e. *mail()*, needs to be changed to using the superior *SMTP* method of sending emails.

Regarding using *mail()*, it should be noted that: 
* Logged into *Admin Standalone* account of CiviCRM this account email is currently set to stwrtn@gmail.com
* With the selected mailer set to *mail()* then the *Save and Send Test* would sucessfully send an email to stwrtn@gmail.com with trhe subject: *Test for PHP mail setting*.
  
### SMTP Settings

For CiviCRM to send out emails, it needs to have a VentraIP email account to pass the emails through and thus find the VentraIP SMTP server which get the mail out onto the internet.

An email account was created on the cmrailtrail.org.au VentraIP account. The name of the account is *bounce*. An email can be sent to this email account by addressing it to *bounce@cmrailtrail.org.au* It was called bounce as later it will be set up so that CiviCRM can read its inbox and see if any "bounced" emails occurred.

Upon selecting the mailer to be *SMTP* the *SMTP Configuration* panel apears and requires the following details to be entered.

* **SMTP Server:** ssl://mail.cmrailtrail.org.au
* **SMTP Port:** 465
* **Authentication:** Yes (checked)
* **SMTP Username:** bounce@cmrailtrail.org.au
* **SMTP Password:** r-8-@

When *Save & Send Test Email* is clicked, then an email is sent to stwrtn@gmail.com with the subject: *Test for SMTP settings*.


```
Ken Stewart
	
	5:27 PM (2 hours ago)
Hi Ian, Hey Ian, Thank you for your reply! PHPmail is enabled on our shared hosting services, although we don't recommend using it when sending mail from it bec
Ian <stwrtn@gmail.com>
	
7:53 PM (6 minutes ago)
	
	
to Ken
Hi Ken,

The VentraIP guy is not really very clear to me, but I guess he doesn't know CiviCRM, so he stays clear of mentioning it.

I figure we need to create in C-Panel an email account called "bounce" along with the 29 other e-mail accounts that exist.
The email is set to have a password of, say, redfred4. MY understanding is that through the bounce account the CiviCRM bulk emails will go out, and CiviCRM will monitor the bounce inbox to see if there were any bounces.

Then  I go ahead with seting up the Administer -->  System and Settings --> Outbound Email (SMNP/Sendmail)  
and select the smtp (instead of mail())
 
For SMTP configuration I set...

    SMTP Server: mail.cmrailtrail.org.au
    SMTP Port: 465
    Authentication: Yes
    Username: bounce@mail.cmrailtrial.org.au
    Password: redfred1

These questions don't seem to be asked...

    Security Type: SSL/TLS
    Authentication Method: Password


In the General Section I leave unchanged. Not that I understand what they are all about i.e.:
Allow mail from logged in contact  Enabled
Simple mail limit: 50
Use Smarty in schedule reminders: Disabled
VERP Separator: .
Treat SMRP Error 450.4.1.2 as permanent: No

I should then be able to simulate sending a bulk email to stwrtn@gmail.com

Moving on... If that works I'll then try setting up:

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


