# Issue and Grievance Management
## _API Contract_

## Revision History

| Version | Date | Changes |
| --- | --- | --- |
| 1.0.0 | 28-Apr-2023 | <ol><li>action_triggered - enums added - NO-ACTION, CANCEL</li><li>issue.issue_action changed to issue_actions</li><li>source.issue_source_type changed to type</li><li>odr.about_info changed to long_desc</li><li>odr.short_desc added</li><li>rating.rating_value changed to value</li><li>issue_status.message.id changed to issue_id</li><li>respondentemail removed</li><li>pos_id removed from respondent_info object</li><li>respondentcontact changed to contact</li><li>respondentchatlink changed to chat_link</li><li>respondentFaqs changed to faqs</li><li>faqs made into an array</li><li>additional_sources made into an array</li><li>resolution.resolution changed to short_desc</li><li>resolution.resolution_remarks changed to long_desc</li><li>dispute_resolution_remarks changed to odr_remarks</li><li>resolution_action changed to action, removed from API contract</li><li>complainant_actions.remarks changed to short_desc</li><li>respondent_actions.remarks changed to short_desc</li><li>Addition of notes on reflection of retail order updates done through core retail APIs based on the resolution provided</li><li>Swagger hub API specs updated</li> |
| ... | ... | ... |
| 0.1 | 05-Dec-2022 | Created |


## Overview
The Issue & Grievance Management (IGM) for ONDC is a mechanism via which issues between users of the network are resolved. The IGM flow has been developed based on the Issue & Grievance Management framework which acts as a facilitator to resolve issues, grievances and disputes between a Complainant and Respondent in a manner that ensures transparency, fairness and data security to the parties.

## Process Flows Document
View the document [here](https://docs.google.com/document/d/135OCfsi5jQ7wh4H_LOoMxb0T0ZrWDYy4LTBvpYS6k_w/edit?usp=sharing)

## API Contract Document
View the document [here](https://docs.google.com/document/d/1UYGIo1fSOcA4ypnk5FuaCgUgNnu9dBQt/edit?usp=sharing)

## SwaggerHub
Access the SwaggerHub [here](https://app.swaggerhub.com/apis/ONDC/ONDC-Protocol-IGM/1.0.0)
