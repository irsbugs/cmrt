# Mail setup for CiviCRM Standalone

## Introduction

CiviCRM defaults to using *mail()* the PHP mailer. VentraIP supports this mailer. However VentraIP, and other documentation, suggest that the *SMTP* mailer is a better choice. This document includes the setting up of SMTP as the mechanism for outgoing mail. It also includes the setting up of an inbox for *bounce* messages, and being able to pass this inbox contents to CiviCRM.

### Prerequisites

Notes and prerequisites for setting up CiviCMR mail:

* VentraIP provide the email service *mail.cmrailtrail.org.au* for CMRT.
* An email account is created using C-Panel --> Email --> Email Accounts
* At least two email accounts need to be created for CiviCRM mailing operations:
  	* An account that is the default that CiviCRM uses as: *Site from Email Address*
  	* The account called *bounce*, that allows SMTP outgoing email, and privides a return address for email bounce errors.
* When installing CiviCRM the administration login account that was created was given a temporary external personal email address. E.g. A gmail address. Having CiviCRM successfully send emails to this external gmail address will be used in testing. 
 
### Site from Email Address Account

Using C-Panel --> Email --> Email Accounts. Create a default outgoing mail sender address. For example: **hello** so that, by default, all bulk emails appear to have been sent by *hello@cmrailtrail.org.au*. If a recipient replies to one of these mails then their reply mail goes into the inbox of the *hello* email account. It is envisaged that the CMRT secretary monitors the inbox of this email account, and responds to any queries raised in these reply emails.

On CiviCRM go to *Site from Email Address* options with either of these links:
* Administer --> CiviMail --> Site from Email Address
* Mailings --> Site from Email Address

Click on *Add Email Address* and enter:
* Display Name: Castlemaine Maryborough Rail Trail
* Email: hello@cmrailtrail.org.au
* Description: Default domain email address and from name.
* Default: Checked

When a bulk email is sent from CiviCRM, then, by default, the recipient sees in their inbox an email from *Castlemaine Maryborough Rail Trail* which has an email address that they can respond to of *hello@cmrailtrail.org.au*

Note that other *from email* addresses may be added. E.g. President or The Committee, etc.  

### The Bounce Email Account

This email account may be given any name, but *bounce* is probably the most appropriate. Thus its email address is *bounce@cmrailtrail.org.au*. The e-mail account serves two purposes:

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

In CiviCRM, upon selecting the radio button for the mailer to be *SMTP* the *SMTP Configuration* panel apears and requires the following details to be entered.

* **SMTP Server:** ssl://mail.cmrailtrail.org.au
* **SMTP Port:** 465
* **Authentication:** Yes (checked)
* **SMTP Username:** bounce@cmrailtrail.org.au
* **SMTP Password:** r-8-@

When *Save & Send Test Email* is clicked, then an email is sent to the email address of the administrator with the emails subject: *Test for SMTP settings*. In this case it went to a personal gmail account as proof it was transmitted through the internet.

## CiviCRM Settings - for Bounced Mail.

If a CiviCRM originated email is undeliverable, a *bounce* message is sent back from the internet mail delivery systems to the *bounce@cmrailtrail.org.au* inbox. CiviCRM reads this inbox and generates report on the emails that bounced.

In CiviCRM go to: Administer --> CiviMail --> Mail Accounts

A default CiviCRM mail account has been created for Bounce Processing. Editing this account enables it to get bounce details from *bounce@mail.cmrailtrail.org.au* 

* **Name:** default - Name of this group of settings.
  
* **Server:** mail.cmrailtrail.org.au - Name or IP address of mail server machine.

* **Username:** bounce@cmrailtrail.org.au - Username to use when polling (for IMAP and POP3).

* **Password:** r-8-@ - Password to use when polling (for IMAP and POP3).

* **Localpart:** (Blank) - Optional local part (e.g., 'civimail+' for addresses like civimail+s.1.2@example.com).

* **Email Domain:** cmrailtrail.org.au - Email address domain (the part after @).

* **Return-Path:**  (Blank) - Contents of the Return-Path header. Consult with your SMTP provider what address to put in here so that the SMTP server accepts outgoing mail from CiviMail. If this field is left blank, the From email address will be used as the Return-Path.

* **Protocol:** IMAP - Name of the protocol to use for polling.

* **Mail Folder:** (Blank) - Inbox is default - Folder to poll from when using IMAP (will default to INBOX when empty), path to poll from when using Maildir, etc..

* **Use SSL?:** Checked - Secure Socket Layer is probablyt best. Whether to use SSL for IMAP and POP3 or not.

* **Used For?:** Bounce Processing - How this mail account will be used. Only one box may be used for bounce processing. It will also be used as the envelope email when sending mass mailings.


Click on *Save and Test*: Connection succeeded. Found at least 2 new messages. There are two messages but they are not bounce messages.

====
Tried *Save & Send Test Email* with admin email address changed to stwrtnzxc@gmail.com at about 11:40. Monitoring bounce@cmrailtrail.org.au for bounce message in inbox.
11:47 nothing added to inbox.
