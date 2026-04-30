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
<a href="https://cmrailtrail.civicrm.org/civicrm/mailing/url?u=167&qid=980&id=400&cs=9617662130870fa4676132bbe5e841e7_1777457844_336">Click to go to questionnaire</a>
```

In the above the query string contains:
* u=167 <-- Internal *URL ID* in the mailing system
* qid=980 <-- Queue ID (which specific email instance was sent to which contact)
* id=400 <-- Contact ID
* cs=9617662130870fa4676132bbe5e841e7_1777457844_336 <-- Checksum

