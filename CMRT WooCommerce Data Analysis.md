# Analysis of WooCommerce Data.

On 2025-01-25 the WooCommerce Membership data was exported by Ken as a csv file.

The file comprised:

* Column headers = 41
* Rows of data = 290

The Order Numbers for the rows are from 

* 302	2026-01-19 20:28 - latest
* 1 2021-08-20 16:24 - oldest
  
There are a total of 290 actual orders of the 302 possible order numbers.
A total of 12 order numbers are missing. Maybe these orders got cancelled if the payment never came through?

The total number of new individual memberships is 151, and an additional 139 are the annual re-newal of memberships. The rows of data were sorted by the person with the oldest membership start date to the most recent membership start date. For each member with membershp renewals, these were added after the new membership. 

The records go back to 20 Aug 2021, when the WooCommerce membership database was created. The first record is for Janice Simpson. The CMRT organisation commenced memberships before 20 Aug 2021, but the data of these earlier membership dates is no longer available.   

As an example, below are some of the fields of data in the rows for Ian Stewart:

Ian Stewart was the 90th member to join CMRT, and has renewed his membership twice:
```
Row Name        No. Member since        Start Date          End Date              CiviCRM Calculated Status if date is 1 Feb 2026
127 Ian	Stewart	90	2023-06-06 15:16	2023-06-06 15:16	2024-06-05 15:16:00   <- Expired
180 Ian	Stewart	90	2023-06-06 15:16	2024-08-26 16:24	2025-08-25 16:24:00   <- Grace
247 Ian	Stewart	90	2023-06-06 15:16	2025-08-17 18:57	2026-08-16 18:57:00   <- Active
```

CiviCRM calculates the Membership Status each day. As of 1 Feb 2026, in the above example, Ian's first entry is *Expired*, the second entry is in the *Grace* period and the third entry is *Active*.

### Membership Status Rules.

The CiviCRM Membership Status Rules are accessed via *Administer -> CiviMember -> Membership Status Rules*.

CiviCRM has had its Membership Status Rules set to comply with the CMRT Charter. In summary:

* *New* - A new membership that is less than 3 months. A new member is unable to vote at the AGM.
* *Active* - A new membership for 4th to 12th months, or a renewing member for the full 12 months.
* *Grace* - A membership for the next 13 to 24th months after becoming a new or renewed member.
* *Expired* - A membershhip from 25 months onward.

The one year membership will end a year later on the day before the start date anniversary. E.g. If start date is on 1 Jan 2026 then the end date is 31 Dec 2026.

Importing membership data via a csv file does not need the *Status* field. Thiss is calculated by CiviCRM as the data is loaded.


### Modification of Data

The fields of many records were modified in order to standardise the data. E.g. All phone numbers commence with the country code. Abbreviations were expanded. E.g. St. and Rd. expanded to Street and Road. Email addresses all lower-case, etc.


#### Corrections to First Name and Last Name.

Where necessary, *First Name* and *Last Name* were modified to match the naming convention being implemented. The first letter of a name is a Capital and the rest of the name is lower case. Exceptions apply. For example, a person with a *Last Name* of *Van der Wal*.

#### Uniqueness of Email Address

The *Email Address* for each contact/member must be unique. The *Email Address* is used as the primary key when mapping data, etc. For example, if a couple both register as members, then they can not share an email address. Also implement Email addresses to be written in all lower case letters. 

## Issues with Uniqueness of Email Addresses

### Issue #1:

The person that uses the email address: kate.couttie@gmail.com has normally been going by the name Kate and last renewed her membership in Sep 2025. However 2 months after Kate Couttie renewed her membership then a Kathleen Couttie "renewed" her membership.

```
Renewing Member	288	Completed	2025-11-09 13:53		Kathleen Couttie	kate.couttie@gmail.com
Renewing Member	252	Completed	2025-09-08 15:45		Kate Couttie		kate.couttie@gmail.com
```

I assume that Kate is the nickname for Kathleen and the nickname is more commonly used.

## Resolved #1:
Changed Kathleen to Kate. Kate need to contact CMRT for refund or credit for next year as she paid twice for the year 2025 membership.

### Issue #2: 

I'm not sure about this data. Might pay to ring them up and have a chat. Phone 400029068 or 438309772

```
	          	271	Completed	2025-10-07 21:37		Deborah Macer	macerfam@yahoo.com.au <-- Name probably meant to by Tony Macer
	          	266	Completed	2025-10-06 22:26		Deborah Macer	macerfam@yahoo.com.au <-- Email probably meant to be debmacer1957@gmail.com
New Member		204	Completed	2024-10-23 17:31		Tony Macer		macerfam@yahoo.com.au
Renewing Member	176	Completed	2024-08-12 13:14		Owen Macer	    owen.macer@gmail.com
```

Resolution: 

It looks to me like it should be the following:
Deborah Macer normally uses the email debmacer1957@gmail.com and accidently used Tony's macerfam@yahoo.com.au for herself.
Tony Macer normally uses the email macerfam@yahoo.com.au
Owen Macer always uses owen.macer@gmail.com

Action: Sent an e-mail to Deborah and Tony requesting information

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
Action: None

## Issue #4
Is it tim.laugher or timelaugher?

170	tim.laugher@gmail.com	tim.laugher@gmail.com	78	Tim	Laugher
223	timlaugher@gmail.com	timlaugher@gmail.com	78	Tim	Laugher

Action:
Opted for tim.laugher in the meantime. Need to check.

## Issue #5

About 20 members had a descrepency between their new membership email address and / or their renewal membership email addresses.

Action:

Pick the email address which they currently appear to use, and make this the email for all memberships.


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


## After Importing the massaged WooCommerce membership data

The following is a screenshot of how the memberships for Ken Stewart are displayed as of 3 Feb 2026.

* *Member Since* remains the date of the initial new membership.
* The 4 x *Membership Start Date* are the dates the annual membership dues were paid.
* The 4 x *Membership Expiry Date* were uploaded from the csv file, to help CiviCRM get the *Status* calculation correct.
* The 4 x *Membership Expiry Date* are the 365th day, or 366th day on leap years, since the *Membership Start Date*.
* CiviCRM calculates the *Status*. This field is not uploaded from the CSV file.
* Two membership are **Active** as one is *Current*, within the last year, and one is "Grace" within 13 to 24 months.
  
 
![ken_memberships](/images/ken_membership_screenshot.png)

