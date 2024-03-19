# Ignore Features:
- Support
- Change Requests
- Container Tracking Weights
# Include Features
- Project Work Phase I
- Project Change Requests
- Membership Declarations (2017-08-01)
- Additional Companies, Lookups & User functionality

By about 2017-05 it seems like some support content is starting to come through on the project app. Maybe add a filter for includes project or recoweb2?

By about 2017-09-26 15:07:31.0766667 its definitely starting to include R3 change requests. I think by this point its definitely talking about R3.

So blanket ban support from before this, and then manually mark some as being part of it. E.g. with a script to ensure repeatable.


Make sure to exclude supplier auction


```sql
-- remove for all other customers
UPDATE T
SET IsDeleted=1
FROM Tickets T
WHERE OrganisationId <> 'D41D0EE2-1ECB-47E0-A9AC-BD9AC0EDABA0'

-- remove R1 values
--SELECT * 
UPDATE T SET IsDeleted=1
from Tickets T
WHERE T.FeatureId in
(
'67C93A0B-B14A-41E0-8841-035EF4CA37B5', -- support
'32548724-5A28-459E-BE90-B673615C97E6', -- change requests
'A9BDEEA1-D4EE-4E2A-9CAF-579C95F6B405' -- container tracking weights
)
AND CreatedUtc < '2017-09-26 15:07:31.0766667'

-- remove cancelled cards
--select * 
UPDATE T SET IsDeleted=1
from Tickets T where [Subject] like '%CANC]%'
```