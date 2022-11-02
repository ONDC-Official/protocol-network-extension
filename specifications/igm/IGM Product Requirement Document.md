# Issue & Grievance Management (IGM)
## _Product Requirement Document (PRD)_

**Revision History**

| **Version** | **Date** | **Changes** |
| --- | --- | --- |
| 0.1 (Draft) | 19-Oct-2022 | Created |

## 1. Overview

The Issue & Grievance Management (IGM) for ONDC is a mechanism via which issues between users of the network are resolved. The IGM flow has been developed based on the Issue & Grievance Management which acts as a facilitator to resolve issues and disputes between a Complainant and Respondent in a manner that ensures transparency, fairness and data security to the parties. The framework is built on the interactions on a tripartite Network Participants (NPs) contract for a unique transaction including logistics services by Logistics Service Provider (LSP) that has been procured on-network. This implies that a complainant shall be raising an issue for a particular transaction on the network which may involve buyer app, seller app, logistics service provider app or any other participants as may be notified by ONDC as identified entities for a given transaction.

## 2. Role of Participants

The table below lists the different participants in a transaction and will be involved in the issue and grievance management process. Every participant listed below shall be an ONDC network participant apart from the online dispute resolution service providers.

| **Entity** | **Description** | **Activity Context** |
| --- | --- | --- |
| Buyer | Buyer is paying for the purchase of a product/ service on ONDC Network | Off Network |
| Seller | Seller is the provider of the product/ service being bought on the network | On Network |
| Buyer App | Buyer App enables the transaction on the buyer's end | On Network |
| Seller App | Seller App enables the transaction on the seller's end | On Network |
| Logistics Seller App | Logistic seller app enables the fulfilment of the order | On Network |
| Complainant | Complainant raises a complaint with an interfacing app. The complainant may be an end user (buyer or seller) or a network participant (buyer app/ seller app/ logistic services provider app) | On Network |
| Interfacing app | Interface for the complainant to raise/ escalate issues faced on a transaction | On Network |
| Respondent | Respondent is the entity that will be providing the resolution of the issue raised. The respondent may be a buyer app, or a seller app or a logistic services provider app| On Network |
| Transaction counterparty | In any transaction, the transaction counterparty is the immediately next entity where the issue/grievance is being traversed to. For illustration, in an issue raised by a buyer, the buyer app is the interfacing app and the seller app becomes the counterparty for the product/ service transaction. | On Network |
| Cascaded counterparty | In the value chain of a transaction, the entity after the transaction counterparty is referred to as the cascaded counterparty. For illustration in an issue raised by a buyer, the buyer app is the interfacing app, the seller app is the counterparty app and the logistic provider app becomes the cascaded counterparty in the transaction in case on network logistics have been procured. | On network |
| GRO | Grievance Redressal Officer is appointed by each network participant (buyer app, seller app, logistic provider app) for consumer grievance redressal | Off Network |
| ODR SP | Online Dispute Resolution (ODR) is the active use of digital framework to help resolve disputes between parties. ODR Service Providers (ODR SP) via dispute resolution methods such as mediation/ conciliation and/or arbitration, will attempt to resolve disputes | Off Network |

## 3. Guiding principles

1. Only the complainant can "close" the complaint. It will be marked as "resolved" by the respondent. Once marked as "resolved", a notification will be triggered to the complainant via the interfacing application. Complainants may choose to close or escalate it further, if applicable.
2. The complainant shall be able to cancel their complaints providing a cancellation reason and remarks (if required). The updated status 'cancelled by complainant' shall be traversed to all network participants involved in the issue resolution flow.
3. The complaint will be marked as "deemed closed" if there is no update form the complainant within 24 business hours.
4. Escalation principles, the option to escalate the issue to the next level shall be made available to complainant via the interfacing application based on following two conditions:
  <ol> a. Time trigger: When time to respond has elapsed </ol>
  <ol> b. Event trigger: Issue is marked as resolved by the respondent and complainant wants to escalate the issue within the permissible time </ol>
5. Suggestive issue handling mechanism for efficient and effective complaint issue/grievance handling such as:
  <ol> a. Chatbot </ol>
  <ol> b. AI enabled ticketing system </ol>
  <ol> c. Voice based support </ol>
  <ol> d. Social media interface </ol>
  <ol> e. Grievance escalations </ol>
  <ol> f. Any other </ol> 
6. Network issue identifier is an unique number assigned to any complaint by the interfacing application at the source. During the life cycle of a complaint, this number will not change and will be communicated to counterparty application.

7. All participants should maintain a mapping of Network issue identifiers with their internal CRM ticket number to keep an audit trail of the issue and its resolution.

8. Option to "Accept" and "Reject" the issue shall be made available. If the respondent opts to reject, the complainant may escalate the complaint.

## 4. Issue and Grievance Management Flow

This section elaborates the process flows for issue and grievance management on ONDC network. Below schematic depicts the four levels framework for resolving issues on the network.

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199414970-adf5cdbd-977e-4901-b7ca-9c814d072f63.png">
</p>

The lifecycle of the issue from the stage of it being raised to its resolution is as follows:

### L1 - Issue resolution by NPs

Whenever there is an issue, the Complainant raises a complaint. The interfacing app, counterparty app and the cascaded counterparty app attempt to provide a resolution to the issue raised. The complainant may escalate the issue post the process if required.

The below diagram shows the typical flow of the issue management and resolution cycle:

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199419351-3fb4ccfe-1240-4bc1-a7c1-2c00635b4591.png">
</p>

The detailed issue resolution process is defined below:

1. Complainant raises a complaint with their respective interfacing app
2. The interfacing app raises a ticket in their complaint management tool with a unique ticket ID along with a network issue identifier.
3. It attempts to resolve the issue through their issue handling tools such as either a customer help desk or an automated resolution tool such as chatbot, drop down list. It provides a resolution for the issue to the complainant, if it is able to provide a resolution. The interfacing app must attempt to offer a resolution within a maximum of 24 business hours of receiving the issue request.
4. If the interfacing app infers that the issue cannot be resolved by the entity, it raises the issue to the transaction counterparty app.
5. The transaction counterparty app having received the issue raises a ticket in their complaint management tool with their unique ticket ID along with the network issue identifier generated and communicated by the interfacing application at source.
6. The counterparty app, which receives the request for issue resolution by the interfacing app, attempts to resolve the issue through their issue handling tools such as either a customer help desk or an automated resolution tool such as chatbot, drop down list. It provides a resolution for the issue to the complainant, showcased on the interfacing app, if it is able to provide a resolution. The counterparty app must attempt to offer a resolution within a maximum of 24 business hours of receiving the issue request.
7. If the counterparty app infers that the issue cannot be resolved by the said entity, the issue is further raised to the cascaded counterparty in the transaction chain.
8. The cascaded counterparty raises a ticket in their complaint management tool with their unique ticket ID along with the network issue identifier generated by the interfacing application at source and communicated to the counterparty application.
9. The cascaded counterparty app attempts to resolve the issue through their issue handling tools such as either a customer help desk or an automated resolution tool such as chatbot, drop down list. It provides a resolution for the issue to the complainant, showcased on the interfacing app. The cascaded counterparty app must attempt to offer a resolution within a maximum of 24 business hours of receiving the issue request.
10. The GRO details shall be part of the issue payload being traversed among the respondents. In the response to an issue, the transaction counterparty app and the cascaded counterparty party shall be sharing their respective GRO details. The interfacing app shall be retaining this information and making the same available when issue is escalated to a grievance.

After the process is completed, either a resolution is provided by any of the entities, or no resolution is provided to the complainant. The complainant has a choice of either escalating or closing the issue. The complainant can raise an escalation of the issue on the interfacing app having not received a resolution or not being satisfied with the resolution provided. The issue becomes a grievance in case it has been escalated by the complainant. The complainant is provided a window of 24 business hours for escalating the issue. If the complainant does not raise an escalation, the issue is deemed closed.

### L2 - Grievance handling by GROs

Grievance redressal is the second stage of the IGM framework, In the absence of a resolution or an unsatisfactory resolution of the issue is provided, the Complainant escalates the issue to a grievance. The Grievance Redressal Officers (GROs) of the interfacing app, counterparty app and the cascaded counterparty app attempt to provide a resolution to the grievance. The complainant may escalate the grievance post the process if required.

The below diagram shows the typical flow of the issue management and resolution cycle with GRO, if escalated:

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199419544-37c47299-6ee2-42b6-9afa-b1a94a8b6cf3.png">
</p>

The detailed grievance resolution process is defined below:

1. Complainant escalates the issue to a grievance on their respective interfacing app.
2. The interfacing app escalates the issue to the next level in their complaint management tool with the mapping of network issue identifiers generated at source.
3. The Grievance Redressal Officers (GRO) of the interfacing app attempts to resolve the grievance. It provides a resolution for the grievance to the complainant, if it is able to provide a resolution. The GRO of the interfacing app must attempt to offer a resolution within a maximum of 48 business hours of receiving the Grievance Order.
4. If the interfacing app's GRO infers that the grievance cannot be resolved by itself, it raises the grievance to the transaction counterparty's GRO. The escalation process to GRO must receive a synchronous response to the API call with an 'Ack' if GRO process is accepted or 'Nack' in case of GRO process is declined by any of either counterparty or cascaded counterparty.
5. The counterparty having received an escalation on the grievance, escalates the ticket in their complaint management tool with a mapping to network issue identifier generated at source and communicated by interfacing app.
6. The two GROs attempt to provide a resolution for the grievance. They provide a resolution for the issue to the complainant, showcased on the complainant's interfacing app, if they are able to provide a resolution. The GROs must attempt to offer a resolution within a maximum of 48 business hours of receiving the grievance order.
7. If the GROs infer that the grievance cannot be resolved by them, the grievance is raised to the cascaded counterparty's GRO.
8. This counterparty escalates the grievance in their complaint management tool with the mapping to Network issue identifier.
9. The GROs attempt to resolve the grievance. The GROs must attempt to offer a resolution within a maximum of 48 business hours of receiving the grievance order.
10. They (the final respondent responsible for providing resolution as identified as proceedings of GRO process) provide a resolution for the issue to the complainant, showcased on the complainant's interfacing app.
11. The update of the resolution remarks shall be the responsibility of the final respondent that may be cascaded to the complainant through the interfacing app.

After the process is completed, either a resolution is provided by any of the GROs, or no resolution is provided to the complainant. The complainant has a choice of either escalating or closing the grievance. The complainant can raise an escalation of the grievance on the interfacing app having not received a resolution or not being satisfied with the resolution provided. The grievance now becomes a dispute if it has been escalated by the complainant. The complainant is provided a window of 24 business hours to escalate the grievance. If the complainant does not raise an escalation, the grievance is deemed closed.

### L3 - Online Dispute Resolution (ODR)

ODR is the third stage of IGM. If the issue is not resolved and is cascaded to the GRO stage, the GRO of the interfacing application, counterparty application, and/or cascaded counterparty application will try to resolve it for the complainant. If the GROs are unable to resolve the grievance, the grievance may be escalated to the ODR stage. At this stage, the complainant will have an option to opt-in for an escalation to ODR and will be given an option to select the empaneled ODRs on the ONDC network. The ODR service providers, via resolution methods such as Mediation/ Conciliation and/or Arbitration, will attempt to resolve the dispute. If an ODR service provider resolves the issue for the end user, the resolution is recorded and closed.

**Onboarding of ODR**

All empaneled ODR service providers will be made available on the ONDC registry. While adding them to the registry, the following details will be captured:

1. ODR Name
2. About ODR
3. URL
4. Price model for the ODR services
5. Resolution Success Ratio

**Process flow**

The below diagram shows the typical flow of ODR selection:

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199419737-5931b2cc-b6fd-4a0b-82fe-bff84c431dc7.png">
</p>

The detailed selection and resolution process is defined below:

1. The complainant will be given an option to select the empaneled ODR service providers on the interfacing application
2. As part of the escalating the grievance to a dispute for ODR proceedings, the complainant will be asked to select a total of (n/2)+1 ODR service providers, where n is the number of total ODRs empaneled on the ONDC network. The complainant will have 24 business hours to select the ODR SP and proceed further.
3. In case, the complainant does not select the ODR within the permissible time, the option to escalate to ODR will be disabled by the interfacing application
4. Once the complainant has selected the ODRs, a notification will be sent to respondent and cascaded counterparty applications to select the (n/2)+1 ODRs respectively. The respondent and cascaded counterparty applications will get a maximum of 24 business hours, for which the time will start as soon as the complainant has selected their list of preferred ODR Service Providers. Time for counterparty app or cascaded counterparty app shall start when the entity has provided an 'ack' to the requestor.
5. Selection of ODRs by respondent and counterparty application will be shared with complainant interfacing application
6. The complainant interfacing application will select the one ODR based on following criteria
  <ol> a. If there is only one common ODR, that will be automatically selected and matter will be escalated to the the same ODR </ol> 
  <ol> b. If there are more than one common ODRs, the system will select the ODR which has lowest service cost </ol> 
  <ol> c. Based on the above criterias, system will assign the ODR to the complainant and respondent </ol> 

7. The selection of ODR will be on network

8. The proceeding of ODR will be off network and resolution will be posted on network by the respondent

9. The resolution of ODR will be made available to complainant by the interfacing application

### L4 - Court

The Complainant (buyer or seller or logistics service provider) has the option to go to court if an ODR service provider is unable to resolve the issue.

## 5. Use cases

In case of GRO and ODR, since these will happen off network, the remarks will be updated and cascaded by the respondent entity on network.

Below diagram depicts the transactions/processing happening on-network and off network:

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199419898-060c5cb1-4610-4734-9a66-298ee5851d76.png">
</p>

## Scenario 1: End User complainant raises an issue on their interfacing app

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199420172-8767c82b-c811-475e-8119-b929865fe69d.png">
</p>

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199420425-a1564bf6-dee9-44e2-9be4-b58e8360eefc.png">
</p>

### **Scenario 1.A:** A buyer raises an issue on the buyer app

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199420546-b9d70655-affe-4b89-85a3-aaf9c34eb41e.png">
</p>

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199420658-5efcb1f7-10de-41e6-b462-dc2391b451e1.png">
</p>

_In case a buyer wants to raise an issue for an order that has items from multiple sellers, separate issues (Issue\_ID) shall be created for each order\_id (as order\_id has a unique combination of BA, SA & LSP)._

### **Scenario 1.B:** A seller raises an issue on the seller app

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199420733-79ab9407-326a-4c4b-a7a9-5c07a5266d37.png">
</p>

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199420811-e5d429d8-d87f-475c-ad7f-ce2bf3857176.png">
</p>

### **Scenario 1.C** : A logistics agent raising an issue on the LSP app, LSP becoming agent's representative

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199421003-80c84ac1-ac08-46f1-b97a-5549d18d724b.png">
</p>

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199421111-b811934c-23ab-4fc4-90d0-954363005d55.png">
</p>

### Scenario 2: Network participant complainant raises an issue

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199421292-a85b39c8-2792-4191-bc61-fb97e2beabff.png">
</p>

<p align="center">
  <img width="700" src="https://user-images.githubusercontent.com/114131968/199421361-a08ab85f-6233-4519-9a39-bf8ab8ba3d14.png">
</p>

## 5. Dataset required

Please find below the link to the dataset schema required for the API flows.

[Dataset Schema IGM](https://docs.google.com/spreadsheets/d/1ARhRAqhBiqNUFQHJPLbivbro8pdZLwIgySr7MBJHYRU/edit?usp=sharing)

