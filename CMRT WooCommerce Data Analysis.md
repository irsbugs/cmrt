# Analysis of WooCommerce Data.

On 2025-01-25 the WooCommerce data was exported by Ken as a csv file.

The file comprised:

* Column headers = 41
* Rows of data = 290

The Order Numbers for the rows are from 

* 302	2026-01-19 20:28 - latest
* 1 2021-08-20 16:24 - oldest

There are a total of 290 actual orders of the 302 possible order numbers.
A total of 12 order numbers are missing. Maybe these orders got cancelled if the payment never came through?

The interest is in those who have become new or renewed members in the last 12 months, and also include those in a grace payment period of an additional 4 months. This is effectively from 31 Jan 2026 and going back to 1 October 2024. These members will have their Contact and Membership data uploaded to Spark CiviCRM. Details are:

* 78 paid-up members over the last 12 month period. Two of these are in *Processing* and one is *On Hold* all others are *Completed*. 
* 9 members are in the 13 to 16 months grace period and are behind with paying their membership or have decided not to renew their membership.

This total of 87 members will have their *contact* and *membership* data uploaded to Spark CiviCRM. Data of former members, who have expired membership, will not be uploaded. If a former member applies for membership again, then they will be treated as a *new* member, and not as a *renew*ing member. 

## Corrections to First Name and Last Name.

Where necessary, *First Name* and *Last Name* were modified to match the naming convention being implemented. The first letter of a name is a Capital and the rest of the name is lower case. Exceptions apply. For example, someone with a *Last Name* of *Van der Wal*.

## Uniqueness of Email Address

The *Email Address* for each contact/member must be unique. The *Email Address* is used as the primary key when mapping data, etc. For example, if a couple both register as members, then they can not share an email address. Also implement Email addresses to be written in all lower case letters. 

## Issues with Uniqueness of Email Addresses

### Issue #1:

The person or persons that use the email address: kate.couttie@gmail.com has normally been going by the name Kate and last renewed her membership in Sep 2025. However 2 months after Kate Couttie renewed her membership then a Kathleen Couttie "renewed" her membership.

```
Renewing Member	288	Completed	2025-11-09 13:53		Kathleen Couttie	kate.couttie@gmail.com
Renewing Member	252	Completed	2025-09-08 15:45		Kate Couttie		kate.couttie@gmail.com
```

I assume they are two people, Kate and Kathleen. E.g. Sisters or Mother and daughter. If so then we need different 2 x different email addresses. E.g. kate.couttie@gmail.com and, say, kathleen.couttie@gmail.com

Might be best to give them a call: 419010609 <-- This is the same number for both Kate and Kathleen

## Resolved #1:
Kathleen should have been Kate. Corrected.  Accidently paid 10 months in advance for 2026 membership. Test CiviCRM to see if it works this out.


### Issue #2: 

I'm not sure about this data. Might pay to ring them up and have a chat. Phone 400029068 or 438309772

```
	          	271	Completed	2025-10-07 21:37		Deborah Macer	macerfam@yahoo.com.au
	          	266	Completed	2025-10-06 22:26		Deborah Macer	macerfam@yahoo.com.au
New Member		204	Completed	2024-10-23 17:31		Tony Macer		macerfam@yahoo.com.au
Renewing Member	176	Completed	2024-08-12 13:14		Owen Macer	    owen.macer@gmail.com
```
It looks to me like: 

* Tony Macer registered as a new member in 2024-10-06 and used the email address: macerfam@yahoo.com.au

* After a year his partner decided to renew Tony's membership, but she put her own name, Deborah Macer, instead of Tony's, however she used the same email address: macerfam@yahoo.com.au

* The next day Deborah decided to register herself for membership and used her own name Deborah and the same email address: macerfam@yahoo.com.au

If there are two members of the Macer family that are members, E.g. Tony and Deborah, then we need two email address. E.g. macerfam@yahoo.com.au and something else.

## Issue #3:

Why did John Cook pay membership and donate 3 times last year?

John Cook phone 438049683
```
For 2025...
Renewing Member	297	Completed	2025-12-25 09:28		John	Cook	wcookjohn@yahoo.com.au
Renewing Member	262	Completed	2025-09-28 16:23		John	Cook	wcookjohn@yahoo.com.au
Renewing Member	233	Completed	2025-05-29 11:22		John	Cook	wcookjohn@yahoo.com.au
For 2024...
Renewing Member	197	Completed	2024-09-13 16:39		John	Cook	wcookjohn@yahoo.com.au
```

## Import Mapping

When transfering WooCommerce csv data to Spark CiviCRM, then three Imports need to be performed:

* **Contacts --> Import Contacts**
* **Contributions --> Import Contributions**
* **Memberships --> Import Memberships**

To simplify the mapping of data, it is easier to rename WooCommmerce column headers so they become the available Spark CiviCRM import fields. Below are the lists of available Spark CiviCRM fields for importing Contacts, Contributions and Memberships.
From Spark CiviCRM V6.9.1 on 2026-01-26

### Contact Fields: 
Some fields have sub-categories. E.g. Main, Billing Primary

```
-do not import-
Addressee
Addressee Custom
Birth Date
City (Main, Billing Primary)
Communication Style
Contact ID *
Contact Source
Contact Subtype
Country (Main, Billing Primary)
Country ID (Main, Billing Primary)
County ID (Main, Billing Primary)
Deceased / Closed
Deceased / Closed Date
Do Not Email
Do Not Mail
Do Not Phone
Do Not Sms
Do Not Trade
Email * (Main, Billing Primary)
Email Greeting
Email Greeting Custom
External Identifier *
First Name *
Formal Title
Gender ID
IM Screen Name (Main, Billing Primary) (Yahoo, MSN, AIM, Gtalk, Jabber, Skype)
Image URL
Individual Prefix
Individual Suffix
Job Title
Last Name *
Legal Identifier
Master Address ID (Main, Billing Primary)
Middle Name
Nickname
No Bulk Emails (User Opt Out)
Note
OpenID (Main, Billing Primary)
Phone (Main, Billing Primary) (Phone, Mobile)
Phone Extension (Main, Billing Primary) (Phone, Mobile)
Postal Code (Main, Billing Primary)
Postal Greeting
Postal Greeting Custom
Preferred Communication Method
Preferred Language
Signature Html (Main, Billing Primary)
Signature Text (Main, Billing Primary)
State (Main, Billing Primary)
State/Province ID (Main, Billing Primary)
Street Address (Main, Billing Primary)
Uniqie ID (OpenID)
Website (Work, Main, Social)

-related contact info- 
Benefits Specialist 
Benefits Specialist is
Case Coordinator
Case Coordinator is
Child of
Employee of
Head of Household for
Health Services Coordinator 
Health Services Coordinator is
Homeless Services Cooordinator 
Homeless Services Cooordinator is
Household Member of
Parent of
Partner of
Senior Service Coordinator
Senior Service Coordinator is
Sibling of
Spouse of
Supervised by
Supervisor
Volunteer for

For the above *related contact info*, these can be expanded. Presumably *Employee of* could select an Organisation.
```

### Contribution Fields: 
Have no sub-categories

```
Contribution ID
Financial Type *
Contribution Page
Payment Method
Contribution Date
Non-deductible Amount
Total Amount *
Fee Amount
Net Amount
Transaction ID
Invoice Reference
Invoice Number
Currency
Cancelled / Refunded Date
Cancellation Refund Reason
Receipt Date
Thank-you Date
Contribution Source
Amount Label
Test Mode
Is Pay Later
Contribution Status
Check Number
Credit Note ID
Tax Amount
Revenue Recognition Date
Note
PAN Truncation

Contact Fields:
Contact ID
External Identifier
Email
```

### Membership Fields:
Have no sub-categories

```
Is Pay Later
Membership Expiration Date
Membership ID
Membership Source
Membership Start Date
Membership Type
Member Since
Status
Status Override
Status Override End date
Test

Contact Fields:
Contact ID
External Identifier
Email
```




