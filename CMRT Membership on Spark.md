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

### Membership Types

Go to: Administer → CiviMember → Membership Types

Confirmed the following:
* Individual Membership (correct fee)
* Grace Period set correctly (you were considering 12 months — confirm)
* Auto-renew unchecked (unless intentionally enabled)
* Renewal reminders not yet activated (or note status)

## STAGE 1 

1. Finalise Membership Structure
   
The CiviCRM Membership Status Rules are accessed via Administer -> CiviMember -> Membership Status Rules.

![Membership Status Rules](/images/membership_status_rules/membership_status_rules.png)

CiviCRM has had its Membership Status Rules set to comply with the CMRT Charter. In summary:

* New - A new membership that is less than 3 months. A new member is unable to vote at the AGM.
* Active - A new membership for 4th to 12th months, or a renewing member for the full 12 months.
* Grace - A membership for the next 13 to 24th months after becoming a new or renewed member.
* Expired - A membership from 25 months onward.
