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

The interest is in those who have become new or renewed members in the last 12 months, and also include those in a grace payment period of an additional 12 months. This is effectively from 31 Jan 2026 and going back to 1 February 2024. These members will have their Contact and Membership data uploaded to Spark CiviCRM. Details are:

* 77 paid-up members over the last 12 month period. Two of these are in *Processing* and one is *On Hold* all others are *Completed*. 
* 14 members are in the 13 to 24 months grace period and are behind with paying their membership or have decided not to renew their membership.

This total of 91 members will have their *contact* and *membership* data uploaded to Spark CiviCRM. Data of former members, who have expired membership, will not be uploaded. If a former member applies for membership again, then they will be treated as a *new* member, and not as a *renew*ing member. 

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
Kathleen should have been Kate. Changed.  Kate effectively paid 10 months in advance for her 2026 membership.

Action: Removed the data to avoid duplication when uploading to Spark
Renewing Member	252	Completed	2025-09-08 15:45		Kate Couttie		kate.couttie@gmail.com


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

Action: Removed 176, 204,and 266 until get response from Macer family.


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
Action: Remove 197, 233, 262. Uploaded 297

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

## Updating Contact and Membership from Massaged WooCommerce CSV file

The csv file to update Spark Essentials will contain the following fields:

### Contact Imported Fields

* **External Identifier**
* **Email**
* First Name
* Last Name
* Street Address
* City
* State
* Postal Code
* Country
* Phone

For fields that have the sub-categories: *Main*, *Billing* and *Primary*, then *Main* will be used.

### Membership Imported Fields

* **External Identifier**
* **Email**
* Member Since
* Membership Start Date
* Membership Expiration Date
* Membership Type
* Status

The External Identifier and the Email are the unique identifiers when importing the Contact and the Membership data. The External Identifier is the *Order Number* that WooCommerce provided.

The import mapping will make use of -do not import- so the one csv file can be used for both Contact and Membership importing.

## Newsletter Subscribers

The Spark CiviCRM database has already been loaded with data for the 400+ subscribers to the Newsletter. The following data was provided for each subscriber:

* Email Address
* First Name
* Last Name

In many cases, when loading the Contact information for members, they will already be in the database as they subscribe to the Newsletter.

 
### Importing error

Invalid value for field(s) : Status,Membership Type

Membership Type of *Individual* needed to be defined

## Modifying Membership Status Rules

Administer --> CiviMember --> Membership Status Rules

## Importing Memberships

Membership status:
* New - Enabled - Set to 3 months. Need to check CiviCRM Charter for how long to be a member before able to vote at the AGM.
* Current - Enabled - Uses Start and Expiry dates. i.e. 1 year
* Grace - Enabled - Edit: Change from 1 month to 1 year. Compliance with CMRT Charter
* Expired - Enabled - Edit: Change to start after end date plus 1 year. Compliance with CMRT Charter
* Pending <-- Uses *Member Since* (which is *Member Start Date*)
* Cancelled <-- Uses *Member Since* (which is *Member Start Date*)
* Deceased

The data being imported will be changed to have 12 months of Current followed by 12 months of Grace

# Errors - Notes:

* Importing does not need *Membership Expiration Date*. This will be calculate based on the Administer -> CiviMember -> Membership Status Rules.

* The one year membership will end one year from Membership Start date, minus one day. For example:
	* Membership Since: January 28th, 2026
 	* Membership Start Date:  January 28th, 2026	
 	* Membership Expiry Date: January 27th, 2027 <-- plus 1 year and minus one day.

* Without the *Membership Expiry Date* the Grace and Expired Status is not calculated and displayed. Status is left as Current.
* Can force the Status fields and not use the Membership Expiry Date, but error:
```
``Status in import row (2) does not match calculated status based on your configured Membership Status Rules (New).
  Record was not imported.
```
* Subtract one day from expiry date in spreadsheet to match calculation done by CiviCRM 

## Spark Membership Status Rules Changes

Accessed via: Administer --> CiviMember --> Membership Status Rules

The default Membership Status Rules before making changes:

![spark1](/images/membership_status_rules/spark_membership_status_rules_1.png)

The Membership Status Rules changed to fit the CMRT Charter:

![spark2](/images/membership_status_rules/spark_membership_status_rules_2.png)


Below are examples of modifying Spark Member Since, Member Start and Member Expiry date to observe when transitioning occurs between *New, Current, Grace, Expiry*:

```
These status results were captured on Spark CiviCRM on 31 Jan 2026

Type               Member Since        Membership Start    Membership Expir     Status
Individual Member  January 31st, 2026  January 31st, 2026  January 30th, 2027	New

Transitioning from New to Current. (3 months after 30 Oct 2025 status becomes Current on 31 Jan 2026)
Type               Member Since        Membership Start    Membership Expir     Status
Individual Member  October 31st, 2025  October 31st, 2025  October 30th, 2026	New
Individual Member  October 30th, 2025  October 30th, 2025  October 29th, 2026	Current

Transitioning from Current to Grace (1 year after 31 Jan  2025 status becomes Grace on 31 Jan 2026)
Type               Member Since        Membership Start    Membership Expir     Status
Individual Member  February 1st, 2025  February 1st, 2025  January 31st, 2026   Current	
Individual Member  January 31st, 2025  January 31st, 2025  January 30th, 2026   Grace

Transitioning from Grace to Expired (2 years after 31 Jan 2024 status becomes Expired on 31 Jan 2026)
Type               Member Since        Membership Start    Membership Expir     Status
Individual Member  February 1st, 2024  February 1st, 2024  January 31st, 2025   Grace
Individual Member  January 31st, 2024  January 31st, 2024  January 30th, 2025   Expired
```

## Importing Membership data with history

Using a csv file to import 3 x memberships for Ian Stewart.

The csv import file is as follows:
```
External Identifier	First Name	Last Name	Email	Member Since	Membership Start Date	Membership Expiration Date	Membership Type
127	Ian	Stewart	ianstewart56@hotmail.com	2023-06-06 15:16	2023-06-06 15:16	2024-06-05 15:16	Individual
180	Ian	Stewart	ianstewart56@hotmail.com	2023-06-06 15:16	2024-08-26 16:24	2025-08-25 16:24	Individual
247	Ian	Stewart	ianstewart56@hotmail.com	2023-06-06 15:16	2025-08-17 18:57	2026-08-16 18:57	Individual
```
After Importing then looking at the Memberships of Ian

![ian](/images/ian_memberships.png)

Having 2 x Active Memberships will be quite common with a long (one year) Grace period.


## Logging in to renew???

Online renewals¶

CiviCRM uses the same page for new memberships as it does for renewals. The only difference is that the page title and introductory message with the text you entered into the renewal fields on the memberships tab when you were configuring your online membership page. The renewal page is automatically displayed at the same URL as the membership join page when viewed by a logged in website visitor that has a valid current or expired membership.

When you are setting up membership sign up pages, it is worth remembering that current members will only see the renewal page if they are logged in. If they are not logged in, they will see the sign up page. If they fill that page in and, based on their contact information, CiviCRM can find their existing contact record then their membership will be renewed. If CiviCRM can't find their existing contact record (perhaps they have changed their email address) then a new contact record and membership will be created. This is one source of duplicates in your database and you need to minimise the chances that this will happen. Two ways to do this are to always include a checksum token in renewal reminder emails and add text to the new member introductory message to remind people that they should log in before they renew


### Modify Macer family
Changes:
* Tony changed to have a fake email address.
* Entry 271 was Deborah. Changed it to Tony.

  Entries now look like this in WooCommerce spreadsheet.
```
266	Completed	2025-10-06 22:26	macerfam@yahoo.com.au	84	Deborah	Macer	1 Newton Street
159	Completed	2024-01-14 18:29	debmacer1957@gmail.com	84	Deborah	Macer	1 Newton Street
150	Completed	2023-11-08 07:12	debmacer1957@gmail.com	84	Deborah	Macer	1 Newton Street
95	Completed	2022-11-20 08:09	debmacer1957@gmail.com	84	Deborah	Macer	1 Newton Street

176	Completed	2024-08-12 13:14	owen.macer@gmail.com	85	Owen	Macer	12 Penhallurick Street
131	Completed	2023-08-07 18:57	owen.macer@gmail.com	85	Owen	Macer	12 Penhallurick Street
71	Completed	2022-07-16 12:18	owen.macer@gmail.com	85	Owen	Macer	12 Penhallurick Street

271	Completed	2025-10-07 21:37	tonymacer@example.com	86	Tony	Macer	1 Newton Street
204	Completed	2024-10-23 17:31	tonymacer@example.com	86	Tony	Macer	1 Newton Street
96	Completed	2022-11-20 08:20	tonymacer@example.com	86	Tony	Macer	1 Newton Street
```
