# Comparison of Extensions

```
  Civi-USA Extensions:                           Civi-AUST Extensions                           
  E = Enabled, R = Required, D = Disabled                                                       
                                                                                                
  Activity Status and Priority                                                                  
  AdminUI (Preview)                             E AdminUI (Preview)                             
  Advanced logging with Changelog                                                               
E Aegir Backups                                                                                 
  API Key Management                                                                            
  Archive Mailings                                                                              
R AuthX                                         R AuthX                                         
  Batch Data Entry                              E Batch Data Entry                              
  Chart Kit                                     E Chart Kit                                     
R Civi-Import                                   E Civi-Import                                   
E CiviCampaign                                  E CiviCampaign                                  
E CiviCase                                      E CiviCase                                      
E CiviContribute                                E CiviContribute                                
E CiviCRM Export to Excel                                                                       
E CiviCRM Log Viewer                            E CiviCRM Log Viewer                            
  CiviCRM Report Error                                                                          
E CiviCRM Spark                                                                                 
  CiviDiscount                                                                                  
E CiviEvent                                     E CiviEvent                                     
D CiviGrant                                     E CiviGrant                                     
E CiviMail                                      E CiviMail                                      
E CiviMember                                    E CiviMember                                    
E CiviPledge                                    E CiviPledge                                    
E CiviReport                                    E CiviReport                                    
  CiviRules                                                                                     
  CiviSEPA Payment Processor                                                                    
E CiviTutorial                                                                                  
E CKEditor4                                     E CKEditor4                                     
  CKEditor5                                                                                     
  Contact Layout Editor                                                                         
E Contribution cancel actions                   E Contribution cancel actions                   
E Coop SymbioTIC                                                                                
E Custom search framework                       E Custom search framework                       
  Data Explorer                                                                                 
  Doc Bot                                                                                       
  Doctor When                                                                                   
  ducttape                                                                                      
E Easy Copy                                     E Easy Copy                                     
  Elavon Payment Processor                      E Elavon Payment Processor                      
  Email API                                                                                     
  Event Cart                                    E Event Cart                                    
  ExtendedReport                                                                                
D Financial ACLs                                E Financial ACLs                                
E Firewall                                                                                      
E Fix Option Translations                       E Fix Option Translations                       
R FlexMailer                                    R FlexMailer                                    
  Flood Control                                                                                 
E Form Code Editor                              E Form Code Editor                              
R Form Core                                     R Form Core                                     
  Form Core Login-Tokens                        E Form Core Login-Tokens                        
  Form Protection                                                                               
E FormBuilder                                   E FormBuilder                                   
E General Data Protection Regulation            E General Data Protection Regulation            
E Genius Platform by Global Payments Integrated                                                 
D iATS Payments                                 E iATS Payments                                 
E Language switcher                             D Language switcher                             
E legacydedupefinder                            E legacydedupefinder                            
  legacyprofiles                                E legacyprofiles                                
E Login Security                                D Login Security                                
                                                E Membership Renewallinks                       
E Message Administration                        E Message Administration                        
E Mosaico                                       E Mosaico                                       
  OAuth Client                                    OAuth Client                                  
E Payment Shared                                                                                
  PayPal Payflow Pro Integration                E PayPal Payflow Pro Integration                
  Postbox                                       E Postbox                                       
E Prevent users from overwriting their record   D Prevent users from overwriting their record   
  Provincial Invoice                                                                            
  Radio Buttons                                                                                 
E reply_to                                      D reply_to                                      
E RiverLea CiviCRM Theme Framework              E RiverLea CiviCRM Theme Framework              
  Scheduled Communications                        Scheduled Communications                      
  Search Kit Reports                              Search Kit Reports                            
R SearchKit                                     R SearchKit                                     
  SearchUI                                        SearchUI                                      
  SEPA Direct Debit                                                                             
  Simple Redirected MailReader                                                                  
E SparkPost integration                                                                         
E Standalone Migrate                            D Standalone Migrate                            
E Stripe Payment Processor                                                                      
  Summernote WYSIWYG editor                                                                     
E Sweet Alert                                                                                   
  SymbioTIC UX                                                                                  
  Tell a Friend                                 D Tell a Friend                                 
E The Island Theme                              E The Island Theme                              
  twilio                                                                                        
  Update Language Files                                                                         
  User Dashboard                                E User Dashboard                                
                                                                                                
```

CiviCRM Standalone on crm.cmrailtrial.org.au

```
[cmrailtr@s03dd civicrm-standalone]$ cv api4 Extension.get '{"select":["label","status"],"orderBy":{"status":"ASC"},"limit":0}' --out=table
+---------------------------------------------+------------------+
| label                                       | status           |
+---------------------------------------------+------------------+
| Tell a Friend                               | disabled         |
| Language switcher                           | disabled-missing |
| Prevent users from overwriting their record | disabled-missing |
| Login Security                              | disabled-missing |
| reply_to                                    | disabled-missing |
| Standalone Migrate                          | disabled-missing |
| AuthX                                       | installed        |
| Batch Data Entry                            | installed        |
| Chart Kit                                   | installed        |
| CiviCampaign                                | installed        |
| CiviCase                                    | installed        |
| CiviContribute                              | installed        |
| CiviEvent                                   | installed        |
| CiviMail                                    | installed        |
| CiviMember                                  | installed        |
| CiviPledge                                  | installed        |
| CiviReport                                  | installed        |
| AdminUI (Preview)                           | installed        |
| CiviGrant                                   | installed        |
| Civi-Import                                 | installed        |
| CKEditor4                                   | installed        |
| Contribution cancel actions                 | installed        |
| Elavon Payment Processor                    | installed        |
| Event Cart                                  | installed        |
| Financial ACLs                              | installed        |
| FlexMailer                                  | installed        |
| Theme: Greenwich                            | installed        |
| iATS Payments                               | installed        |
| IFrame Connector                            | installed        |
| Custom search framework                     | installed        |
| legacydedupefinder                          | installed        |
| legacyprofiles                              | installed        |
| Message Administration                      | installed        |
| PayPal Payflow Pro Integration              | installed        |
| Postbox                                     | installed        |
| reCAPTCHA                                   | installed        |
| RiverLea CiviCRM Theme Framework            | installed        |
| SearchKit                                   | installed        |
| Sequential credit notes                     | installed        |
| CiviCRM Standalone Users                    | installed        |
| User Dashboard                              | installed        |
| FormBuilder                                 | installed        |
| Form Core                                   | installed        |
| Form Code Editor                            | installed        |
| Form Core Login-Tokens                      | installed        |
| CiviCRM Log Viewer                          | installed        |
| Easy Copy                                   | installed        |
| Fix Option Translations                     | installed        |
| Membership Renewallinks                     | installed        |
| The Island Theme                            | installed        |
| General Data Protection Regulation          | installed        |
| Mosaico                                     | installed        |
| SearchUI                                    | uninstalled      |
| eway Single currency extension              | uninstalled      |
| Legacy Batch Data Entry                     | uninstalled      |
| OAuth Client                                | uninstalled      |
| oEmbed                                      | uninstalled      |
| Scheduled Communications                    | uninstalled      |
| Search Kit Reports                          | uninstalled      |
| Mock Form Collection                        | uninstalled      |
+---------------------------------------------+------------------+

```
## Jobs Scheduled

Scheduled Jobs for cmrailtrail.civirm.org - CIvi USA
```
Name (Frequency)                                      Last Run               Enabled?

CiviCRM Update Check (Daily)                          October 1st, 2026 12:52 PM  Yes  
Clean-up Temporary Data and Files (Daily)             October 1st, 2026 12:52 PM  Yes  
Disable expired relationships (Daily)                 October 1st, 2026 12:52 PM  Yes  
Firewall: Cleanup (Daily)                             October 1st, 2026 12:52 PM  Yes  
Process CiviMail Queue items (Hourly)                 October 1st, 2026 3:09 PM   Yes  
Process PaymentProcessor Webhooks (Always)            October 1st, 2026 3:55 PM   Yes  
Rebuild Smart Group Cache (Daily)                     October 1st, 2026 12:52 PM  Yes  
Send Scheduled Mailings (Always)                      October 1st, 2026 3:55 PM   Yes  
Send Scheduled Reminders (Daily)                      October 1st, 2026 12:52 PM  Yes  
Stripe: Cleanup (Hourly)                              October 1st, 2026 3:09 PM   Yes  
TSYS Payments Recurring Contributions (Daily)         October 1st, 2026 12:52 PM  Yes  
Update Membership Statuses (Daily)                    October 1st, 2026 12:52 PM  Yes  
Update Participant Statuses (Daily)                   October 1st, 2026 12:52 PM  Yes  

NO - NOT ENABLED
Name (Frequency)                                      Last Run               Enabled?

Fetch Bounces (Hourly) no parameters                  never                       No  
Geocode and Parse Addresses (Daily)                   never                       No  
iATS Payments 1stPay Query Transactions (Hourly)      February 14th, 2020 9:18 AM No  
iATS Payments Get Legacy Transaction Journal (Hourly) February 14th, 2020 9:18 AM No  
iATS Payments Recurring Contributions (Daily)         February 14th, 2020 1:34 AM No  
iATS Payments Verification (Hourly)                   February 14th, 2020 9:18 AM No  
Mail Reports (Daily)                                  never                       No  
Process Inbound Emails (Hourly)                       never                       No  
Process Pledges (Daily)                               never                       No  
Process Survey Respondents (Always)                   never                       No  
Send Scheduled SMS (Always)                           never                       No  
Update Greetings and Addressees (Daily)               never                       No  
Validate Email Address from Mailings. (Daily)         never                       No  
```

CiviCRM Jobs on crm.cmrailtrail.org.au

```
[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.get '{"select":["name","run_frequency","is_active"],"orderBy":{"is_active":"ASC"},"limit":0}' --out=table
+----+----------------------------------------------+---------------+-----------+
| id | name                                         | run_frequency | is_active |
+----+----------------------------------------------+---------------+-----------+
| 4  | Process Inbound Emails                       | Hourly        |           |
| 5  | Process Pledges                              | Daily         |           |
| 6  | Geocode and Parse Addresses                  | Daily         |           |
| 7  | Update Greetings and Addressees              | Daily         |           |
| 8  | Mail Reports                                 | Daily         |           |
| 12 | Process Survey Respondents                   | Always        |           |
| 14 | Send Scheduled SMS                           | Always        |           |
| 17 | Validate Email Address from Mailings.        | Daily         |           |
| 1  | CiviCRM Update Check                         | Daily         | 1         |
| 2  | Send Scheduled Mailings                      | Always        | 1         |
| 3  | Fetch Bounces                                | Hourly        | 1         |
| 9  | Send Scheduled Reminders                     | Daily         | 1         |
| 10 | Update Participant Statuses                  | Daily         | 1         |
| 11 | Update Membership Statuses                   | Daily         | 1         |
| 13 | Clean-up Temporary Data and Files            | Daily         | 1         |
| 15 | Rebuild Smart Group Cache                    | Daily         | 1         |
| 16 | Disable expired relationships                | Daily         | 1         |
| 41 | Process CiviMail Queue items                 | Hourly        | 1         |
| 42 | iATS Payments 1stPay Query Transactions      | Hourly        | 1         |
| 43 | iATS Payments Recurring Contributions        | Daily         | 1         |
| 44 | iATS Payments Get Legacy Transaction Journal | Hourly        | 1         |
| 45 | iATS Payments Verification                   | Hourly        | 1         |
+----+----------------------------------------------+---------------+-----------+
[cmrailtr@s03dd civicrm-standalone]$ 



[cmrailtr@s03dd civicrm-standalone]$ cv api4 Job.get +s name,run_frequency,is_active limit=0 --out=table
+----+----------------------------------------------+---------------+-----------+
| id | name                                         | run_frequency | is_active |
+----+----------------------------------------------+---------------+-----------+
| 1  | CiviCRM Update Check                         | Daily         | 1         |
| 2  | Send Scheduled Mailings                      | Always        | 1         |
| 3  | Fetch Bounces                                | Hourly        | 1         |
| 4  | Process Inbound Emails                       | Hourly        |           |
| 5  | Process Pledges                              | Daily         |           |
| 6  | Geocode and Parse Addresses                  | Daily         |           |
| 7  | Update Greetings and Addressees              | Daily         |           |
| 8  | Mail Reports                                 | Daily         |           |
| 9  | Send Scheduled Reminders                     | Daily         | 1         |
| 10 | Update Participant Statuses                  | Daily         | 1         |
| 11 | Update Membership Statuses                   | Daily         | 1         |
| 12 | Process Survey Respondents                   | Always        |           |
| 13 | Clean-up Temporary Data and Files            | Daily         | 1         |
| 14 | Send Scheduled SMS                           | Always        |           |
| 15 | Rebuild Smart Group Cache                    | Daily         | 1         |
| 16 | Disable expired relationships                | Daily         | 1         |
| 17 | Validate Email Address from Mailings.        | Daily         |           |
| 41 | Process CiviMail Queue items                 | Hourly        | 1         |
| 42 | iATS Payments 1stPay Query Transactions      | Hourly        | 1         |
| 43 | iATS Payments Recurring Contributions        | Daily         | 1         |
| 44 | iATS Payments Get Legacy Transaction Journal | Hourly        | 1         |
| 45 | iATS Payments Verification                   | Hourly        | 1         |
+----+----------------------------------------------+---------------+-----------+
[cmrailtr@s03dd civicrm-standalone]$ 
```

## All the CiviCRM entities available on crm.cmrailtrail.org.au

The cv api *get* should work with all these entities.
```
[cmrailtr@s03dd civicrm-standalone]$ cv api4 Entity.get +s name limit=0 --out=table
+------------------------------+
| name                         |
+------------------------------+
| ACL                          |
| ACLEntityRole                |
| ActionSchedule               |
| Activity                     |
| ActivityContact              |
| Address                      |
| Afform                       |
| AfformBehavior               |
| AfformSubmission             |
| AuthxCredential              |
| Batch                        |
| BouncePattern                |
| BounceType                   |
| Campaign                     |
| Case                         |
| CaseActivity                 |
| CaseContact                  |
| CaseType                     |
| Contact                      |
| ContactType                  |
| Contribution                 |
| ContributionPage             |
| ContributionProduct          |
| ContributionRecur            |
| ContributionSoft             |
| Country                      |
| County                       |
| CustomField                  |
| CustomGroup                  |
| Dashboard                    |
| DashboardContact             |
| DedupeException              |
| DedupeRule                   |
| DedupeRuleGroup              |
| Discount                     |
| Domain                       |
| Email                        |
| EmailMessage                 |
| Entity                       |
| EntityBatch                  |
| EntityFile                   |
| EntityFinancialAccount       |
| EntityFinancialTrxn          |
| EntitySet                    |
| EntityTag                    |
| Event                        |
| EventCartParticipant         |
| ExampleData                  |
| Extension                    |
| File                         |
| FinancialAccount             |
| FinancialItem                |
| FinancialTrxn                |
| FinancialType                |
| Grant                        |
| Group                        |
| GroupContact                 |
| GroupNesting                 |
| GroupOrganization            |
| GroupSubscription            |
| Household                    |
| IM                           |
| Iframe                       |
| Individual                   |
| Job                          |
| JobLog                       |
| LineItem                     |
| LocBlock                     |
| LocationType                 |
| Log                          |
| MailSettings                 |
| Mailing                      |
| MailingComponent             |
| MailingEventBounce           |
| MailingEventConfirm          |
| MailingEventDelivered        |
| MailingEventOpened           |
| MailingEventQueue            |
| MailingEventReply            |
| MailingEventSubscribe        |
| MailingEventTrackableURLOpen |
| MailingEventUnsubscribe      |
| MailingGroup                 |
| MailingJob                   |
| MailingTrackableURL          |
| Managed                      |
| Mapping                      |
| MappingField                 |
| Membership                   |
| MembershipBlock              |
| MembershipLog                |
| MembershipStatus             |
| MembershipType               |
| MessageTemplate              |
| MosaicoTemplate              |
| Navigation                   |
| Note                         |
| OpenID                       |
| OptionGroup                  |
| OptionValue                  |
| Order                        |
| Organization                 |
| PCP                          |
| PCPBlock                     |
| Participant                  |
| ParticipantStatusType        |
| Payment                      |
| PaymentProcessor             |
| PaymentProcessorType         |
| PaymentToken                 |
| Permission                   |
| Phone                        |
| Pledge                       |
| PledgeBlock                  |
| PledgePayment                |
| PreferencesDate              |
| Premium                      |
| PremiumsProduct              |
| PriceField                   |
| PriceFieldValue              |
| PriceSet                     |
| PriceSetEntity               |
| PrintLabel                   |
| Product                      |
| Queue                        |
| QueueItem                    |
| RecentItem                   |
| Relationship                 |
| RelationshipCache            |
| RelationshipType             |
| ReportInstance               |
| RiverleaStream               |
| Role                         |
| RolePermission               |
| Route                        |
| SavedSearch                  |
| SearchDisplay                |
| SearchParamSet               |
| SearchSegment                |
| Session                      |
| Setting                      |
| SiteEmailAddress             |
| SiteToken                    |
| SmsProvider                  |
| StateProvince                |
| StatusPreference             |
| SubscriptionHistory          |
| Survey                       |
| System                       |
| Tag                          |
| Totp                         |
| Translation                  |
| TranslationSource            |
| UFField                      |
| UFGroup                      |
| UFJoin                       |
| UFMatch                      |
| User                         |
| UserJob                      |
| UserRole                     |
| Website                      |
| WordReplacement              |
| WorkflowMessage              |
| WorldRegion                  |
+------------------------------+
```
