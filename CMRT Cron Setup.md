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

## Step 2: Install the CiviCRM CLI Utility (cv)

The utility will be placed in the ~/bin directory. 

* Go to C-Panel Terminal
* `cd ~/bin`
  
*` wget -q https://download.civicrm.org/cv/cv.phar -O cv`

* `chmod +x cv`

Performing downloading of cv utility into ~/bin
```
[cmrailtr@s03dd bin]$ ls -l
total 8
-rwxr-xr-- 1 cmrailtr cmrailtr 221 May 29  2025 hello
[cmrailtr@s03dd bin]$ wget -q https://download.civicrm.org/cv/cv.phar -O cv
[cmrailtr@s03dd bin]$ chmod +x cv
[cmrailtr@s03dd bin]$ ls -l
total 3344
-rwxrwxr-x 1 cmrailtr cmrailtr 3415269 Mar 20 16:58 cv
-rwxr-xr-- 1 cmrailtr cmrailtr     221 May 29  2025 hello
```

Test
```
[cmrailtr@s03dd ~]$ cv --version
cv 0.3.71

```
    



