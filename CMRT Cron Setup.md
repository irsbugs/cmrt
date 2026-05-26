# Cron Setup

The Cron utility is used so that the Linux operating system can trigger *scheduled jobs* to run in CiviCRM Standalone.

VentraIP has a C-Panel application called *Cron Jobs*. New cron jobs can be added using *Add New Cron Job*. The new cron job has a *Common Setting* that has been selected to be *Once per Five Minutes(\*5\*\*\*\*)*. Every five minutes the following command is excecuted:

`/usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=civicrm_cron --cwd=/home/cmrailtr/civicrm-standalone`

To understand this command, the following is a break down of its components:
* `/usr/local/bin/php` tells linux to find `php` down the path `/usr/local/bin/`
* `/home/cmrailtr/bin/cv` tells `php` to find `cv` utility down the path `/home/cmrailtr/bin/`
* The CiviCRM `cv` utility is a command-line tool designed for managing CiviCRM installations, allowing users to perform various administrative tasks directly from the terminal.
* `cv api` tells `cv` to use the CiviCRM *Application Programming Interface*, `api`. It should default to using the more modern `api4`, rather than `api3`.
* `job.execute` is the command passed to the `api`, to fire the relavent tasks on the CiviCRM Scheduled Jobs list.
* `--user=civicrm_cron` defines the username of the account `civicrm_cron` that has administrative priviledge that allows access to the api.  
* `--cwd=/home/cmrailtr/civicrm-standalone` is the path to the current-working-directory where CiviCRM is located.



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
## Step 3: Configure the cPanel Cron Job Settings

* Log into your VentraIP **cPanel**.
* Scroll down to the **Advanced** section and click on **Cron Jobs**.
* Under **Add New Cron Job**, apply the following settings:


You can have cron send an email every time it runs a command which produces output. 

If you do not want an email to be sent for an individual cron job, you can redirect the command’s output to /dev/null. For example: mycommand >/dev/null 2>&1 

The --user=admin-cron flag tells the cv utility to log into CiviCRM as that specific user before running the background tasks. Because CiviCRM is running via the server's command line, it has no web browser session to tell it who is performing the action. Giving it a username lets CiviCRM know:
* It has the correct administrator permissions to execute system tasks.
* How to record the actions in the system logs (e.g., if a contact is updated by a cron job, the change log will correctly show it was modified by your cron user).



* Email: stwrtn@gmail.com
* Clicked: Update Email
* Current Email: stwrtn@gmail.com
* Common Settings: `Once per Five Minutes(*/5 ****)`
* Minute: `*/5 Oncew Per Five Minutes(*/5)`
* Hour: `* Every Hour(*)`
* Day: `* Every Day(*)`
* Month: `* Every Month(*)`
* Weekday: `* Every Day(*)`

PHP command examples: /usr/local/bin/php /home/cmrailtr/public_html/path/to/cron/script 

Command: 
* `/usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=admin-cron --cwd=/home/cmrailtr/civicrm-standalone >/dev/null 2>&1`
* Click: Add New Cron Job


Displays: Current Cron Jobs
```
Minute 	Hour 	Day 	Month 	Weekday 	Command
*/5     *       *       *       *           /usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=admin-cron --cwd=/home/cmrailtr/civicrm-standalone >/dev/null 2>&1
```

## Step 4: Verify It Is Running

Once configured in cPanel, CiviCRM handles the individual micro-jobs inside its own UI database.
* Go back into your CiviCRM interface.
* Navigate to Administer > System Settings > Scheduled Jobs.
* Look at any active job (like Send Scheduled Mailings or Clean-up temp data). Check the Last Run column. It should show a timestamp matching your newest cron cycle.


[Job.version_check](https://docs.civicrm.org/user/en/latest/initial-set-up/scheduled-jobs/#job_version_check)

Checks for CiviCRM version updates. Important for keeping the database secure. Also sends anonymous usage statistics to civicrm.org to to assist in prioritizing ongoing development efforts.

    Name of scheduled job created by default: CiviCRM Update Check
    Recommended frequency: daily
    Parameters: none



Not triggering

Rewmoved
* >/dev/null 2>&1

So should send emails to me every 5 mins?

Changed to:

 `/usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=admin-cron --cwd=/home/cmrailtr/civicrm-standalone`


drwxr-x---  7 cmrailtr nobody       4096 May 26 09:48 public_html
drwxr-x---  8 cmrailtr nobody       4096 May 25 15:41 civicrm-standalone
750

Change civicrm-strandalone to 755:

drwxr-xr-x  8 cmrailtr nobody       4096 May 25 15:41 civicrm-standalone

/usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=cron --cwd=/home/cmrailtr/civicrm-standalone >/dev/null 2>&1

/usr/local/bin/php /home/cmrailtr/bin/cv api job.execute --user=admin-cron --cwd=/home/cmrailtr/civicrm-standalone >/dev/null 2>&1

