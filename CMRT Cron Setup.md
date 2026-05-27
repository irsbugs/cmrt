# Cron Setup

The Cron utility is used so that the Linux operating system can trigger *scheduled jobs* to run in CiviCRM Standalone.

VentraIP has a C-Panel application called *Cron Jobs*. New cron jobs can be added using *Add New Cron Job*. The new cron job has a *Common Setting* that has been selected to be *Once per Five Minutes(\*5\*\*\*\*)*. Every five minutes the following command is excecuted:
```
/usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=civicrm_cron --cwd=/home/cmrailtr/civicrm-standalone >/dev/null 2>&1
```

To understand this command, the following is a break down of its components:
* `/usr/local/bin/php` tells linux to find `php` down the path `/usr/local/bin/`
* `/home/cmrailtr/bin/cv` tells `php` to find `cv` utility down the path `/home/cmrailtr/bin/`
* `cv` utility is a command-line tool designed for managing CiviCRM installations, allowing users to perform various administrative tasks directly from the terminal.
* `cv api` tells `cv` to use the CiviCRM *Application Programming Interface*, `api`. It should default to using the more modern `api4`, rather than `api3`.
* `job.execute` is the command passed to the `api`, to fire the relavent tasks on the CiviCRM Scheduled Jobs list.
* `--user=civicrm_cron` defines the username of the account `civicrm_cron` that has administrative priviledge that allows access to the api.  
* `--cwd=/home/cmrailtr/civicrm-standalone` is the path to the current-working-directory where CiviCRM is located.
* `>/dev/null 2>&1` is to run the command in the background and not to send any emails or logs about it.


There are two options for scheduling the CiviCRM jobs:
* Cron - Time-based job scheduler.
* [Systemd timers](https://docs.civicrm.org/sysadmin/en/latest/setup/jobs/#systemd-timers)  Used as a cron-like job scheduler.

Although the Systemd timers is a better solution, it would require admin staff at VentraIP to implement it for CMRT. Therefore cron will initially be used.

Although CiviCRM documents the setting up of [Schedule Jobs](https://docs.civicrm.org/sysadmin/en/latest/setup/jobs/), Gemini AI was used to create a document with the implementation steps.

## Step 1: Create a Dedicated Cron User in CiviCRM 

* For security and traceability, do not use your primary admin account to fire cron tasks.  
* Log in to your CiviCRM Standalone site.
* Go to Administer > Users and Permissions > User Accounts.
* Create a User with the user *civicrm_cron*, or similar, and assign them the Administrator role.
* Also register the User as an Individual contact.

Using Administrator > Users and Permissions > User Accounts, there is currently the account with the username *civicrm_admin* which was created as part of the CiviCRM Standalone installation process:

* Role: *Administrator*
* Username: *civicrm_admin*
* Contact: *Admin, Standalone*
* User Email: *Leave Blank to use the primary email from the selected contact*.
* Enabled: *Checked*
* Timezone: *Server Default Timezone*
* Preferred Language: *Server Default Language* 


Using Administrator > Users and Permissions > User Accounts, the following Cron administration account was setup using *+ Add User* to *Edit User account*:
* Role: *Administer*
* Username: *civicrm_cron*
* Contact: *Admin, Cron* Note: Clicking New Individual opens a registration window to add a new individual contact with email address.
* User Email: *Leave Blank to use the primary email from the selected contact*. Cron Admin Individual Contact email is: cron@cmrailtrail.org.au
* Enabled: *Checked*
* Timezone: *Server Default Timezone*
* Preferred Language: *Server Default Language*

Test. The following should work OK in Terminal from civicrm-standalone directory:
```
`[cmrailtr@s03dd civicrm-standalone]$ cv api job.execute --user=civicrm_cron
```
OR this from another directory:
```
[cmrailtr@s03dd ~]$ /usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=civicrm_cron --cwd=/home/cmrailtr/civicrm-standalone
```

## Step 2: Install the CiviCRM CLI Utility (cv)

The utility will be placed in the ~/bin directory. 

* Go to C-Panel Terminal
* `cd ~/bin`
* `wget -q https://download.civicrm.org/cv/cv.phar -O cv`
* `chmod +x cv`

For wget command:
    * -q (quiet): This turns off wget's progress bar and logging output, matching the -s (silent) flag you used in curl.
    * -O cv (output document): This tells wget to save the downloaded file specifically with the filename cv (capital O is critical here).

In software, a PHAR (PHP Archive) file is a package format to enable distribution of applications and libraries by bundling many PHP code files and other resources (e.g. images, stylesheets, etc.) into a single archive file.

PHAR files may be in one of three formats: tar, and ZIP, which are compatible with their respective tooling, and a custom PHAR format. Regardless of the format used, all PHAR files use the .phar file extension. Tar and Zip format archives may be created and unpacked using standard tar and zip utilities, while the PHAR format requires custom PHP code using the PHAR extension for PHP, or the PEAR PHP_Archive package.     

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

## Step 3: Cron email address

Create an email account for cron messages to go to.
* In CPanel > Email Accounts
* Domain: cmrailtrailo.org.au
* Username: cron
* Password: r-8-@
* Click: Create

```
Client Configuration settings for "cron@cmrailtrail.org.au".
	
Mail Client Manual Settings
Secure SSL/TLS Settings (Recommended)
Username: 	cron@cmrailtrail.org.au
Password: 	Use the email account's password.
Incoming Server: 	mail.cmrailtrail.org.au

    IMAP Port: 993 POP3 Port: 995 

Outgoing Server: 	mail.cmrailtrail.org.au

    SMTP Port: 465 

IMAP, POP3, and SMTP require authentication.
```

## Step 4: Configure the cPanel Cron Job Settings

* Log into your VentraIP **cPanel**.
* Scroll down to the **Advanced** section and click on **Cron Jobs**.
* Under **Add New Cron Job**, apply the following settings:


You can have cron send an email every time it runs a command which produces output. 

If you do not want an email to be sent for an individual cron job, you can redirect the command’s output to /dev/null. For example: mycommand >/dev/null 2>&1 

The `--user=civicrm_cron` flag tells the cv utility to log into CiviCRM as that specific user before running the background tasks. Because CiviCRM is running via the server's command line, it has no web browser session to tell it who is performing the action. Giving it a username lets CiviCRM know:
* It has the correct administrator permissions to execute system tasks.
* How to record the actions in the system logs (e.g., if a contact is updated by a cron job, the change log will correctly show it was modified by your cron user).


* Email: cron@cmrailtrail.org.au
* Clicked: Update Email
* Current Email: cron@cmrailtrail.org.au
  
* Common Settings: `Once per Five Minutes(*/5 ****)`
* Minute: `*/5 Oncew Per Five Minutes(*/5)`
* Hour: `* Every Hour(*)`
* Day: `* Every Day(*)`
* Month: `* Every Month(*)`
* Weekday: `* Every Day(*)`

Command Normal Usage: 
* `/usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=civicrm_cron --cwd=/home/cmrailtr/civicrm-standalone >/dev/null 2>&1`
Command when wanting to send an email confirmation every time the Cron job fires
* `/usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=civicrm_cron --cwd=/home/cmrailtr/civicrm-standalone`
* Click: Add New Cron Job


Displays: Current Cron Jobs
```
Minute 	Hour 	Day 	Month 	Weekday 	Command
*/5     *       *       *       *      /usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=civicrm_cron --cwd=/home/cmrailtr/civicrm-standalone >/dev/null 2>&1
```
When cron job fires successfully, without the >/dev/null 2>&1 in the command, the email logged will look like this:
```
Cron <cmrailtr@s03dd> /usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=civicrm_cron --cwd=/home/cmrailtr/civicrm-standalone
Contact photo
From (Cron Daemon) on 2026-05-27 09:10
Details Headers
{
    "is_error": 0,
    "version": 3,
    "count": 1,
    "values": 1
}
```

## Step 5: Verify It Is Running

Once configured in cPanel, CiviCRM handles the individual micro-jobs inside its own UI database.
* Go back into your CiviCRM interface.
* Navigate to Administer > System Settings > Scheduled Jobs.
* Look at any active job (like Send Scheduled Mailings or Clean-up temp data). Check the Last Run column. It should show a timestamp matching your newest cron cycle.

### Testing using Version Check 
[Job.version_check](https://docs.civicrm.org/user/en/latest/initial-set-up/scheduled-jobs/#job_version_check)

Checks for CiviCRM version updates. Important for keeping the database secure. Also sends anonymous usage statistics to civicrm.org to to assist in prioritizing ongoing development efforts.

    Name of scheduled job created by default: CiviCRM Update Check
    Recommended frequency: daily
    Parameters: none
Change the frequency from Dailty to Every Five Minutes, or Hourly, to check cron jobs aare firing OK.


## Links to Places to Review Cron Job status, etc:

The following are links to aspects related to Cron, the Cron Account, and Scheduled Jobs
* [Administer User Accounts](https://crm.cmrailtrail.org.au/civicrm/admin/users)
* [Cron Admin Individual Contact](https://crm.cmrailtrail.org.au/civicrm/contact/view?reset=1&cid=3)
* [Manage Schedule Jobs](https://crm.cmrailtrail.org.au/civicrm/admin/job?reset=1)
* [CiviCRM System Status](https://crm.cmrailtrail.org.au/civicrm/a/#/status)

Email
* [Email Accounts](https://s03dd.syd6.hostingplatform.net.au:2083/cpsess9498689760/frontend/jupiter/email_accounts/index.html#/list)
* [Cron Email account](https://s03dd.syd6.hostingplatform.net.au:2096/cpsess7418404251/3rdparty/roundcube/?_task=mail&_mbox=INBOX)


Documentation
* [Documentation Scheduled Jobs](https://docs.civicrm.org/sysadmin/en/latest/setup/jobs/)
* [Documentation - Systemd Timer](https://docs.civicrm.org/sysadmin/en/latest/setup/jobs/#systemd-timers)

## CiviCRM Standalone - Scheduled Jobd list

CiviCRM Standalone is supplied with a list of 22 Jobs to review and decide if they are to be enabled.
Note that the Cron job is run every five minutes

```
Job                                 Frequency                  Enabled  API
---------------------------------------------------------------------------------------------------------
CiviCRM Update Check                 Daily                       Yes    Job.version_check 
Clean-up Temporary Data and Files    Weekly                      Yes    Job.cleanup 
Dedupe Contacts                      Daily                       No     Job.process_batch_merge 
Disable expired relationships        Daily                       No     Job.disable_expired_relationships 
Fetch Bounces                        Hourly                      No     Job.fetch_bounces 
Geocode and Parse Addresses          Daily                       No     Job.geocode 
Group Cache Flush                    Hourly                      No     Job.group_cache_flush 
Mail Reports                         Daily                       No     Job.mail_report 
Process CiviMail Queue items         Hourly                      No     Mailing.runQueue 
Process Inbound Emails               Hourly                      No     Job.fetch_activities 
Process Pledges                      Daily                       No     Job.process_pledge 
Process Survey Respondents           Every time cron job is run  No     Job.process_respondent 
Rebuild Smart Group Cache            Hourly                      No     Job.group_rebuild 
Send Scheduled Mailings              Every time cron job is run  No     Job.process_mailing 
Send Scheduled Reminders             Hourly                      No     Job.send_reminder 
Send Scheduled SMS                   Every time cron job is run  No     Job.process_sms 
Update Individual Addressee          Daily                       No     Job.update_greeting 
Update Individual Email Greeting     Daily                       No     Job.update_greeting 
Update Individual Postal Greeting    Daily                       No     Job.update_greeting 
Update Membership Statuses           Daily                       No     Job.process_membership 
Update Participant Statuses          Every time cron job is run  No     Job.process_participant 
Validate Email Address from Mailings Daily                       No     Mailing.update_email_resetdate 
```
