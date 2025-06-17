# ABN Code field

Alter SIC Code field with a maximum length of 8 characters to be called ABN and have a maximum length of 20 characters.

In Civicrm main screen --> Customize Data and Screens --> Word Replacements

* Enabled: Checked
* Original: SIC Code
* Replacement: ABN
* Exact Match: Checked

...then *Save*

Reference:

https://civicrm.stackexchange.com/questions/37389/how-to-increase-the-size-of-a-note-field-type
you can update the field type from text to longtext:

*ALTER TABLE `civicrm_value_table_name` MODIFY `field_name` LONGTEXT DEFAULT NULL;*

Command to increase SIC_Code from 8 Characters to 20 to support ABN numbers in Australia.

*`ALTER TABLE `civicrm_contact` MODIFY `sic_code` varchar(20) DEFAULT NULL;`*

Originally...
```
MariaDB [civicrm]> show columns from civicrm_contact;
+--------------------------------+------------------+------+-----+---------------------+-------------------------------+
| Field                          | Type             | Null | Key | Default             | Extra                         |
| sic_code                       | varchar(8)       | YES  |     | NULL                |                               |
```

Perform the alteration...
```
MariaDB [civicrm]> ALTER TABLE `civicrm_contact` MODIFY `sic_code` varchar(20) DEFAULT NULL;
Query OK, 0 rows affected (0.022 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

After altering...
```
MariaDB [civicrm]> show columns from civicrm_contact;
+--------------------------------+------------------+------+-----+---------------------+-------------------------------+
| Field                          | Type             | Null | Key | Default             | Extra                         |
| sic_code                       | varchar(20)      | YES  |     | NULL                |                               |
```

Review of civicrm_contact table...
```
MariaDB [civicrm]> select ID, first_name, last_name,sic_code from civicrm_contact;
+----+------------+-----------+----------+
| ID | first_name | last_name | sic_code |
+----+------------+-----------+----------+
|  1 | NULL       | NULL      | NULL     |
|  2 | Ian        | Stewart   | NULL     |
|  3 | Joseph     | Bloggs    | NULL     |
|  4 | Joseph     | Bloggs    | NULL     |
|  5 | Joseph     | Bloggs    | NULL     |
|  6 | Joseph     | Bloggs    | NULL     |
|  7 | Joseph     | Bloggs    | NULL     |
|  8 | Joseph     | Bloggs    | NULL     |
|  9 | Joseph     | Bloggs    | NULL     |
| 10 | Joseph     | Bloggs    | NULL     |
| 11 | Joseph     | Bloggs    | NULL     |
+----+------------+-----------+----------+
11 rows in set (0.000 sec)

MariaDB [civicrm]> 
```
Might need a reboot for change to take effect???

In Civicrm main screen --> Customize Data and Screens --> Dropdown options --> Phone Types 
Changed the order so Mobile (2) at the top and Phone (1) below it.

There is a possiblility of changing the values. swap the 2 and 1

====

https://docs.civicrm.org/user/en/latest/initial-set-up/customizing-the-user-interface/

if your organization does not typically refer to monetary transactions as "contributions," but prefers to use the term "donations," you can define a word replacement and have it automatically altered throughout your instance of CiviCRM.

