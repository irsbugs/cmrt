# Who can log in to CMRT Website? - V2 

**DRAFT - 2025-07-10 - Switched First name and Last name - Input/Changes Welcomed**

### General Public, CMRT Members, CMRT Volunteers and CMRT Doners, etc.

The cmrailtrail.org.au website is publically available and there is no account login for general members, volunteers, doners, etc. 

As there is no additional data that is publically hidden there is no need for a provision for members, etc. to log in to an account to view such data. 

If someone notices a mistake on the website, then they may phone or e-mail a CMRT official to request a correction to the data.

When receiving bulk e-mails from CiviCRM/WordPress then the receiver has the right to request to have no further bulk e-mails sent to them. This is performed by the receiver by checking a field on the bulk mail they received. Alternatively they can ring a CMRT Official and request them to set the no-bulk-email flag for this client/organization/contact.

### CMRT Officiers

The CMRT officers need to be able to login to the Ventraip account and/or the Wordpress account. The website login pages are:

* Webmail: https://cmrailtrail.org.au/webmail
* WordPress Admin: https://cmrailtrail.org.au/wp-admin  Note: *wp-admin* - may be changed for security reasons.


### Webmail

Ventraip provide a Webmail service. This is used by CMRT officials to receive emails sent to the account they are responsible for operating. These include:

* President CMRT - president@cmrailtrail.org.au - Currently: Janice.
* Vice President CMRT - vicepresident@cmrailtrail.org.au - Currently Geoff
* Treasurer CMRT - treasurer@cmrailtrail.org.au - Currently: Des
* Secretary CMRT - secretary@cmrailtrail.org.au - Currently: Maureen.
* Committee CMRT - committee@cmrailtrail.org.au - Currently: Steve F., Ken, Greg, Steve H. and Kate.

* Admin CMRT - admin@cmrailtrail.org.au - Current IT Support Admistrator(s). Currently: Ken, Castlemaine IT company?, Ian.
  
If there is a change in the person that performs any of the above roles, then the login details and the email account is passed to the replacement person.

Additional email accounts may exist, which would normally be routinely checked by the Secretary or Admin:

* hello@cmrailtrail.org.au
* no-reply@cmrailtrail.org.au ?
* Keep email accounts for backwards compatibility - E.g. janice@cmrailtrail.org.au
* Set up additional redirection of emails. 

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
* CMRT_Vicepresident
* CMRT_Treasurer
* CMRT_Secretary
* CMRT_Committee

...and for IT Administration and tech support:

* CMRT_Admin 

From the CiviCRM System Administrators Guide:
[Synchronize WordPress users to CiviCRM contacts](https://docs.civicrm.org/sysadmin/en/latest/integration/wordpress/#synchronize-wordpress-users-to-civicrm-contacts)

    CiviCRM offers a function to synchronize WordPress *users* to CiviCRM *contacts*: CiviCRM will check each user record for a contact record. 
    A new contact record will be created for each user where one does not already exist. To perform this function go to 
    **Administer -> Users and Permissions -> Synchronize Users to Contacts**. 

This synchronization is now  automatically performed when a *user* is added to WordPress. However the information collected from the WordPress *user* in the CiviCRM *contact* is minimal. It is necessary to edit each of these *contacts* and supply additional data. This *editing* may be performed by importing a .csv file.

Thus, the CiviCRM database will be synchronized to contain the above five *Contacts*.

These six *Contacts* are the only people registered in CiviCRM who can send emails from the CiviCRM application. 

For example: Maureen may write an email in CiviCRM to send to all Castlemaine residents who are listed in the CiviCRM database. E.g. Contacts in CiviCRM with a *postcode*'s of *3450* and *3451*. She may sign off the email as "Maureen - CMRT Secretary".  The Castlemaine recipients of the e-mail will see that it is from secretary@cmrailtrial.org.au. If they decide to reply to Maureen then the reply goes back to: secretary@cmrailtrial.org.au. Webmail then forwards this to Maureen's personal Webmail account maureen@cmtrailtril.org.au.

**Operational Considerations**

* In using CiviCRM it may be convenient to have two tabs open on your browser. One tab is for Webmail the other tab is for CiviCRM.
  
* When there is a change of an official, then rather than having a new email account created for the new official and forwarding their emails to their personal email account, the new official may wish to log directly into the officials Webmail. i.e. They do not need to have a personal email account.

### External Identifier

The *External Identifier* appears to need unique numbering, even if data is imported from different .csv files. Have an *External Identifier* policy like this:

* 1 Default Organization. CMRT
* 10 - 99 Official Positions of the CMRT Community organization. President, Secretary etc.
* 100 - 399 Organization Business
* 400 - 699 Organization Community
* 700 - 799 Organization Goverment - Federal
* 800 - 899 Organization Government - Local
* 900 - 999 Organization Government - State   
* 1000+ Individual

How would this work with an Individual contact that subscribes via an input form on the website? Have no *external identifier* but *contact source* file as *website input*.

Upon a extract as .csv and restore then *external identifiers* can be set correctly.

### Identifiers

**ID**: WordPress *user* identification number
**id**: CiviCRM Contact ID. Sequential Deleted *contacts* remain in the database. ID is not re-alllocated.
**external_identifier**: Supplied via .csv import file. No duplication of External Identifiers between .csv import files.
**user**: WordPress sequential. Deleted users are removed from WordPress database and User ID is lost.

The WordPress database has *ID* as a sequential number. Initial experimenting used *ID* numbers 1 to 13, then these *users* were deleted. Their numbers are not re-used. Then next *user* added to WordPress would receive the *ID* of 20
```
MariaDB [cmrailtr_czhn1]> SELECT ID, user_login, user_nicename, display_name, user_status, user_email FROM bsen_users;
+----+--------------------+--------------------+---------------------+-------------+----------------------------------+
| ID | user_login         | user_nicename      | display_name        | user_status | user_email                       |
+----+--------------------+--------------------+---------------------+-------------+----------------------------------+
| 14 | CMRT_President     | cmrt_president     | President CMRT      |           0 | president@cmrailtrail.org.au     |
| 15 | CMRT_Treasurer     | cmrt_treasurer     | Treasurer CMRT      |           0 | treasurer@cmrailtrail.org.au     |
| 16 | CMRT_Secretary     | cmrt_secretary     | Secretary CMRT      |           0 | secretary@cmrailtrail.org.au     |
| 17 | CMRT_Committee     | cmrt_committee     | Committee CMRT      |           0 | committee@cmrailtrail.org.au     |
| 18 | CMRT_Admin         | cmrt_admin         | Admin CMRT          |           0 | admin@cmrailtrail.org.au         |
| 19 | CMRT_Vicepresident | cmrt_vicepresident | Vice President CMRT |           0 | vicepresident@cmrailtrail.org.au |
+----+--------------------+--------------------+---------------------+-------------+----------------------------------+
```

When CiviCRM loads the additional csv data for the *contacts* an *External Identifier* of unique numbers are included as one of the columns of data in the csv file. CiviCRM provides each *contact* with a unique *id* number. Note that in the following case it is just coincidental that the value of the *id* is the same as the value of the *external_identifier*.

```
MariaDB [cmrailtr_czhn1]> SELECT ID, user_login, user_nicename, display_name, user_status, user_email FROM bsen_users;
+----+--------------------+--------------------+---------------------+-------------+----------------------------------+
| ID | user_login         | user_nicename      | display_name        | user_status | user_email                       |
+----+--------------------+--------------------+---------------------+-------------+----------------------------------+
| 14 | CMRT_President     | cmrt_president     | President CMRT      |           0 | president@cmrailtrail.org.au     |
| 15 | CMRT_Treasurer     | cmrt_treasurer     | Treasurer CMRT      |           0 | treasurer@cmrailtrail.org.au     |
| 16 | CMRT_Secretary     | cmrt_secretary     | Secretary CMRT      |           0 | secretary@cmrailtrail.org.au     |
| 17 | CMRT_Committee     | cmrt_committee     | Committee CMRT      |           0 | committee@cmrailtrail.org.au     |
| 18 | CMRT_Admin         | cmrt_admin         | Admin CMRT          |           0 | admin@cmrailtrail.org.au         |
| 19 | CMRT_Vicepresident | cmrt_vicepresident | Vice President CMRT |           0 | vicepresident@cmrailtrail.org.au |
+----+--------------------+--------------------+---------------------+-------------+----------------------------------+
```

CiviCRM .csv file when importing additional data on the CMRT officiers.

```
External Identifier	First Name	Last Name	Preferred Communication Method	Preferred Language	Contact Source	Communication Style	Employee of	Street Address	City	Post Code	State	Country	Phone	Email	Website
10	President	CMRT	Email	en_AU	CMRT_contact.csv	Formal	Castlemaine-Maryborough Rail Trail	Unit 6, 167-171 Railway St.	Maryborough	3465	VIC	Australia	61428660038	president@cmrailtrail.org.au	https://cmrailtrail.org.au
11	Treasurer	CMRT	Email	en_AU	CMRT_contact.csv	Formal	Castlemaine-Maryborough Rail Trail	Unit 6, 167-171 Railway St.	Maryborough	3465	VIC	Australia	61428660038	treasurer@cmrailtrail.org.au	https://cmrailtrail.org.au
12	Secretary	CMRT	Email	en_AU	CMRT_contact.csv	Formal	Castlemaine-Maryborough Rail Trail	Unit 6, 167-171 Railway St.	Maryborough	3465	VIC	Australia	61428660038	secretary@cmrailtrail.org.au	https://cmrailtrail.org.au
13	Committee	CMRT	Email	en_AU	CMRT_contact.csv	Formal	Castlemaine-Maryborough Rail Trail	Unit 6, 167-171 Railway St.	Maryborough	3465	VIC	Australia	61428660038	committee@cmrailtrail.org.au	https://cmrailtrail.org.au
14	Admin	CMRT	Email	en_AU	CMRT_contact.csv	Formal	Castlemaine-Maryborough Rail Trail	Unit 6, 167-171 Railway St.	Maryborough	3465	VIC	Australia	61428660038	admin@cmrailtrail.org.au	https://cmrailtrail.org.au
<img width="1946" height="101" alt="image" src="https://github.com/user-attachments/assets/08d30858-75f3-435b-8d73-b5a2e1dcf5b6" />

```
### Deleting CiviCRM *Contacts* and WordPress *Users* 

The following demonstrates the deleting of contacts.

Every WordPress *user account* automatically becomes a CiviCRM *contact*. The CiviCRM *contact* can not be deleted, unless the WordPress *user account* has already been deleted. Thus, keeping WordPress *user accounts* to a tidy format and at a minimum reduces *contacts* existing on CiviCRM that may not be necessary.

When deleting CiviCRM *contacts* note they remain in the CiviCRM database, but with the *is_deleted* field set to *True*. If *delete permanently* is selected this removes the *contact* entry from the CiviCRM database.

Email accounts created in Webmail do not proliferate their existance or data to WordPress or CiviCRM. Thus, apart from the five detailed above for CMRT officiers, there can be any number of other email accounts.

Upon deleting a WordPress *User*, then it is probably appropriate to backup and delete any Webmail account(s) of the *User*. 

Example: WordPress database: After *ian* and *president* and other experimental *users* were deleted. Then *president* was added again and is assigned the WordPress ID = 14
```
MariaDB [cmrailtr_czhn1]> SELECT ID, user_login, user_nicename, display_name, user_status, user_email FROM bsen_users;
+----+----------------+----------------+----------------+-------------+------------------------------+
| ID | user_login     | user_nicename  | display_name   | user_status | user_email                   |
+----+----------------+----------------+----------------+-------------+------------------------------+
| 14 | CMRT_President | cmrt_president | President CMRT |           0 | president@cmrailtrail.org.au |
| 15 | CMRT_Treasurer | cmrt_treasurer | Treasurer CMRT |           0 | treasurer@cmrailtrail.org.au |
| 16 | CMRT_Secretary | cmrt_secretary | Secretary CMRT |           0 | secretary@cmrailtrail.org.au |
| 17 | CMRT_Committee | cmrt_committee | Committee CMRT |           0 | committee@cmrailtrail.org.au |
| 18 | CMRT_Admin     | cmrt_admin     | Admin CMRT     |           0 | admin@cmrailtrail.org.au     |
+----+----------------+----------------+----------------+-------------+------------------------------+
```
CiviCRM Datebase: Showing *ian* id=2 and *President* id=3  having *is_deleted* = 1 = True. Note that id's 4 to 9 were *deleted permanently* by CiviCRM, thus they no longer show up in the database.

Then *President* added again and is allocated CiviCRM *id* of 10.
```
MariaDB [cmrailtr_civicrm]> select id, contact_type, display_name, is_deleted, external_identifier, contact_type from civicrm_contact;
+----+--------------+------------------------------------+------------+---------------------+--------------+
| id | contact_type | display_name                       | is_deleted | external_identifier | contact_type |
+----+--------------+------------------------------------+------------+---------------------+--------------+
|  1 | Organization | Castlemaine-Maryborough Rail Trail |          0 | 1                   | Organization |
|  2 | Individual   | ianstewart56@hotmail.com           |          1 | NULL                | Individual   |
|  3 | Individual   | CMRT President                     |          1 | NULL                | Individual   |
| 10 | Individual   | President CMRT                     |          0 | NULL                | Individual   |
| 11 | Individual   | Treasurer CMRT                     |          0 | NULL                | Individual   |
| 12 | Individual   | Secretary CMRT                     |          0 | NULL                | Individual   |
| 13 | Individual   | Committee CMRT                     |          0 | NULL                | Individual   |
| 14 | Individual   | Admin CMRT                         |          0 | NULL                | Individual   |
+----+--------------+------------------------------------+------------+---------------------+--------------+
```
In the above the two CiviCRM *contacts* were *deleted*, but not *deleted permanently*. They may be permanently deleted from the CivCRM database using the followig SQL command:
```
MariaDB [cmrailtr_civicrm]> DELETE FROM civicrm_contact WHERE is_deleted=1;
Query OK, 2 rows affected (0.012 sec)
```
The CiviCRM database now displays the following contacts:
```
MariaDB [cmrailtr_civicrm]> select id, contact_type, display_name, is_deleted, external_identifier, contact_type from civicrm_contact;
+----+--------------+------------------------------------+------------+---------------------+--------------+
| id | contact_type | display_name                       | is_deleted | external_identifier | contact_type |
+----+--------------+------------------------------------+------------+---------------------+--------------+
|  1 | Organization | Castlemaine-Maryborough Rail Trail |          0 | 1                   | Organization |
| 10 | Individual   | President CMRT                     |          0 | NULL                | Individual   |
| 11 | Individual   | Treasurer CMRT                     |          0 | NULL                | Individual   |
| 12 | Individual   | Secretary CMRT                     |          0 | NULL                | Individual   |
| 13 | Individual   | Committee CMRT                     |          0 | NULL                | Individual   |
| 14 | Individual   | Admin CMRT                         |          0 | NULL                | Individual   |
+----+--------------+------------------------------------+------------+---------------------+--------------+
```

### Actions 

**On the simulation computer**:

* Enter five WordPress Users.
* Check previous action automatically synchronized WordPress users to be CiviCRM contacts.
* Export the five CiviCRM contacts as a csv file.
* Edit the .csv file to have more information that was collected with WordPress.
* Remove unwanted columns. For example don't have Contact ID, matching is made using First Nae, Last Name and Email.
* Import the .csv file to *fill* in the additional details of the *Individual* CiviCRM 
* Test/Check.
* Set up mail sending capabilities in CiviCRM for these contacts.

**On CMRT system**:

* Add Webmail accounts for the above contacts
* Manually add WordPress *user accounts* for the above contacts.
* Check WordPress *users* data was automatically transferred to become CiviCRM *contacts*.
* Import the .csv file to supply more *Individual* data for each CiviCRM *contact*.
* Set up mail sending capabilities in CiviCRM for these contacts.
* Test/Check. 

**TO DO**

* Check: If an email originates from the CiviCRM Application from the Secretary, then does a copy of the mail get placed in the Secretaries Webmail sent folder? Where does CiviCRM store copies of sent emails / one copy of bulk sent emails?

* Check-out/Clean-up who can log into:

    * C-Panel: https://cmrailtrail.org.au/cpanel
    * VIP Control: https://vip.ventraip.com.au/login (2FA)
