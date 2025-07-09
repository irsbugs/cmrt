# Who can log in to CMRT Website?

**DRAFT - 2025-07-09 - Input/Changes Welcomed**

### General Public, CMRT Members, CMRT Volunteers and CMRT Doners, etc.

The cmrailtrail.org.au website is publically available and there is no account login for general members, volunteers, doners, etc. 

As there is no additional data that is publically hidden there is no need for a provision for members, etc. to log in to an account to view such data. 

If someone notices a mistake on the website, then they may phone or e-mail a CMRT official to request a correction to the data.

When receiving bulk e-mails from CiviCRM/WordPress then the receiver has the right to request to have no further bulk e-mails sent to them. This is performed by the receiver by checking a field on the bulk mail they received. Alternatively they can ring a CMRT Official and request them to set the no-bulk-email flag for this client/organization/contact.

### CMRT Official

The CMRT officals need to be able to login to the Ventraip account and/or the Wordpress account. The website login pages are:

* Webmail: https://cmrailtrail.org.au/webmail
* WordPress Admin: https://cmrailtrail.org.au/wp-admin  Note: *wp-admin* - may be changed for security reasons.


### Webmail

Ventraip provide a Webmail service. This is used by CMRT officials to receive emails sent to the account they are responsible for operating. These include:

* CMRT President - president@cmrailtrail.org.au - Currently: Janice and Geoff
* CMRT Treasurer - treasurer@cmrailtrail.org.au - Currently: Des
* CMRT Secretary - secretary@cmrailtrail.org.au - Currently: Maureen.
* CMRT Committee - committee@cmrailtrail.org.au - Currently: Steve F., Ken, Greg, Steve H. and Kate.

* CMRT Admin - admin@cmrailtrail.org.au - Current IT Support Admistrator(s). Currently: Ken, Wayne, Castlemaine IT company?, Ian.
  
If there is a change in the person that performs any of the above roles, then the login details and the e-mail account is passed to the replacement person.

Additional email accounts will exist, which would normally be routinely checked by the Secretary:

* hello@cmrailtrail.org.auCMRT
* info@cmrailtrail.org.au
* no-reply@cmrailtrail.org.au ?
* ? Keep some old email accounts for backwards compatibility - janice@cmrailtrail.org.au - Can e-mail be re-directed ? 

Old / No-longer-used accounts should be reviewed and have the data backed-up or moved, then the account is deleted.

**Ventraip Account Management**

As well as the CMRT Administrator(s) having a Webmail account, they also have access to overall management of the website by logging into the accounts:

* C-Panel: https://cmrailtrail.org.au/cpanel
* VIP Control: https://vip.ventraip.com.au/login (2FA)
  
### Wordpress Account

The WordPress *Users* have accounts managed by the WordPress application. On logging into a WordPress account management functions may be performed on WordPress and its plugins. The CiviCRM plugin for WordPress has the ability to control the privileges a *User* is granted for modifying CiviCRM. 

The WordPress *User* account names, will also be *contacts* in CiviCRM database.

The login to WordPress is:

* https://cmrailtrail.org.au/wp-admin

The WordPress login requires a Username and Password. The Usernames will be:

* CMRT_President
* CMRT_TreasurerAdmin
* CMRT_Secretary
* CMRT_Committee

...and for IT Administration and support:

* CMRT_Admin

From the CiviCRM System Administrators Guide:
[Synchronize WordPress users to CiviCRM contacts](https://docs.civicrm.org/sysadmin/en/latest/integration/wordpress/#synchronize-wordpress-users-to-civicrm-contacts)

CiviCRM offers a function to synchronize users to contacts: CiviCRM will check each user record for a contact record. A new contact record will be created for each user where one does not already exist. To perform this function go to **Administer -> Users and Permissions -> Synchronize Users to Contacts**. This is automatic upon cli

The CiviCRM database will be synchronized to contain the above five *Contacts*.

These six *Contacts* are the only people registered in CiviCRM who can send emails from the CiviCRM application. 

For example: Maureen may write an email in CiviCRM to send to all Castlemaine residents who are listed in the CiviCRM database. E.g. Contacts in CiviCRM with a postcode of 3450. She may sign off the email as "Maureen - CMRT Secretary".  The Castlemaine recipients of the e-mail will see that it is from secretary@cmrailtrial.org.au. If they decide to reply to Maureen then the reply goes back to: secretary@cmrailtrial.org.au. Maureen logs into her Webmail to read the reply.

The *CMRT_Admin_WP* adinistrator, would not have privileges to perform tasks in CiviCRM. The rational is that one IT administrator may be focused on WordPress and another IT administrator focused on CiviCRM.

**Operational Consideration**

In using CiviCRM it may be convenient to have two tabs open on your browser. One tab is for Webmail the other tab is for CiviCRM. 

### Actions 

On the simulation computer:

* Enter sixaDMIN WordPress Users.
* Synchronize WordPress users to be CiviCRM contacts.
* Test/Check.
* Set up mail sending capabilities in CiviCRM for these contacts.

On CMRT system:
* Add Webmail accounts for the above contacts
* Add WordPress User accounts for the above contacts
* Synchronize WordPress users to be CiviCRM contacts.
* Set up mail sending capabilities in CiviCRM for these contacts.
* Test/Check. 

**TO DO**

If an email originates from the CiviCRM Application from the Secretary, then does a copy of the mail get placed in the Secretaries Webmail sent folder?

Check-out/Clean-up who can log into:

* C-Panel: https://cmrailtrail.org.au/cpanel
* VIP Control: https://vip.ventraip.com.au/login (2FA)
