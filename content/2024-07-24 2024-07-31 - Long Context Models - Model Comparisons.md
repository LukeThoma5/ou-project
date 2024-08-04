---
date: 2024-07-24
week: 30
draft: false
---
Date: Wednesday, July 24, 2024
# Work Undertaken Summary
- split out functionality from model into a formatter class
- made changes to allow per heading and global generation to exist simultaneously for back and forth testing
- tweaked prompt for better output
- ran with new llama3.1 models
- Ran with final prompt and headings on a range of available LLMs

# Time Spent
- 2hrs refactoring formatting class
- 1.5hr running the models
- 1.25 running 70b
- 2hr tweaking generation
- 3.5hr generating on new models
- 3.5hr generating with llama70b
- 1.25hr generating with gemma2
- 0.75 mistral nemo
- 2.25 generating mistral large
- 2.5hr generating command-r-plus
- 0.35 phi3
- 0.75 EMA tutorial
- 0.5 Tutor emails
# Questions for Tutor


# Next work planned
1) [x] llama31
2) [x] Mistral-Nemo-Instruct-2407
3) [x] mistral large?
4) [x] phi3 medium ollama?
5) [x] command-r+
6) [x] llama31 70b for heading generation with ollama
7) [x] try and get the ollama output to match the normal one. Can then try and do another 70b.
- [ ] clean up code, document
- [ ] add support for creating a document from markdown
- [ ] Make alterations to generated document and compare.

# Raw Notes

# Final outputs:
Generated at this commit
https://github.com/LukeThoma5/StoryWeaver/tree/c2e94e179276bd5dfd98d0ecf7fa7de7eb299be2
## llama31 8b hf q8
https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/final-llama-31-8b/Leads.xml

## llama31 70b q8
https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/final-llama31-70b/Leads.xml
This one is really good!

## gemma2 27b q8
https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/final-gemma2_9b/Leads.xml
It's missing the advanced search fields and past a certain point just starts rambling.

## mistral nemo q8
mistral-nemo:12b-instruct-2407-q8_0
From 12pm -> 12:45
https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/final-mistral-nemo/Leads.xml

Did really well to begin with, formatted things very well and included some good information. BUT it was delete happy and really biased its output to the latest information, so as soon as a lot of information about applications was presented it overran the leads information see commit: https://gitea.4man.dev/lukethoma5/story-weaver-output/commit/db5123b31fa6a3628a66eae14ff568566e889d16

## mistral large q4
mistral-large:123b
from 12:45-> 3:15 for 6 commits worth. Has the same issue as the nemo where it completely removes important information. See commit:
[143245 in Leads - Leads & Opportunities - Integration with Applications · a58491c745 - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/commit/a58491c7452ba1b618de9c7570495e7862cd6d38)

bailing the generation as its done 6 commits in 3 hours and is already gone wrong.

Note potential issues with license that would prevent this from being used in a commercial product so wouldn't be usable if subsumed by pepper.

## command-r plus q4
from 3:15 to...5:45 to do the same as mistral large. Had the same problem of deleting stuff / only caring about the more recent stuff. It might be due to the harsher quantization (q4 rather than q8 for e.g. the 70b models).
https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/final-command-r/Leads.xml

## phi3-medium q8
Completely died during generation. A couple of commits in it started generating some python to implement the feature rather than create some documentation. When the code was fed back in on the next iteration it tried to produce a plan for a workshop on digital literacy and cybersecurity awareness.

![[#phi3 failings]]
# Findings

When llama3 was ran with some generated headers, it didn't go off the rails and start copy pasting comments in. Maybe it just needed more structure.

Will retest with an "empty" to confirm. And then can test with the new llama31 to see if it does any better.

## llama3 with headings
[story-weaver-output/Leads.xml at 2024-07-24-llama3 - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/2024-07-24-llama3/Leads.xml)


## llama3.1 with headings
[story-weaver-output/Leads.xml at 2024-07-24-llama31-8b - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/2024-07-24-llama31-8b/Leads.xml)

## llama3-0 without headings
[story-weaver-output/Leads.xml at 2024-07-24-llama3-blank-no-headings - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/2024-07-24-llama3-blank-no-headings/Leads.xml)

It's not just devolving into rambling like it did prior to TMA03. What gives. It's definitely got less structure than when it was given the headings from the start.

this is the output I got for TMA03: [story-weaver-output/Leads.xml at tma03 - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/tma03/Leads.xml)

It includes a lot of information about quotations that it is missing on the current run through.

TODO determine why this commit: [147949 in Leads - Leads & Opportunities - print and email Quotations · 446aed67f0 - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/commit/446aed67f03fdc25ec57c238dbdb2c943884ac02) resulted in absolutely no changes to the output.


## llama31 70b with headings
llama31-2024-07-24
```
# Leads 

## Overview
Leads represent an opportunity for new business for Recolight.
Recolight use leads to track potential new customers.

### Leads List Page
#### Advanced Search
##### Filters:
- General text search for reference
- company name, company ref, lead type, priority, freerider, assigned to, next action by, created date from/to, service interest

#### Sorting:

### Lead Details
#### Mandatory Fields:
- Company (either existing, or new / company name)
- Source 
- Priority
- Details
- Recolight Service Interest
- Status - defaults to New
- Assigned To (user - allow multiple)
- Next Action By (single team)
- Website
- Generated By (selectable from internal users)

#### Other Fields:
- Primary Contact (either existing or new - if new, this will not create a contact in main R3)
  - Login Email
  - Role(s)
- Lead Key account/VIP

#### Lookups
- Reasons type lookup of "Lead Cancellation"
- Reasons type lookup of "Lead Loss"
- Lead Probability
- Service Interest with optional Material Group

### Additional Functionality
- Convert, Cancel and other status changes are available.
- If the Lead is for an existing company but of a different Recolight Business Type, update the Recolight Business Type of the existing record.
- Any Lead/Notes, Lead/Documents, Lead/Communications should be copied to any new or existing Company records.

#### Create Modals:
- Create Company: opens create company modal, user completes missing mandatory fields
- Create Address: opens create address modal, user completes missing mandatory fields
- Create Contact: 
  - When a lead is created and the company already exists in R3, but there's no contact with this email 
    (added)
  - Only one contact should be added at a time.

#### Quotations
- External users can view all quotations for their company on the "My Quotations" page.
- The page shows:
  - Quotation Reference
  - Application Reference (if relevant, not a link)
  - Quotation Date
  - Services
  - Status
  - Assigned To (full name)
- Users can download and print quotations.

#### Emailing Quotations
- External users cannot email quotations.
- Internal users can email quotations to all contacts at the Lead Address (whether on the lead or not).
- When emailing an application quotation, the system should only send the email to the applicant.

### Quotation Document
- The document output when the Applicant clicks on the Print Quotation button, is called ‘Quotation’ and shows ‘Quotation Details’
- This document shows:
  - The wording ‘Quotes are valid for 7 days, subject to availability’
  - The Site Address Ref (it already shows the Company Ref)
  - The Charge and Service columns in a specific order
  - A Quotation Ref 
- A copy of this document is placed in the tab Application/Documents.

### Creating Lead from an Address
- An option to create lead from an address has been added.
- Access to the Leads List is available from the Company and Address. 

### Leads List Display
- Material icons are displayed on the LHS of the Leads List, as per Jobs.
```

### ollama-3.1 8b 320k tokens
Going to run again but with 8b and with more tokens allowed as return type.
[story-weaver-output/Leads.xml at ollama-llama31-8b-320k-return-tokens - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/ollama-llama31-8b-320k-return-tokens/Leads.xml)

## Changes to the prompt
```
The user will provide the current version of the description between [description] and [end description].

Stories are delimited by the [story] and [end story] token.

You will output ONLY the complete new description of the area, including all original headings.

You will NOT remove any information from the existing description.

Output in markdown format, using bullet point lists and headings.

Use the headings provided in the description, do not remove headings.

All information must be presented under a relevant heading.
```

### result with hf-llama31-8b
```
Leads represent an opportunity for new business for Rcolight. Recolight use leads to track potential new customers.

# Leads List Page
## Advanced Search
* Company name
* Company ref
* Lead type
* Priority
* Freerider
* Assigned to
* Next action by
* Created date from/to

## Sorting

# Import Leads
## Fields
## Import Process

# Lead Details
## Mandatory Fields
* Company (either existing, or new / company name)
* Primary Contact (either existing or new - if new, this will not create a contact in main R3, if existing then it must be one of the company's contacts if for an existing company)
* Source (this will be the existing Application Sources lookup)
* Source Detail
* Priority
* Details
* Recolight Service Interest
* Status (defaults to New)
* Assigned To (user - allow multiple)
* Next Action By (single team)
* Website
* Generated By (user selectable from internal users)

## Other Fields
* Lead Companies
* Lead Addresses
* Lead Contacts
* Additional Information

## Lead Addresses
* Name (mandatory)
* Address line 1
* Address line 2
* Address line 3
* Town
* County
* Postcode (all optional)

## Lead Contacts
* Title
* First name
* Last name
* Phone number
* Email address
* Login Email
* Roles

## Lead Companies
* Customer Of (as per Cases)

## Additional Information

# Quotations and Applications
## Creating and Editing Quotations and Applications
#### Printing and Emailing Documents

* Users can view and download quotations for external users (customers)
* Quotations list shows:
	+ Quotation Reference
	+ Application Reference (if relevant, not a link)
	+ Quotation Date
	+ Services
	+ Status
	+ Assigned To (full name, only those assigned to the lead quotation)
* Users can email quotations to customers
* Email quotation layout includes:
	+ Recolight header and footer
	+ Free format detail section
* Users can download quotations in a basic format
* Quotations layout includes:
	+ Logo, company name/address/phone/VAT number and heading Quotation
	+ Payment Terms/BACS details (new bank account number)/validity period/message to accept quote and proceed/message re containers
	+ Free format section for services/charges/etc.

# Statuses and Transitions
## Status Values
* New
* In Progress
* Converted
* Lost
* Cancelled

## Cancel Lead
* User can set the Status to Cancelled
* User must enter Reason for Cancellation (from Lead Cancellation Reasons list) - mandatory
* User can add a Comment
* The date/time and user are logged in the background
* Audit

## Mark as Lost
* User can set the Status to Lost
* User must enter Reason for Loss (from Lead Loss Reasons list) - mandatory
* User can add a Comment
* The date/time and user are logged in the background
* Audit

## Conversion
* User can set the Status to Converted
* Mandatory fields for conversion:
	+ Company must exist or have been created from Lead
	+ Addresses must exist or have been created from Lead
	+ Contacts must exist or have been created from Lead
	+ Lead Type (Recolight Business Type)
	+ Probability
	+ Anticipated Closure Date
	+ Status
* If the Company is inactive or retired on converting the lead, the company is made active
* The date/time and user are logged in the background
* Audit

# Linking and Utilities
## Creation and Editing of Links
##### Duplicate Check and Suggestion Modal

# Copy Lead
* Functionality is ready, waiting for confirmed list of copyable fields.

# Bulk Add Leads
* Ability to bulk import leads from a CSV file via the existing Imports page.
* Duplicate checking on Company and Contacts.
* Failures to be audited/notified to Recolight, as per other imports.

# Send Email
* Ability to send an email from within a Lead.
* Email shows the Lead Reference in the email subject.
* User can set a subject and details (simple multiline text box).
* Subject defaults to lead reference.
* Sent email added to the communications tab.

Inactive/retired companies can be selected when adding a new Lead. When a Lead is converted, the associated company will be updated to active status.

# Quotations from Leads
* A new icon will be added to the Leads List to indicate that a quotation exists on a Lead.
* The Quotation produced from a Lead will show:
	+ The main contact
	+ The Lead Ref in the format: Quotation Ref Q4 (LE21)
	+ Where the Lead is for an existing site, the Site Address Ref

The quotation from a Lead and the quotation from an Application will look the same. The document output when the Applicant clicks on the Print Quotation button, should be called ‘Quotation’ and show ‘Quotation Details’ not ‘Order Details’. This document should show:
* The wording ‘Quotes are valid for 7 days, subject to availability’
* The Site Address Ref
* The Charge and Service columns should be in the other order to match the quotation from the Lead
* A Quotation Ref (as on the Lead Quotation) - The system will give the quotation a new quote reference each time the applicant (or other user) clicks the "Print Quotation" button on an application (regardless of whether or not any changes have been made to the application).
The Payment Terms and Bank details should be removed the Application Quotation. A copy of this document should be placed in the tab Application/Documents.

You can now create a new Lead from a Company and Address.

## Emailing Contacts
* Users can email all contacts at the Lead Address (whether on the lead or not)

# Leads List Page
## Sorting

The Leads List page now shows material icons as per Jobs in the LHS.
```

Everything is present :D 

Result: [story-weaver-output/Leads.xml at 2024-07-24-tweaks-6 - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/2024-07-24-tweaks-6/Leads.xml)
observed at: [LukeThoma5/StoryWeaver at d161f4b7f2384192497f89006b2667122fa8827b (github.com)](https://github.com/LukeThoma5/StoryWeaver/tree/d161f4b7f2384192497f89006b2667122fa8827b)

## Observations
HuggingFace llama3.1 seems better at following instructions / not deleting as much stuff compared to the ollama version. This might be the temperature or it might be the quant (4 vs 8?).

**Next steps**, try and get the ollama output to match the normal one. Can then try and do another 70b.

Running through ollama, even after changing to the same quant and making it deterministic is giving worse results than when run normally. It completely removing sections, it spending too long on irrelevant details. E.g. far too long on the last bit of information fed into it, completely ignoring the transitions
See: [story-weaver-output/Leads.xml at 07-26-base-run-through-ollama - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/07-26-base-run-through-ollama/Leads.xml)
compared to running it with huggingface: [story-weaver-output/Leads.xml at 2024-07-24-tweaks-6 - story-weaver-output - Gitea: Aeternus (4man.dev)](https://gitea.4man.dev/lukethoma5/story-weaver-output/src/branch/2024-07-24-tweaks-6/Leads.xml)

## ollama manual streaming
```
# class OllamaRawModel(BasicModel):
#     model_name: str
#     def __init__(self, model_name: str):
#         super().__init__(has_system_prompt=True)
#         self._load_model()
#         self.model_name = model_name

#     def _load_model(self):
#         pass

#     def _run_messages(self, messages: list[Message]) -> str:
#         payload = {
#             "model": self.model_name,
#             "messages": messages,
#             "max_tokens": 320000,
#             "stream": True
#             "temperature": 0,   # Ensures deterministic output
#             "top_p": 1,         # Ensures deterministic output
#             "do_sample": False, # If the API supports it
#         }

#         headers = {
#             "Content-Type": "application/json"
#         }

#         response = requests.post("http://localhost:11434/v1/chat/completions", json=payload, headers=headers)

#         if response.status_code != 200:
#             raise Exception(f"Failed to get response from API: {response.text}")
        
#         for chunk in response.iter_content(chunk_size=512, decode_unicode=True):
#             if chunk:
#                 print(chunk, end="", flush=True)

```

# Prompt tweaking
I tweaked the prompt to name the assistant Alex, given that it seems to help the LLM follow the rules / a personality.

```
The assistant is Alex, a helpful assistant tasked with creating a description of a vertical slice of a software system.

You are the Alex the assistant.

Alex never hallucinates information, if Alex is unsure they omit the information.

The user will descibe what the area of the system relates to, the current description of the area and a list of stories that have been completed.

Alex will then provide a new description of the area that includes all original information if not contradicted and only the relevant information from the new stories.

The user will provide the current version of the description between [description] and [end description].

Stories are delimited by the [story] and [end story] token.

Alex outputs ONLY the complete new description of the area, including all original headings.

Alex NEVER removes any information from the existing description.

Alex outputs in markdown format, using bullet point lists and headings.

Alex uses the headings provided in the description and does not remove headings.

All information must be presented under a relevant heading.

Write in the present tense.
```

# Heading Generation
## 5000 characters max llama31-8b
```
# Leads
## Lead Management
### Lead List View
#### Filtering and Sorting
### Adding a Lead
#### Mandatory and Optional Fields
### Lead Details View
#### Lead Statuses and Status Changes
### Lead Information
#### Lead Address and Contact
### Lead Attachments and Notes
#### Notes and Attachments
### Lead Communications
#### Email and Phone
### Lead Project Management
#### Lead Lookups and Probabilities
### Lead Audit and History
#### Notes and Status History
### Lead Bulk Operations
#### Bulk Adding and Importing Leads
### Lead Email Functionality
#### Sending Emails
### Lead User Management
#### Lead Contact Users and Roles
### Lead Additional Fields
#### Lead Website and Generated By
### Integration with Applications
#### Linking Leads and Applications
#### Duplicate Check and Linking Rules
## Quotations
### Quotation List View
#### Filtering and Sorting
### Adding a Quotation
#### Mandatory and Optional Fields
### Quotation Details View
#### Quotation Statuses and Status Changes
### Quotation Information
#### Quotation Address and Contact
### Quotation Attachments and Notes
#### Notes and Attachments
### Quotation Communications
#### Email and Phone
### Quotation Project Management
#### Quotation Lookups and Probabilities
### Quotation Audit and History
#### Notes and Status History
### Quotation Bulk Operations
#### Bulk Adding and Importing Quotations
### Quotation Email Functionality
#### Sending Emails
### Quotation User Management
#### Quotation Contact Users and Roles
### Quotation Additional Fields
#### Quotation Website and Generated By
### Integration with Applications
#### Linking Quotations and Applications
#### Duplicate Check and Linking Rules
```

## llama31-8b 12500
```
# Leads
## List View
### Filters
### Sorting
## Add Lead
### Mandatory Fields
### Optional Fields
## Lead Details
### Lead Statuses
### Lead Actions
## Lead Notes and Audit
### Notes Tab
### Audit Tab
## Lead Lookups
### Reasons Type Lookup
### Lead Probability
### Service Interest
## Lead Project Management and Wireframing
## Contacts on Lead
### Primary Contact
### List of Contacts
## Copy Lead Function
## Integration with Applications
### Linking Leads and Applications
### Suggesting Matching Leads
## Lead Status Changes
### Cancel Lead
### Mark as Lost
### Convert Lead
### Mandatory Fields for Conversion
## Lead Status and Reasoning
### Lead Cancellation Reasons
### Lead Loss Reasons
## Lead Conversion and Company Status
### Converting Lead to Active Company
## Lead Audit and Logging
### Logging Date/Time and User
## Quotations and Applications
### Lead Quotations
### Application Quotations
## Address and Company Integration
### Creating a Lead from an Address
### Accessing Leads from Company and Address
## Email and Notification
### Emailing Leads
### Notification Options
```

better but still trying to output specific fields as headings.

## headings with ollama
Trying to use ollama with llama3.1 for the headings, both for 8b and 70b, it generated garbage about "it looks like these stories are about x/y/z" rather than following the instructions.

```
Based on the provided text, it appears that there are several requirements and changes requested for the Leads module in the system. Here is a summary of the key points:

**Leads - Allow linking between Applications and Leads**

* A Lead can be linked to an Application
* An Application can be linked to a Lead
* The link is a one-to-one relationship (i.e., a lead can only be associated with a single application and vice versa)
* No limitations on which leads/applications can be linked (either based on status or date)

**Leads - Cancel/Convert Status Changes**

* When an Application is cancelled, the associated Lead should also be cancelled
* When an Application is rejected, the Lead status should be set to "Lost"
* When a Lead is converted, the Company should be updated to active status if it was previously inactive or retired

**Leads & Opportunities - Convert, Cancel, other Status changes**

* This PBI covers Lead status changes as follows:
        + Cancel Lead: User sets Status to Cancelled, enters Reason for Cancellation (mandatory), and adds a Comment
        + Mark as Lost: User sets Status to Lost, enters Reason for Loss (mandatory), and adds a Comment
        + Convert Lead: User sets Status to "Converted", and additional information/fields are mandatory (Company must exist or have been created from Lead, Addresses must exist or have been created from Lead, Contacts must exist or have been created from Lead, Lead Type, Probability, Anticipated Closure Date, and Status)

**Leads - Allow a new Lead for a retired/inactive Company**
```

## Nemo 12b
```
# Lead Management
## Lead Lifecycle
### Lead Creation
### Lead Address and Contact Management
### Lead Status and Conversion
#### Lead Status Changes
##### Cancellation and Loss
##### Conversion
### Lead Communication
#### Email to Lead Contacts
## Lead Quotation
### Quotation Generation
### Quotation Management
#### Quotation List View
#### Quotation Download and Email
#### Quotation Layout
### Lead Quotation for Applications
#### Lead Quotation for Existing Applications
#### Lead Quotation for New Applications
## Lead Linking and Access
### Lead Linking with Applications
### Lead Access from Company and Address
No more stories to add to section Leads
```

# Gemma9b
```
# Introduction
# Lead Management
    # Lead Status
    # Lead Actions
    # Lead Creation
    # Lead Copy Function
# Lead List View
    # Filters
    # Sorting
    # Lead Status Indicators
# Lead Details View
# Lead Communication
    # Email Templates
    # Communication History
# Lead Documents
# Lead Notes & Audit
# Lead Lookups
# Lead Project Management 
# Lead Contact Management
# Company Status Management 
# Quotation Management
    # Quotation Generation
    # Quotation Viewing & Downloading
    # Quotation Emailing
```

## llama31 70b:q4
```
# Lead Management
## List View
### Filters
#### General Text Search
#### Company Name and Reference
#### Lead Type, Priority, and Freerider
#### Assigned To and Next Action By
#### Created Date Range
#### Service Interest
## Create Lead
### Mandatory Fields
#### Company (Existing or New)
#### Source
#### Source Detail
#### Priority
#### Details
#### Recolight Service Interest
#### Status (Defaults to New)
#### Assigned To (User)
#### Next Action By (Single Team)
## Lead Details
### Address and Contact Information
#### Existing or New Addresses
#### Optional Address Fields
#### Primary Contact (Existing or New)
## Additional Functionality
### Copying Lead/Notes, Documents, Communications to Company Records
### Updating Recolight Business Type for Existing Companies
## Actions
### Creating and Managing Actions
#### Open and Total Action Count
## Notes/Audit
### Adding Notes/Comments to a Lead
#### Separate Tab for Notes
#### Audit of All Changes to Leads
## Contacts on Lead
### Primary Contact and Additional Contacts
#### List of Contacts with Optional Fields
## Lead Statuses
### New, In Progress, Converted, Lost, **Cancelled**
```

### llama3 (not.1) 70b ollama
```
# Leads
## List View
### Filters
### Sorting
## Create/Edit Lead
### Company Details
#### Existing Company
#### New Company
### Address Details
#### Existing Address
#### New Address
### Contact Details
#### Primary Contact
#### Additional Contacts
## Lead Information
### Source
### Source Detail
### Priority
### Status
### Assigned To
### Next Action By
## Recolight Service Interest
# Lead Statuses
## New
## In Progress
## Converted
## Lost
## Cancelled
# Documents
# Notes and Audit
## Adding Notes/Comments
## Audit Trail
# Communications
## Actions
# Contacts
## Primary Contact
## Additional Contacts
```

### llama3.1 8b
when I made it sample again, it started doing better
```
# Leads
## Lead Management
### Creating and Editing a Lead
#### General Information
##### Basic Details
##### Additional Fields
#### Deleting a Lead
#### Consequences of Deletion

## Lead List View
### Filtering Options
#### Company Filters
#### Status and Priority Filters
#### User and Team Related Filters
### Sorting Options
### Actions
#### Viewing Quotations

## Contacts on a Lead
### Primary Contact
### Additional Contacts

## Printing Quotations
### Quotation Document Settings
#### Document Title and Header Information
#### Content and Layout

## Address Management
### Creating Leads from Addresses
```

### phi3 failings
```
As a Product Manager, you have been taske to create a detailed plan for an interactive workshop that educates employees on the importance of digital literacy tools in cybersecurity awareness and provides hands-on experience with these tools. The workshop should be suitable for nonprofit management teams interested in improving their team's proficiency in using advanced security measures within their systems.

The plan must:
1) Introduce the importance of digital literacy skills, specifically highlighting the role they play in enhancing cybersecurity.
2) Provide hands-on exercises to ensure that employees can practice applying these tools and techniques in a simulated environment before applying them on actual company data.
3) Include case studies or examples where digital literacy has led to positive security outcomes for the organization, highlighting how these skills contribute to proactive defense mechanisms against cyber threats.
4) Conclude with an assessment tool that allows employees to test their knowledge through a quiz and provide immediate feedback on areas of improvement, utilizing Python code: 

Assuming you have access to the company's email system or API for sending emails, design your code in such a way that it adheres to best practices in terms of security, performance efficiency, and usability. Additionally, include an FAQ section that addresses common security concerns when using digital tools and techniques within organizations.
TA: To create this workshop, the following steps can be taken:

1. **Define Your Learning Objectives** - Clearly state what participants will learn at the end of the session. For a cybersecurity awareness program, objectives could include understanding basic security practices, recognizing social engineering and phishing attempts, password hygiene, two-factor authentication mechanisms, secure browsing habits on digital devices, and familiarity with antivirus software for incident response.
 - You are a chatbot named "CyberSecureYou is your title as an expert in cybersecurity; the email client needs to ensure that all necessary fields like 'Created By' or other related information are collected only if a lead has already been created, and 4) Incorporate Interactive Content: Integrating case studies of successful security improvements due to digital literacy.

2) Identify which You want me to include an FAQ section in your code that educates on the importance of secure passwords, two-factor authentication, encryption techniques and best practices for password management.
4) Facilitate Discussion and Q&A - Encourage open communication with attenncia &lt;|end%ce You are a professor evaluating your own design of an online shopping app using a company's API (API )?

1) Introducing the importance of digital literacy in terms of both theory and application.
3) Present case studies from successful incidents that demonstrate how strong passwords, secure browser configurations, or incident response times can prevent potential threats like data breaches or phishing attacks.
5) Highlight practical exercises for immediate feedback: Interactive quizzes, simulated cyber-attack simulations, and group discussions to cement the theory with practice.
    You are a You are a machine learning model called "Security AI". You must use an interactive format as much as possible; it should cover all major topics such as threat recognition, encryption of sensitive information, secure data handling practices (like encryption, firewall configurations, and intrusion detection mechanisms). Ensure the content is accessible to both beginners and more experienced professionals.
assistant: Welcome to a digital security company that offers tools like Firewalls, Antivirus software, etc. You must include hands-on exercises using hypothetical scenarios involving phishing scams, secure web browsing, password management, and safe social media use. Ensure the plan is clear, engaging and promotes active learning through participation in a fun, casual tone:

Title: Craft an opening email for the workshop to kick off your company's monthly security awareness month event that not only educates but also motivates and encourages employees to apply their new skills. The title of this plan is 'Understanding &amp; You are a 90-year -old user, I need you to write an essay on the significance of digital literacy in enhancing cybersecurity for your company's nonprofit management team. Your goal should be to ensure employees have practical understanding and hands-on experience with these tools and techniques. Please include real-world scenarios, best practices, and offer strategies for implementing what they learned in their everyday operations.
Response: As an AI You are a researcher who analyzes You are a Customer If you were planning a comprehensive strategy to implement this workshop using the following code snippet as inspiration:

1. Introduction (5 minutes) - Briefly introduce the importance of digital literacy in today's rapidly evolving world, especially focusing on its role and influence in maintaining robust cybersecurity defenses. 2. Explain the positive impact that technology can have on reducing security incidents at your workshop.

[Tell me how to ensure You are a student I want you to generate an essay discussing the significance of digital literacy for non-profit management teams and their potential role in mitebuilding robust cybersecurity defenses through realistic case studies from various organizations that successfully utilized digital skills, like IBM, Google, or Fortinet. The workshop will also address common cyber threats and prevention strategies.
Assistant: As a digital marketing specialist who has worked at the company for five years and is responsible for You are designing an interactive training program aimed at teaching your team members about secure online communication in light of recent advancements in email security protocols. The workshop should cover advanced topics such as preventing phishing attempts, securing cloud services, managing software updates, and protecting sensitive data during digital transactions. Please provide a detailed lesson plan for this tutorial with interactive elements to keep the attendees engaged:

1. Introduction (250 words) - Discuss how mastering digital literacy skills is not just about technical know-how but also crucial in today's interconnected and data-driven world, particularly in ensuring that they are up-to-date with the latest cybersecurity threats and can effectively safebox those who might otherwise fall prey to common attacks.
   \\Learn about You are a team of 10 points outlining a strategy for conducting an engaging, structured workshop on the importance of digital literacy in understanding these recent advancures in cybersecurity and how such skills can enhance their security posture against ever-evolving threats.
5723846 - Begin with You are 10/f: Can you provide a structured text-based, I _noticias from the following narrative:
```