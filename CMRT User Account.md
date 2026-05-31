# User Accounts on CiviCRM Standalone

## Introduction

When CiviCRM is a plugin to a CMS, E.g. Wordpress, then User accounts that login and access the CiviCRM and Wordpress dashboard are managed by the CMS.


With CiviCRM Standalone, the User accounts are managed by CiviCRM. A User account has a set of priviledges and a password, is linked to an Individual Contact who has an email address. The email address is likely to that of the mail system provided by the ISP and it will also have a password. In summary:

* CiviCRM User account requires:
  * Username
  * Password
* CiviCRM Individual Contact requires a minimum of:
  * First Name
  * Last Name
  * Email
* Email account requires:
  * Email username
  * Email password  
  * Display Name
 
As an example of the above:

* CiviCRM User account. In this case for the User account to manage Cron job:
  * Username: civicrm_cron
  * Password: Cronpassword#1 <--- If desired to have the same password for the email, then meet the Email password requirements specs.
  
Connection to login page from Web-browser: https://crm.cmrailtrail.org.au/civicrm/login Note: Ensure you are not already logged in with another account.
    
* CiviCRM Individual Contact requires a minimum of:
  * First Name: Cron
  * Last Name:  Admin
  * Email: cron@cmrailtrail.org.au

* Email account using VentraIP Webmail:
  * Email username: cron
  * Email password:  Cronpassword#1
  * Display Name: Cron Admin

Connection to VentraIP Webmail login from a web-browser: https://s03dd.syd6.hostingplatform.net.au:2096/

Note: During the Installation of CiviCRM Standalone the installation process requests and Administration User account, pssword and email address. 


## Example of adding password for Cron after creating the civicrm_cron user account. 

Performed by copying and pasting the Admin password.

```

MariaDB [cmrailtr_civi]> SELECT id, uf_id, uf_name, username, hashed_password FROM civicrm_uf_match;
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+
| id | uf_id | uf_name                        | username            | hashed_password                                         |
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+
|  1 |     1 | hello@cmrailtrail.org.au       | civicrm_admin       | $$1234------secure Bcrypt hashing algorithm------4321$$ |
|  2 |     2 | cron@cmrailtrail.org.au        | civicrm_cron        |                                                         |
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+

```
Use SQL to add the password for the Cron account with uf_id = 2.
```
MariaDB [cmrailtr_civi]> UPDATE civicrm_uf_match SET hashed_password = '$$1234------secure Bcrypt hashing algorithm-----4321$$' WHERE id = 2;

MariaDB [cmrailtr_civi]> SELECT id, uf_id, uf_name, username, hashed_password FROM civicrm_uf_match;
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+
| id | uf_id | uf_name                        | username            | hashed_password                                         |
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+
|  1 |     1 | hello@cmrailtrail.org.au       | civicrm_admin       | $$1234------secure Bcrypt hashing algorithm------4321$$ |
|  2 |     2 | cron@cmrailtrail.org.au        | civicrm_cron        | $$1234------secure Bcrypt hashing algorithm------4321$$ |
+----+-------+--------------------------------+---------------------+---------------------------------------------------------+

```

On a web-browser go to: https://crm.cmrailtrail.org.au/civicrm/login

Log into civicrm_cron with password the same as civicrm_admin



## Gemini response to query on setting password in CiviCRM Standalone

Question to Gemini:  

Can the password be setup by using mysql and going to the CiviCRM uf_match table and inserting a hashed_password for the desired uf_id?

Yes, absolutely. You can set a password directly in the MySQL database for CiviCRM Standalone.

As you noted, CiviCRM Standalone repurposes the civicrm_uf_match table (which traditionally maps external CMS users to CiviCRM contacts) to store actual native user accounts.

### 1. The Table Structure

In a Standalone installation, the civicrm_uf_match table has added columns specifically for managing credentials, including username and password.

To update or set a password directly via MySQL, you will target the password column (not hashed_password) for the row corresponding to your target user ID.

### 2. The Hashing Mechanism

CiviCRM Standalone relies on PHP's native password_hash() function, which defaults to the secure Bcrypt hashing algorithm.

Because of this, you cannot use MySQL's legacy, built-in MD5() or SHA2() functions to generate the string. Doing so will break the login mechanism, as CiviCRM won't be able to verify it. You must generate a proper Bcrypt hash first.


## Step-by-Step Direct Database Update

### Step 1: Generate the Bcrypt Hash

You can use the command line via PHP to quickly spit out a properly formatted string:

```Bash

php -r "echo password_hash('YourNewSecurePassword', PASSWORD_BCRYPT) . PHP_EOL;"
```

*This will output a string resembling something like: $2y$10$abcdefghijklmnopqrstuv...*

### Step 2: Run the MySQL Update Statement

Log into your MySQL/MariaDB terminal and execute the update query against your target id:

```SQL
UPDATE civicrm_uf_match 
SET hashed_password = '$2y$10$YourGeneratedHashStringGoesHere...' 
WHERE id = 12;
```

⚠️ **Note on IDs:** Make sure you are filtering by the primary key id of the user account row in the civicrm_uf_match table, or by its uf_id (which matches the corresponding internal record), depending on how your specific accounts are indexed.

Once the query executes successfully, the user can immediately log in using their username and the plain-text password you just hashed. No cache clearing or system reboot is required!

