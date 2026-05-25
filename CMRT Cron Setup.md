# Cron Setup

Cron utility will be used so that Linux can trigger [*scheduled jobs*](https://docs.civicrm.org/sysadmin/en/latest/setup/jobs/) to run in CiviCRM Standalone.

There are two options for scheduling the CiviCRM jobs:
* Cron - Time-based job scheduler.
* [Systemd timers](https://docs.civicrm.org/sysadmin/en/latest/setup/jobs/#systemd-timers)  Used as a cron-like job scheduler.

Although the Systemd timers is a better solution, it would require admin staff at VentraIP to implement it for CMRT. Therefore cron will initially be used.





