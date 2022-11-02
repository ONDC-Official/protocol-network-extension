# Reconciliation and Settlement API Contract

## Revision History

| Version | Date | Changes |
| --- | --- | --- |
| 0.2 | 28-Oct-2022 | <ol><li>Updated contract with new APIs</li><ol><li>/recon_status and /on_recon_status<li>/receiver_recon and /on_receiver_recon</li></ol><li>API Name Change</li><ol><li>/recon to /collector_recon</li><li>/on_recon to /on_collector_recon</li></ol><li>Updated error scenarios</li></ol>|

## 1. SwaggerHub Link

Link is [here](https://app.swaggerhub.com/apis/ONDC/ONDC-Protocol-RSP/0.1.0-draft#/).

## 2. Overview

The objective of this note is to propose a **Reconciliation and Settlement** framework for Network Participants (NP), such as Buyer Platforms, Seller Platforms, Logistics Platform etc, on ONDC. The construct defined will provide a framework for participants to settle funds against transactions to respective parties and create an audit trail of transactions. Following are the enumerated design principles for reconciliation and settlement framework:

1. Enable seamless settlement of funds collected by participants
2. Non-repudiable information dissemination all through network entities
3. Maintaining Audit trail to ensure evidence security
4. Defining standards of message communication for transparency, efficiency and machine readability of Information
5. Building trust through safeguarding fund flow for a transaction through well defined triggers for money withdrawal from Nodal Like account
6. Ensuring non-repudiability through digital signatures and payload authentication
7. Seamless integration using protocol with all stakeholders including settlement agency, reconciliation service providers and participants.

Standardising the money flow as per RBI guidelines shall ensure transparency and trust in the ONDC network. The reconciliation and settlement framework shall provide assistance to the Network Participants to settle funds collected on behalf of counterparties at defined intervals. The generation of the recon file will be in batches which will have to be run at defined intervals as per their banking relationship requirements and or as per RBI guidelines. The framework primarily entails the following stages, three of which are pertinent from ONDC network perspective. A schematic depicting the framework is shown below:

1. **Collection and Collation:** Each NP would be expected to be able to collect and collate a record of all their transactions with the intent of creating what money is owed to which entity and by when. This function can be provided by the Reconciliation Service Provider (RSP) or Preparer or by NP itself. The collation could be across 3 elements
  - Payment Gateway/Cash Collection report (as applicable)
  - Books of account / Bank Statement
  - Order details / Transaction triggers (e.g. order dispatched, order delivered etc.)
2. **Preparation of the Settlement Advice:** This is a statement which will provide an amalgamated advice that can be consumed by a bank which will contain order-wise settlement details and this will be defined in the API. Each settlement advice to be sent to the bank will also have a detailing for each counterparty specific report that would be needed to be sent to the counterparty so that they can tally up their accounts.
3. **Routing:** the above mentioned Settlement Advice would be either sent back to the Network Participant who would in turn send it to their bank or NPCI, or the RSP can send it directly to the bank or NPCI as per the standing instructions of the Network Participant.
4. **Actual settlement:** Based on the Settlement Advice shared with the bank, money will be moved within T+1 days of receipt of the settlement advice. Confirmation of the above will be sent back to the Network Participant using /settle API which in turn can also be shared with the counterparty.
5. An optional reconciliation step by receivers against recon file received from collectors is also envisioned, whereby the receivers of the funds may update their recon status against each transaction. The same recon file along with recon status may be cascaded back to respective collectors.

## 3. Role of participants in a transaction

The table below lists the different participants in a transaction and will be involved in the reconciliation and settlement process. Every participant listed below in the reconciliation and settlement process may not be a ONDC network participant.

| **Entity** | **Description** | **Activity Context** |
| :-----: | :-----: | :-----: |
| Buyer | Buyer paying for the purchase on ONDC Network | Off Network |
| Buyer App | Buyer App enables the transaction on the buyer's end | Off Network |
| Seller App | Seller App enables the transaction on the seller's end | Off Network |
| Collector | Collector is the entity that shall be collecting the amount paid by the buyer.For the convenience of understanding the example quoted in this document, assume the Buyer App is the collector. (_The collector may also be the Seller App or the Logistics Provider_) | On Network |
| Collector Bank (CB) | Nodal like account (CNLA) for the Collector (Buyer App) as exist today along with certain additional tenets | Off Network |
| Preparer | Any entity, within or outside the participant boundary, that performs reconciliation of order book, Payment Gateway/Cash collection report, bank statement, etc. to generate the payment settlement advice | Off Network |
| Reconciliation Service Provider (RSP) | Any entity, within or outside the participant boundary, that receives the payment advice from the preparer and initiates the transfer of funds between Nodal like accounts through the settlement agency | On Network |
| Settlement Agency | Any RBI regulated body, within or outside the participant boundary, that receives the payment instructions form the RSP and performs the settlement to counterpart bank accounts and provide due confirmation to RSP post settlement | On Network |
| Receiver | Receiver is the entity that shall be receiving its portion of the amount paid by the buyer.For the convenience of understanding the example quoted in this document, assume the Seller app is the receiver.(_The Receiver may also be the Buyer App or the Logistics Provide_r) | On Network |
| Receiver Bank (RB) | Nodal like account (RNLA) for the Receiver (Seller App) as exist today along with certain additional tenets | Off Network |

## 4. Reconciliation & Settlement Process Flow

This section elaborates the process flows for Reconciliation & Settlement in ONDC. Below schematic depicts the step by step process of reconciliation and settlement.

<p align="center">
<img width="700" src="https://user-images.githubusercontent.com/109668555/199409104-2aee43a1-afa8-4180-a0bc-d7ef631a79c8.png">
<br>Figure 1: Reconciliation and Settlement Process Flow
</p>

1. Collector: Collector is an NP who is responsible for collecting the money from the customer for a transaction executed on the network. Collector can be a Buyer App, Seller App, or Logistics service provider.
2. Preparer: Preparer is an entity (could be Collector or RSP) who would be expected to be able to collect and collate a record of all transactions with the intent of creating what money is owed to which entity and by when. Preparer will be consuming following reports shared via Collector for the reconciliation:
  - Payment Gateway/Cash Collection report of the collector
  - Books of account / Bank Statement
  - Order details / Transaction triggers (e.g. order dispatched, order delivered etc.)

In this step, it is expected to reconcile these three statements and prepare a recon statement. This will be a 3 way reconciliation. This statement will provide an amalgamated advice that can be consumed by a bank which will contain order-wise settlement details and this will be defined in the API. Each settlement advice to be sent to the bank will also have a detailing for each counterparty specific report that would be needed to be sent to the counterparty so that they can tally up their accounts.

1. Routing and Settlement: The Settlement Advice would be either sent back to the Collector or to the RSP who would in turn send it to their bank or settlement agency. Settlement agency will then further settle the money with the intended receivers. Post successful confirmation, the settlement agency will share the UTRs with RSP or the collector. Based on the Settlement Advice shared with the bank, money will be moved within T+1 days of receipt of the settlement advice. RSP will be responsible for providing the response to the collector or prepared within 2 calendar days.
2. An optional reconciliation step by receivers against recon file received from collectors is also envisioned, whereby the receivers of the funds may update their recon status against each transaction. The same recon file along with recon status may be cascaded back to respective collectors.
3. Receiver Side Reconciliation: Optionally, the receiver may perform an additional reconciliation on their end and update the status in the same recon file and cascade back to each collector. This will ensure the closure of transactions on both sides, and will also serve as an early indicator of any possible issue in the settlement. If the collector receives the status of reconciliation as not reconciled, the collector may raise an issue in their internal ticketing system and perform investigation. There are three scenarios in this case that needs to be handled as part of API Contract:
  - Counterparty Reconciliation: As part of counterparty reconciliation status as received by the collector as non-reconciled, the collector may raise a ticket with their internal ticketing system. Upon investigation if the collector finds a settlement anomaly, respective attributes in the following recon file's "correction" status will be filled, and settlement will happen at gross level. Should the ticket result in money due from receiver, Collector will raise a ticket using IGM flow and receiver may return money in following recon cycle through correction flow
  - Self Realisation of issue: In case collector identifies an issue in settlement on their own accord, they will raise an issue reference in their own CRM and publish the correction section of flow.
  - Correction against Issue: Either collector or Receiver may have issues with payment settlement and they are required to raise an issue through Issue and Grievance Management (IGM) APIs and protocols and respective party may perform investigation at their end. Once the anomaly is established, the correction section of recon shall be filled by the concerned participant and the same will flow in the next recon cycle. The participant responsible for amount disbursement will assume the role of a collector.

Receiver will be responsible for providing the response to the collector or RSP within 7 calendar days.

### Scenario 1: When Collector, Preparer and RSP are different entities

<p align="center">
<img width="700" src="https://user-images.githubusercontent.com/109668555/199433063-f728ebf6-052f-4a93-a9ca-0cc241a500b1.png">
<br>Figure 2: Scenario 1 of reconciliation flow where collector, preparer and RSP are different entities
</p>

### Scenario 2: When Collector is performing all three roles i.e. Collector, Preparer, and RSP and availing the services of settlement agency for final settlement with receiver

<p align="center">
<img width="700" src="https://user-images.githubusercontent.com/109668555/199433560-9ed0feba-ba67-4e4e-9f89-063e6bf47295.png">
<br>Figure 3: Scenario 2 of reconciliation flow where collector, preparer and RSP are the same entity
</p>

### Scenario 3: When Collector is working as preparer and availing the services of RSP for the settlement with receiver

<p align="center">
<img width="700" src="https://user-images.githubusercontent.com/109668555/199433772-6bed57ea-ac20-48be-800f-a4ea412745b3.png">
<br>Figure 4: Scenario 3 of reconciliation flow where collector is working as preparer and availing the services of RSP for the settlement with receiver
</p>


## 5. Technical details for Recon & Settlement

Reconciliation & Settlement terms will be communicated using the Recon object. This section shows the **Recon** object at different steps for each of the process flows presented earlier. Each of these scenarios only shows the parameters relevant to that specific scenario. **All values shown in the scenarios below are indicative and only for the purpose of illustration and nothing else.**

### Reconciliation Flow

#### Step 1 - 3-way reconciliation

Collector will share the following reports with the preparer for the reconciliation and preparation of the settlement file:

- Payment Gateway/Cash Collection report of the collector
- Books of account / Bank Statement
- Order details / Transaction triggers (e.g. order dispatched, order delivered etc.)

#### Step 2 - /collector_recon (request initiation)

Collector (or preparer) will call the /recon API per unique seller along with following information which are mandatory. Therefore, in case there is an order which has products from two different sellers, the /recon API has to be called two times for the different sellers. Collector may either use UPI or Bank A/C. 'upi_address' is mandatory when 'settlement_type' is "UPI". If the collector does not receive /on_recon response from the RSP, it should wait until ttl expires. Post expiry of ttl or before then, the collector may call /recon_status to enquire about the status.

Mandatory attributes:
```
{
  "context": {
    "domain": "nic2004:52110",
    "country": "IND",
    "city": "std:080",
    "action": "status",
    "core_version": "0.9.3",
    "bap_id": "abc.collectorapp.com",
    "bap_uri": "https://abc.collectorapp.com",
    "bpp_id": "abc.receiverapp.com",
    "bpp_uri": "https://abc.receiverapp.com",
    "transaction_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
    "message_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
    "timestamp": "2022-10-28T10:34:58.469Z",
    "key": "string",
    "ttl": "string"
  },
  "message": {
    "orderbook": {
      "orders": [
        {
          "id": "K106403902112759",
          "invoice_no": "2022/XYZ/12345-2",
          "collector_app_id": "abc.collectorapp.com",
          "receiver_app_id": "abc.receiverapp.com",
          "state": "Delivered",
          "provider": {
            "name": {
              "name": "SABJI XPRESS PVT LTD - BANASWADI",
              "code": "18275-ONDC-1"
            },
            "address": "NewDelhi"
          },
          "payment": {
            "uri": "string",
            "tl_method": "http/get",
            "params": {
              "transaction_id": "string",
              "transaction_status": "string", (enum)
              "amount": "1234",
              "currency": "string"
            },
            "type": "ON-ORDER",
            "status": "PAID",
            "collected_by": "BAP",
            "@ondc/org/collected_by_status": "Assert",
            "@ondc/org/buyer_app_finder_fee_type": "Amount",
            "@ondc/org/buyer_app_finder_fee_amount": "+1234",
            "@ondc/org/withholding_amount": "+12345",
            "@ondc/org/withholding_amount_status": "Assert",
            "@ondc/org/return_window": "string",
            "@ondc/org/return_window_status": "Assert",
            "@ondc/org/settlement_basis": "Collection",
            "@ondc/org/settlement_basis_status": "Assert",
            "@ondc/org/settlement_window": "string",
            "@ondc/org/settlement_window_status": "Assert",
            "@ondc/org/settlement_details": [
              {
                "settlement_counterparty": "buyer-app",
                "settlement_phase": "sale-amount",
                "settlement_type": "neft", (enum)
                "settlement_bank_account_no": "99679007677676",
                "settlement_ifsc_code": "HDFC900008",
                "upi_address": "string",
                "bank_name": "HDFC",
                "branch_name": "Delhi",
                "beneficiary_address": "Delhi",
                "settlement_status": "PAID", (enum)
                "settlement_reference": "K106403902112759",
                "settlement_timestamp": "2022-10-28T10:34:58.469Z"
              }
            ]
          },
          "withholding_tax_gst": {
            "currency": "string",
            "value": "-123"
          },
          "withholding_tax_tds": {
            "currency": "string",
            "value": "0673658"
          },
          "deduction_by_collector": {
            "currency": "string",
            "value": "-234"
          },
          "order_recon_status": "null",
          "payerdetails": {
            "payer_name": "“Example1 company Pvt. Ltd",
            "payer_address": "Ghaziabad",
            "payer_account_no": 509424924294248,
            "payer_bank_code": "“HDFC0000000”",
            "payer_virtual_payment_address": "80abc@abctMh2h"
          },
          "settlement_reason_code": "01",
          "payout_bank_uri": "https://rsp.somebank.com/rsp/",
          "transaction_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
          "created_at": "2022-10-28T10:34:58.472Z",
          "updated_at": "2022-10-28T10:34:58.472Z"
        }
      ]
    }
  }
}
```

In case of reverse flow, the seller app will be calling /recon, and will provide following values mandatorily:
- Buyer Name & Code, under the provider object
- Seller_app_id in collector_app_id attribute
- buyer_app_id in reciever_app_id attribute
- Payment.collected_by i.e. "BPP"
- Return Amount
- Buyer App Bank details under settlement object

#### Step 3 - /settle (settlement initiation)

RSP will call the /settle API with the settlement details and send it for settlement processing. If RSP does not receive /on_settle response from settlement agency, it should wait until ttl expires.

Mandatory attributes:
```
{
  "context": {
    "domain": "string",
    "country": "string",
    "city": "string",
    "action": "string",
    "core_version": "string",
    "bap_id": "string",
    "bap_uri": "string",
    "bpp_id": "string",
    "bpp_uri": "string",
    "transaction_id": "string",
    "message_id": "string",
    "timestamp": "2022-10-18T16:14:40.395Z",
    "key": "string",
    "ttl": "string" //2 days
  },
  "message": {
    "settlement": {
      "settlements": [
        {
          "payer_name": "“Example1 company Pvt. Ltd",
          "payer_address": "New Delhi, Delhi",
          "payer_account_no": 509424924294248,
          "payer_bank_code": "“HDFC0000000”",
          "curr_type": "INR",
          "amount": {
            "currency": "INR",
            "value": "123"
          },
          "timestamp": "2022-10-18T16:14:40.396Z",
          "payee_name": "A to Z Printing Solutions Pvt. Ltd",
          "payee_address": "delhi",
          "payee_account_no": "99679007677676",
          "payee_bank_code": "HDFC900008",
          "payment_type": "01", (enum)
          "purpose_code": "01", (enum)
          "payee_account_type": "01", (enum)
          "remarks": {
            "name": "string"
          },
          "settlement_id": "121313"
        }
      ]
    }
  }
}
```

#### Step 4 - /on_settle (settlement processed)

The Settlement Agency will respond with the /on_settle API after processing the settlement with details for settlement_status, settlement_reference_no, error_code if any and corresponding error_message.

Mandatory attributes:
```
{
  "context": {
    "domain": "string",
    "country": "string",
    "city": "string",
    "action": "string",
    "core_version": "string",
    "bap_id": "string",
    "bap_uri": "string",
    "bpp_id": "string",
    "bpp_uri": "string",
    "transaction_id": "string",
    "message_id": "string",
    "timestamp": "2022-10-18T16:14:40.395Z",
    "key": "string",
    "ttl": "string"
  },
  "message": {
    "settlement": {
      "settlements": [
        {
          "payer_name": "“Example1 company Pvt. Ltd",
          "payer_address": "string",
          "payer_account_no": 509424924294248,
          "payer_bank_code": "“HDFC0000000”",
          "curr_type": "INR", (enum)
          "amount": {
            "currency": "INR", (enum)
            "value": 123"
          },
          "timestamp": "2022-10-18T16:14:40.396Z",
          "payee_name": "A to Z Printing Solutions Pvt. Ltd",
          "payee_address": "delhi",
          "payee_account_no": "99679007677676",
          "payee_bank_code": "HDFC900008",
          "payment_type": "01", (enum)
          "purpose_code": "01", (enum)
          "payee_account_type": "01", (enum)`
          "remarks": {
            "name": "string"
          },
          "settlement_id": "121313",
           "state": "01",
          "prev_settlement_reference_no": [
            "1234ABCD",
            "2345qwer"
          ],
          "settlement_reference_no": "3718683618631",
          "error_code": "01",
          "error_message": "Account not active or not found"

	
        }
      ]
    }
  }
}
```

#### Step 5a - /receiver_recon (call to receiver from RSP)

RSP will call the /receiver_recon API to send the order book along with UTR number and other settlement details to the receiver.

Mandatory attributes:
```
{
  "context": {
"domain": "nic2004:52110",
 "country": "IND",
 "city": "std:080",
  "action": "status",
  "core_version": "0.9.3",
  "bap_id": "abc.collectorapp.com",
  "bap_uri": "https://abc.collectorapp.com",
  "bpp_id": "abc.receiverapp.com",
  "bpp_uri": "https://abc.receiverapp.com",
  "transaction_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
  "message_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
  "timestamp": "2022-10-28T10:34:58.469Z",
  "key": "string",
   "ttl": "string"
    
  },
  "message": {
    "orderbook": {
      "orders": [
        {
          "id": "K106403902112759",
          "invoice_no": "2022/XYZ/12345-2",
          "collector_app_id": "abc.collectorapp.com",
          "receiver_app_id": "abc.receiverapp.com",
          "state": "Delivered",
          "provider": {
            "name": {
              "name": "SABJI XPRESS PVT LTD - BANASWADI",
              "code": "18275-ONDC-1"
            },
            "address": "Delhi"
          },
          "payment": {
            "uri": "string",
            "tl_method": "http/get",
            "params": {
              "transaction_id": "string",
              "transaction_status": "string",   (enum)
              "amount": "123",
              "currency": "string"
            },
            "type": "ON-ORDER",
            "status": "PAID",
            "collected_by": "BAP",
            "@ondc/org/collected_by_status": "Assert",
            "@ondc/org/buyer_app_finder_fee_type": "Amount",
            "@ondc/org/buyer_app_finder_fee_amount": "+602.0",
            "@ondc/org/withholding_amount": "+124",
            "@ondc/org/withholding_amount_status": "Assert",
            "@ondc/org/return_window": "string",
            "@ondc/org/return_window_status": "Assert",
            "@ondc/org/settlement_basis": "Collection",
            "@ondc/org/settlement_basis_status": "Assert",
            "@ondc/org/settlement_window": "string",
            "@ondc/org/settlement_window_status": "Assert",
            "@ondc/org/settlement_details": [
              {
                "settlement_counterparty": "buyer-app",
                "settlement_phase": "sale-amount",
                "settlement_type": "neft",  (enum)
                "settlement_bank_account_no": "99679007677676",
                "settlement_ifsc_code": "HDFC900008",
                "upi_address": "string",
                "bank_name": "HDFC",
                "branch_name": "Delhi",
                "beneficiary_address": "delhi",
                "settlement_status": "PAID",  (enum)
                "settlement_reference": "string",
                "settlement_timestamp": "2022-10-28T10:34:58.469Z"
              }
            ]
          },
          "withholding_tax_gst": {
            "currency": "string",
            "value": "-123"
          },
          "withholding_tax_tds": {
            "currency": "string",
            "value": "0673658"
          },
          "deduction_by_collector": {
            "currency": "string",
            "value": "-123"
          },
          "order_recon_status": "null",
          "payerdetails": {
            "payer_name": "“Example1 company Pvt. Ltd",
            "payer_address": "string",
            "payer_account_no": 509424924294248,
            "payer_bank_code": "“HDFC0000000”",
            "payer_virtual_payment_address": "80abc@abctMh2h"
          },
          "settlement_reason_code": "01",
          "payout_bank_uri": "https://rsp.somebank.com/rsp/",
          "transaction_id": "string",
          "settlement_id": "121313",
          "settlement_reference_no": "3718683618631",
          "recon_status": "01",  (enum)
          "created_at": "2022-10-28T10:34:58.472Z",
          "updated_at": "2022-10-28T10:34:58.472Z"
        }
      ]
    }
  }
}
```

#### Step 5c - /on_receiver_recon Receiver may call /on_receiver_recon to RSP

Mandatory attributes:
```
{
  "context": {
  "domain": "nic2004:52110",
 "country": "IND",
 "city": "std:080",
  "action": "status",
  "core_version": "0.9.3",
  "bap_id": "abc.collectorapp.com",
  "bap_uri": "https://abc.collectorapp.com",
  "bpp_id": "abc.receiverapp.com",
  "bpp_uri": "https://abc.receiverapp.com",
  "transaction_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
  "message_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
  "timestamp": "2022-10-28T10:34:58.469Z",
  "key": "string",
   "ttl": "string"

  },
  "message": {
    "orderbook": {
      "orders": [
        {
          "id": "K106403902112759,
          "invoice_no": "2022/XYZ/12345-2",
          "collector_app_id": "abc.collectorapp.com",
          "receiver_app_id": "abc.receiverapp.com",
          "order_recon_status": "final",
          "transaction_id": "string",
          "settlement_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
          "settlement_reference_no": "3718683618631",
          "recon_status": "01"
        }
      ]
    }
  }
}
```

#### Step 5d- /on_collector_recon

Mandatory attributes:
```
{
  "context": {
  "domain": "nic2004:52110",
 "country": "IND",
 "city": "std:080",
  "action": "status",
  "core_version": "0.9.3",
  "bap_id": "abc.collectorapp.com",
  "bap_uri": "https://abc.collectorapp.com",
  "bpp_id": "abc.receiverapp.com",
  "bpp_uri": "https://abc.receiverapp.com",
  "transaction_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
  "message_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
  "timestamp": "2022-10-28T10:34:58.469Z",
  "key": "string",
   "ttl": "string"

  },
  "message": {
    "orderbook": {
      "orders": [
        {
          "id": "K106403902112759,
          "invoice_no": "2022/XYZ/12345-2",
          "collector_app_id": "abc.collectorapp.com",
          "receiver_app_id": "abc.receiverapp.com",
          "order_recon_status": "final",
          "transaction_id": "string",
          "settlement_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
          "settlement_reference_no": "3718683618631",
          "recon_status": "01"
        }
      ]
    }
  }
}
```

#### Correction flow

In case there is a mismatch between the settlement provided by the collector and settlement amount expected by the receiver, the receiver may initiate a correction flow based on the following details using /recon. If there is a mismatch, they can raise a dispute using the issue and grievance management system.

Mandatory attributes:
```
"settlement_reason_code": "01", (enum)
"payout_bank_uri": "https://rsp.somebank.com/rsp/",
"rsp_uri": "https://somersp.com/rsp/v1",
"rsp_id": "ABF428684",
"correction":
{
    "issue_initiator_ref": "1243242GQT$",
    "issue_responder_ref": "122424HGYG98", #maybe null in case self correction flow by the initiator
    "issue_type": "01", (enum)
    "issue_subtype": "01", (enum)
    "order_id": "12345654321",
    "order_amount":
    {
        "currency": "INR",
        "value": "123",
        "estimated_value": "123",
        "computed_value": "123",
        "listed_value": "123",
        "offered_value": "123",
        "minimum_value": "123",
        "maximum_value": "123"
    },
    "order_correction_amount":
    {
        "currency": "INR",
        "value": "345",
        "estimated_value": "345",
        "computed_value": "345",
        "listed_value": "345",
        "offered_value": "345",
        "minimum_value": "345",
        "maximum_value": "345"
    },
    "order_state": "string", (enum)
    "previous_settled_amount":
    {
        "currency": "INR",
        "value": "123",
        "estimated_value": "345",
        "computed_value": "345",
        "listed_value": "345",
        "offered_value": "345",
        "minimum_value": "345",
        "maximum_value": "345"
    },
    "settlement_id": "121313", 
    "settlement_reference_no": "3718683618631",
    "prev_settlement_reference_no":
    [
        "1234ABCD",
        "2345qwer"
    ],
    "recon_status": "01", (enum)
    "diff_amount":
    {
    "currency": "INR
    "value": "123",
    "estimated_value": "123",
    "computed_value": "123",
    "listed_value": "123",
    "offered_value": "123",
    "minimum_value": "123",
    "maximum_value": "123"
    },
}
```

### Recon status API - /recon_status

In case collector or RSP is looking for a status update, they will call /recon_status API to check an update on the status by providing the transaction id.

Mandatory fields:
```
{
  "context": {
   "domain": "nic2004:52110"
     "country": "IND",
     "city": "std:080",
     "action": "status",
    "core_version": "0.9.3",
    "bap_id": "abc.collectorapp.com",
   "bap_uri": "https://abc.collectorapp.com",
   "bpp_id": "abc.receiverapp.com",
   "bpp_uri": "https://abc.receiverapp.com",
   "transaction_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
   "message_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
   "timestamp": "2022-10-28T10:34:58.469Z",
   "key": "string",
   "ttl": "string"


  },
  "message": {
    "reconstatus": {
      "transaction_id": "string"
    }
  }
}
```

### Recon status API - /on_recon_status

Mandatory fields:
```
{
  "context": {
    "domain": "nic2004:52110"
     "country": "IND",
     "city": "std:080",
     "action": "status",
    "core_version": "0.9.3",
    "bap_id": "abc.collectorapp.com",
   "bap_uri": "https://abc.collectorapp.com",
   "bpp_id": "abc.receiverapp.com",
   "bpp_uri": "https://abc.receiverapp.com",
   "transaction_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
   "message_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
   "timestamp": "2022-10-28T10:34:58.469Z",
   "key": "string",
   "ttl": "string"

  },
  "message": {
    "orderbook": {
      "orders": [
        {
         "id": "K106403902112759,
           "invoice_no": "2022/XYZ/12345-2",
           "collector_app_id": "abc.collectorapp.com",
           "receiver_app_id": "abc.receiverapp.com",
           "order_recon_status": "final",
           "transaction_id": "string",
            "settlement_id": "6baa811a-6cbe-4ad3-94e9-cbf96aaff343",
           "settlement_reference_no": "3718683618631",
           "recon_status": "01"
        }
      ]
    }
  }
}
```

### API response

- Success with Schema validated (Mandatory attributes)
```
{
  "message":
  {
    "ack":
    {
      "status": "ACK"
    }
  },
}
```
- Failure (Mandatory attributes not supplied)
```
{
  “message":
  {
    "ack":
    {
      "status": "NACK"
    }
  },
  "error":
  {
    "code": "01",
    "path": "string",
    "message": "error_code, error_message is mandatory incase settlement_status = ERROR along with the schema mismatch”
  }
}
```

### Error Scenarios

1. Those Endpoints implemented on collector app, receiver app and settlement agency, which RSP will be calling, if RSP is not getting ACK response from them, RSP will keep retrying for a fixed time.
