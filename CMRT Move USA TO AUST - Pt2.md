# Move USA TO AUST Part 2

## Resolving Errors

After the AUST application uses the USA Database, the *System Status reports:

```
Extension Errors
There are 21 extension errors:

    "Aegir Backups" (aegirbackups) is installed but missing files.
    "CiviCRM Export to Excel" (ca.bidon.civiexportexcel) is installed but missing files.
    "CiviCRM Log Viewer" (ca.civicrm.logviewer) is installed but missing files.
    "TSYS" (com.aghstrategies.tsys) is installed but missing files.
    "Stripe" (com.drastikbydesign.stripe) is installed but missing files.
    "Easy Copy" (easycopy) is installed but missing files.
    "Prevent users from overwriting their record" (eu.tttp.noverwrite) is installed but missing files.
    "Firewall" (firewall) is installed but missing files.
    "Fix Option Translations" (fixoptiontranslations) is installed but missing files.
    "Language switcher" (kamlanguage) is installed but missing files.
    "Login Security" (loginsecurity) is installed but missing files.
    "MJWShared" (mjwshared) is installed but missing files.
    "FIXME" (org.civicrm.mycivi) is installed but missing files.
    "CiviTutorial" (org.civicrm.tutorial) is installed but missing files.
    "reply_to" (reply_to) is installed but missing files.
    "SparkPost integration" (sparkpost) is installed but missing files.
    "Standalone Migrate" (standalonemigrate) is installed but missing files.
    "Sweet Alert" (sweetalert) is installed but missing files.
    "Coop SymbioTIC" (symbiotic) is installed but missing files.
    "The Island Theme" (theisland) is installed but missing files.
    "General Data Protection Regulation" (uk.co.vedaconsulting.gdpr) is installed but missing files.

To resolve any errors, go to Manage Extensions.
```

Gemini AI states that 11 of the above are Spark extensions and are no longer used. The recommendation is to set these Spark exctensions to be in-active:

```
MariaDB [cmrailtr_civicrm]> UPDATE civicrm_extension 
    -> SET is_active = 0 
    -> WHERE full_name IN (
    ->   'org.civicrm.mycivi',
    ->   'aegirbackups',
    ->   'symbiotic',
    ->   'org.civicrm.tutorial',
    ->   'com.drastikbydesign.stripe',
    ->   'mjwshared',
    ->   'com.aghstrategies.tsys',
    ->   'firewall',
    ->   'ca.bidon.civiexportexcel',
    ->   'sweetalert',
    ->   'sparkpost'
    -> );
Query OK, 11 rows affected (0.003 sec)
Rows matched: 11  Changed: 11  Warnings: 0

MariaDB [cmrailtr_civicrm]> SELECT id, type, full_name, name, file, is_active FROM civicrm_extension;
+----+--------+------------------------------+---------------------------------------------+---------------------------+-----------+
| id | type   | full_name                    | name                                        | file                      | is_active |
+----+--------+------------------------------+---------------------------------------------+---------------------------+-----------+
|  2 | module | org.civicrm.flexmailer       | FlexMailer                                  | flexmailer                |         1 |
|  4 | module | uk.co.vedaconsulting.mosaico | Mosaico                                     | mosaico                   |         1 |
|  5 | module | org.civicrm.mycivi           | FIXME                                       | mycivi                    |         0 |
|  6 | module | com.drastikbydesign.stripe   | Stripe                                      | stripe                    |         0 |
|  7 | module | com.iatspayments.civicrm     | iATS Payments                               | iats                      |         0 |
|  8 | module | mjwshared                    | MJWShared                                   | mjwshared                 |         0 |
|  9 | module | aegirbackups                 | Aegir Backups                               | aegirbackups              |         0 |
| 10 | module | com.aghstrategies.tsys       | TSYS                                        | tsys                      |         0 |
| 11 | module | firewall                     | Firewall                                    | firewall                  |         0 |
| 12 | module | sequentialcreditnotes        | Sequential credit notes                     | sequentialcreditnotes     |         1 |
| 13 | module | org.civicrm.tutorial         | CiviTutorial                                | tutorial                  |         0 |
| 15 | module | financialacls                | financialacls                               | financialacls             |         0 |
| 16 | module | ca.bidon.civiexportexcel     | CiviCRM Export to Excel                     | civiexportexcel           |         0 |
| 17 | module | greenwich                    | Theme: Greenwich                            | greenwich                 |         1 |
| 18 | module | contributioncancelactions    | contributioncancelactions                   | contributioncancelactions |         1 |
| 19 | module | symbiotic                    | Coop SymbioTIC                              | symbiotic                 |         0 |
| 20 | module | recaptcha                    | reCAPTCHA                                   | recaptcha                 |         1 |
| 21 | module | ckeditor4                    | CKEditor4                                   | ckeditor4                 |         1 |
| 22 | module | legacycustomsearches         | Custom search framework                     | legacycustomsearches      |         1 |
| 23 | module | sweetalert                   | Sweet Alert                                 | sweetalert                |         0 |
| 24 | module | org.civicrm.afform           | Afform: Core Runtime                        | afform                    |         1 |
| 25 | module | org.civicrm.afform-html      | Afform: HTML                                | afform_html               |         1 |
| 26 | module | org.civicrm.afform_admin     | Afform: Form Builder                        | afform_admin              |         1 |
| 27 | module | org.civicrm.search_kit       | Search Kit                                  | search_kit                |         1 |
| 28 | module | sparkpost                    | SparkPost integration                       | sparkpost                 |         0 |
| 29 | module | kamlanguage                  | Language switcher                           | kamlanguage               |         1 |
| 30 | module | civigrant                    | CiviGrant                                   | civigrant                 |         0 |
| 31 | module | uk.co.vedaconsulting.gdpr    | General Data Protection Regulation          | gdpr                      |         1 |
| 32 | module | authx                        | AuthX                                       | authx                     |         1 |
| 33 | module | ca.civicrm.logviewer         | CiviCRM Log Viewer                          | logviewer                 |         1 |
| 34 | module | easycopy                     | Easy Copy                                   | easycopy                  |         1 |
| 35 | module | eu.tttp.noverwrite           | Prevent users from overwriting their record | noverwrite                |         1 |
| 36 | module | civi_event                   | CiviEvent                                   | civi_event                |         1 |
| 37 | module | civi_contribute              | CiviContribute                              | civi_contribute           |         1 |
| 38 | module | civi_member                  | CiviMember                                  | civi_member               |         1 |
| 39 | module | civi_mail                    | CiviMail                                    | civi_mail                 |         1 |
| 40 | module | civi_case                    | CiviCase                                    | civi_case                 |         1 |
| 41 | module | civi_report                  | CiviReport                                  | civi_report               |         1 |
| 42 | module | theisland                    | The Island Theme                            | theisland                 |         1 |
| 43 | module | loginsecurity                | Login Security                              | loginsecurity             |         1 |
| 45 | module | iframe                       | IFrame Connector                            | iframe                    |         1 |
| 46 | module | legacydedupefinder           | legacydedupefinder                          | legacydedupefinder        |         1 |
| 47 | module | civiimport                   | Civi-Import                                 | civiimport                |         1 |
| 48 | module | riverlea                     | RiverLea CiviCRM Theme Framework            | riverlea                  |         1 |
| 49 | module | reply_to                     | reply_to                                    | reply_to                  |         1 |
| 50 | module | fixoptiontranslations        | Fix Option Translations                     | fixoptiontranslations     |         1 |
| 51 | module | civi_pledge                  | CiviPledge                                  | civi_pledge               |         1 |
| 52 | module | civi_campaign                | CiviCampaign                                | civi_campaign             |         1 |
| 53 | module | message_admin                | Message Administration                      | message_admin             |         1 |
| 54 | module | standalonemigrate            | Standalone Migrate                          | standalonemigrate         |         1 |
| 55 | module | standaloneusers              | CiviCRM Standalone Users                    | standaloneusers           |         1 |
+----+--------+------------------------------+---------------------------------------------+---------------------------+-----------+
51 rows in set (0.000 sec)

```
However this does no stop the errors being reported. Even after $ cv flush. Thus, using the *Administer --> System Settings --> Extensions* they are de-installed.

After removing 11 error messages no longer appear.
Continue removing:  
* Sparkpost >  sparkpost
* sweetaler >   'sweetalert'
* symbiotic  ->   'symbiotic',
* CiviCRM Export to Excel (ca.bidon.civiexportexcel)
* financialacls <-- was set to inactive already? No in the SQL command
* CiviTutorial (org.civicrm.tutorial)   ->   'org.civicrm.tutorial',
* Firewall (firewall  >    'firewall
* TSYS (com.aghstrategies.tsys)     ->   'com.aghstrategies.tsys
* Aegir Backups (aegirbackups)"     ->   'aegirbackups',
* Payment Shared (mjwshared)     ->   'mjwshared', "
* "iATS Payments (com.iatspayments.civicrm)" 
* com.drastikbydesign.stripe   ->   'com.drastikbydesign.stripe',
* FIXME (org.civicrm.mycivi)"     ->   'org.civicrm.mycivi',
* 


After Removing the Spark releated extension:
```
There are 10 extension errors:

    "CiviCRM Log Viewer" (ca.civicrm.logviewer) is installed but missing files.
    "Easy Copy" (easycopy) is installed but missing files.
    "Prevent users from overwriting their record" (eu.tttp.noverwrite) is installed but missing files.
    "Fix Option Translations" (fixoptiontranslations) is installed but missing files.
    "Language switcher" (kamlanguage) is installed but missing files.
    "Login Security" (loginsecurity) is installed but missing files.
    "reply_to" (reply_to) is installed but missing files.
    "Standalone Migrate" (standalonemigrate) is installed but missing files.
    "The Island Theme" (theisland) is installed but missing files.
    "General Data Protection Regulation" (uk.co.vedaconsulting.gdpr) is installed but missing files.

To resolve any errors, go to Manage Extensions.
```

After uninstalling the Spark extensions:
```
MariaDB [cmrailtr_civicrm]> SELECT id, type, full_name, name, file, is_active FROM civicrm_extension;
+----+--------+------------------------------+---------------------------------------------+---------------------------+-----------+
| id | type   | full_name                    | name                                        | file                      | is_active |
+----+--------+------------------------------+---------------------------------------------+---------------------------+-----------+
|  2 | module | org.civicrm.flexmailer       | FlexMailer                                  | flexmailer                |         1 |
|  4 | module | uk.co.vedaconsulting.mosaico | Mosaico                                     | mosaico                   |         1 |
| 12 | module | sequentialcreditnotes        | Sequential credit notes                     | sequentialcreditnotes     |         1 |
| 17 | module | greenwich                    | Theme: Greenwich                            | greenwich                 |         1 |
| 18 | module | contributioncancelactions    | contributioncancelactions                   | contributioncancelactions |         1 |
| 20 | module | recaptcha                    | reCAPTCHA                                   | recaptcha                 |         1 |
| 21 | module | ckeditor4                    | CKEditor4                                   | ckeditor4                 |         1 |
| 22 | module | legacycustomsearches         | Custom search framework                     | legacycustomsearches      |         1 |
| 24 | module | org.civicrm.afform           | Afform: Core Runtime                        | afform                    |         1 |
| 25 | module | org.civicrm.afform-html      | Afform: HTML                                | afform_html               |         1 |
| 26 | module | org.civicrm.afform_admin     | Afform: Form Builder                        | afform_admin              |         1 |
| 27 | module | org.civicrm.search_kit       | Search Kit                                  | search_kit                |         1 |
| 29 | module | kamlanguage                  | Language switcher                           | kamlanguage               |         1 |
| 30 | module | civigrant                    | CiviGrant                                   | civigrant                 |         0 |
| 31 | module | uk.co.vedaconsulting.gdpr    | General Data Protection Regulation          | gdpr                      |         1 |
| 32 | module | authx                        | AuthX                                       | authx                     |         1 |
| 33 | module | ca.civicrm.logviewer         | CiviCRM Log Viewer                          | logviewer                 |         1 |
| 34 | module | easycopy                     | Easy Copy                                   | easycopy                  |         1 |
| 35 | module | eu.tttp.noverwrite           | Prevent users from overwriting their record | noverwrite                |         1 |
| 36 | module | civi_event                   | CiviEvent                                   | civi_event                |         1 |
| 37 | module | civi_contribute              | CiviContribute                              | civi_contribute           |         1 |
| 38 | module | civi_member                  | CiviMember                                  | civi_member               |         1 |
| 39 | module | civi_mail                    | CiviMail                                    | civi_mail                 |         1 |
| 40 | module | civi_case                    | CiviCase                                    | civi_case                 |         1 |
| 41 | module | civi_report                  | CiviReport                                  | civi_report               |         1 |
| 42 | module | theisland                    | The Island Theme                            | theisland                 |         1 |
| 43 | module | loginsecurity                | Login Security                              | loginsecurity             |         1 |
| 45 | module | iframe                       | IFrame Connector                            | iframe                    |         1 |
| 46 | module | legacydedupefinder           | legacydedupefinder                          | legacydedupefinder        |         1 |
| 47 | module | civiimport                   | Civi-Import                                 | civiimport                |         1 |
| 48 | module | riverlea                     | RiverLea CiviCRM Theme Framework            | riverlea                  |         1 |
| 49 | module | reply_to                     | reply_to                                    | reply_to                  |         1 |
| 50 | module | fixoptiontranslations        | Fix Option Translations                     | fixoptiontranslations     |         1 |
| 51 | module | civi_pledge                  | CiviPledge                                  | civi_pledge               |         1 |
| 52 | module | civi_campaign                | CiviCampaign                                | civi_campaign             |         1 |
| 53 | module | message_admin                | Message Administration                      | message_admin             |         1 |
| 54 | module | standalonemigrate            | Standalone Migrate                          | standalonemigrate         |         1 |
| 55 | module | standaloneusers              | CiviCRM Standalone Users                    | standaloneusers           |         1 |
+----+--------+------------------------------+---------------------------------------------+---------------------------+-----------+
38 rows in set (0.000 sec)

```
## Alternate Gemini Query

After transfering database from Spark Essentials civicrm 6.17.2 to a system with Standalone CivicRM 6.17.2 why do I get the following errors There are 21 extension errors:


### Response 

These errors occur because you copied the database schema and records, but not the physical extension files.

In CiviCRM, an extension's status is tracked in the civicrm_extension database table. Spark Essentials comes pre-loaded with a customized suite of extensions (such as aegirbackups, standalonemigrate, theisland, and mjwshared). Because your new Standalone CiviCRM environment has the database records telling it these extensions should be active, but lacks the corresponding PHP code directories on the filesystem, CiviCRM flags them as "installed but missing files".

Additionally, hosting-specific tools (like aegirbackups) should not exist in your Standalone environment.

### Step 1: Remove Spark-Specific & Unneeded Extensions from the Database

Extensions specific to the Spark infrastructure (Aegir, Standalone Migrate, etc.) are unnecessary and should be completely disabled/uninstalled directly in the database.

Run this SQL query against your new CiviCRM database to deactivate and remove them:
```
SQL

DELETE FROM civicrm_extension 
WHERE full_name IN (
  'aegirbackups',
  'standalonemigrate',
  'symbiotic',
  'theisland',
  'org.civicrm.mycivi'
);
```
Verification: Check the database with `SELECT full_name, is_active FROM civicrm_extension;` to confirm these entries no longer appear.

### Step 2: Decide on the Remaining Extensions

For the remaining extensions (e.g., Stripe, ca.bidon.civiexportexcel, sparkpost, uk.co.vedaconsulting.gdpr), choose one of two options:

Option A: If you need them (Re-download the files)

    Go to Administer > System Settings > Extensions (or use the CLI tool cv).

    Download or git clone the compatible releases for your version directly into your Standalone extensions directory (<civicrm_root>/ext/ or your configured extensionsDir).

    Ensure web server permissions (chown -R www-data:www-data ext/ or equivalent) are set properly.

Option B: If you do not need them (Disable/Remove them)

If you do not plan to use them, remove them from the database:
```
SQL

DELETE FROM civicrm_extension 
WHERE full_name IN (
  'ca.bidon.civiexportexcel',
  'ca.civicrm.logviewer',
  'com.aghstrategies.tsys',
  'com.drastikbydesign.stripe',
  'easycopy',
  'eu.tttp.noverwrite',
  'firewall',
  'fixoptiontranslations',
  'kamlanguage',
  'loginsecurity',
  'mjwshared',
  'org.civicrm.tutorial',
  'reply_to',
  'sparkpost',
  'sweetalert',
  'uk.co.vedaconsulting.gdpr'
);
```

### Step 3: Clear CiviCRM Caches and Triggers

After modifying the civicrm_extension table, flush CiviCRM's metadata caches to clear the alerts:

Using cv (CLI):

```
    Bash

    cv flush
```

Verification: Navigate to Administer > System Settings > Extensions. The 21 missing file warnings should be gone.
