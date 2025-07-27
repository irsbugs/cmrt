# Guidelines for CiviCRM data.

Draft: Ian 2025-07-25

### Contact Categories

* Individual
* Organisation -> Business
* Organisation -> Community
* Organisation -> Government-Federal
* Organisation -> Government-State
* Organisation -> Government-Local


### Organisation -> Government - Federal Relationship

In CiviCRM, Using *Administer --> Custom Data and Screens --> Relationship Types* the **Electorate** relationship between organisations me be added.

The top-level Federal Organisation is:

* Parliament of Australia

CMRT is interested in the Federal Electoral Divisions in the Castlemaine-Maryborough area:

* Federal Electoral Division of Ballarat
* Federal Electoral Division of Bendigo
* Federal Electoral Division of Mallee


The Organisation -> Goverment-Federal. Consists of only one organisation i.e. Parliament House in Canberra. While Parliament House could remain in CiviCRM database as an organisation, its unlikely anyone will use the data to contact someone in Parliament House. 

From https://en.wikipedia.org/wiki/List_of_Australian_Government_entities there are many "organisations" that would come under "Organisation -> Goverment-Federal", but it looks to me that it would be unlikely there would be direct contact by CMRT and one of these organisation. Most of the federal organisations have equivalents at a Victorian state level. See: https://en.wikipedia.org/wiki/List_of_Victorian_government_agencies so I think that CMRT would be dealing with these state organisations.

In the catagory of Organisation --> Government-Federal, there be *Federal Electoral District of xxxx* organisations like this:

* Federal Electoral Division of Mallee
* Federal Electoral Division of Bendigo
* Federal Electoral Division of Ballerat

See: https://en.wikipedia.org/wiki/Electorates_of_the_Australian_House_of_Representatives

The above Organisations would have a relationship with an individual(s). Normally the MP or their staff.

The above "Organisations" would currently have "Employee of" relationships with these "Inividuals": Anne Webster, Lisa Chesters and Martha Hayett. When these people change (via elections) then the Organisation ramains, and these individuals job title is prefixed with "Former:". Hopefully the newly elected representative supports CMRT so they are added as an individual to their respective organisation. 
 
Also there may be, say, a secretary working for one of these "Member of Parliament" organisations, and they are the CMRT point of contact. The secretary, whose name and email details are known, becomes an "Individual"/"Employee of" their "Member of Parliament" organisation in the CMRT database. Otherwise the secretary would be in a relationship as "Employee of" "Parliament House". This may be true with regards to where their salary comes from, but there could be 10 secretaries in the CMRT database and they wouldn't be in a relationship with their respective "Member of Parliament" organisation. 

In the case of Letters of Support, then these will all come from organisations. The link to the Letter of Support that CMRT received is stored in the Organisation not the individual. E.g. the Letter of Support comes from the *Member of Parliament for Mallee* orgnisation and their letter writer at the time was *Anne Webster*.

**Schools**

Of the six schools in the Letter of Support list, their e-mail addresses end with *.vic.gov.au*. This suggests to me that they should all be under "Orgnisation -> Government-State". There is a word before the *.vic.gov.au* but I suspect this just indicates which mail server the school uses. E.g. "education", "edumail", "highview" and "olivet". i.e. They use a governemnt supplied server or have their own mail server.

If you see https://en.wikipedia.org/wiki/List_of_Victorian_government_agencies It states: *The over 1,500 councils of schools in the state school system are considered individual public entities responsible to the department*. 

Not that there are any at this stage, but I guess non-state schools are in the category "Organisation -> Business".

**Two persons entry as one**

The letter of Support for *Togs Cafe* is from: Elissa Wilsher and Jason Wilsher.

I assume they are co-owners/managers.

Lets say they share an e-mail address like: elissa-and-jason@togs.com.

CiviCRM is really expecting two seperate people with two seperate email addresses, but maybe two "First Names" are suppled:

Maybe the "Individual" entries are:
First Name: Elissa and Jason
Last Name: Wilsher
Email: elissa-and-jason@togs.com

Which is all very good, unless they become CMRT members, which insists on having individual membership (not couples). It also expects different e-mail address for each person.

**To be continued**

Groups and Tags

**Titles**

I thought that few people have titles. However I see there's some *Dr.* E.g. *Dr. Anne Webster*, but she drops the Dr. on her website, and *Cr* which I think is Councillor. Plus I think some want a title of *Hon*.

Maybe instead of entering the "Title" field when loading CSV files, then their *First Name* is prefixed with the title. E.g. First Name: Dr. Anne, Last Name: Webster.

**Job Title**

In most cases a single Individual is employed/volunteer by a single organisation. Thus the Individuals *job title* is simple. E.g. Owner, Propriator, Manager, secretary, etc. of the Organisation.

Does CiviCRM support a single Individual having two job titles and be an employee of two organisation. For example, Peter Strang sent in two Letters of Support. One is from Maldon Cycling where he is the President, and the other from Mt. Alexander Cycling where he is the Secretary. So I'm not sure if CiviCRM supports this or not.





