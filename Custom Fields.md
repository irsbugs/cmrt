# Custom Fields

When importing data from csv files into CiviCRM one aim is that the columns being imported have the same names as the field names reserved by CiviCRM. This simplifies and automates the matching of the imported fields with the CiviCRM fields. For example, If the field on the csv file is *Surname* then change the csv file so the field is *Last Name*, which is what CiviCRM expects.

If data needs to be imported, for which there is not an appropriate CiviCRM field, then a *Custom* field may be created.

For importing to CiviCRM the following *Custom* fields were created:

For Individual Contacts:
* Info

For Organizations:
* Australian Business Number. ABN.

### Info Field

When importing a CSV file for *Individual* contacts, then the *Info* column will be matched with the *Info* custom field. The *Info* has been created using a *Note* data type. This provides multi-line text entry, and has been initially setup to be have maximums of 100 characters per row and 10 rows.

For the data imported from MailChimp the *NOTES* column was renamed *Info* to perform the import. This column contained time-stamped information. Some records had multiple time-stamped information in, what is now, the *Info* column. Typing *Crtl Enter* in a spreadsheet allows a cells data to contain a *newline*. For example a single cell can be changed from:
```
[2021-11-07 10:55:36] Donated $30 8/12/20 @Janice audit 3 Nov 2021 [2021-11-01 04:28:57] Community Ambassador Yapeen
```

...to:
```
[2021-11-07 10:55:36] Donated $30 8/12/20 @Janice audit 3 Nov 2021 
[2021-11-01 04:28:57] Community Ambassador Yapeen
```

When creating the *Individual* contacts for the CMRT officers, the *Info* field contains the 2025 elected officials name. E.g. For *President CMRT* the Info field is: *2025: Janice Simpson*. This was done as a way of havig some data for testing the importing of the csv file. The *Info* for these six *Individual* contacts is open for change or additional information.


### ABN Field

All Australian Organizations have an Australian Business Number. The 11 integers ABN is normally presented in the formaat *ABN 12 987 654 321*. The Field has been created with a single-line of up to 20 Characters. When importing *Organization* contact details, then CiviCRM is expecting a column with the heading *ABN*.


### Relationships

There are two tyes of relationship that exist between an *Organization* and an *Individual*.

* Individual: *Employee of* and Organisation: *Employer of*.
* Individual: *Volunteer for* and Organisation: *Volunteer is*.

When importing a csv *Individual* contact, then either the *Employee of* or *Volunteer for* field can be set. Ensure in the fields being imported there is an *Organisation Name* column. During importing, from the drop-down menu next to *Organisation Name*, select either  *Employee of* or *Volunteer for*. It then opens an adjacent drop-down menu in which *Organisation* is then selected. in the case where there are both volunteers and employees, then this requires that two separate csv files be imported. One for importing *Volunteer for* and one for importing *Employee of*.

If the Organisation does not already exist as an *Organisation* contact, then it will be created, with minimal details, as part of the importing of the *Individual* contact. The *Organisation* and *Individual* contacts contain a *Relationship* tab. From the *Relatonship* tab you observe who are the volumteers and employees, etc.


### Tags

The data exported from MailChimp had a *TAGS* column of data. Some individuals had many tags in their tag field, while other had none. At this stage no data from *TAGS* has been imported to a CiviCRM *Individual* contact. A Summary of the content of the TAGS is as follows, where *No.* is the number of individuals that were tagged with this tag:
```
No. TAG
  6 member-renewal-03-2024
 63 AGM 2023 Members
  2 member-renewal-06-June-2024
 17 member-renewal-10-october-2024
  4 member-renewal-12-December-2024
  1 member-renewal-postAGM-11-November-2024
  2 renewal-01-jan-2023
  4 committee
 12 renewal-02-feb-2023
  5 member-renewal-08-August-2024
  2 member-renewal-04-2024
 47 Carisbrook Walk 2024
 97 donor $20K community
 15 renewal-03-mar-2023
  3 renewal-08-aug-2023
  5 Donors
  1 member-renewal-06-June-2025
 69 agm-fin-member-31-oct-2022
  3 agm-sep-2022-lapsed-member-prod
  4 renewal-12-dec-2023
  8 renewal-12-dec-2022
 28 volunteer project
  6 supporter
167 member
 50 agm-jan-aug-2022-lapsed-member-prod
  2 member-renewal-05-May-2025
  5 member-renewal-05-may-2024
 76 donor
 38 AGM 2023 Lapsed Members
 72 friend
  7 volunteer project candidate
  5 renewal-05-may-2023
  2 member lapsed
  1 member-renewal-01-January-2025
105 VIPs Members current July 2023 donors $100+
  5 renewal-04-apr-2023
 12 member-renewal-03-March-2025
  1 renewal-01-jan-2024
 40 volunteer casual
 62 AGM 2024 Members
  7 gov rdv working group
  6 sponsor major
  1 member-renewal-07-July-2024
  4 renewal-09-2023
  4 member-renewal-09-september-2024
  1 VIP Reminder #2
  2 renewal-07-jul-2023
  2 volunteer resigned
 40 24 August 2023 Study Project Volunteers + Foundation Donors + Stakeholders
  3 agm-oct-2022-lapsed-member-prod
 32 council gov
 26 cycling affiliate
  5 renewal-06-jun-2023
 11 donor $20K foundation
  8 renewal-10-oct-2023
 68 members current July 2023
  7 member-renewal-02-2024
  3 member-renewal-02-February-2025
  2 member-renewal-preAGM-11-November-2024
 16 renewal-11-nov-2023
  9 renewal-11-nov-2022
 57 Member 2024
 62 Fin Members AGM 2022 Reminder
  2 VIP Reminder

Total Number of records:          408
Number of records with no tags:    78
Number records with tags:         330
Total Number of tags in records: 1432
```

Please review this *TAGS* data and decide if it is of any use in CiviCRM and therefore needs to be imported or not.



