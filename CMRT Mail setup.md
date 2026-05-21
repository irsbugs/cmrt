# Mail setup for CiviCRM Stanalone

## Introduction

CiviCRM defaults to using PHP mailer, mail(). Which VentraIP supports. However VentraIP, and othjer documentation, suggest that SNMP mailing is superior.

* VentraIP provide the e-mail service *mail.cmrailtrail.org.au*
* An e-mail account is created Using C-Panel -> Email -> Email Accounts
* The account may be named *bounces*, so its address for incoming emails from the internet is: *bounces@mail.cmrailtrail.org.au*


Is this true?

* All bulk e-mails out of CiviCRM will go through [this account] go through *mail.cmrialtrail.org.au* to find the VentraIP SNMP server and be delivered to the recipient.
* CiviCRM has outgoing *throttle* settings to control the flow-rate of the bulk emails bering sent.
* In the event that a recipient does not exist, the internet mail system will return a bounce message to *bounces@mail.cmrailtrail.org.au* 

* CiviCRM run a cron job that monitors the bounce@mail.cmrailtrail.org.au account

The account could be 

must exist
