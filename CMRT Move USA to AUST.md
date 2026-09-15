# Moving CiviCRM from the USA system to the VentraIP sub-domain

2026-09-15

## Introduction

In 2026 the *Spark*/*civicrm.org* organization hosted the CMRT CiviCRM on systems in USA. They used the CiviCRM for Drupal platform. In September they changed the platform to CiviCRM Standalone. 

For many years *VentraIP* organization in Australia has provided the hosting for the CMRT Wordpress website with the domain *cmrailtrail.org.au*. A sub-domain, *crm.cmrailtrail.org.au*, has been created to host the CiviCRM Standalone for CMRT. CiviCRM Standalone was installed on the VentraIP system and tested.

This document describes the process of moving CiviCRM data from the USA system to the VentraIP system. The data on the USA is backed-up using the *Administer --> Backups* utility. The cmrailtrail.civicrm.org-20260915002449.tar file was downloaded to a local PC and expanded. The top two levels of the directory tree are:

```
ian@hp:~/civicrm_2026-09-15$ tree -L 2
.
├── database.sql <-- renamed database_2026-09-15.sql
├── drushrc.php
├── files
│   ├── adminimal-custom.css
│   ├── advagg_css
│   ├── advagg_js
│   ├── civicrm
│   ├── css
│   ├── ctools
│   ├── deployment
│   ├── feeds
│   ├── imagecache
│   ├── images
│   ├── js
│   ├── locations
│   ├── logo_lg.png
│   ├── pictures
│   ├── styles
│   ├── tmp
│   └── xmlsitemap
├── nginx-custom.conf
└── upload
    ├── custom
    ├── ext
    ├── persist
    └── upload
```

The *database.sql* file of 13MB was SCPed to the VentraIP system. The VentraIP sytstem contained the databases:

```
[cmrailtr@s03dd ~]$ mysql --defaults-file=/home/cmrailtr/.my_civi.cnf --execute='SHOW DATABASES;'
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civi      | <--- civicrm strandalone - AUST testing
| cmrailtr_czhn1     | <--- wo0rdpress website
| information_schema |
+--------------------+
```

A new database was created.

```
mysql> CREATE DATABASE cmrailtr_civicrm CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```
So the following databases now exist:

```
MariaDB [(none)]> show DATABASES;
+--------------------+
| Database           |
+--------------------+
| cmrailtr_civi      |
| cmrailtr_civicrm   | <--- New database for CiviCRM USA
| cmrailtr_czhn1     |
| information_schema |
+--------------------+
```
The data from USA was uploaded to the new database:

```
mysql -u cmrailtr_czhn1 -p cmrailtr_civicrm < database_2026-09-15.sql
```

At this stage the AUST testing CiviCRM Standalone database, *cmrailtr_civi*, could be compared with the USA database, *cmrailtr_civicrm*.

## Database Comparison

The AUST CiviCRM database contains 164 tables. These tables are all included in the USA CiviCRM database. However the USA database contains a total of 191 tables. i.e. There are an additional 27 tables, as follows:

```
civicrm_cxn
civicrm_firewall_ipaddress
civicrm_iats_faps_journal
civicrm_iats_journal
civicrm_iats_request_log
civicrm_iats_response_log
civicrm_iats_ukdd_validate
civicrm_iats_verify
civicrm_login_security_device
civicrm_mailing_event_forward
civicrm_mosaico_msg_template
civicrm_paymentprocessor_webhook
civicrm_stripe_customers
civicrm_stripe_paymentintent
civicrm_stripe_plans
civicrm_stripe_subscriptions
civicrm_value_cmrt_voluntee_11
civicrm_value_contribution_page_terms_and_conditions_7
civicrm_value_contribution_terms_and_conditions_acceptan_8
civicrm_value_event_terms_and_conditions_7
civicrm_value_event_terms_and_conditions_acceptance_9
civicrm_value_individual_in_8
civicrm_value_member_engage_9
civicrm_value_member_involv_10
civicrm_value_organization__7
civicrm_value_payment_detai_6
civicrm_value_sla_acceptance_4

```

Some of these additional tables are easily explained by the fact that additional functionality had been invoked on the USA CiviCRM. Namely: Memberships, Mailing, Strip payment system. Other tables may be related to the USA platform. E.g. `civicrm_firewall_ipaddress` and `civicrm_login_security_device`.


