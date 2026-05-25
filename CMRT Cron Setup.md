# Cron Setup

Cron utility will be used so that Linux can trigger *scheduled jobs* to run in CiviCRM Standalone.

There are two options for scheduling the CiviCRM jobs:
* Cron - Time-based job scheduler.
* [Systemd timers](https://docs.civicrm.org/sysadmin/en/latest/setup/jobs/#systemd-timers)  Used as a cron-like job scheduler.

Although the Systemd timers is a better solution, it would require admin staff at VentraIP to implement it for CMRT. Therefore cron will initially be used.

Although CiviCRM documents the setting up of [Schedule Jobs](https://docs.civicrm.org/sysadmin/en/latest/setup/jobs/), Gemini AI was used to create a document with the implementation steps.

## Step 1: Create a Dedicated Cron User in CiviCRM 

* For security and traceability, do not use your primary admin account to fire cron tasks.  
* Log in to your CiviCRM Standalone site.
* Go to Administer > Users and Permissions > Manage Users.
* Create a user named cron (or similar) and assign them the Administrator role.

Currently there is the administration account:
* Username: admin
* First name: CMRT  
* Last name: Admin
* Email: admin@cmrailtrail.org.au
* Password:
* Status: Active
* Role: Administrator

The following was Cron administration account was setup
* Username: admin-cron
* First name: CMRT  
* Last name: Admin-Cron
* Email: stwrtn@gmail.com Later make it: admin-cron@cmrailtrail.org.au
* Password: r-6-4
* Status: Active
* Role: Administrator

  
