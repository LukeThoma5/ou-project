---
date: 2024-08-09
week: 32
draft: false
---
Date: Friday, August 09, 2024
# Work Undertaken Summary
0.5hr TMA03 Feedback
1.25 improve heading generation
1.5 System development to output chatlog for inclusion in report.
1hr Export to pdf
0.5 review llama31 8b output and modify to correctness.
1.5hr re-run with only 1 story per generation
1.5hr text comparisons.
0.75 quantitively compare the original and updated
0.5 tutor communications.

# Risks


# Time Spent


# Questions for Tutor


# Next work planned
- Generate using llama3.1 8b hf and feed it only 1 story at a time. See if it picks up the bulk stuff. (It did!).

It worked better when feeding a single story at a time, I guess because it was more focused on the change so was less likely to lose something. It initially worked better when feeding a couple at a time, I guess so it could create a better structure but that's not necessary any more after introducing using headers.

- [story-weaver-output/Leads.xml at llama31-8b-single-story - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/llama31-8b-single-story/Leads.xml)
- Next action: Fixup this and then compare how similar they are. (done!)
- clean up code for display and update the diagrams to match.

# Raw Notes
# Improving Header generation
What if we ran the header generation all at once, and just fed it the entire set of stories in one go.

It is running incredibly slowly to start. It started just trying to produce a summary of the stories, however it started with lead quotation which makes me believe that its lost track of any of the stories before it.
This was tested with llama3.1 70b q8

```
The provided text appears to be a collection of stories or user requirements for a software development project. The stories are related to lead quotations, application quotations, and address management within a customer relationship management (CRM) system.

Here's a brief summary of each story:

1. **Lead Quotation**: The objective is to make the quotation from a Lead look similar to the quotation from an Application. Requirements include showing the main contact, Lead Ref, and Site Address Ref on the Leads List.
2. **Application Quotation**: This story aims to modify the document output when the Applicant clicks on the Print Quotation button to match the Lead Quotation format. Changes include adding a Quotation Ref, wording for quote validity, and removing payment terms and bank details.
3. **Address - create Lead**: This story adds an option to create a lead from an address.
4. **Leads List - from Company and Address**: This story provides access to the Leads List from the Company and Address, allowing users to view leads associated with existing companies or addresses.
5. **For Lead, allow email to all contacts at the Lead Address (whether on the lead or not)**: This story allows users to send emails to all contacts at a lead address, even if they are not explicitly listed as contacts for that lead.
6. **Leads List - show material icons**: This story adds material icons to the Leads List, similar to those used in Jobs, to provide a visual representation of service interests.

Overall, these stories aim to improve the user experience and functionality of the CRM system by streamlining quotation processes, enhancing address management, and adding features for lead management and communication.
```


## Actually improving it
Made some tweaks to the system prompt and used hf-llama31 which is better at following instructions and asked it and got the following result:
[improve heading generation · LukeThoma5/StoryWeaver@27128a2 (github.com)](https://github.com/LukeThoma5/StoryWeaver/commit/27128a214603326077b961533b264f7ae67ae9fd)
```
# Lead Management
## Lead Statuses
## Lead Types

# Lead List View
## Filters
## Sorting
## Lead Status Indicators

# Lead Details View
## Mandatory Fields
## Optional Fields
## Lead Status
## Lead Actions

# Lead Actions and Status Changes
## Actions List
## Add/Edit Actions
## Cancel Lead
## Mark as Lost
## Convert Lead

# Lead Contacts and Integration
## Primary Contact
## Additional Contacts
## Linking Leads to Applications
## Integration with Application Status Changes

# Lead Quotations and Documents
## Lead Quotations
## Application Quotations
## Document Management

# Lead Import and Export
## Bulk Import Leads
## Lead Export

# Lead Address and Company
## Creating Leads from Addresses
## Accessing Leads from Company and Address
```

# Export to pdf
Considered markdown book but only really focused on online.
Ended up using a simple export to single markdown file and then convert with pandoc. Don't reinvent the wheel.

# Text similarity
Referred to: [Text-Similarity-Theory (kaggle.com)](https://www.kaggle.com/code/jurk06/text-similarity-theory)

## **Jaccard Similarities**

`J(A,B) = |A∩B| / |A∪B|`
Similarity of the sets of words, maybe not appropriate for this comparison as the comparison is likely to have the same words, but order and context should matter.

[rapidfuzz/Levenshtein: The Levenshtein Python C extension module contains functions for fast computation of Levenshtein distance and string similarity (github.com)](https://github.com/rapidfuzz/Levenshtein)

## **Cosine Similarities**
convert the document into vectors, and then see if the vectors are pointing in the same direction. A little too abstract for my project I think

## **Levenshtein distance**
Edit distance, how many (insertions, deletions or substitutions) are needed to get to the final text. Maybe should compare it at the word level rather than character.

Could use the `Damerau-Levenshtein ` variant so that blocks of text are allowed to move about. NOT the restricted version e.g. osa. [fuzzt - crates.io: Rust Package Registry](https://crates.io/crates/fuzzt)

Could potentially modify the algo to work based on words not characters.

```rust
use fuzzt::algorithms::{normalized_damerau_levenshtein, normalized_levenshtein};

fn main() {
    // load the files (at build time for simplicity)
    let original = include_str!("original.md");
    let updated = include_str!("updated.md");
    // https://github.com/luizvbo/fuzzt/blob/main/src/algorithms/damerau_levenshtein.rs#L171
    // 1.0 - (dist as f64) / (max(len1, len2) as f64)
    // 1.0 same string, 0 exactly opposite.
    let damerau = normalized_damerau_levenshtein(original, updated);
    let leven = normalized_levenshtein(original, updated);
    dbg!("{} {}", damerau, leven);
}

```

gives values of:
```
[src\main.rs:12:5] damerau = 0.9073965537451647
[src\main.rs:12:5] leven = 0.9072793341929434
```

so 90.7% the same file. So well within our bounds of useful.
# Final Manually fixed
Took me about 15 minutes to review and revise the details.
```
# Leads represent an opportunity for new business for Recolight. Recolight use leads to track potential new customers.

## Leads List Page
### Advanced Search
- Company name
- Company ref
- Lead type
- Priority
- Freerider
- Assigned to
- Next action by
- Created date from/to
- Updated date from/to
- Service interest
- Status

## Lead Details
### Mandatory Fields
- Company (either existing, or new / company name)
- Primary Contact (either existing or new - if new, this will not create a contact in main R3, if existing then it must be one of the company's contacts if for an existing company)
- Source (this will be the existing Application Sources lookup)
- Source Detail
- Priority
- Details
- Recolight Service Interest
- Status (defaults to New)
- Assigned To (user - allow multiple)
- Next Action By (single team)
- Generated By (user selectable from internal users)
- Website

### Other Fields
- Customer Of
- Lead Type
- Freerider
- Created By
- Created Date
- Updated By
- Updated Date

### Lead Companies
- Key Account
- VIP

### Lead Addresses
- Name (mandatory)
- Address line 1
- Address line 2
- Address line 3
- Town
- County
- Postcode (all optional)

### Lead Contacts
- Title
- First name
- Last name
- Phone number
- Email address (all optional)
- Login Email
- Roles
- List of contacts on a Contacts tab for Recolight to be able to add additional contacts

### Communications & Send Emails
- The ability to send emails from the lead details page has been added.
- The email will show the Lead Reference in the email subject.
- The user can set a subject and details (simple multiline text box).
- The subject will default to lead reference.
- The sent email will be added to the communications tab.
-  allow email to all contacts at the Lead Address (whether on the lead or not)

### Actions
- A new task has been added to show the number of open/total actions (like on e.g. Company > Actions tab)

### Notes and Audit
- Ability to add Notes/Comments to a Lead/Opportunity
  - Separate tab for notes
  - Audit of all changes to Leads & Opportunities

### Contacts on Lead
- The Lead will have a Primary Contact, however there will also be a list of contacts on a Contacts tab for Recolight to be able to add additional contacts.
  - Show the number of contacts on the tab header.

### Copy Lead
- The Copy Lead function is now available, allowing users to copy a lead.

## Bulk Leads / Import Leads
### Fields
- Company
- Primary Contact
- Address

### Import Process
- Bulk import leads from a CSV file - via the existing Imports page. Failures to be audited/notified to Recolight.
- Headings can be in any order but must be an exact match.
- Duplicate checking on Company and Contacts.

## Statuses and Transitions
### Status Values
- New
- In Progress
- Converted
- Lost
- Cancelled

### Cancel Lead
- User would set the Status to Cancelled
- User would enter Reason for Cancellation (from Lead Cancellation Reasons list) - mandatory
- Allow Addition of a Comment
- Please log the date/time and user in the background in case this is later needed on reports
- Audit

### Mark as Lost
- User would set the Status to Lost
- User would enter Reason for Loss (from Lead Loss Reasons list) - mandatory
- Allow Addition of a Comment
- Please log the date/time and user in the background in case this is later needed on reports
- Audit

### Conversion
- User would set the Status to "Converted"
- At this point, additional information/fields are mandatory and the lead can't be converted without these - see notes below
- If the Company is inactive or retired on converting the lead, please make the company active
- Please log the date/time and user in the background in case this is later needed on reports
- Audit

Mandatory fields for converting a lead:
- Company must exist or have been created from Lead
- Addresses must exist or have been created from Lead
- Contacts must exist or have been created from Lead
- Lead Type (Recolight Business Type)
- Probability
- Anticipated Closure Date
- Status

## Additional Conversion Information
- If the Lead is for an existing company, but of a different Recolight Business Type (e.g. exists as a Member and the Lead is for a Collection Point), update the Recolight Business Type of the existing record
- Any Lead/Notes, Lead/Documents, Lead/Communications should be copied to any new or existing Company records

## Integration with Applications
- When an application is signed off, the system will alert the user if there are any existing Leads linked to any contacts on the application.
- The check will be on contact last name, contact email or CP site postcode.
- A button will be available to create a link to the Lead on the application sign-off page.
- The Lead/Application reference will show on the Lead overview and Application header.
- A modal will be available to search for a specific Lead if one is known (based on Lead Reference, Company or Address) or to choose one of the paginated options that the system has suggested.
- When an application is cancelled, the associated Lead will be cancelled as well.
- When an application is rejected, the associated Lead will be set to 'lost'.
- There will be the ability to link a Lead to an application from the Lead details page.
- The application-lead date will be a one-to-one relationship (i.e. a lead can only be associated with a single application and vice versa).

## New Lead for Retired/Inactive Company
- A new lead can be created for a retired/inactive company.

## My Quotations
- A new page for external users (customers) to show:
  - Quotation Reference
  - Application Reference (if relevant, not a link)
  - Quotation Date
  - Services
  - Status
  - Assigned To (full name, only those assigned to the lead quotation)
- User should be able to download and print a Quotation.
- Show ALL Quotations for that customer (not user), i.e. external user should see all quotations regardless of who created them and how.
- This is based on lead quotations for any addresses they are linked to.
- For application quotations, don't change the existing logic for who is allowed to view/edit an application.
- Email option, to email the quotation to the customer, internal view only.
- Download option, to download the quotation (both for internal and external users).

## Lead Quotation
- The quotation from a Lead and the quotation from an Application look the same.
- The fact that a quotation exists on an Lead should be clear on the Leads List (new icon?).
- The Quotation produced from a Lead should also show:
  - The main contact
  - The Lead Ref (at present it only shows the Quotation Ref) in the format:
    Quotation Ref Q4 (LE21)
    so not specifically naming the Lead Ref

## Application Quotation
	- The document output when the Applicant clicks on the Print Quotation button, should be called ‘Quotation’ and show ‘Quotation Details’ not ‘Order Details’
  - This document should show:
	    - The wording ‘Quotes are valid for 7 days, subject to availability’
    - The Site Address Ref (it already shows the Company Ref)
    - The Charge and Service columns should be in the other order to match the quotation from the Lead
    - A Quotation Ref (as on the Lead Quotation) - The system will give the quotation a new quote reference each time the applicant (or other user) clicks the "Print Quotation" button on an application (regardless of whether or not any changes have been made to the application).
  - The Payment Terms and Bank details should be removed the Application Quotation
  - A copy of this document should be placed in the tab Application/Documents. Note that this would be added every time the user downloads a Quote document (so there could be multiple/duplicates if they do it more than once).

## Lead - Create from Address
- A new option has been added to create a lead from an address.
- A new tab on the Company and Address for Leads is available, showing only Leads for existing Companies/Addresses.

### New Feature
- The Leads List page now shows material icons as per Jobs in the LHS.
```

# Manually modified documentation Failure
This was built up from the documentation generated by https://gitea.4man.dev/lukethoma5/story-weaver-output/commits/branch/final-llama31-70b however I noticed that it was missing stuff like lead company and lead address. So the smaller model actually did better.
```
# Leads
Leads represent an opportunity for new business for Recolight.
Recolight use leads to track potential new customers.

## Leads List Page
- The Lead List view shows Customer Of (as per Cases).
- Sorting: tbc
- Icon indicating if a quotation exists on the Lead
- Material icons are displayed in the LHS of Leads List, as per Jobs.
### Advanced Search
- General text search for reference
- company name
- company ref
- lead type
- priority
- freerider
- assigned to
- next action by
- created date from/to
- service interest

## Lead Details
### Mandatory Fields

- Company (either existing, or new / company name)
- Source (this will be the existing Application Sources lookup)
- Priority
- Details
- Recolight Service Interest
- Status - defaults to New
- Assigned To (user - allow multiple)
- Next Action By (single team)

### Other Fields

- Primary Contact (either existing or new - if new, this will not create a contact in main R3, if existing then it must be one of the company's contacts if for an existing company) 
- Source Detail - TBC
- Lead Key account/VIP 
- Application Reference (displayed on Lead overview page)
- Probability
- Anticipated Closure Date

### Linked Applications

- A lead can only be associated with a single application and vice versa.
- The system will alert the user on the application sign-off page if there are any existing Leads linked to any contacts on the application.
- A button to create the link to the Lead on the application sign off page.

### Cancelling or Rejecting an Application

- When an application is cancelled, the associated lead's status will be set to 'cancelled' with cancellation reason 'Application cancelled'.
- When an application is rejected, the associated lead's status will be set to 'lost'.

## Lead Status Changes

- If a lead is only for Recolight Business Type of Collection Point and its associated application is approved or cancelled, the lead's status will be updated accordingly.

### Converting a Lead
- User would set the Status to "Converted"
- Mandatory fields: Company, Addresses, Contacts, Lead Type (Recolight Business Type), Probability, Anticipated Closure Date

### Cancelling a Lead
- User would set the Status to Cancelled
- Reason for Cancellation - Application cancelled or rejected 
- Additional Reason for cancellation is required.

## My Quotations List 

- Show ALL Quotations for that customer (not user), i.e. external user should see all quotations regardless of who created them and how.
- Each quotation will show: Quotation reference, date, status, lead/application reference (if applicable) 
- Option to download a quotation in PDF format
- Internal users can email the quotation directly from this page

### Email Quotations 

- Simple email with quote attached 
- If the Quotation is from an Application, then the email should only go to the Applicant.
- For quotations that come from Leads created in the Leads screen, there should only be one contact, but in the event there are more, only send to the first (added).
- Email format will include ‘Quotes are valid for 7 days, subject to availability’

### Quotation Document

- The quotation document output when the Applicant clicks on the Print Quotation button should show:
    - Quotation Ref
    - Site Address Ref (in addition to Company Ref)
    - Charge and Service columns in reverse order
    - ‘Quotes are valid for 7 days, subject to availability’
- The Payment Terms and Bank details will be removed from the Application Quotation.
- A copy of this document should be placed in the tab Application/Documents. 

### Applications List
- An icon indicating that a quotation exists on an Application


## Company and Address
- Leads List tab available, showing only leads for existing Companies/Addresses

### Address
- Option to create a lead

## Emailing Leads 
- For a Lead, it is possible to email all contacts at the Lead Address (whether on the lead or not)

```

# Manual Modification Success
Was missing some details that were only present on the wireframes, would need a multimodal llm to fix that.
Had to add information for bulk leads, seems to have gotten missed, maybe because too many stories were generated together? To try doing them separately.
Based off: [story-weaver-output/Leads.xml at final-llama-31-8b - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/final-llama-31-8b/Leads.xml)
```
# Leads
## Overview
Leads represent an opportunity for new business for Rcolight. Recolight use leads to track potential new customers.

## Leads List Page
- Material icons are shown in the LHS of the Leads List page
### Advanced Search
- Company name
- Company ref
- Lead type
- Priority
- Freerider
- Assigned to
- Next action by
- Created date from/to

## Lead Details
### Mandatory Fields
- Company (either existing, or new / company name)
- Primary Contact (either existing or new - if new, this will not create a contact in main R3, if existing then it must be one of the company's contacts if for an existing company)
- Source (this will be the existing Application Sources lookup)
- Source Detail
- Priority
- Details
- Recolight Service Interest
- Status - defaults to New
- Assigned To (user - allow multiple)
- Next Action By (single team)
- Website
- Generated By (user selectable from internal users)

### Other Fields
- Lead Companies
- Lead Addresses
- Additional Information

### Lead Companies
- Name (mandatory)
- Main Business Type
- Key Account/VIP (checkbox for new addresses, sub-sectors that would be selected by the user for new addresses)

### Lead Addresses
- Name (mandatory)
- Address line 1
- Address line 2
- Address line 3
- Town
- County
- Postcode (all optional)

### Additional Information
- Created By
- Created Date
- Updated By
- Updated Date

### Lead Contacts
- Title
- First name
- Last name
- Phone number
- Email address
- Login Email
- Roles (all optional)

## Bulk Leads / Import Leads
- Bulk import leads from a CSV file - via the existing Imports page. Failures to be audited/notified to Recolight.
- Headings can be in any order but must be an exact match.
- Duplicate checking on Company and Contacts.

## Statuses and Transitions
### Status Values
- New
- In Progress
- Converted
- Lost
- Cancelled

### Cancel Lead
- When an Application is cancelled, set Lead status to 'cancelled' with cancellation reason 'Application cancelled'
- User can enter Reason for Cancellation (from Lead Cancellation Reasons list) - mandatory
- Allow Addition of a Comment
- Log the date/time and user in the background in case this is later needed on reports
- Audit

### Mark as Lost
- When an Application is rejected, set Lead status to 'lost'
- User can enter Reason for Loss (from Lead Loss Reasons list) - mandatory
- Allow Addition of a Comment
- Log the date/time and user in the background in case this is later needed on reports
- Audit

### Conversion
#### Convert Lead to Opportunity
##### Mandatory Fields for Conversion
- Company must exist or have been created from Lead
- Addresses must exist or have been created from Lead
- Contacts must exist or have been created from Lead
- Lead Type (Recolight Business Type)
- Probability
- Anticipated Closure Date
- Status

## Send Email
### Email Functionality
- Send email from within a Lead
- Email subject defaults to Lead Reference
- User can set subject and details
- Add sent email to communications tab
- Users can send an email to all contacts at the Lead Address (whether on the lead or not).

## Quotations and Applications
### Creating and Editing Quotations and Applications
#### Printing and Emailing Documents
- External users can view and download quotations
- External users can email quotations to customers
- Internal users can print and email quotations
- Quotations can be downloaded in a basic format
- Quotations will include the Recolight logo, company name, address, phone, VAT number, and a free format detail section

#### Linking Leads and Applications
##### Duplicate Check and Suggestion Modal
- The system will alert the user on the application sign-off page if there are any existing Leads linked to any contacts on the application
- The check will be on contact last name, contact email, or CP site postcode
- A button to create the link to the Lead on the application sign off
- The Lead/Application reference will show on the Lead overview and Application header rather than on the individual Contacts
- The modal will allow searching for a specific Lead if one is known (based on Lead Reference, Company, or Address) or alternatively choosing one of the paginated options that the system has suggested
- Clicking on a Lead will fill the green box with details on the Lead to allow an informed decision for if they are the same Lead/Application
- Additionally showing why the system is suggesting the Lead to help with decision making

## Contacts on Lead
- Primary Contact
- List of contacts on a Contacts tab
- Show the number of contacts on the tab header

## Quotation from Lead
- The quotation from a Lead and the quotation from an Application will look the same
- The fact that a quotation exists on an Lead will be clear on the Leads List (new icon)
- The Quotation produced from a Lead will also show:
  - The main contact
  - The Lead Ref (at present it only shows the Quotation Ref) in the format: Quotation Ref Q4 (LE21)
  - Where the Lead is for an existing site, the Site Address Ref

## New Features
- Users can create a new Lead from an address.
- Users can access the Leads List from the Company and Address page.
```

# Exporting chat
```
<|begin_of_text|><|start_header_id|>system<|end_header_id|>

Cutting Knowledge Date: December 2023
Today Date: 26 Jul 2024

You are a helpful assistant tasked with creating a description of a vertical slice of a software system.
You never hallucinate information, if you are unsure you omit the information.
The user will descibe what the area of the system relates to, the current description of the area and a list of stories that have been completed.
You will then provide a new description of the area that includes all original information if not contradicted and only the relevant information from the new stories.
The user will provide the current version of the description between [description] and [end description].
Stories are delimited by the [story] and [end story] token.
You will output ONLY the complete new description of the area, including all original headings.
You will NOT remove any information from the existing description.
Output in markdown format, using bullet point lists and headings.
Use the headings provided in the description, do not remove headings.
All information must be presented under a relevant heading.
Write in the present tense.<|eot_id|><|start_header_id|>user<|end_header_id|>

Describe Applications
[description]
Applications is a form which propspective users fill out to request services.[end description]
[story]Applicants can create a user to complete the application[end story]
[story]Existing applicants can see a list of applications and can create or edit their applications[end story]
[story]Internal users can see a list of applications, edit or approve.[end story]<|eot_id|><|start_header_id|>assistant<|end_header_id|>

Applications is a form which propspective users fill out to request services.
From the applications list applicants and internal users can:
- Create
- Edit

Internal users can:
- Approve<|eot_id|><|start_header_id|>user<|end_header_id|>

Describe the Leads functional area.
[description]
Leads represent an opportunity for new business for Rcolight.
Recolight use leads to track potential new customers.
# Leads List Page
## Advanced Search

# Lead Details
## Mandatory Fields
## Other Fields
## Lead Companies
## Lead Addresses
## Lead Contacts
## Additional Information

# Bulk Leads / Import Leads
## Fields
## Import Process

# Copy Lead

# Statuses and Transitions
## Status Values
## Cancel Lead
## Mark as Lost

## Conversion
### Convert Lead to Opportunity
#### Mandatory Fields for Conversion

# Send Email

# Quotations and Applications
## Creating and Editing Quotations and Applications
### Printing and Emailing Documents
## Linking Leads and Applications
### Duplicate Check and Suggestion Modal[end description]
[story][Title]Leads List & Details views[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]See attached wireframes.

We are not having Opportunities as a separate concept now. Use 'LE' as prefix for lead reference.

User needs to be able to select an existing company or enter the name of a new company (this will not create a new company in R3 - this will be manual, or via an application, when they are ready to do so). If the Company is an existing Company, need to also show the Customer Of from the Company in the typeahead.
  
User needs to be able to select an existing address (if it is an existing company) or enter a new address using postcode lookup or manual entry, similar to e.g. applications (this will not create a new address in R3 - this will be manual, or via an application, when they are ready to do so).

This PBI includes:
  
- List view, add, view details of leads - The Lead List view needs to show Customer Of (as per Cases)
- Filters:
    - General text search for reference
    - company name, company ref, lead type, priority, freerider, assigned to, next action by, created date from/to, service interest
- Sorting:
    - tbc

Save the Created By, Created Date, Updated By, Updated Date. Update the Updated Date / By if any fields are changed.

Lead Statuses are:

1. New
2. In Progress
3. Converted - extra functionality around setting this status is covered under another PBI
4. Lost - extra functionality around setting this status is covered under another PBI
5. Cancelled - extra functionality around setting this status is covered under another PBI

Mandatory fields are:

- Company (either existing, or new / company name)
- ~~Primary Contact~~ (either existing or new - if new, this will not create a contact in main R3, if existing then it must be one of the company's contacts if for an existing company) [Riley - Membership have advised there are time when they do not have a contact name, just a company name, so contact will have to be optional]
- Source (this will be the existing Application Sources lookup)
- Source Detail - TBC, asked on Trello to confirm
- Priority
- Details
- Recolight Service Interest
- Status - defaults to New
- Assigned To (user - allow multiple)
- Next Action By (single team)[End Requirements]
[Comment 0 by Lucy]for actions should show total number like 131948[End Comment 0 by Lucy]
[Comment 1 by Lucy]Confirmed with Leslie:   1) Swimlane is not a thing.   2) Created By/Updated BY should have same layout as cases       Assumed:   1) Use same date format as cases[End Comment 1 by Lucy]
[Comment 2 by Lucy]How does Lead Key account/VIP work? a) Is it for existing company/address its if company/address is key/vip b) What to do for new address? checkbox for key account. checkbox for vip? Or do they need to select subsectors? Would they select only the special subsectors or can they select any subsector. [Riley - Key Account/VIP are only for companies/addresses that exist (already or created for new companies/addresses. They are sub-sectors that would be selected by the user for new addresses (they are Recolight Business Type Sub-Sectors). The user would select Key Account, VIP and any others that are relevant] 2) What fields are required to be stored for a "Lead only address" [Riley - name (mandatory), address line 1, address line 2, address line 3, town, county, postcode (all optional)] 3) What fields are required to be stored for a "Lead only contact" [Riley - title, first name, last name, phone number, email address (all optional)] 4) What filters are required in the advanced search? [company name, company ref, lead type, priority, freerider, assigned to, next action by, created date from/to, service interest][End Comment 2 by Lucy]
[Comment 3 by Lucy]New UAT Task - 142198[End Comment 3 by Lucy]
[Comment 4 by Leslie]One more task to be included in Release 75 ([UAT] Contact during add modal and make address optional)[End Comment 4 by Leslie]
[end story]
[story][Title][DUP] Leads & Opportunities - Convert, Cancel, other Status changes[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]None[End Requirements]
[Comment 0 by Lucy]Further comments from https://trello.com/c/FCERszwH/111-leads-list-views-add-edit-addresses-contacts-20220802       3d, If the Lead is for an existing company, but of a different Recolight Business Type (e.g. exists as a Member and the Lead is for a Collection Point), update the Recolight Business Type of the existing record 3e, Any Lead/Notes, Lead/Documents, Lead/Communications should be copied to any new or existing Company records[End Comment 0 by Lucy]
[Comment 1 by Leslie]Duplicate of 144416[End Comment 1 by Leslie]
[end story]
[story][Title]Leads & Opportunities - Documents[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]None[End Requirements]
[end story]
[story][Title]Leads & Opportunities - Communications[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]None[End Requirements]
[end story]
[story][Title]Leads & Opportunities - Actions[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]None[End Requirements]
[Comment 0 by Leslie]New task added to show the number of open/total actions (like on e.g. Company > Actions tab)[End Comment 0 by Leslie]
[end story]
[story][Title]Leads & Opportunities - Notes/Audit[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]1, Ability to add Notes/Comments to a Lead/Opportunity

1a, Separate tab

1b, Replicate functionality on other Notes/Comments tabs

1c, Tab to also show audit of all changes to Leads & Opportunities (per other Audits)[End Requirements]
[Comment 0 by Lucy]Ready for testing: Notes tab add / edit + audit notes showing       Audit notes still WIP e.g. company/address/contact still missing[End Comment 0 by Lucy]
[end story]
[story][Title]Leads Lookups[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]New lookups, which will be used on Leads, as follows:
  
- New Reasons type lookup of "Lead Cancellation" (with other Reasons lookups)
- New Reasons type lookup of "Lead Loss" (with other Reasons lookups)
- Lead Probability[End Requirements]
[Comment 0 by Lucy]And Service Interest[End Comment 0 by Lucy]
[Comment 1 by Leslie]Note that the CRM Lookups tiles are currently all singular, where the other tiles are plural - leave this as is, but need to change the Add/Edit functionality as described in bug details to make it consistent across the CRM lookups at least.[End Comment 1 by Leslie]
[end story]
[story][Title]Leads Project Management & Wireframing[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]None[End Requirements]
[Comment 0 by Leslie]Excludes time previously spent on proposals, discussions, wireframes etc. prior to sign off[End Comment 0 by Leslie]
[end story]
[story][Title]Contacts on Lead[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]The Lead will have a Primary Contact, however there will also be a list of contacts on a Contacts tab for Recolight to be able to add additional contacts.
  
Show the number of contacts on the tab header.[End Requirements]
[Comment 0 by Leslie]Awaiting confirmation from Recolight on which fields are needed on a lead contact[End Comment 0 by Leslie]
[Comment 1 by Lucy]3) What fields are required to be stored for a "Lead only contact" [Riley - title, first name, last name, phone number, email address (all optional)][End Comment 1 by Lucy]
[Comment 2 by Lucy]Riley has confirmed that contact can't be mandatory as members don't always have a contact. We added contact to the main modal because it was mandatory, we are removing it now to keep the modal simpler.       If they ask for it in the future we can add contact to the add-lead screen but should not have it on edit as it would be ambigious if they are trying to update the details of person A or change the "primary" contact to a new person B (but still want to keep person a)[End Comment 2 by Lucy]
[Comment 3 by Lucy]Riley confirmed on call that they should be able to not have a contact, but if they do require that they have input atleast a last name as they may not have much more detail than this. (They obviously need more detail before it can be converted).       Also he confirmed that if the lead is for an existing company we will limit existing contact to that company. However if for a new company they can choose any existing contact (with email and primary address to disambiguate) just like on the internal company > add contact modal.[End Comment 3 by Lucy]
[end story]
[story][Title]Copy Lead function[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]None[End Requirements]
[Comment 0 by Lucy]Functionality is ready, waiting for confirmed list of copyable fields.[End Comment 0 by Lucy]
[end story]
[story][Title]Leads & Opportunities - Bulk Add Leads[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]Add the ability to bulk import leads from a CSV file - via the existing Imports page.

The system would look through the headers to identify the data, so the headings can be in any order but must be an exact match in terms of the column heading wording.

Failures to be audited/notified to Recolight, as per other imports.

We need duplicate checking on Company and Contacts.

See attached example - ignore any fields that we don't have in RecoWeb (mostly the last set of columns).[End Requirements]
[Comment 0 by Lucy]For initial implementation we will only do for existing companies / addresses / contacts.       This will be expanded to create lead companies/addresses/contacts once we have confirmed what detail will be added.[End Comment 0 by Lucy]
[Comment 1 by Billie]check deploy please[End Comment 1 by Billie]
[Comment 2 by Alex]Deployment is fixed now New permissions required[End Comment 2 by Alex]
[end story]
[story][Title]Leads & Opportunities - Send Email[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]In the same way it is possible to send an email from within an Application or Case, it should be possible to send an email from within a Lead.

The email should show the Lead Reference in the email subject.

Allow the user to set a subject and details (simple multiline text box).

Subject to default to lead reference.[End Requirements]
[Comment 0 by Lucy]Add the sent email to the communications tab.[End Comment 0 by Lucy]
[end story]
[story][Title]Leads - List views, Add/Edit, Addresses & Contacts 20220802[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]Add Website To Lead

Add "Generated By" to Lead [Lucy - the person responsible for drumming up the business]

There will be options for Create Company, Create Address, Create Contacts.

For Create Company, it would open the create company modal and the user would complete missing mandatory fields, as if creating a company from the company list screen.

Same for create address.

For create contacts, it would automatically create all contacts/users (when the single create button is pressed on contact list) as we assume we would already have the mandatory fields for contacts on the lead. (Added login email and roles)

The lead must be for an existing company before you can make the address, the address must be made before you can make the contacts.

Background - Member leads will be converted into actual Companies/Contacts/Addresses using the above modals. Collection Point leads will be converted into the above using applications (another story).[End Requirements]
[Comment 0 by Leslie]The Login Email is not currently a field on the Lead Contact. Recolight would like us to add this, along with Roles. A single button would create all contacts and would also create users for any contacts where the Login Email and Role fields have been entered.[End Comment 0 by Leslie]
[Comment 1 by Leslie]From Riley on Trello: Agreed that it makes sense to keep Created By as the automatically generated field, and add a new field Generated By which is user selectable from internal users.[End Comment 1 by Leslie]
[Comment 2 by Leslie]Lead Generated By and Website in Release 74.5[End Comment 2 by Leslie]
[end story]
[story][Title]Leads & Opportunities - Integration with Applications[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]We will not create any leads from applications (as applications will be included in lead reporting unless linked to a lead).

Instead, the system will alert the user on the application sign-off page if there are any existing Leads linked to any contacts on the application. The check would be on contact last name, contact email or CP site postcode.

This will be done from the sign off page and will be available from the "Application Quotation cut down" sign off page as well.

Having a button to create the link to the Lead on the application sign off.

Suggestion is to have the Lead/Application reference show on the Lead overview and Application header rather than on the individual Contacts. Allowing for future expansion on what the duplicate check is made on.

The modal will allow searching for a specific Lead if one is known (based on Lead Reference, Company or Address) or alternatively choosing one of the paginated options that the system has suggested. Clicking on a Lead will fill the green box with details on the Lead to allow an informed decision for if they are the same Lead/Application. Additionally showing why the system is suggesting the Lead to help with decision making.

(Note that it will only show one of the three options, i.e. 1) There is no linked Lead or 2) there is no linked Lead and the system has identified a possible link or 3) there is a linked Lead.

Riley - if an Application for a Lead that is ONLY Recolight Business Type of Collection Point, is cancelled, the associated Lead should be cancelled as well.

No limitations on which leads/applications can be linked (either based on status or date).

There would also be the ability to link a Lead to an application from the Lead. This way, the linking can be done on bulk imported leads, manually created leads, and at any point during the lead processing.  

The application-lead date would be a one-to-one relationship (i.e. a lead can only be associated with a single application and vice versa).
  
![](download-url-not-generated-yet)![](https://redriversoftware.tpondemand.com/Attachment.aspx?AttachmentID=21924)[End Requirements]
[Comment 0 by Lucy]Still to do (waiting on lead status changes story):   Whe approving the application convert the lead. (Agreed that we won't be converting the lead on approval with Leslie 8/11/22. Thinking is its a can of worms and we've previously mentioned on calls that we won't have all the mandatory fields needed to convert the lead, and more are likely to be created later).   Choosing an approved application converting the lead. Unlinking setting the lead back to in progress..    When cancelling an application cancel the lead, unlinking the lead set back to in progress.   [Edit: There was nothing in the trello card about what happens when you link leads together, safest thing is to do nothing as if they're linking after approval/cancellation they are manually intervening so we should let them fix the data. Agreed with Leslie 8/11/22][End Comment 0 by Lucy]
[Comment 1 by Lucy]Outstanding questions   1) Does rejecting an applicaiton set the lead to cancelled or lost? [Riley call 8/11/2022. Riley to confirm] 2) Regarding only updating if a collection point only lead, does this apply for approval (converting the lead) as well?[End Comment 1 by Lucy]
[Comment 2 by Lucy]Per discussion this morning, have confirmed with Customer Services:  1, When Application is cancelled, set Lead status to 'cancelled' with cancellation reason 'Application cancelled' 2, When Application is rejected, set Lead status to 'lost'[End Comment 2 by Lucy]
[end story]
[story][Title]Leads - Allow a new Lead for a retired/inactive Company[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]An inactive/retired status Company may be/have a new Lead, which when the Lead is converted, would mean the Company would be updated to active status.

This PBI is for allowing the user to select an inactive/retired company when adding a new Lead.[End Requirements]
[end story]
[story][Title]Leads & Opportunities - Convert, Cancel, other Status changes[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]This PBI is to cover Lead status changes as follows:
  
1. Cancel Lead
    - User would set the Status to Cancelled
    - User would enter Reason for Cancellation (from Lead Cancellation Reasons list) - mandatory
    - Allow Addition of a Comment
    - Please log the date/time and user in the background in case this is later needed on reports
    - Audit
2. Mark as Lost
    - User would set the Status to Lost
    - User would enter Reason for Loss (from Lead Loss Reasons list) - mandatory
    - Allow Addition of a Comment
    - Please log the date/time and user in the background in case this is later needed on reports
    - Audit
3. Convert Lead
    - User would set the Status to "Converted"
    - At this point, additional information/fields are mandatory and the lead can't be converted without these - see notes below
    - If the Company is inactive or retired on converting the lead, please make the company active
    - Please log the date/time and user in the background in case this is later needed on reports
    - Audit

Mandatory fields for converting a lead:

- Company must exist or have been created from Lead
- Addresses must exist or have been created from Lead
- Contacts must exist or have been created from Lead
- Lead Type (Recolight Business Type)
- Probability
- Anticipated Closure Date
- Status[End Requirements]
[Comment 0 by Billie]new task added[End Comment 0 by Billie]
[Comment 1 by Leslie]New task added for Cancellation/Loss Comments, plus a new bug to be looked at[End Comment 1 by Leslie]
[end story]
[story][Title]Leads & Opportunities - print and email Quotations[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]"My Quotations" page for external users (customers) to show:
  
- Quotation Reference
- Application Reference (if relevant, not a link)
- Quotation Date
- Services
- Status
- Assigned To (full name, only those assigned to the lead quotation, this is so they know who to speak to if they want to discuss the quotation)

User should be able to download and print a Quotation.

Show ALL Quotations for that customer (not user), i.e. external user should see all quotations regardless of who created them and how. This is based on lead quotations for any addresses they are linked to.

For application quotations, don't change the existing logic for who is allowed to view/edit an application. ~~If the user is able to view/edit the application the list will include a clickable link for the application ref. Otherwise they'Leslie only have the option to see the quote in the list and download the quote from the my quotes list. ~~[Lucy - We are showing the application in the list if they are a contact on the application, the applicant or they belong to an address on the application]
 
 Email option, to email the quotation to the customer, internal view only. This will be a simple email with quote attached. See attached Email Formats spread sheet, tab R3-35. 

New comment on Trello: When the Quotation is from an Application, then the email should only go to the Applicant (If the applicant is doing the quote on behalf his customer and they are one of the contacts on the application … we don’t know if they’re quoting them a different price. So to avoid any complaints the quotation should only go to the applicant and they can decide what they’re going to charge). For quotations that come from Leads created in the Leads screen, there should only be one contact, but in the event there are more, only send to the first (added).

Download option, to download the quotation (both for internal and external users). The quotation layout is a basic format (e.g. Recolight header and footer, with a free format detail section). See attached. Re quotation template, suggestion is the system prints:

a. The logo, company name/address/phone/VAT number and heading Quotation
 b. The Payment Terms/BACS details (new bank account number)/validity period/message to accept quote and proceed/message re containers

The part in the middle where the services/charges/etc. is shown, is the free format section.[End Requirements]
[Comment 0 by Leslie]Requested email text and download layout[End Comment 0 by Leslie]
[Comment 1 by Lucy]show lead quotes, and then also show application quotes different lines. But if a lead quote has an application then have that show on the lead quote line.[End Comment 1 by Lucy]
[Comment 2 by Leslie]Question on whether My Quotations list should show applications without a quotation. Some further changes coming in later PBIs (awaiting sign off).[End Comment 2 by Leslie]
[end story]
[story][Title]Lead Quotation[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]The objective is that the quotation from a Lead and the quotation from an Application look the same.

1, The fact that a quotation exists on an Lead should be clear on the Leads List (new icon?)

2, The Quotation produced from a Lead should also show
 2a, The main contact
 2b, The Lead Ref (at present it only shows the Quotation Ref) in the format:

Quotation Ref Q4 (LE21)

so not specifically naming the Lead Ref

2c, Where the Lead is for an existing site, the Site Address Ref[End Requirements]
[Comment 0 by Leslie]See also 152489 - Application Quotation[End Comment 0 by Leslie]
[end story]
[story][Title]Application Quotation[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]The objective is that the quotation from a Lead and the quotation from an Application look the same.

1, The document output when the Applicant clicks on the Print Quotation button, should be called ‘Quotation’ and show ‘Quotation Details’ not ‘Order Details’
 1a, This document should show:
 1a.i, The wording ‘Quotes are valid for 7 days, subject to availability’ (as on the Lead Quotation)
 1a.ii, The Site Address Ref (it already shows the Company Ref)
 1a. iii, The Charge and Service columns should be in the other order to match the quotation from the Lead

1a. iv, A Quotation Ref (as on the Lead Quotation) - The system will give the quotation a new quote reference each time the applicant (or other user) clicks the "Print Quotation" button on an application (regardless of whether or not any changes have been made to the application).

1b, The Payment Terms and Bank details should be removed the Application Quotation
 2, A copy of this document should be placed in the tab Application/Documents. Note that this would be added every time the user downloads a Quote document (so there could be multiple/duplicates if they do it more than once).

Note - none of the above should change the existing Service Request document produced when the Application has been fully completed and submitted

3, The fact that a quotation exists on an Application should be clear on the Applications List (new icon)[End Requirements]
[Comment 0 by Leslie]See also 152319 - Lead Quotation[End Comment 0 by Leslie]
[end story]
[story][Title]Address - create Lead[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]Add option to create lead from an address[End Requirements]
[Comment 0 by Lucy]implemented by 348481[End Comment 0 by Lucy]
[end story]
[story][Title]Leads List - from Company and Address[End Title]
[Type]Change Request[End Type]
[Customer Description]Provide access to the Leads List from the Company and Address

This a new tab on the Company and Address for Leads? (we have assumed this in the SWAG).

This would only show Leads for existing Companies/Addresses.[End Customer Description]
[Requirements]None[End Requirements]
[end story]
[story][Title]For Lead, allow email to all contacts at the Lead Address (whether on the lead or not)[End Title]
[Type]Change Request[End Type]
[Customer Description]None[End Customer Description]
[Requirements]None[End Requirements]
[end story]
[story][Title]Leads List - show material icons[End Title]
[Type]Change Request[End Type]
[Customer Description]In LHS of Leads List show the material icons as per Jobs[End Customer Description]
[Requirements]Add Material Group to the Service Interest Lookup optional on the service interest (Due to membership service interest).

If missing material group / no service interests, the icon would not show on the leads LHS.[End Requirements]
[end story]<|eot_id|>
```

# Email To Tutor
Hi Amanda,

The project work is nearing completion and I am starting to focus on writing my final assignment.
In the last week I've improved the generation of headings (through improvements to the system prompt) which is the starting point of the documentation generation.

I've tweaked the generation of the documentation to enforce it occurs a single story at a time, as this helped the LLM focus more on the individual stories and resulted in better output (at the expense of longer generation times).

I've ran the final generation of the documentation, created the revised version off the back of it and validated that the revised version is 90% the same (using normalised levenshtein) as the initial version, which is significantly better than the benchmark I had set for the tool to be deemed useful :).

'All' that is left is a little bit of code clean-up and an awful lot of report writing. I'm sure I'll be in touch with questions regarding the EMA in the coming weeks.

My latest project logbook is available at:

Best Regards,
Luke