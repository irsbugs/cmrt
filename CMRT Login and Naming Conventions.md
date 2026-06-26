# Login and Naming Conventions

2026-06-27

## Introduction

For the management and operation of the CMRT IT systems a variety of login's are a requirement. This document is a guideline to the account login naming conventions. 

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

To reach the login screen of the WordPress accounts on the primary domain: *https://cmrailtral.org.au/wp-admin*

These accounts are used by the WordPress administrators to make changes to the Website. They may also modify Wordpress plugins. An aim it that there will not be data needingto be collected, etc, from in WordPress (E.g woocommerce data) as this fole is not performed by CiviCRM














