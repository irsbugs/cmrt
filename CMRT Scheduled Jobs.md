# Scheduled Jobs

## Introduction

The *Scheduled Jobs* may be observed from *Administer --> Systemn Settings --> Scheduled Jobs*

Via api4 this Scheduled Jobs information can be obtained with: `$ cv api4 Job.get`

The following is the status of the Scheduled Jobs after crm.cmrailtrail.org.au went online. The Jobs that are scheduled are based primarily on the Jobs that Spark Essentials had scheduled. The exception is that "
*Fetch Bounces* was not done by Spark Essentials and has been added to the active Jobs for crm.cmrailtrail.org.au 
```
$ cv api4 Job.get +w "is_active = 1" +s id,name,run_frequency,is_active -T 
+----+-----------------------------------+---------------+-----------+
| id | name                              | run_frequency | is_active |
+----+-----------------------------------+---------------+-----------+
| 1  | CiviCRM Update Check              | Daily         | 1         |
| 2  | Send Scheduled Mailings           | Always        | 1         |
| 3  | Fetch Bounces                     | Hourly        | 1         |
| 9  | Send Scheduled Reminders          | Daily         | 1         |
| 10 | Update Participant Statuses       | Daily         | 1         |
| 11 | Update Membership Statuses        | Daily         | 1         |
| 13 | Clean-up Temporary Data and Files | Hourly        | 1         |
| 15 | Rebuild Smart Group Cache         | Daily         | 1         |
| 16 | Disable expired relationships     | Daily         | 1         |
| 41 | Process CiviMail Queue items      | Always        | 1         |
| 46 | Process PaymentProcessor Webhooks | Always        | 1         |
| 48 | Firewall: Cleanup                 | Daily         | 1         |
| 50 | Stripe: Cleanup                   | Hourly        | 1         |
+----+-----------------------------------+---------------+-----------+
```
Jobs that are not active are:
```
[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.get +w "is_active = 0" +s id,name,run_frequency,is_active -T 
+----+----------------------------------------------+---------------+-----------+
| id | name                                         | run_frequency | is_active |
+----+----------------------------------------------+---------------+-----------+
| 4  | Process Inbound Emails                       | Hourly        |           |
| 5  | Process Pledges                              | Daily         |           |
| 6  | Geocode and Parse Addresses                  | Daily         |           |
| 7  | Update Greetings and Addressees              | Daily         |           |
| 8  | Mail Reports                                 | Daily         |           |
| 12 | Process Survey Respondents                   | Always        |           |
| 14 | Send Scheduled SMS                           | Always        |           |
| 17 | Validate Email Address from Mailings.        | Daily         |           |
| 42 | iATS Payments 1stPay Query Transactions      | Hourly        |           |
| 43 | iATS Payments Recurring Contributions        | Daily         |           |
| 44 | iATS Payments Get Legacy Transaction Journal | Hourly        |           |
| 45 | iATS Payments Verification                   | Hourly        |           |
+----+----------------------------------------------+---------------+-----------+

```
All Jobs available are shown below. This command was run a2026-10-13 at 19:30: 

```
$ cv api4 Job.get --in=json --out=table <<EOF
{
  "select": ["id", "name", "title", "run_frequency", "is_active", "last_run"],
  "orderBy": {"is_active": "DESC"}
}
EOF

+----+----------------------------------------------+---------------+-----------+---------------------+
| id | name                                         | run_frequency | is_active | last_run            |
+----+----------------------------------------------+---------------+-----------+---------------------+
| 1  | CiviCRM Update Check                         | Daily         | 1         | 2026-10-12 21:50:04 |
| 2  | Send Scheduled Mailings                      | Always        | 1         | 2026-10-13 19:25:07 |
| 3  | Fetch Bounces                                | Hourly        | 1         | 2026-10-13 18:55:04 |
| 9  | Send Scheduled Reminders                     | Daily         | 1         | 2026-10-12 22:30:06 |
| 10 | Update Participant Statuses                  | Daily         | 1         | 2026-10-12 22:30:07 |
| 11 | Update Membership Statuses                   | Daily         | 1         | 2026-10-12 22:30:06 |
| 13 | Clean-up Temporary Data and Files            | Hourly        | 1         | 2026-10-13 18:50:04 |
| 15 | Rebuild Smart Group Cache                    | Daily         | 1         | 2026-10-12 22:10:05 |
| 16 | Disable expired relationships                | Daily         | 1         | 2026-10-12 22:10:04 |
| 41 | Process CiviMail Queue items                 | Always        | 1         | 2026-10-13 19:25:05 |
| 46 | Process PaymentProcessor Webhooks            | Always        | 1         | 2026-10-13 19:25:06 |
| 48 | Firewall: Cleanup                            | Daily         | 1         | 2026-10-13 19:05:03 |
| 50 | Stripe: Cleanup                              | Hourly        | 1         | 2026-10-13 18:55:05 |
| 4  | Process Inbound Emails                       | Hourly        |           |                     |
| 5  | Process Pledges                              | Daily         |           |                     |
| 6  | Geocode and Parse Addresses                  | Daily         |           |                     |
| 7  | Update Greetings and Addressees              | Daily         |           |                     |
| 8  | Mail Reports                                 | Daily         |           |                     |
| 12 | Process Survey Respondents                   | Always        |           |                     |
| 14 | Send Scheduled SMS                           | Always        |           |                     |
| 17 | Validate Email Address from Mailings.        | Daily         |           |                     |
| 42 | iATS Payments 1stPay Query Transactions      | Hourly        |           | 2026-10-08 20:20:05 |
| 43 | iATS Payments Recurring Contributions        | Daily         |           | 2026-10-07 21:55:03 |
| 44 | iATS Payments Get Legacy Transaction Journal | Hourly        |           | 2026-10-08 20:20:05 |
| 45 | iATS Payments Verification                   | Hourly        |           | 2026-10-08 20:20:05 |
+----+----------------------------------------------+---------------+-----------+---------------------+
```

## Feedback from Gemini on Scheduled Jobs

CiviCRM Update Check, Send Scheduled Mailings, Fetch Bounces, Send Scheduled Reminders, Update Participant Statuses, Update Membership Statuses, Clean-up Temporary Data and Files, Rebuild Smart Group Cache, Disable expired relationships, Process CiviMail Queue items, Process PaymentProcessor Webhooks, Firewall: Cleanup, Stripe: Cleanup
         
         
         
Standard Recommended Scheduled Jobs

Once you share your current list, we can compare it against the standard core jobs essential for production sites:

Send Scheduled Reminders (Job.send_reminder):

    Frequency: Daily

    Purpose: Sends automated membership renewal reminders, event reminders, and scheduled notices.

Clean-up Temporary Data and Files (Job.cleanup):

    Frequency: Hourly

    Purpose: Clears session caches, temporary tables, and old logs to prevent database bloat.

Send Scheduled Mailings (Job.process_mailing):

    Frequency: Every time cron is run

    Purpose: Queues and delivers CiviMail newsletters and bulk email campaigns.

Fetch Bounces (Job.fetch_bounces) & Process Inbound Emails (Job.fetch_activities):

    Frequency: Hourly

    Purpose: Tracks bounced emails and handles incoming reply processing.

Update Participant Statuses (Job.update_participant_status):

    Frequency: Hourly / Every time cron is run

    Purpose: Moves pending event registrations to "Expired" based on timeout settings.

Rebuild Smart Group Cache (Job.group_rebuild):

    Frequency: Daily or Hourly (depending on database size)

    Purpose: Keeps Smart Group contact counts and lists up to date without slowing down user searches.
    
        
======================


Based on your job list, you already have the most vital core jobs active—including Send Scheduled Reminders, Update Membership Statuses, Send Scheduled Mailings, and maintenance tasks like Clean-up Temporary Data and Files and Rebuild Smart Group Cache.
Here are a few specific recommendations and adjustments depending on how your organization operates:
1. Key Jobs to Consider Enabling (If Applicable)
    • Process Inbound Emails (Job.fetch_activities):
        ◦ Frequency: Hourly or Daily
        ◦ Why: If you use CiviCRM to process incoming reply emails or log activities directly from incoming mailboxes, enable this. (If you only send outbound emails and track bounces, your current setup is fine).
    • Geocode and Parse Addresses (Job.geocode):
        ◦ Frequency: Daily
        ◦ Why: Necessary if you map contact addresses or rely on spatial/distance searches in CiviCRM.
2. Frequency Tuning Adjustments
    • Clean-up Temporary Data and Files (Job ID 13):
        ◦ Current: Daily
        ◦ Recommendation: Change frequency to Hourly. Standard core installations run this hourly to clear out session data, temporary tables, and old logs quickly before they accumulate.
    • Process CiviMail Queue items (Job ID 41):
        ◦ Current: Hourly
        ◦ Recommendation: Consider running this Every time cron is run (Always) if you send bulk newsletters or mailings regularly. An hourly interval means bulk emails or automated queued items may wait up to 60 minutes before delivery starts.

Summary Checklist for cmrailtrail.org.au
Job Name	Current	Recommended Status
Send Scheduled Reminders	Daily (Active)	Keep Active (Handles membership renewal notices)
Update Membership Statuses	Daily (Active)	Keep Active (Rolls over active/grace/expired memberships)
Send Scheduled Mailings	Always (Active)	Keep Active
Clean-up Temporary Data	Daily (Active)	Adjust to Hourly
Process CiviMail Queue	Hourly (Active)	Adjust to Always (if using bulk email heavily)
Geocode and Parse Addresses	Disabled	Enable (only if mapping contacts/addresses)

Would you like the cv api4 CLI commands to adjust the frequencies for the Clean-up or CiviMail Queue jobs?

 Would you like the cv api4 CLI commands to adjust the frequencies for the Clean-up or CiviMail Queue jobs? Yes please.

Here are the cv api4 commands to update those job frequencies:
1. Change "Clean-up Temporary Data and Files" (ID 13) to Hourly
Bash

cv api4 Job.update +v '{"run_frequency":"Hourly"}' +w '[["id","=",13]]'

2. Change "Process CiviMail Queue items" (ID 41) to Always
Bash

cv api4 Job.update +v '{"run_frequency":"Always"}' +w '[["id","=",41]]'

Batch Command (Run Both Together)

If you prefer to execute both updates in a single command using id IN (13, 41):
Bash

cv api4 Job.update +w '[["id","=","13"]]' +v '{"run_frequency":"Hourly"}'
cv api4 Job.update +w '[["id","=","41"]]' +v '{"run_frequency":"Always"}'

Verification

After running the updates, verify that the frequencies changed as intended:
Bash

cv api4 Job.get +w '[["id","IN",[13,41]]]' +s id,name,run_frequency -T


Currently scheduled...

[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.get +w 'id=13' +s id,name,run_frequency -T
+----+-----------------------------------+---------------+
| id | name                              | run_frequency |
+----+-----------------------------------+---------------+
| 13 | Clean-up Temporary Data and Files | Daily         | < change to Hourly
+----+-----------------------------------+---------------+
[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.get +w 'id=41' +s id,name,run_frequency -T
+----+------------------------------+---------------+
| id | name                         | run_frequency |
+----+------------------------------+---------------+
| 41 | Process CiviMail Queue items | Hourly        |<- Change to always
+----+------------------------------+---------------+


CHANGING THE FREQUENCIES...

=====

I modified the commands and these worked...

[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.get +w 'id=13' +s id,name,run_frequency -T
+----+-----------------------------------+---------------+
| id | name                              | run_frequency |
+----+-----------------------------------+---------------+
| 13 | Clean-up Temporary Data and Files | Daily         |
+----+-----------------------------------+---------------+
[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.update +v 'run_frequency=Hourly' +w 'id=13'
[
    {
        "id": 13,
        "run_frequency": "Hourly",
        "custom": null,
        "check_permissions": null
    }
]
[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.get +w 'id=13' +s id,name,run_frequency -T
+----+-----------------------------------+---------------+
| id | name                              | run_frequency |
+----+-----------------------------------+---------------+
| 13 | Clean-up Temporary Data and Files | Hourly        |
+----+-----------------------------------+---------------+
[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.get +w 'id=41' +s id,name,run_frequency -T
+----+------------------------------+---------------+
| id | name                         | run_frequency |
+----+------------------------------+---------------+
| 41 | Process CiviMail Queue items | Hourly        |
+----+------------------------------+---------------+
[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.update +v 'run_frequency=Always' +w 'id=41'
[
    {
        "id": 41,
        "run_frequency": "Always",
        "custom": null,
        "check_permissions": null
    }
]
[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.get +w 'id=41' +s id,name,run_frequency -T
+----+------------------------------+---------------+
| id | name                         | run_frequency |
+----+------------------------------+---------------+
| 41 | Process CiviMail Queue items | Always        |
+----+------------------------------+---------------+

    
