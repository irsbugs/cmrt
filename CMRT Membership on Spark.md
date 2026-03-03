# Implementation of Membership on Spark Essentails

## Introduction

On 25 January 2026, the WooCommerce data from the CMRT website was exported to CSV file. In theory this data is for all membership transactions since the WooCommerce database was first implemented on 20 August 2021. However, from the sequencial WooCommerce *Order Number*, from the 302 transactions, 12 are missing.

The WooCommerce csv file was massaged to correct typos, etc. Also, where necessary, Field Headers were renamed to match the defaults used by CiuviCRM. E.g. *Surname* changed to *Last Name*. 

The Contact and Membership csv data was uploaded to Spark Essentials CiviCRM database on 14 Feb 2026. The CiviCRM fields uploaded to Spark essentails database for each member are:

The Individuals Contact Details Fields:

* First Name
* Last Name
* Street Address
* City
* State
* Postal Code
* Country
* Phone
* Email

The Individuals Membership Information Fields

* Member Since
* Membership Start Date
* Membership Expiration Date
* Membership Type

Notes: 
* An *External Identifier* number was made to match the *Contact ID* of the Individual. This could be handy in future.
* For fields that have the sub-categories: Main, Billing and Primary, then Main was used.
* As part of the Membership uploading process CiviCRM calculates the Membership *Status* for each Individual. There have been a total of 150 since 2021. This is the status as of 14 February 2026:
  * 5 New
  * 70 Current
  * 19 Grace
  * 56 Expired
 
Chatgpt was used to generate the following Audit and  Implementation Plan
 
## PART 1  - Audit

### 1 Membership Types

Go to: Administer → CiviMember → Membership Types

Confirmed the following - 2026-03-03:
* Individual Membership. - Minimum fee $15.
* Grace Period set correctly. - Duration 1 year.
* Auto-renew Option. - No. Nothing checked. Choices: No auto-renew option, Give option, but not required and Auto-renew required.
* Renewal reminders not yet activated. - Note: Configure membership renewal reminders using [Schedule Reminders](https://cmrailtrail.civicrm.org/civicrm/admin/scheduleReminders?reset=1). If you have previously configured renewal reminder templates, you can re-use them with your new scheduled reminders. [Schedule Reminders documentation](https://docs.civicrm.org/user/en/latest/email/scheduled-reminders/)

### 2 Contribution Page (Join/Renew Form)

Go to: Administer → CiviContribute → Manage Contribution Pages

Ken created:
* CMRT Donate. - Configure 8 sections, Contributions 3 sections, Links 2 sections, more 3 options
* CMRT Membership Signup Page
  

TODO: Confirm the following - 2026-03-xx:
* One active *Join / Renew Membership* page. - CMRT Membership Signup Page
* Connected to correct Membership Type(s) - huh?
* Stripe processor selected (IPN 4 is correct for Spark — yes, keep it while WooCommerce still runs) - huh?
* Thank-you page wording correct - huh?
* Test payment works (you already confirmed 200 success) - huh?

### 3 Profiles (Public Form Fields)

Go to: Administer → Customize Data and Screens → Profiles

TODO Confirmed the following on - 2026-03-xx:
* Membership signup profile exists. - 
* First Name / Last Name added (thanks to Ian)
* Email required
* Volunteer interest question present (if desired)
* No unnecessary legal checkbox (you wisely removed electronic signature)

### 4 Groups

Go to: Contacts → MAnage Groups

TODO: Confirmed on 2026-03-xx:
* *Current Members* - huh ? No
* *Expired Members* - huh ? No
* *Newsletter* <-- CMRT Newsletter Subscriber - created by Admin CMRT
* *Committee group* <-- CMRT Committee - created by Admin CMRT

Other groups - created by Admin CMRT:
* CMRT Test Newsletter
* CMRT Letter of Support
* Donors
* Membership Intake
* Paid Members
* Volunteers
 
Make sure membership type is set to automatically add/remove from “Current Members”. - huh?

### 5 Email & Receipts

Checked on 2026-03-xx:

* Receipt sender name/email updated (remove John’s details). huh?
* Organisation name = Castlemaine Maryborough Rail Trail. - Legal Name: Castlemaine Maryborough Rail Trail Inc
* CMRT used only in informal contexts. huh?
* Test receipt looks correct. huh?

## PART 2 — Implementation Plan (Practical Roll-Out)

You are currently in a parallel system phase:
• WooCommerce = still live
• Spark = configured but not yet primary

So we implement in stages.

## STAGE 1 

### 1. Finalise Membership Structure

* Confirm Grace Period (recommend 12 months if matching model rules — your admin-saving insight was correct).
   
The CiviCRM Membership Status Rules are accessed via Administer -> CiviMember -> Membership Status Rules.

![Membership Status Rules](/images/membership_status_rules/membership_status_rules.png)

CiviCRM has had its Membership Status Rules set to comply with the CMRT Charter. In summary:

* New - A new membership that is less than 3 months. A new member is unable to vote at the AGM.
* Active - A new membership for 4th to 12th months, or a renewing member for the full 12 months.
* Grace - A membership for the next 13 to 24th months after becoming a new or renewed member.
* Expired - A membership from 25 months onward.

* Set Renewal Reminders:
  * 30 days before expiry. - Ken - 20 days?
  * 7 days before expiry.
  * 1 month after expiry (optional). ???
 
Civi automatically stops reminders once someone renews — not a dumb question, you were right.


TO BE CONTINUED...
