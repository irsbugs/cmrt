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








