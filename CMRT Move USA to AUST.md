# Moving CiviCRM from the USA system to the VentraIP sub-domain

2026-09-15

## Introduction

In 2026 the *Spark*/*civicrm.org* organization hosted the CMRT CiviCRM on systems in USA. They used the CiviCRM for Drupal platform. In September they changed the platform to CiviCRM Standalone. 

For many years *VentraIP* organization in Australia has provided the hosting for the CMRT Wordpress website with the domain *cmrailtrail.org.au*. A sub-domain, *crm.cmrailtrail.org.au*, has been created to host the CiviCRM Standalone for CMRT. CiviCRM Standalone was installed on the VentraIP system and tested.

The USA CiviCRM was at version 6.17.2. The AUST CiviCRM was upgraded to also be at version 6.17.2

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

Some of these additional tables are easily explained by the fact that additional CRM functionality had been invoked on the USA CiviCRM. Namely: Memberships, Mailing, Strip payment system. Other tables may be related specifically to the USA platform. E.g. `civicrm_firewall_ipaddress` and `civicrm_login_security_device`.

## Defining of the Database

### Database Connection in CiviCRM Standalone

CiviCRM Standalone determines its database connection through specific configuration settings.

#### Configuration File

The database connection details are stored in the file private/civicrm.settings.php. This file is generated during the installation process of CiviCRM Standalone.

#### Editing Database Settings

If necessary, users can manually edit the civicrm.settings.php file to update the database connection settings. This allows for flexibility in managing the database connection, especially if the database location or credentials change after installation.

```
[cmrailtr@s03dd civicrm-standalone]$ ls -l private
-rw-r--r-- 1 cmrailtr cmrailtr 26072 May 16 21:05 civicrm.settings.php

```

By editing this configuration file, CiviCRM Standalone can effectively connect to the designated database, ensuring that all data operations function correctly.
The database that CiviCRM Standalone uses is defined at line 129 of *civicrm-standalone/private/civicrm.settings.php*:
```
    define('CIVICRM_DSN', 'mysql://cmrailtr_czhn1:W.---password---40@127.0.0.1:3306/cmrailtr_civi?new_link=true');
```
To change from *cmrailtr_civi* to *cmrailtr_civicrm* the command would be edited to be:
```
    define('CIVICRM_DSN', 'mysql://cmrailtr_czhn1:W.---password---40@127.0.0.1:3306/cmrailtr_civicrm?new_link=true');
```

## Uploads Directory

The USA CiviCRM backup includes a directory named *uploads*. This includes the directories:

```
ian@hp:~/civicrm_2026-09-15/upload$ ls
custom  ext  persist  upload
```

The *custom* and *ext* directories contain no files. The *upload* directory contains: *version-msgs-cache.json* which is an html message on the latest civiCRM upgrades available.

```
ian@hp:~/civicrm_2026-09-15/upload$ tree custom
custom
├── CiviMail.ignored
│   └── 2026
│       └── 05
│           └── 22
│               ├── cur
│               ├── new
│               └── tmp
└── CiviMail.processed
    └── 2026
        └── 05
            └── 22
                ├── cur
                ├── new
                └── tmp

15 directories, 0 files
ian@hp:~/civicrm_2026-09-15/upload$ tree ext
ext

0 directories, 0 files
ian@hp:~/civicrm_2026-09-15/upload$ tree upload
upload
└── version-msgs-cache.json
```

The *persist* directory appears to contain all the files related to bulk mails that have been created.

```
ian@hp:~/civicrm_2026-09-15/upload$ tree persist
persist
├── contribute
│   ├── dyn
│   │   └── index.html
│   ├── images
│   │   ├── image-20260128085555-1.png
│   │   ├── index.html
│   │   └── uploads
│   │       ├── 1024x576_owharoa_falls_3688bf0ca52cf68184beee1f4e1f911b.jpg
│   │       ├── 1024x576_owharoa_falls_af4b57c75d7e311df277170f14535721.jpg
│   │       ├── 1024x576_owharoa_falls_c2603e9f4dc047eb150d86ed92a5454a.jpg
│   │       ├── 2025_01_21_e51438c4fcf7713c334783febe21955a.jpg
│   │       ├── Adventures_Kate_03_cropped_00ed020e9a5e91df750415ec840964b6.jpg
│   │       ├── Adventures_Kate_03_jpg_2e8de4d19afa900a0d6488f5372ad084.jpg
│   │       ├── Adventures_Kate_03_jpg_e8cb3ccf844fc12a3642de9f69901730.jpg
│   │       ├── Blue_Pyrenees_Estate_5eaa87056ad9fd0741dda0ce7f6bb543.jpeg
│   │       ├── Cairn_Curran_Bridge_2_5f6658d7478ae64f7f2b29bc1ddcd05b.jpg
│   │       ├── Cairn_Curran_Bridge_Edit_07cff7d921eb2adc1aaa4f0b863debf9.jpg
│   │       ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_1l_892b5b2777e8657d3bdeb949153a9da8.jpg
│   │       ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_59f0ef64f47eec451fdde561c271d11d.jpg
│   │       ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_97186b08c2a7c599857a7233ec582696.jpg
│   │       ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_b552e01ba5be077e086d38d6efad3438.jpg
│   │       ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_e120b512e1423cc41a9563b23d3020e3.jpg
│   │       ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_c2cdb468fe17f94744b62e7b59993133.jpg
│   │       ├── Cairn_Curran_Bridge_with_Fog_45aacedc029e6b9ac48f6be6495298a7.jpg
│   │       ├── Chewton_streetscape_768x576_539295d2e15cadd4b2885a6f4693f589.jpg
│   │       ├── Chewton_streetscape_768x576_82ee92d60175362de4a23e5df682b6ff.jpg
│   │       ├── Chewton_streetscape_768x576_da3c0ff04225badb1bd9b3bdc1e366fe.jpg
│   │       ├── CiviCRM_logo_2019_F2_200px_e29d80a3ace77856909805ef5f75a3d5.png
│   │       ├── cmrt_600_x_50_018a197c71b5641115a229b9f88c58bb.png
│   │       ├── cmrt_600_x_50_23c4b15cecfef17e9eca478b54e68feb.png
│   │       ├── cmrt_600_x_50_57653862dfe422300853bc827abdfecb.png
│   │       ├── cmrt_600_x_50_71f3c4101d6a9ba26fb352e2c8028f12.png
│   │       ├── cmrt_600_x_50_84cff001c3dc6c26ac751a8a0b2cd0a1.png
│   │       ├── cmrt_600_x_50_9827288d9f62758c875bef43113218bb.png
│   │       ├── cmrt_600_x_50_no_inc_74ba12dc88efc78c05da7b87e7c63dfa.png
│   │       ├── cmrt_600_x_80_db15a5db5b94a25314b893b0f0aa5201.png
│   │       ├── CMRT_7_People_1500px_Green_plus_big_title_2187f3675231c7a601b91e72b21bd16c.png
│   │       ├── CMRT_7_People_1500px_Green_plus_big_title_a51ea899e02fae5eba1cae604ddad85b.png
│   │       ├── CMRT_7_People_1500px_Green_plus_title_9fbd4a882c018608c276a24c2d39e8f6.png
│   │       ├── CMRT_7_People_1500px_Green_plus_title_afae35050034cee0dd75a139f2c8eafb.png
│   │       ├── CMRT_7_People_1500px_Green_plus_title_daff4f3c53b7389364989f78d31632fc.png
│   │       ├── cmrt_logo_49_x_49_65a6862f4436348be0709ac0288b502b.png
│   │       ├── cmrt_logo_512dade5de5ff26bfb4f357f4aa93635.png
│   │       ├── cmrt_logo_535_x_150_15a920dd94b30ae861443216a658f5cf.png
│   │       ├── cmrt_logo_535_x_150_9b07c94b9f8257a789e359d876f5da94.png
│   │       ├── cmrt_logo_535_x_150_v2_65b6892117bfe27e904de0b4931a3e3b.png
│   │       ├── cmrt_logo_535_x_150_v2_ae9acaefdc6aea7679500a3085c1c452.png
│   │       ├── cmrt_logo_535_x_150_v2_d0b3a59e64a8e060650efb0804e2f3fb.png
│   │       ├── cmrt_logo_535_x_150_v2_df197f719a67d42948229010aa7733bc.png
│   │       ├── cmrt_logo_7a4f8b57a55f58b0c92d2ea758e076a3.png
│   │       ├── CMRT_Logo_a5b63adceeec0feb3afac53ea27242f0.png
│   │       ├── cmrt_logo_c05822e98b7f5b458e3ddd8eb1039f20.png
│   │       ├── cmrt_logo_c2745b943d6809285c335ece36edd840.png
│   │       ├── CMRT_Logo_cc0d4d481145f986ae423954310a376f.png
│   │       ├── Design_1140_x_340_this_one_22cef6b0998bf51010fcca4e89901422.png
│   │       ├── Dunkeld_0cc1ae07a41d20f48cc0b9c34b5692f3.jpeg
│   │       ├── giant_anytour_e_plus_ea3d3a488217b5bcc47e68e1dd1c04aa.png
│   │       ├── giant_anytour_e_plus_f5253b76d7524c21a198711d14d1f1c4.png
│   │       ├── Janice_cropped_1_b07b0f362ccb7cd29b77f41341059277.jpg
│   │       ├── Janice_cropped_2_778f23105b594f52ba611535997bb6a7.jpg
│   │       ├── Janice_cropped_2_890c3d4915098dac629fbb1e9adba543.jpg
│   │       ├── Janice_cropped_a93222ff0d088e15014f97c7135c92fb.jpg
│   │       ├── letterhead_image_v9_2_graphic_strip_1327cae39584e16806699ce33a71d518.png
│   │       ├── letterhead_image_v9_2_graphic_strip_9b4b96d2b420694278c29757de232c98.png
│   │       ├── Loddon_River_Bridge_Guildford_8c9d6ea96eaaae5f008d7bc9fb2a6aed.jpg
│   │       ├── logo_120x120_d50d3944da01d2a8b5d2fbff73bb57d4.png
│   │       ├── logo_circle_139_x_139_text_219165da2ac49eab837c82f8d2dea07e.png
│   │       ├── logo_circle_139_x_139_text_366802f63c399add31256d9dfaa697f3.png
│   │       ├── logo_circle_4_lines_no_inc_abece4f7263cfd2ec20339f41d195093.png
│   │       ├── logo_circle_5d5c46666ef027ddfef2801e6a110a82.png
│   │       ├── logo_circle_cf7c00bb743110a0bdacd34b1fb4a74e.png
│   │       ├── newsletter_7_person_9e3da7e4d935aebfca3f4cfa96a59b0b.png
│   │       ├── PXL_20230823_231824378_1_3948c8fcc5921c71ba015c5d215d0c00.jpg
│   │       ├── PXL_20230926_013048514_1_Cropped_385e7b683f1c7f574c23f6fc3d09a420.jpg
│   │       ├── PXL_20230926_013048514_1_Cropped_d29d530d141202ac44a2ad9fdfffec78.jpg
│   │       ├── PXL_20230926_013048514_Scaled_43240d082592c43b0aa9fa8c3cd363e4.jpg
│   │       ├── Royal_Mail_Hotel_39571012c24629dfb92e97d0b8fb1f70.jpg
│   │       ├── static
│   │       │   ├── 1024x576_owharoa_falls_3688bf0ca52cf68184beee1f4e1f911b.jpg
│   │       │   ├── 1024x576_owharoa_falls_af4b57c75d7e311df277170f14535721.jpg
│   │       │   ├── 1024x576_owharoa_falls_c2603e9f4dc047eb150d86ed92a5454a.jpg
│   │       │   ├── 2025_01_21_e51438c4fcf7713c334783febe21955a.jpg
│   │       │   ├── Adventures_Kate_03_cropped_00ed020e9a5e91df750415ec840964b6.jpg
│   │       │   ├── Adventures_Kate_03_jpg_2e8de4d19afa900a0d6488f5372ad084.jpg
│   │       │   ├── Blue_Pyrenees_Estate_5eaa87056ad9fd0741dda0ce7f6bb543.jpeg
│   │       │   ├── Cairn_Curran_Bridge_2_5f6658d7478ae64f7f2b29bc1ddcd05b.jpg
│   │       │   ├── Cairn_Curran_Bridge_Edit_07cff7d921eb2adc1aaa4f0b863debf9.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_1l_892b5b2777e8657d3bdeb949153a9da8.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_97186b08c2a7c599857a7233ec582696.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_b552e01ba5be077e086d38d6efad3438.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_e120b512e1423cc41a9563b23d3020e3.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_c2cdb468fe17f94744b62e7b59993133.jpg
│   │       │   ├── Cairn_Curran_Bridge_with_Fog_45aacedc029e6b9ac48f6be6495298a7.jpg
│   │       │   ├── Chewton_streetscape_768x576_82ee92d60175362de4a23e5df682b6ff.jpg
│   │       │   ├── Chewton_streetscape_768x576_da3c0ff04225badb1bd9b3bdc1e366fe.jpg
│   │       │   ├── CiviCRM_logo_2019_F2_200px_e29d80a3ace77856909805ef5f75a3d5.png
│   │       │   ├── cmrt_600_x_50_018a197c71b5641115a229b9f88c58bb.png
│   │       │   ├── cmrt_600_x_50_23c4b15cecfef17e9eca478b54e68feb.png
│   │       │   ├── cmrt_600_x_50_57653862dfe422300853bc827abdfecb.png
│   │       │   ├── cmrt_600_x_50_71f3c4101d6a9ba26fb352e2c8028f12.png
│   │       │   ├── cmrt_600_x_50_84cff001c3dc6c26ac751a8a0b2cd0a1.png
│   │       │   ├── cmrt_600_x_50_9827288d9f62758c875bef43113218bb.png
│   │       │   ├── cmrt_600_x_50_no_inc_74ba12dc88efc78c05da7b87e7c63dfa.png
│   │       │   ├── cmrt_600_x_80_db15a5db5b94a25314b893b0f0aa5201.png
│   │       │   ├── CMRT_7_People_1500px_Green_plus_big_title_2187f3675231c7a601b91e72b21bd16c.png
│   │       │   ├── CMRT_7_People_1500px_Green_plus_big_title_a51ea899e02fae5eba1cae604ddad85b.png
│   │       │   ├── CMRT_7_People_1500px_Green_plus_title_9fbd4a882c018608c276a24c2d39e8f6.png
│   │       │   ├── CMRT_7_People_1500px_Green_plus_title_afae35050034cee0dd75a139f2c8eafb.png
│   │       │   ├── CMRT_7_People_1500px_Green_plus_title_daff4f3c53b7389364989f78d31632fc.png
│   │       │   ├── cmrt_logo_49_x_49_65a6862f4436348be0709ac0288b502b.png
│   │       │   ├── cmrt_logo_512dade5de5ff26bfb4f357f4aa93635.png
│   │       │   ├── cmrt_logo_535_x_150_15a920dd94b30ae861443216a658f5cf.png
│   │       │   ├── cmrt_logo_535_x_150_9b07c94b9f8257a789e359d876f5da94.png
│   │       │   ├── cmrt_logo_535_x_150_v2_65b6892117bfe27e904de0b4931a3e3b.png
│   │       │   ├── cmrt_logo_535_x_150_v2_ae9acaefdc6aea7679500a3085c1c452.png
│   │       │   ├── cmrt_logo_535_x_150_v2_d0b3a59e64a8e060650efb0804e2f3fb.png
│   │       │   ├── cmrt_logo_535_x_150_v2_df197f719a67d42948229010aa7733bc.png
│   │       │   ├── cmrt_logo_7a4f8b57a55f58b0c92d2ea758e076a3.png
│   │       │   ├── CMRT_Logo_a5b63adceeec0feb3afac53ea27242f0.png
│   │       │   ├── cmrt_logo_c05822e98b7f5b458e3ddd8eb1039f20.png
│   │       │   ├── cmrt_logo_c2745b943d6809285c335ece36edd840.png
│   │       │   ├── CMRT_Logo_cc0d4d481145f986ae423954310a376f.png
│   │       │   ├── Design_1140_x_340_this_one_22cef6b0998bf51010fcca4e89901422.png
│   │       │   ├── Dunkeld_0cc1ae07a41d20f48cc0b9c34b5692f3.jpeg
│   │       │   ├── giant_anytour_e_plus_ea3d3a488217b5bcc47e68e1dd1c04aa.png
│   │       │   ├── giant_anytour_e_plus_f5253b76d7524c21a198711d14d1f1c4.png
│   │       │   ├── Janice_cropped_1_b07b0f362ccb7cd29b77f41341059277.jpg
│   │       │   ├── Janice_cropped_2_778f23105b594f52ba611535997bb6a7.jpg
│   │       │   ├── Janice_cropped_2_890c3d4915098dac629fbb1e9adba543.jpg
│   │       │   ├── Janice_cropped_a93222ff0d088e15014f97c7135c92fb.jpg
│   │       │   ├── letterhead_image_v9_2_graphic_strip_1327cae39584e16806699ce33a71d518.png
│   │       │   ├── letterhead_image_v9_2_graphic_strip_9b4b96d2b420694278c29757de232c98.png
│   │       │   ├── Loddon_River_Bridge_Guildford_8c9d6ea96eaaae5f008d7bc9fb2a6aed.jpg
│   │       │   ├── logo_120x120_d50d3944da01d2a8b5d2fbff73bb57d4.png
│   │       │   ├── logo_circle_139_x_139_text_219165da2ac49eab837c82f8d2dea07e.png
│   │       │   ├── logo_circle_139_x_139_text_366802f63c399add31256d9dfaa697f3.png
│   │       │   ├── logo_circle_4_lines_no_inc_abece4f7263cfd2ec20339f41d195093.png
│   │       │   ├── logo_circle_5d5c46666ef027ddfef2801e6a110a82.png
│   │       │   ├── logo_circle_cf7c00bb743110a0bdacd34b1fb4a74e.png
│   │       │   ├── newsletter_7_person_9e3da7e4d935aebfca3f4cfa96a59b0b.png
│   │       │   ├── PXL_20230823_231824378_1_3948c8fcc5921c71ba015c5d215d0c00.jpg
│   │       │   ├── PXL_20230926_013048514_1_Cropped_385e7b683f1c7f574c23f6fc3d09a420.jpg
│   │       │   ├── PXL_20230926_013048514_1_Cropped_d29d530d141202ac44a2ad9fdfffec78.jpg
│   │       │   ├── PXL_20230926_013048514_Scaled_43240d082592c43b0aa9fa8c3cd363e4.jpg
│   │       │   ├── Royal_Mail_Hotel_39571012c24629dfb92e97d0b8fb1f70.jpg
│   │       │   ├── Trail_communters_c9ccdc8cd5e1769650cb9e016d762c7c.png
│   │       │   ├── trail_commuters_8db4b1baf1930924f133ddf231bc608e.png
│   │       │   ├── Trail_commuters_d7725cf3fbca96094f8ea5bef503c529.png
│   │       │   ├── Trail_commuters_transparant_1790ce957688ef29864c0acbcd31b0aa.png
│   │       │   ├── trail_people_8bc0e8416e4a1ff8f64e6300b4cdbd6a.png
│   │       │   ├── Untitled_design_1_ecf01205825bf7cbeb5d696201480a29.png
│   │       │   ├── Untitled_design_b7ecb5d9b81cff1c247f748bebe19ffa.png
│   │       │   ├── Untitled_design_cropped_702aa8b02378a78c7f4adf32ef8e328a.png
│   │       │   ├── Untitled_design_f4d2dbf8fd7ca1606faef7308ff09ba6.png
│   │       │   ├── Wickens_Royal_Mail_Dunkeld_47a1db84edc469220beac932004fc035.jpg
│   │       │   └── Wickens_Royal_Mail_Dunkeld_ae67c8223990bd6e962817f22e7b09f3.jpg
│   │       ├── thumbnails
│   │       │   ├── 1024x576_owharoa_falls_3688bf0ca52cf68184beee1f4e1f911b.jpg
│   │       │   ├── 1024x576_owharoa_falls_af4b57c75d7e311df277170f14535721.jpg
│   │       │   ├── 1024x576_owharoa_falls_c2603e9f4dc047eb150d86ed92a5454a.jpg
│   │       │   ├── 2025_01_21_e51438c4fcf7713c334783febe21955a.jpg
│   │       │   ├── Adventures_Kate_03_cropped_00ed020e9a5e91df750415ec840964b6.jpg
│   │       │   ├── Adventures_Kate_03_jpg_2e8de4d19afa900a0d6488f5372ad084.jpg
│   │       │   ├── Adventures_Kate_03_jpg_e8cb3ccf844fc12a3642de9f69901730.jpg
│   │       │   ├── Blue_Pyrenees_Estate_5eaa87056ad9fd0741dda0ce7f6bb543.jpeg
│   │       │   ├── Cairn_Curran_Bridge_2_5f6658d7478ae64f7f2b29bc1ddcd05b.jpg
│   │       │   ├── Cairn_Curran_Bridge_Edit_07cff7d921eb2adc1aaa4f0b863debf9.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_1l_892b5b2777e8657d3bdeb949153a9da8.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_59f0ef64f47eec451fdde561c271d11d.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_97186b08c2a7c599857a7233ec582696.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_b552e01ba5be077e086d38d6efad3438.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_2_e120b512e1423cc41a9563b23d3020e3.jpg
│   │       │   ├── Cairn_Curran_Bridge_will_be_crossed_by_the_Rail_Trail_c2cdb468fe17f94744b62e7b59993133.jpg
│   │       │   ├── Cairn_Curran_Bridge_with_Fog_45aacedc029e6b9ac48f6be6495298a7.jpg
│   │       │   ├── Chewton_streetscape_768x576_539295d2e15cadd4b2885a6f4693f589.jpg
│   │       │   ├── Chewton_streetscape_768x576_82ee92d60175362de4a23e5df682b6ff.jpg
│   │       │   ├── Chewton_streetscape_768x576_da3c0ff04225badb1bd9b3bdc1e366fe.jpg
│   │       │   ├── CiviCRM_logo_2019_F2_200px_e29d80a3ace77856909805ef5f75a3d5.png
│   │       │   ├── cmrt_600_x_50_018a197c71b5641115a229b9f88c58bb.png
│   │       │   ├── cmrt_600_x_50_23c4b15cecfef17e9eca478b54e68feb.png
│   │       │   ├── cmrt_600_x_50_57653862dfe422300853bc827abdfecb.png
│   │       │   ├── cmrt_600_x_50_71f3c4101d6a9ba26fb352e2c8028f12.png
│   │       │   ├── cmrt_600_x_50_84cff001c3dc6c26ac751a8a0b2cd0a1.png
│   │       │   ├── cmrt_600_x_50_9827288d9f62758c875bef43113218bb.png
│   │       │   ├── cmrt_600_x_50_no_inc_74ba12dc88efc78c05da7b87e7c63dfa.png
│   │       │   ├── cmrt_600_x_80_db15a5db5b94a25314b893b0f0aa5201.png
│   │       │   ├── CMRT_7_People_1500px_Green_plus_big_title_2187f3675231c7a601b91e72b21bd16c.png
│   │       │   ├── CMRT_7_People_1500px_Green_plus_big_title_a51ea899e02fae5eba1cae604ddad85b.png
│   │       │   ├── CMRT_7_People_1500px_Green_plus_title_9fbd4a882c018608c276a24c2d39e8f6.png
│   │       │   ├── CMRT_7_People_1500px_Green_plus_title_afae35050034cee0dd75a139f2c8eafb.png
│   │       │   ├── CMRT_7_People_1500px_Green_plus_title_daff4f3c53b7389364989f78d31632fc.png
│   │       │   ├── cmrt_logo_49_x_49_65a6862f4436348be0709ac0288b502b.png
│   │       │   ├── cmrt_logo_512dade5de5ff26bfb4f357f4aa93635.png
│   │       │   ├── cmrt_logo_535_x_150_15a920dd94b30ae861443216a658f5cf.png
│   │       │   ├── cmrt_logo_535_x_150_9b07c94b9f8257a789e359d876f5da94.png
│   │       │   ├── cmrt_logo_535_x_150_v2_65b6892117bfe27e904de0b4931a3e3b.png
│   │       │   ├── cmrt_logo_535_x_150_v2_ae9acaefdc6aea7679500a3085c1c452.png
│   │       │   ├── cmrt_logo_535_x_150_v2_d0b3a59e64a8e060650efb0804e2f3fb.png
│   │       │   ├── cmrt_logo_535_x_150_v2_df197f719a67d42948229010aa7733bc.png
│   │       │   ├── cmrt_logo_7a4f8b57a55f58b0c92d2ea758e076a3.png
│   │       │   ├── CMRT_Logo_a5b63adceeec0feb3afac53ea27242f0.png
│   │       │   ├── cmrt_logo_c05822e98b7f5b458e3ddd8eb1039f20.png
│   │       │   ├── cmrt_logo_c2745b943d6809285c335ece36edd840.png
│   │       │   ├── CMRT_Logo_cc0d4d481145f986ae423954310a376f.png
│   │       │   ├── Design_1140_x_340_this_one_22cef6b0998bf51010fcca4e89901422.png
│   │       │   ├── Dunkeld_0cc1ae07a41d20f48cc0b9c34b5692f3.jpeg
│   │       │   ├── giant_anytour_e_plus_ea3d3a488217b5bcc47e68e1dd1c04aa.png
│   │       │   ├── giant_anytour_e_plus_f5253b76d7524c21a198711d14d1f1c4.png
│   │       │   ├── Janice_cropped_1_b07b0f362ccb7cd29b77f41341059277.jpg
│   │       │   ├── Janice_cropped_2_778f23105b594f52ba611535997bb6a7.jpg
│   │       │   ├── Janice_cropped_2_890c3d4915098dac629fbb1e9adba543.jpg
│   │       │   ├── Janice_cropped_a93222ff0d088e15014f97c7135c92fb.jpg
│   │       │   ├── letterhead_image_v9_2_graphic_strip_1327cae39584e16806699ce33a71d518.png
│   │       │   ├── letterhead_image_v9_2_graphic_strip_9b4b96d2b420694278c29757de232c98.png
│   │       │   ├── Loddon_River_Bridge_Guildford_8c9d6ea96eaaae5f008d7bc9fb2a6aed.jpg
│   │       │   ├── logo_120x120_d50d3944da01d2a8b5d2fbff73bb57d4.png
│   │       │   ├── logo_circle_139_x_139_text_219165da2ac49eab837c82f8d2dea07e.png
│   │       │   ├── logo_circle_139_x_139_text_366802f63c399add31256d9dfaa697f3.png
│   │       │   ├── logo_circle_4_lines_no_inc_abece4f7263cfd2ec20339f41d195093.png
│   │       │   ├── logo_circle_5d5c46666ef027ddfef2801e6a110a82.png
│   │       │   ├── logo_circle_cf7c00bb743110a0bdacd34b1fb4a74e.png
│   │       │   ├── newsletter_7_person_9e3da7e4d935aebfca3f4cfa96a59b0b.png
│   │       │   ├── PXL_20230823_231824378_1_3948c8fcc5921c71ba015c5d215d0c00.jpg
│   │       │   ├── PXL_20230926_013048514_1_Cropped_385e7b683f1c7f574c23f6fc3d09a420.jpg
│   │       │   ├── PXL_20230926_013048514_1_Cropped_d29d530d141202ac44a2ad9fdfffec78.jpg
│   │       │   ├── PXL_20230926_013048514_Scaled_43240d082592c43b0aa9fa8c3cd363e4.jpg
│   │       │   ├── Royal_Mail_Hotel_39571012c24629dfb92e97d0b8fb1f70.jpg
│   │       │   ├── Trail_communters_c9ccdc8cd5e1769650cb9e016d762c7c.png
│   │       │   ├── trail_commuters_8db4b1baf1930924f133ddf231bc608e.png
│   │       │   ├── Trail_commuters_d7725cf3fbca96094f8ea5bef503c529.png
│   │       │   ├── Trail_commuters_transparant_1790ce957688ef29864c0acbcd31b0aa.png
│   │       │   ├── trail_people_8bc0e8416e4a1ff8f64e6300b4cdbd6a.png
│   │       │   ├── Untitled_design_1_ecf01205825bf7cbeb5d696201480a29.png
│   │       │   ├── Untitled_design_9d8b9fc3193d70edd19707330c7d5a33.png
│   │       │   ├── Untitled_design_b7ecb5d9b81cff1c247f748bebe19ffa.png
│   │       │   ├── Untitled_design_cropped_702aa8b02378a78c7f4adf32ef8e328a.png
│   │       │   ├── Untitled_design_f4d2dbf8fd7ca1606faef7308ff09ba6.png
│   │       │   ├── Wickens_Royal_Mail_Dunkeld_47a1db84edc469220beac932004fc035.jpg
│   │       │   └── Wickens_Royal_Mail_Dunkeld_ae67c8223990bd6e962817f22e7b09f3.jpg
│   │       ├── Trail_communters_c9ccdc8cd5e1769650cb9e016d762c7c.png
│   │       ├── trail_commuters_8db4b1baf1930924f133ddf231bc608e.png
│   │       ├── Trail_commuters_d7725cf3fbca96094f8ea5bef503c529.png
│   │       ├── Trail_commuters_transparant_1790ce957688ef29864c0acbcd31b0aa.png
│   │       ├── trail_people_8bc0e8416e4a1ff8f64e6300b4cdbd6a.png
│   │       ├── Untitled_design_1_ecf01205825bf7cbeb5d696201480a29.png
│   │       ├── Untitled_design_9d8b9fc3193d70edd19707330c7d5a33.png
│   │       ├── Untitled_design_b7ecb5d9b81cff1c247f748bebe19ffa.png
│   │       ├── Untitled_design_cropped_702aa8b02378a78c7f4adf32ef8e328a.png
│   │       ├── Untitled_design_f4d2dbf8fd7ca1606faef7308ff09ba6.png
│   │       ├── Wickens_Royal_Mail_Dunkeld_47a1db84edc469220beac932004fc035.jpg
│   │       └── Wickens_Royal_Mail_Dunkeld_ae67c8223990bd6e962817f22e7b09f3.jpg
│   └── index.html
├── crm-ckeditor-default.js
└── index.html

7 directories, 248 files

```

The layout of files is different for the AUST CiviCRM. The root level has 5 directories:

```
drwxrwxr-x  2 cmrailtr cmrailtr  4096 Sep 15 09:55 cgi-bin
-rw-r--r--  1 cmrailtr cmrailtr  1160 May  7 08:21 civicrm.standalone.php
drwxr-xr-x 24 cmrailtr cmrailtr  4096 Aug  7 08:22 core
-rw-r--r--  1 cmrailtr cmrailtr 11549 May 27 15:51 error_log
drwxrwxr-x  3 cmrailtr cmrailtr  4096 Sep 15 09:55 ext
-rw-r--r--  1 cmrailtr cmrailtr  1039 May  7 08:21 index.php
drwxrwxr-x  7 cmrailtr cmrailtr  4096 Sep 15 10:00 private
drwxrwxr-x  4 cmrailtr cmrailtr  4096 Sep 15 09:55 public
```

The *core* directory contains the main files. A total of 2934 directories with 18508 files.

The *cgi-bin* directory is empty

```
[cmrailtr@s03dd civicrm-standalone]$ tree cgi-bin
cgi-bin

0 directories, 0 files
```

The *ext* directory has 125 directories, 959 files. These all seem to relate to *mosiaco* application.

```
[cmrailtr@s03dd civicrm-standalone]$ tree ext

ext
└── uk.co.vedaconsulting.mosaico

```

The *private* directory contains 819 directories, 29 files. Mostly cache and Australia language provision.

The *public* directory contains:

```
[cmrailtr@s03dd civicrm-standalone]$ tree public
public
├── index.html
├── media
│   ├── dyn
│   │   ├── angular-modules.0563dd785f1bed696b5969e11ee07f30.json
│   │   ├── angular-modules.53f8ee7ddb5928377c50b4bfa78f067f.js
│   │   ├── angular-modules.633cd3dd566cdb39081f608ba1ddf1dd.json
│   │   ├── angular-modules.9445c2782b648c6f8af93783d7a67d6c.js
│   │   ├── angular-modules.c017771e50151faa355ab64de29cd771.js
│   │   ├── angular-modules.ca95644dec6a6302fe9520734fc75d2b.json
│   │   ├── crm-l10n.40b4472a93eaf74a54bbce3fef6030be.js
│   │   ├── crm-l10n.44610ee8059629e129800ecf57f9f5bf.js
│   │   ├── crm-l10n.a87fb7fdde624ade29f76cca4ee8a19d.js
│   │   ├── crm-l10n.b42513f8e1e1eb7ffef4d3ecf294f960.js
│   │   ├── river.05618812cbb7a6b4fa0829c4c39aae72.css
│   │   ├── river.48c58b60d98aa875f757c9b8e526cc90.css
│   │   ├── river.7bb5fd9ea5d29df3e35393af5a65af10.css
│   │   └── river.fa654000bb3a02de4ea4331d38115ed2.css
│   ├── images
│   │   ├── index.html
│   │   └── uploads
│   │       ├── static
│   │       └── thumbnails
│   └── index.html
└── persist
    └── crm-ckeditor-default.js

7 directories, 18 files
```

The images for Mosaico are stored in */public/media/images/uploads/* *static* or *thumbnails*. E.g. image of Karen_Andrews has been added to a bulk mail.

```
[cmrailtr@s03dd civicrm-standalone]$ tree public/media/images
public/media/images
├── index.html
└── uploads
    ├── Karen_Andrews_de3f4b54a61fa63303361fab6feecbd0.jpeg
    ├── static
    │   └── Karen_Andrews_de3f4b54a61fa63303361fab6feecbd0.jpeg
    └── thumbnails
        └── Karen_Andrews_de3f4b54a61fa63303361fab6feecbd0.jpeg

```
