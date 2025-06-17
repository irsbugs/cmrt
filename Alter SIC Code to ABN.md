# ABN Code field

Alter SIC Code field with a maximum length of 8 characters to be called ABN and have a maximum length of 20 characters.

In Civicrm main screen --> Customize Data and Screens --> Word Replacements

Enabled: Checked
Original: SIC Code
Replacement: ABN
Exact Match: Checked

Then Save

Reference:
https://civicrm.stackexchange.com/questions/37389/how-to-increase-the-size-of-a-note-field-type
you can update the field type from text to longtext
ALTER TABLE `civicrm_value_table_name` MODIFY `field_name` LONGTEXT DEFAULT NULL;

Command to increase SIC_Code from 8 Characters to 20 to support ABN numbers in Australia.

ALTER TABLE `civicrm_contact` MODIFY `sic_code` varchar(20) DEFAULT NULL;

Originally...
MariaDB [civicrm]> show columns from civicrm_contact;
+--------------------------------+------------------+------+-----+---------------------+-------------------------------+
| Field                          | Type             | Null | Key | Default             | Extra                         |
| sic_code                       | varchar(8)       | YES  |     | NULL                |                               |


MariaDB [civicrm]> ALTER TABLE `civicrm_contact` MODIFY `sic_code` varchar(20) DEFAULT NULL;
Query OK, 0 rows affected (0.022 sec)
Records: 0  Duplicates: 0  Warnings: 0

After altering...
MariaDB [civicrm]> show columns from civicrm_contact;
+--------------------------------+------------------+------+-----+---------------------+-------------------------------+
| Field                          | Type             | Null | Key | Default             | Extra                         |
| sic_code                       | varchar(20)      | YES  |     | NULL                |                               |


Might need a reboot for change to take effect???
