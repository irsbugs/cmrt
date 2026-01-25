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

This total of 87 members will have their *contact* and *membership* data uploaded to Spark CiviCRM. Data of former members, who have expired membership, will not be uploaded. If a former member applies for membership again, then they will be treated a a *new* member, and not as a *renew*ing member. 

## Corrections to First Name and Last Name.

Where necessary, *First Name* and *Last Name* were modified to match the naming convention being implemented. The first letter of a name is a Capital and the rest of the name is lower case. Exceptions apply. For example, someone with a *Last Name* of *Van der Wal*.

## Uniqueness of Email Address

The *Email Address* for each contact/member must be unique. the *Email Address* is used as the primary key when mapping data, etc. For example, if a couple both register as members, then they can not share an emal address. Also implement all Email addresses to be all lower case. 

## Issues with Uniqueness of Email Addresses

### Issue #1:

The person or persons that use the email address: kate.couttie@gmail.com has normally been going by the name Kate and last renewed her membership in Sep 2025. However 2 months after Kate Couttie renewed her membership then a Kathleen Couttie renewed her membership.

```
Renewing Member	288	Completed	2025-11-09 13:53		Kathleen Couttie	kate.couttie@gmail.com
Renewing Member	252	Completed	2025-09-08 15:45		Kate Couttie		kate.couttie@gmail.com
```

I assume they are two people, Kate and Kathleen. E.g. Sisters or Mother and daughter. If so then we need different 2 x different email addresses. E.g. kate.couttie@gmail.com and, say, kathleen.couttie@gmail.com

Might be best to give them a call: 419010609 <-- This is the same number for both Kate and Kathleen


### Issue #2: 

I'm not sure about this data. Might pay to ring them up and have a chat. Phone 400029068 or 438309772

```
	          	271	Completed	2025-10-07 21:37		Deborah Macer	macerfam@yahoo.com.au
	          	266	Completed	2025-10-06 22:26		Deborah Macer	macerfam@yahoo.com.au
New Member		204	Completed	2024-10-23 17:31		Tony Macer		macerfam@yahoo.com.au
```

It looks to me like: 

* Tony Macer registered as a new member in 2024-10-06 and used the email address: macerfam@yahoo.com.au

* After a year his partner decided to renew Tony's membership, but she put her own name, Deborah Macer, instead of Tony's, however she used the same email address: macerfam@yahoo.com.au

* the next day Deborah decided to register herself for membership and used her own name Deborah and the same email address: macerfam@yahoo.com.au

If there are two members of the Macer family that are members, E.g. Tony and Deborah, then we need two email address. E.g. macerfam@yahoo.com.au and something else.






