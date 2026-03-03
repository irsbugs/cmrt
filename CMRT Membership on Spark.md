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
* As part of the uploading process CiviCRM calculates the Membership *Status* for each Individual. This is the current the status:
  * 5 New
  * 70 Current
  * 19 Grace
  * 56 Expired
  * 150 Total members since 2021.
 
