# Setup of the Campaign Manager Role

## Introduction

CiviCRM Standalone defaults to providing the account roles: *Admin*, *Staff* and *Everyone*. To display the screen of these Roles, click on...

Administer -> Users and Permissions -> User Roles

If an additional role has been created then it will also be displayed. This document describes the addition of the *Campaign Manager* role.

When creating the *Campaign Manager* role it consists only these two permissins:
* CiviCampaign: administer CiviCampaign
* CiviCampaign: manage campaign

A person who is allocated the *Campaign Manager* role also is given the *Staff* role. The permissions of the *Staff* role are:
n

In CiviCRM Standalone (which relies entirely on CiviCRM's native permissions and ACL engine rather than a CMS like Drupal or WordPress), assigning a set of permissions to a group of contacts like a "Staff" list involves a precise chain of connections.

To accomplish this via APIv4, you need to link three pieces together:

* The Group: Your "Staff" contact list (Group).
* The ACL Role: A role created to represent what Staff can do (OptionValue within the acl_role group).
* The ACL Rule: The actual permission policy assigning data/actions to that role (Acl).

Here is the exact APIv4 code to create these linkages and grant your Staff list its permissions.


Run this command in your terminal to extract the staff role's permission array. The -T flag outputs the results as a formatted text table:
$ cv api4 Role.get -T '+w' 'name = "staff"' '+s' 'id,name,label,permissions'

Total permissions: 213
Admin permissions: 213
Staff permissions: 77
Everyone permissions: 6

Everyone
```
$ cv api4 Role.get '{"where":[["name","=","everyone"]],"select":["permissions"]}'
[
    {
        "id": 1,
        "permissions": [
            "access CiviMail subscribe/unsubscribe pages",
            "make online contributions",
            "view event info",
            "register for events",
            "access password resets",
            "authenticate with password"
        ]
    }
]
```



Admin
```
$ cv api4 Role.get '{"where":[["name","=","admin"]],"select":["permissions"]}'
[
    {
        "id": 2,
        "permissions": [
            "all CiviCRM permissions and ACLs"
        ]
    }
]

```
===

To query the civicrm_role table directly for the staff entry, run this exact command:
1. The Clean cv api4 Table Format
`cv api4 Role.get -T '+w' 'name = "staff"' '+s' 'id,name,label,permissions'`

2. The JSON Format
If you just want the raw permissions array block dumped out:

```
$ cv api4 Role.get '{"where":[["name","=","staff"]],"select":["permissions"]}'
[
    {
        "id": 3,
        "permissions": [
            "access AJAX API",
            "access CiviCRM",
            "access Contact Dashboard",
            "access uploaded files",
            "add contacts",
            "view my contact",
            "view all contacts",
            "edit all contacts",
            "edit my contact",
            "delete contacts",
            "import contacts",
            "access deleted contacts",
            "merge duplicate contacts",
            "edit groups",
            "manage tags",
            "administer Tagsets",
            "view all activities",
            "delete activities",
            "add contact notes",
            "view all notes",
            "access CiviContribute",
            "delete in CiviContribute",
            "edit contributions",
            "make online contributions",
            "view my invoices",
            "access CiviEvent",
            "delete in CiviEvent",
            "edit all events",
            "edit event participants",
            "register for events",
            "view event info",
            "view event participants",
            "gotv campaign contacts",
            "interview campaign contacts",
            "manage campaign",
            "release campaign contacts",
            "reserve campaign contacts",
            "sign CiviCRM Petition",
            "access CiviMail",
            "access CiviMail subscribe/unsubscribe pages",
            "delete in CiviMail",
            "view public CiviMail content",
            "access CiviMember",
            "delete in CiviMember",
            "edit memberships",
            "access all cases and activities",
            "access my cases and activities",
            "add cases",
            "delete in CiviCase",
            "access CiviPledge",
            "delete in CiviPledge",
            "edit pledges",
            "access CiviReport",
            "access Report Criteria",
            "administer reserved reports",
            "save Report Criteria",
            "profile create",
            "profile edit",
            "profile listings",
            "profile listings and forms",
            "profile view",
            "close all manual batches",
            "close own manual batches",
            "create manual batch",
            "delete all manual batches",
            "delete own manual batches",
            "edit all manual batches",
            "edit own manual batches",
            "export all manual batches",
            "export own manual batches",
            "reopen all manual batches",
            "reopen own manual batches",
            "view all manual batches",
            "view own manual batches",
            "access all custom data",
            "access contact reference fields",
            "cms:view user account"
        ]
    }
]

```

1. List EVERY Permission in the System
To get a full dump of all available permission strings registered in your Standalone instance, run:
`cv api4 Permission.get -T '+s' 'name,title,description'`

Reduce to just the name:

`cv api4 Permission.get -T '+s' 'name'`
```
$ cv api4 Permission.get -T '+s' 'name'
+----------------------------------------------------+
| name                                               |
+----------------------------------------------------+
| *always deny*                                      |
| *always allow*                                     |
| *authenticated*                                    |
| add contacts                                       |
| view all contacts                                  |
| edit all contacts                                  |
| view my contact                                    |
| edit my contact                                    |
| delete contacts                                    |
| access deleted contacts                            |
| import contacts                                    |
| import SQL datasource                              |
| edit groups                                        |
| administer CiviCRM                                 |
| skip IDS check                                     |
| access uploaded files                              |
| profile listings and forms                         |
| profile listings                                   |
| profile create                                     |
| profile edit                                       |
| profile view                                       |
| access all custom data                             |
| view all activities                                |
| delete activities                                  |
| edit inbound email basic information               |
| edit inbound email basic information and content   |
| access CiviCRM                                     |
| access Contact Dashboard                           |
| translate CiviCRM                                  |
| manage tags                                        |
| administer reserved groups                         |
| administer Tagsets                                 |
| administer reserved tags                           |
| administer queues                                  |
| administer dedupe rules                            |
| merge duplicate contacts                           |
| force merge duplicate contacts                     |
| view debug output                                  |
| view all notes                                     |
| add contact notes                                  |
| access AJAX API                                    |
| access contact reference fields                    |
| create manual batch                                |
| edit own manual batches                            |
| edit all manual batches                            |
| close own manual batches                           |
| close all manual batches                           |
| reopen own manual batches                          |
| reopen all manual batches                          |
| view own manual batches                            |
| view all manual batches                            |
| delete own manual batches                          |
| delete all manual batches                          |
| export own manual batches                          |
| export all manual batches                          |
| administer payment processors                      |
| render templates                                   |
| edit message templates                             |
| edit system workflow message templates             |
| edit user-driven message templates                 |
| view my invoices                                   |
| edit api keys                                      |
| edit own api keys                                  |
| send SMS                                           |
| administer CiviCRM system                          |
| administer CiviCRM data                            |
| all CiviCRM permissions and ACLs                   |
| access CiviEvent                                   |
| edit event participants                            |
| edit all events                                    |
| register for events                                |
| view event info                                    |
| view event participants                            |
| delete in CiviEvent                                |
| manage event profiles                              |
| access CiviContribute                              |
| edit contributions                                 |
| refund contributions                               |
| make online contributions                          |
| delete in CiviContribute                           |
| access CiviMember                                  |
| edit memberships                                   |
| delete in CiviMember                               |
| access CiviMail                                    |
| access CiviMail subscribe/unsubscribe pages        |
| delete in CiviMail                                 |
| view public CiviMail content                       |
| create mailings                                    |
| schedule mailings                                  |
| approve mailings                                   |
| access CiviPledge                                  |
| edit pledges                                       |
| delete in CiviPledge                               |
| delete in CiviCase                                 |
| administer CiviCase                                |
| access my cases and activities                     |
| access all cases and activities                    |
| add cases                                          |
| access CiviReport                                  |
| access Report Criteria                             |
| save Report Criteria                               |
| administer private reports                         |
| administer reserved reports                        |
| administer Reports                                 |
| view report sql                                    |
| administer CiviCampaign                            |
| manage campaign                                    |
| reserve campaign contacts                          |
| release campaign contacts                          |
| interview campaign contacts                        |
| gotv campaign contacts                             |
| sign CiviCRM Petition                              |
| administer search_kit                              |
| manage own search_kit                              |
| authenticate with password                         |
| authenticate with api key                          |
| generate any authx credential                      |
| validate any authx credential                      |
| administer afform                                  |
| manage own afform                                  |
| access password resets                             |
| cms:administer users                               |
| cms:view user account                              |
| cms:bypass maintenance mode                        |
| administer authx                                   |
| administer recaptcha                               |
| administer standaloneusers                         |
| has user role admin                                |
| has user role staff                                |
| @afformPageToken                                   |
| @afform:afformQuickAddIndividual                   |
| @afform:afformQuickAddOrganization                 |
| @afform:afformQuickEditHousehold                   |
| @afform:afformQuickEditIndividual                  |
| @afform:afformQuickEditOrganization                |
| @afform:afformSiteEmailAddress                     |
| @afform:afformSiteToken                            |
| @afform:afsearchAdminCustomFields                  |
| @afform:afsearchAdminCustomGroups                  |
| @afform:afsearchCustomFieldOptions                 |
| @afform:afsearchSiteEmailAddresses                 |
| @afform:afsearchSiteTokens                         |
| @afform:afsearchTabNote                            |
| @afform:afsearchTabRel                             |
| @afform:afsearchMosaicoTemplateList                |
| @afform:afformEditMyAccount                        |
| @afform:afformEditRole                             |
| @afform:afformEditUserAccount                      |
| @afform:afsearchAdministerRoles                    |
| @afform:afsearchAdministerUserAccounts             |
| @afform:afsearchMyAccount                          |
| @afform:afsearchPermissions                        |
| @afform:afAdminFormSubmissionList                  |
| @afform:afblockContactAddress                      |
| @afform:afblockContactEmail                        |
| @afform:afblockContactIM                           |
| @afform:afblockContactNote                         |
| @afform:afblockContactPhone                        |
| @afform:afblockContactWebsite                      |
| @afform:afblockEventLocBlock                       |
| @afform:afblockNameHousehold                       |
| @afform:afblockNameIndividual                      |
| @afform:afblockNameOrganization                    |
| @afform:afblockParticipantNote                     |
| @afform:crmMsgadmMonaco                            |
| @afform:afsearchAllImports                         |
| @afform:afsearchMyImports                          |
| @afform:afsearchTemplates                          |
| @afform:afformTabMember                            |
| @afform:afsearchAdminBadgelayout                   |
| @afform:afsearchAdminContactTypes                  |
| @afform:afsearchAdminFinancialTypes                |
| @afform:afsearchAdminScheduledReminders            |
| @afform:afsearchAdministerLocationTypes            |
| @afform:afsearchAdministerMembershipStatusRules    |
| @afform:afsearchAdministerNavigationMenu           |
| @afform:afsearchAdministerPaymentProcessors        |
| @afform:afsearchAdministerPriceFieldValues         |
| @afform:afsearchAdministerPriceFields              |
| @afform:afsearchAdministerPriceSets                |
| @afform:afsearchAssignUsersToRoles                 |
| @afform:afsearchAssignedFinancialAccounts          |
| @afform:afsearchCiviCRMQueues                      |
| @afform:afsearchFinancialAccounts                  |
| @afform:afsearchHeadersFootersAndAutomatedMessages |
| @afform:afsearchImportExportMappings               |
| @afform:afsearchLabelFormats                       |
| @afform:afsearchMailAccounts                       |
| @afform:afsearchMailingBrowseDraft                 |
| @afform:afsearchMailingBrowseScheduled             |
| @afform:afsearchMailingClickThroughsResults        |
| @afform:afsearchManageACLs                         |
| @afform:afsearchManageContributionPages            |
| @afform:afsearchManageGroups                       |
| @afform:afsearchManageScheduledJobs                |
| @afform:afsearchPersonalCampaignPages              |
| @afform:afsearchPremiumProducts                    |
| @afform:afsearchPrintPagePDFFormats                |
| @afform:afsearchProfileFields                      |
| @afform:afsearchProfiles                           |
| @afform:afsearchRelationshipTypes                  |
| @afform:afsearchSMSProvider                        |
| @afform:afsearchScheduledJobsLog                   |
| @afform:afsearchSettingsDatePreferences            |
| @afform:afsearchTabActivity                        |
| @afform:afsearchTabCase                            |
| @afform:afsearchTabMember                          |
| @afform:afsearchTabParticipant                     |
| @afform:afsearchTabPledge                          |
| @afform:afsearchEmailBounceHistory                 |
| @afform:afformNewDonation                          |
| @afform:afsearchCampaignDashboard                  |
| @afform:afsearchSurveyOptionGroup                  |
+----------------------------------------------------+
```



```
$ cv api4 Permission.get -T '+s' 'name,title'
+----------------------------------------------------+---------------------------------------------------------------------------+
| name                                               | title                                                                     |
+----------------------------------------------------+---------------------------------------------------------------------------+
| *always deny*                                      | Generic: Deny all users                                                   |
| *always allow*                                     | Generic: Allow all users (including anonymous)                            |
| *authenticated*                                    | Generic: Allow any authenticated contact                                  |
| add contacts                                       | CiviCRM: add contacts                                                     |
| view all contacts                                  | CiviCRM: view all contacts                                                |
| edit all contacts                                  | CiviCRM: edit all contacts                                                |
| view my contact                                    | CiviCRM: view my contact                                                  |
| edit my contact                                    | CiviCRM: edit my contact                                                  |
| delete contacts                                    | CiviCRM: delete contacts                                                  |
| access deleted contacts                            | CiviCRM: access deleted contacts                                          |
| import contacts                                    | CiviCRM: import contacts                                                  |
| import SQL datasource                              | CiviCRM: import SQL datasource                                            |
| edit groups                                        | CiviCRM: edit groups                                                      |
| administer CiviCRM                                 | CiviCRM: administer CiviCRM                                               |
| skip IDS check                                     | CiviCRM: skip IDS check                                                   |
| access uploaded files                              | CiviCRM: access uploaded files                                            |
| profile listings and forms                         | CiviCRM: profile listings and forms                                       |
| profile listings                                   | CiviCRM: profile listings                                                 |
| profile create                                     | CiviCRM: profile create                                                   |
| profile edit                                       | CiviCRM: profile edit                                                     |
| profile view                                       | CiviCRM: profile view                                                     |
| access all custom data                             | CiviCRM: access all custom data                                           |
| view all activities                                | CiviCRM: view all activities                                              |
| delete activities                                  | CiviCRM: Delete activities                                                |
| edit inbound email basic information               | CiviCRM: edit inbound email basic information                             |
| edit inbound email basic information and content   | CiviCRM: edit inbound email basic information and content                 |
| access CiviCRM                                     | CiviCRM: access CiviCRM backend and API                                   |
| access Contact Dashboard                           | CiviCRM: access Contact Dashboard                                         |
| translate CiviCRM                                  | CiviCRM: translate CiviCRM                                                |
| manage tags                                        | CiviCRM: manage tags                                                      |
| administer reserved groups                         | CiviCRM: administer reserved groups                                       |
| administer Tagsets                                 | CiviCRM: administer Tagsets                                               |
| administer reserved tags                           | CiviCRM: administer reserved tags                                         |
| administer queues                                  | CiviCRM: administer queues                                                |
| administer dedupe rules                            | CiviCRM: administer dedupe rules                                          |
| merge duplicate contacts                           | CiviCRM: merge duplicate contacts                                         |
| force merge duplicate contacts                     | CiviCRM: force merge duplicate contacts                                   |
| view debug output                                  | CiviCRM: view debug output                                                |
| view all notes                                     | CiviCRM: view all notes                                                   |
| add contact notes                                  | CiviCRM: add contact notes                                                |
| access AJAX API                                    | CiviCRM: access AJAX API                                                  |
| access contact reference fields                    | CiviCRM: access contact reference fields                                  |
| create manual batch                                | CiviCRM: create manual batch                                              |
| edit own manual batches                            | CiviCRM: edit own manual batches                                          |
| edit all manual batches                            | CiviCRM: edit all manual batches                                          |
| close own manual batches                           | CiviCRM: close own manual batches                                         |
| close all manual batches                           | CiviCRM: close all manual batches                                         |
| reopen own manual batches                          | CiviCRM: reopen own manual batches                                        |
| reopen all manual batches                          | CiviCRM: reopen all manual batches                                        |
| view own manual batches                            | CiviCRM: view own manual batches                                          |
| view all manual batches                            | CiviCRM: view all manual batches                                          |
| delete own manual batches                          | CiviCRM: delete own manual batches                                        |
| delete all manual batches                          | CiviCRM: delete all manual batches                                        |
| export own manual batches                          | CiviCRM: export own manual batches                                        |
| export all manual batches                          | CiviCRM: export all manual batches                                        |
| administer payment processors                      | CiviCRM: administer payment processors                                    |
| render templates                                   | CiviCRM: render templates                                                 |
| edit message templates                             | CiviCRM: edit message templates                                           |
| edit system workflow message templates             | CiviCRM: edit system workflow message templates                           |
| edit user-driven message templates                 | CiviCRM: edit user-driven message templates                               |
| view my invoices                                   | CiviCRM: view my invoices                                                 |
| edit api keys                                      | CiviCRM: edit api keys                                                    |
| edit own api keys                                  | CiviCRM: edit own api keys                                                |
| send SMS                                           | CiviCRM: send SMS                                                         |
| administer CiviCRM system                          | CiviCRM: administer CiviCRM System                                        |
| administer CiviCRM data                            | CiviCRM: administer CiviCRM Data                                          |
| all CiviCRM permissions and ACLs                   | CiviCRM: all CiviCRM permissions and ACLs                                 |
| access CiviEvent                                   | CiviEvent: access CiviEvent                                               |
| edit event participants                            | CiviEvent: edit event participants                                        |
| edit all events                                    | CiviEvent: edit all events                                                |
| register for events                                | CiviEvent: register for events                                            |
| view event info                                    | CiviEvent: view event info                                                |
| view event participants                            | CiviEvent: view event participants                                        |
| delete in CiviEvent                                | CiviEvent: delete in CiviEvent                                            |
| manage event profiles                              | CiviEvent: manage event profiles                                          |
| access CiviContribute                              | CiviContribute: access CiviContribute                                     |
| edit contributions                                 | CiviContribute: edit contributions                                        |
| refund contributions                               | CiviContribute: Refund contributions                                      |
| make online contributions                          | CiviContribute: make online contributions                                 |
| delete in CiviContribute                           | CiviContribute: delete in CiviContribute                                  |
| access CiviMember                                  | CiviMember: access CiviMember                                             |
| edit memberships                                   | CiviMember: edit memberships                                              |
| delete in CiviMember                               | CiviMember: delete in CiviMember                                          |
| access CiviMail                                    | CiviMail: access CiviMail                                                 |
| access CiviMail subscribe/unsubscribe pages        | CiviMail: access CiviMail subscribe/unsubscribe pages                     |
| delete in CiviMail                                 | CiviMail: delete in CiviMail                                              |
| view public CiviMail content                       | CiviMail: view public CiviMail content                                    |
| create mailings                                    | CiviMail: create mailings                                                 |
| schedule mailings                                  | CiviMail: schedule mailings                                               |
| approve mailings                                   | CiviMail: approve mailings                                                |
| access CiviPledge                                  | CiviPledge: access CiviPledge                                             |
| edit pledges                                       | CiviPledge: edit pledges                                                  |
| delete in CiviPledge                               | CiviPledge: delete in CiviPledge                                          |
| delete in CiviCase                                 | CiviCase: delete in CiviCase                                              |
| administer CiviCase                                | CiviCase: administer CiviCase                                             |
| access my cases and activities                     | CiviCase: access my cases and activities                                  |
| access all cases and activities                    | CiviCase: access all cases and activities                                 |
| add cases                                          | CiviCase: add cases                                                       |
| access CiviReport                                  | CiviReport: access CiviReport                                             |
| access Report Criteria                             | CiviReport: access Report Criteria                                        |
| save Report Criteria                               | CiviReport: save Report Criteria                                          |
| administer private reports                         | CiviReport: administer private reports                                    |
| administer reserved reports                        | CiviReport: administer reserved reports                                   |
| administer Reports                                 | CiviReport: administer Reports                                            |
| view report sql                                    | CiviReport: view report sql                                               |
| administer CiviCampaign                            | CiviCampaign: administer CiviCampaign                                     |
| manage campaign                                    | CiviCampaign: manage campaign                                             |
| reserve campaign contacts                          | CiviCampaign: reserve campaign contacts                                   |
| release campaign contacts                          | CiviCampaign: release campaign contacts                                   |
| interview campaign contacts                        | CiviCampaign: interview campaign contacts                                 |
| gotv campaign contacts                             | CiviCampaign: GOTV campaign contacts                                      |
| sign CiviCRM Petition                              | CiviCampaign: sign CiviCRM Petition                                       |
| administer search_kit                              | SearchKit: edit and delete all searches                                   |
| manage own search_kit                              | SearchKit: edit and delete own searches                                   |
| authenticate with password                         | AuthX: Authenticate to services with password                             |
| authenticate with api key                          | AuthX: Authenticate to services with API key                              |
| generate any authx credential                      | AuthX: Generate new JWT credentials for other users via the API           |
| validate any authx credential                      | AuthX: Validate credentials for other users via the API                   |
| administer afform                                  | FormBuilder: edit and delete forms                                        |
| manage own afform                                  | FormBuilder: edit and delete own forms                                    |
| access password resets                             | CiviCRM Standalone Users: Allow users to access the reset password system |
| cms:administer users                               | CiviCRM Standalone Users: Administer user accounts                        |
| cms:view user account                              | CiviCRM Standalone Users: View user accounts                              |
| cms:bypass maintenance mode                        | CiviCRM Standalone Users: Bypass maintenance mode                         |
| administer authx                                   | AuthX: Administer settings                                                |
| administer recaptcha                               | reCAPTCHA: Administer settings                                            |
| administer standaloneusers                         | CiviCRM Standalone Users: Administer settings                             |
| has user role admin                                | User Role: Administrator                                                  |
| has user role staff                                | User Role: Staff                                                          |
| @afformPageToken                                   | Generic: Anyone with secret link                                          |
| @afform:afformQuickAddIndividual                   | Afform: Inherit permission of afformQuickAddIndividual                    |
| @afform:afformQuickAddOrganization                 | Afform: Inherit permission of afformQuickAddOrganization                  |
| @afform:afformQuickEditHousehold                   | Afform: Inherit permission of afformQuickEditHousehold                    |
| @afform:afformQuickEditIndividual                  | Afform: Inherit permission of afformQuickEditIndividual                   |
| @afform:afformQuickEditOrganization                | Afform: Inherit permission of afformQuickEditOrganization                 |
| @afform:afformSiteEmailAddress                     | Afform: Inherit permission of afformSiteEmailAddress                      |
| @afform:afformSiteToken                            | Afform: Inherit permission of afformSiteToken                             |
| @afform:afsearchAdminCustomFields                  | Afform: Inherit permission of afsearchAdminCustomFields                   |
| @afform:afsearchAdminCustomGroups                  | Afform: Inherit permission of afsearchAdminCustomGroups                   |
| @afform:afsearchCustomFieldOptions                 | Afform: Inherit permission of afsearchCustomFieldOptions                  |
| @afform:afsearchSiteEmailAddresses                 | Afform: Inherit permission of afsearchSiteEmailAddresses                  |
| @afform:afsearchSiteTokens                         | Afform: Inherit permission of afsearchSiteTokens                          |
| @afform:afsearchTabNote                            | Afform: Inherit permission of afsearchTabNote                             |
| @afform:afsearchTabRel                             | Afform: Inherit permission of afsearchTabRel                              |
| @afform:afsearchMosaicoTemplateList                | Afform: Inherit permission of afsearchMosaicoTemplateList                 |
| @afform:afformEditMyAccount                        | Afform: Inherit permission of afformEditMyAccount                         |
| @afform:afformEditRole                             | Afform: Inherit permission of afformEditRole                              |
| @afform:afformEditUserAccount                      | Afform: Inherit permission of afformEditUserAccount                       |
| @afform:afsearchAdministerRoles                    | Afform: Inherit permission of afsearchAdministerRoles                     |
| @afform:afsearchAdministerUserAccounts             | Afform: Inherit permission of afsearchAdministerUserAccounts              |
| @afform:afsearchMyAccount                          | Afform: Inherit permission of afsearchMyAccount                           |
| @afform:afsearchPermissions                        | Afform: Inherit permission of afsearchPermissions                         |
| @afform:afAdminFormSubmissionList                  | Afform: Inherit permission of afAdminFormSubmissionList                   |
| @afform:afblockContactAddress                      | Afform: Inherit permission of afblockContactAddress                       |
| @afform:afblockContactEmail                        | Afform: Inherit permission of afblockContactEmail                         |
| @afform:afblockContactIM                           | Afform: Inherit permission of afblockContactIM                            |
| @afform:afblockContactNote                         | Afform: Inherit permission of afblockContactNote                          |
| @afform:afblockContactPhone                        | Afform: Inherit permission of afblockContactPhone                         |
| @afform:afblockContactWebsite                      | Afform: Inherit permission of afblockContactWebsite                       |
| @afform:afblockEventLocBlock                       | Afform: Inherit permission of afblockEventLocBlock                        |
| @afform:afblockNameHousehold                       | Afform: Inherit permission of afblockNameHousehold                        |
| @afform:afblockNameIndividual                      | Afform: Inherit permission of afblockNameIndividual                       |
| @afform:afblockNameOrganization                    | Afform: Inherit permission of afblockNameOrganization                     |
| @afform:afblockParticipantNote                     | Afform: Inherit permission of afblockParticipantNote                      |
| @afform:crmMsgadmMonaco                            | Afform: Inherit permission of crmMsgadmMonaco                             |
| @afform:afsearchAllImports                         | Afform: Inherit permission of afsearchAllImports                          |
| @afform:afsearchMyImports                          | Afform: Inherit permission of afsearchMyImports                           |
| @afform:afsearchTemplates                          | Afform: Inherit permission of afsearchTemplates                           |
| @afform:afformTabMember                            | Afform: Inherit permission of afformTabMember                             |
| @afform:afsearchAdminBadgelayout                   | Afform: Inherit permission of afsearchAdminBadgelayout                    |
| @afform:afsearchAdminContactTypes                  | Afform: Inherit permission of afsearchAdminContactTypes                   |
| @afform:afsearchAdminFinancialTypes                | Afform: Inherit permission of afsearchAdminFinancialTypes                 |
| @afform:afsearchAdminScheduledReminders            | Afform: Inherit permission of afsearchAdminScheduledReminders             |
| @afform:afsearchAdministerLocationTypes            | Afform: Inherit permission of afsearchAdministerLocationTypes             |
| @afform:afsearchAdministerMembershipStatusRules    | Afform: Inherit permission of afsearchAdministerMembershipStatusRules     |
| @afform:afsearchAdministerNavigationMenu           | Afform: Inherit permission of afsearchAdministerNavigationMenu            |
| @afform:afsearchAdministerPaymentProcessors        | Afform: Inherit permission of afsearchAdministerPaymentProcessors         |
| @afform:afsearchAdministerPriceFieldValues         | Afform: Inherit permission of afsearchAdministerPriceFieldValues          |
| @afform:afsearchAdministerPriceFields              | Afform: Inherit permission of afsearchAdministerPriceFields               |
| @afform:afsearchAdministerPriceSets                | Afform: Inherit permission of afsearchAdministerPriceSets                 |
| @afform:afsearchAssignUsersToRoles                 | Afform: Inherit permission of afsearchAssignUsersToRoles                  |
| @afform:afsearchAssignedFinancialAccounts          | Afform: Inherit permission of afsearchAssignedFinancialAccounts           |
| @afform:afsearchCiviCRMQueues                      | Afform: Inherit permission of afsearchCiviCRMQueues                       |
| @afform:afsearchFinancialAccounts                  | Afform: Inherit permission of afsearchFinancialAccounts                   |
| @afform:afsearchHeadersFootersAndAutomatedMessages | Afform: Inherit permission of afsearchHeadersFootersAndAutomatedMessages  |
| @afform:afsearchImportExportMappings               | Afform: Inherit permission of afsearchImportExportMappings                |
| @afform:afsearchLabelFormats                       | Afform: Inherit permission of afsearchLabelFormats                        |
| @afform:afsearchMailAccounts                       | Afform: Inherit permission of afsearchMailAccounts                        |
| @afform:afsearchMailingBrowseDraft                 | Afform: Inherit permission of afsearchMailingBrowseDraft                  |
| @afform:afsearchMailingBrowseScheduled             | Afform: Inherit permission of afsearchMailingBrowseScheduled              |
| @afform:afsearchMailingClickThroughsResults        | Afform: Inherit permission of afsearchMailingClickThroughsResults         |
| @afform:afsearchManageACLs                         | Afform: Inherit permission of afsearchManageACLs                          |
| @afform:afsearchManageContributionPages            | Afform: Inherit permission of afsearchManageContributionPages             |
| @afform:afsearchManageGroups                       | Afform: Inherit permission of afsearchManageGroups                        |
| @afform:afsearchManageScheduledJobs                | Afform: Inherit permission of afsearchManageScheduledJobs                 |
| @afform:afsearchPersonalCampaignPages              | Afform: Inherit permission of afsearchPersonalCampaignPages               |
| @afform:afsearchPremiumProducts                    | Afform: Inherit permission of afsearchPremiumProducts                     |
| @afform:afsearchPrintPagePDFFormats                | Afform: Inherit permission of afsearchPrintPagePDFFormats                 |
| @afform:afsearchProfileFields                      | Afform: Inherit permission of afsearchProfileFields                       |
| @afform:afsearchProfiles                           | Afform: Inherit permission of afsearchProfiles                            |
| @afform:afsearchRelationshipTypes                  | Afform: Inherit permission of afsearchRelationshipTypes                   |
| @afform:afsearchSMSProvider                        | Afform: Inherit permission of afsearchSMSProvider                         |
| @afform:afsearchScheduledJobsLog                   | Afform: Inherit permission of afsearchScheduledJobsLog                    |
| @afform:afsearchSettingsDatePreferences            | Afform: Inherit permission of afsearchSettingsDatePreferences             |
| @afform:afsearchTabActivity                        | Afform: Inherit permission of afsearchTabActivity                         |
| @afform:afsearchTabCase                            | Afform: Inherit permission of afsearchTabCase                             |
| @afform:afsearchTabMember                          | Afform: Inherit permission of afsearchTabMember                           |
| @afform:afsearchTabParticipant                     | Afform: Inherit permission of afsearchTabParticipant                      |
| @afform:afsearchTabPledge                          | Afform: Inherit permission of afsearchTabPledge                           |
| @afform:afsearchEmailBounceHistory                 | Afform: Inherit permission of afsearchEmailBounceHistory                  |
| @afform:afformNewDonation                          | Afform: Inherit permission of afformNewDonation                           |
| @afform:afsearchCampaignDashboard                  | Afform: Inherit permission of afsearchCampaignDashboard                   |
| @afform:afsearchSurveyOptionGroup                  | Afform: Inherit permission of afsearchSurveyOptionGroup                   |
+----------------------------------------------------+---------------------------------------------------------------------------+


```
