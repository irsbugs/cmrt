# Custom Fields

When importing data from csv files into CiviCRM one aim is that the columns being imported have the same names as the field names reserved by CiviCRM. This simplifies and automates the matching of the imported fields with the CiviCRM fields. For example, If the field on the csv file is *Surame* then change the csv file so the field is "Last Name", which is what CiviCRM expects.

If data needs to be imported, for which there is not an appropriate CiviCRM field, then a *Custom* field may be created.

For importing to CiviCRM the following *Custom* fields were creaated:

For Individual Contacts:
* Info

For Organizations:
* Australian Business number. ABN.

### Info Field

When importing a CSV file for *Individual* contacts, then the *Info* column will be matched with the *Info* custom field. The *Info* has been created using a *Note* data type. This provides multiline text entry, and has been initially setup to be have maximums of 100 characters per row and 10 rows.

For the data imported from MailChimp the *NOTES* column was renamed *Info* to perform the import. This column contained time-stamped information. Some records had multiple time-stamped information in, what is now, the *Info* column. Typing *Crtl Enter* in a spreadsheet allows a cells data to contain a *newline*. For example a single cell can be changed from:
```
[2021-11-07 10:55:36] Donated $30 8/12/20 @Janice audit 3 Nov 2021 [2021-11-01 04:28:57] Community Ambassador Yapeen
```

...to:
```
[2021-11-07 10:55:36] Donated $30 8/12/20 @Janice audit 3 Nov 2021 
[2021-11-01 04:28:57] Community Ambassador Yapeen
```

When creating the Individual contacts for the CMRT officer, the Info field contains the 2025 elected officials name. E.g. For *President CMRT* th Info field is: 2025: Janice Simpson

### ABN Field

