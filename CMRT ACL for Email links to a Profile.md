# CMRT ACL for Email links to a Profile

2026-04-30 - Ian Stewart

## Objective 

Have CMRT Mailing send an email to each contact in group within CMRT (E.g. "Current Members"). Each email contains a link to click on. Each of these links is a unique URL and is only for the contact that received the email. When Spark Essentials recieves the URL request it will open up a Profile ("questionnaire") for the contact in the group. The responses to the questionaire are saved. 

If the contact had previously filled in the questionnaire, then they will see their existing responses, and may make updates to these contacts.

## Background

### Notes: 

* With HTML5 the html `&amp;` is the same as html `&`.
* The tail of a URL may contain the *query* "?" component. This is single *attribute=value* pair, or, multiple *attribute=value* pairs separated by the `&` or `&amp;` delimiter.
* The email editor provides the insertion of "tokens". For example: `id={contact.contact_id}` will insert the unique contact identifier number for each email that is sent.
* Some tokens are an attribute=value pair. For example: `{contact.checksum}` expands to `cs=aaaaaaaaaaaaaaa`, where `cs` is the attribute *checksum*.

An example of a link that is embedded inside an email so that the email receipent can be taken to a questionnaire to fill out.

```html
https://cmrailtrail.civicrm.org/civicrm/profile/edit?gid=17&reset=1&id={contact.contact_id}&{contact.checksum}
```
In the above the query string contains:
* gid=17 <-- The profile (questionnaire) with an id of 17
* reset=1 <-- Clear the questionnaire when loading it.
* id={contact.contact_id} <-- The CiviCRM contacts identification. Unique integer for each contact.
* {contact.checksum} <-- Checksum this URL is using.

Note: The *profile/edit* has opther options, like *profile/create*, *profile/view*

The above link my be placed in a hyperlink `<a>` tag which has the `href` asttribute. For example:
```html
<a href="https://cmrailtrail.civicrm.org/civicrm/profile/edit?
gid=17&reset=1&id={contact.contact_id}&{contact.checksum}">Click to go to questionnaire</a>
```

When Spark Essentials performs mailings it re-writes the links for tracking before sending. Thus the above hyperlink may be embedded in the email as:

```html
<a href="https://cmrailtrail.civicrm.org/civicrm/mailing/url?
u=167&qid=980&id=400&cs=9617662130870fa4676132bbe5e841e7_1777457844_336">Click to go to questionnaire</a>
```

In the above the query string contains:
* u=167 <-- Internal *URL ID* in the mailing system. Resolves u=167 to the original URL
* qid=980 <-- Queue ID to identify the recipient. Which specific email instance was sent to which contact
* id=400 <-- Contact ID
* cs=9617662130870fa4676132bbe5e841e7_1777457844_336 <-- Checksum

## Issue - Forced to Login

When the tracking link is clicked, the Spark system may conclude that the contact does not have sufficient permissions to access the profile (questionnaire). The Spark system then launches a Login screen, such that if the contact logged into an account with sufficient permissions then the profile (questionnaire) could be accessed and displayed.

### Solution

On Spark Essentials, go to...

Administer --> Users and Permissions --> Permissions (Access Control)

This will display the screen: https://cmrailtrail.civicrm.org/civicrm/admin/access?reset=1

Click option **3. Manage ACLs**

This will display the screen: https://cmrailtrail.civicrm.org/civicrm/acl?reset=1

There will be one item on the list which allows the Administrator account to *Edit All Contacts*.

Click on **Add ACL**.

Fill in the form as follows:

* *Description:* Allow access to profiles
* *Role:* Everybody
* *Operation:* Edit
* *Type of Data:* A profile
* *Mode:* Allow
* *Priority:* 2
* *Profile:* All profiles
* *Enabled:* Checked.

Filling out form will apppear as follows:

![ACL Profile Form](/images/ACL_Profile_Form.png)

After saving the above form the Manage ACLs is now displayed as follows, with the second entry providing Everyone having access to Profiles:

![ACL Manage](/images/ACL_Manage.png)

### Testing

* Create a test email. Mailings --> New Mailing
* *Mailing Name:* Test Questionnaire
* *Recipients:* CMRT Test Newsletter
* *Subject:* Test ACL to Questionniare
* *Click -->* Continue
* *Select-->* versafix-1
* *Edit -->* Drop a text block.
* *Select source and paste -->*
```html
<p>Hi {contact.first_name},</p>
<p>This is a test of accessing the CMRT questionnaire.</p>
<p><a href="https://cmrailtrail.civicrm.org/civicrm/profile/edit?gid=17&amp;reset=1&amp;id={contact.contact_id}&amp;{contact.checksum}">Click to go to questionnaire</a></p>
```
* *Test -->* click **Test** and in *Send test email:* enter an email address you have access to.
* *Receive Email -->* Click on the link in email and you should go to the questionnaire and allow updating questionnaire details for this contact.

Note: It seems that *hotmail* can block emails from Spark Essentials or there is something unstable with Spark Essentials *test mailing*, as some emails are not received.
