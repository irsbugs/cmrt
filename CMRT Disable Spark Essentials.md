# Disabling of Spark Essentials

## Introduction 

Around the 5th September 2026 Spark Essentials migrated the CiviCRM from being Drupal based to a Standalone based application.

During September and October 2026 the Spark Essentials Standalone version of CiviCRM was migrated to CiviCRM Standalone on the sub-domain crm.cmrailtrail.org.au. During this period there was a time when both CiviCRM's were in operation. As a result both systems may have been performing duplications where they sent out the same reminder email, etc.

On 10 October 2026 the Spark Essentials CiviCRM was completely neutralized while maintaining administrative fallback access. This document describes the steps performed on Spark Essentials. 


## Steps Performed Disabling of Spark Essentials

To ensure Spark Essentials is completely neutralized while maintaining your administrative fallback access:

Log into Spark Essentials administration dashboard (cmrailtrail.civicrm.org).

====

### Disable non-esstential User accounts

Administer --> Users and Permissions --> User Accounts

Disabled 9 x Committee member accounts

Accounts still enabled: (username / email)

admin / admin@cmrailtrial.org.au
ken@cmrailtrail.org.au / kjstewart52@gmail.com
maintenance / spark@civicrm.org

### Disable All Scheduled Jobs in Spark Essentials

Go to Administer > System Settings > Scheduled Jobs.

Of the 26 jobs listed, 13 were enabled.
The following 13 jobs which were enabled, have now been changed to disabled.

* CiviCRM Update Check (Daily)
* Clean-up Temporary Data and Files (Daily)
* Disable expired relationships (Daily)
* Firewall: Cleanup (Daily)
* Process CiviMail Queue items (Hourly)
* Process PaymentProcessor Webhooks (Always)
* Rebuild Smart Group Cache (Daily)
* Send Scheduled Mailings (Always)
* Send Scheduled Reminders (Daily)
* Stripe: Cleanup (Hourly)
* TSYS Payments Recurring Contributions (Daily)
* Update Membership Statuses (Daily)
* Update Participant Statuses (Daily)

### Disable Outbound Email Delivery (Extra Safety Net)

To guarantee that no accidental manual trigger or background task sends emails to real users from Spark Essentials:

Go to Administer > System Settings > Option Groups > Outbound Email.


There is no Option Group called: Outbound Email.

However, this link: https://cmrailtrail.civicrm.org/civicrm/admin/setting/smtp?reset=1

...went to Settings - Outbound Mail.

In Mailer Configuration

...there is: Mailer Select: which was set to: mail()

Changed this to: Disable Outbound mail.

Saved Settings.

### Sent an email to: Test Newsletter Group

How to verify: Send a test mailing or email from within Spark Essentials; no email should arrive in a live recipient's inbox.

    Pay special attention to:
        Send Scheduled Reminders (membership renewals/reminders)
        Process Inbound Emails
        Geocode and Parse Addresses
        Mailings Scheduler / Send Scheduled Mailings

How to verify: Check the Scheduled Jobs list. The status for every row should display as Disabled, and the "Last Run" column should no longer update automatically.

On sending two error messages reported mail not sent.

https://cmrailtrail.civicrm.org/civicrm/mailing/report?mid=118&reset=1

CiviMail Report: Test mail that should not go out
Delivery Summary
Delivery has not yet begun for this mailing. If the scheduled delivery date and time is past, ask the system administrator or technical support contact for your site to verify that the automated mailer task ('cron job') is running - and how frequently. Learn more...
Intended Recipients 2
Successful Deliveries 0 (0.00%) ReportAdvanced Search
Unique Opens 0 (0.00%) ReportAdvanced Search

CiviCRM System Status reports:

Invalid outbound email method
Outgoing emails are not using SMTP delivery.

Outbound Email Disabled
Warning: Outbound email is disabled in system settings. Proper settings should be enabled on production servers.

### Put Spark Essentials in Maintenance Mode (Optional)

If you want to ensure no staff or logged-in users accidentally work on the old system while keeping admin access open:

Go to Administer > System Settings > Maintenance Mode (or update site availability via CiviCRM settings).

Enable maintenance mode with a message stating: "This CiviCRM instance has moved to crm.civicrm.org.au."

Once you are fully confident that all data migration is complete and crm.civicrm.org.au is handling all live activities smoothly, you can proceed with contacting CiviCRM Spark management to cancel and close the account.

There is no option to go to "Maintenance Mode". Should be OK as Most Users have now been disabled.

