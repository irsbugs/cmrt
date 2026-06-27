# Login and Naming Conventions

2026-06-27

## Introduction

For the management and operation of the CMRT IT systems a variety of login's are a requirement. This document is a guideline to the account login naming conventions. 

To provide examples in this document assume there is a *Joe Bloggs*. Joe is a member of CMRT, so he is registered in CiviCRM as an Individual Contact.  Joe is a member of the CMRT committee so he has a CMRT Webmail account and a personal account on the CiviCRM system. Joe looks after the IT systems so he also has administration accounts.

There is also a *Joe Another* on the CMRT committee. The first-name is normally only needed for account naming, etc., but for uniqueness of these two the first letter of the surname is appended and they are referred as *joea* and *joeb* 

Thus for Joe Bloggs these will be his accounts as a committee member:

* CMRT Webmail: joeb@cmrailtrail.org.au
* CiviCRM Account Username: joeb@cmrailtrail.org.au

* CiviCRM Contact Firstname: Joe
* CiviCRM Contact Lastname: Bloggs
* CiviCRM Contact Email (Main): joe_bloggs@example.com

Joe, as the IT administrator, also has the passwords to access these accounts:

* VentraIP top-level-account.
* VentraIP cPanel.
* WordPress wp-admin
* WordPress database
* CiviCRM database
  
* CMRT Webmail: admin@cmrailtrail.org.au
* CiviCRM Account Username: admin
  

## Systems

VentraIP provide hosting services for two domains for CMRT:
* https://cmrailtrail.org.au - WordPress Website and Webmail
* https://crm.cmrailtrail.org.au - CiviCRM

## What can be logged into

The following is a list of accounts and the URL to get to the logon prompts

* VentraIP Management: https://vip.ventraip.com.au
* Webmail: https://cmrailtrail.org.au:2096/
* WordPress Website Dashboard: https//:cmrailtrail.org.au/wp-admin

* Main cPanel: https://cmrailtrail.org.au:2083/
* CiviCRM Dashboard: https//:cmrailtrail.org.au/logon

* CiviCRM Webmail: https://crm.cmrailtrail.org.au:2096
* CiviCRM cPanel: https://crm.cmrailtrail.org.au:2083/

## VentraIP Management: https://vip.ventraip.com.au

This account is provided by VentraIP. It is the top-level account that provides access to everything. For day-to-day operations it is not normally necessary to log into this account. Common reasons for logging into this account are:
* Webmail management. E.g. Create or delete a webmail account.
* IT administrators wanting to use SSH and needing to whitelist their IP addresses.

## Webmail

The Webmail service is provided for: 

* CMRT Executives, Committee and Contractors of CMRT. Webmail accounts normally use the persons first name, and if there is first name duplications then the first letter of the Surname is added.  E.g. *steve@cmrailtrail.org.au* and *steveh@cmrailtrail.org.au*

* There are also generic email accounts that are assigned to differnet CMRT representatives to monitor. These *@cmrailtrail.org.au* email addresses are prefixed with names like: *president, secretary, admin, hello, noreply, cron*.

The username of a Webmail account is also used as the username to login to a CiviCRM account.

It is best to setup a Webmail password first as it has the most integrity requirements. E.g. Must be 11 characters, etc. Then, for simplicity, this password could then be used for CiviCRM login.

## WordPress

To reach the login screen of the WordPress accounts on the primary domain: *https://cmrailtrail.org.au/wp-admin*

These accounts are used by the WordPress administrators to make changes to the Website. They may also modify Wordpress plugins. An aim it that there will not be data needing to be collected, etc, from in WordPress or its plugins. (E.g woocommerce data, as this role is now performed by CiviCRM.

##  CiviCRM

To reach the login screen for CiviCRM accounts on the sub-domain: *https://crm.cmrailtrai.org.au*

The CMRT executives, committee and contractors have individual accounts. To login they use the same username as for their Webmail account login. E.g*steve@cmrailtrail.org.au*

There are also CiviCRM accounts with gereric usernames for logging in. E.g. *admin* and *cron*. When these accounts also have Webmail then the webmail name account may akternatively be used as the username. E.g. *admin@cmrailtrail.org.au* and *cron@cmrailtrail.org.au*

All CMRT executive and committee will be Individual contacts in the CiviCRM database. Using Administer -->  Users and Permissions --> User Accounts displays *Administer User Accounts*. Each account may be *editied*.  The fields are: Roles, Username, Contact, User Email, Enabled, Timezone and Preferred Language. 

From this list the fields the *Username* and *Contact* are indicated as mandatory. As previously stated the *Username* is normally the same as the Webmail email address. E.g. steve@cmrailtrail.org.au. The *Contact* 


















