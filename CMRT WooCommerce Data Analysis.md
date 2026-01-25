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

The interest is in those who have become new or renewed members in the last 12 months, and include those in a grace payment period of an additional 4 months. This is effectively from 31 Jan 2026 back to 1 October 2024. These members will have their Contact and Membership data uploaded to Spark CiviCRM. Details are:

* 77 paid-up members in the last 12 months. Two of these are in *Processing* and one is *On Hold* all others are *Completed*. 
* 9 members are in the 13 to 16 months grace period and are behind with paying their membership or have decided not to renew their membership.


## Corrections to First Name and Last Name.

Where necessary names were modified to match the naming convention being implemented, where the first letter of a name is a Capital and the rest of the name is lower case.

## Uniqueness of Email Address

The 








