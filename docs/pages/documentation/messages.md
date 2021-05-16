---
layout: default
title: Messages
nav_order: 4
description: ""
permalink: /Documentation/Messages
parent: Documentation
---

# IDS Messages
{: .fs-9 }

...
{: .fs-6 .fw-300 }

---

## Message Types

IDS messages and their content are defined [here](http://htmlpreview.github.io/?https://github.com/IndustrialDataSpace/InformationModel/blob/feature/message_taxonomy_description/model/communication/Message_Description.htm).
The table below lists the supported message types. Thereby, it is to be distinguished whether the
Connector provides functionality for sending messages as request or response, or for processing
incoming messages.

| IDS Message Type                    | Outgoing           | Incoming | Description              |
|:------------------------------------|:------------------:|---------:|:-------------------------|
| ArtifactRequestMessage              | request            | x        | message asking for retrieving a specified artifact  |
| DescriptionRequestMessage           | request            | x        | message requesting metadata (If no URI is supplied via the ids:requestedElement field, this messages is treated like a self-description request.) |
| ContractRequestMessage              | request            | x        | message containing a contract offer |
| ArtifactResponseMessage             | response           |          | message that contains the artifact's data in the payload |
| DescriptionResponseMessage          | response           |          | message containing the metadata of a requested object |
| ContractAgreementMessage            | request + response |          | message containing a contract agreement |
| ContractRejectionMessage            | response           |          | message indicating rejection of a contract |
| RejectionMessage                    | response           |          | message that notifies the issuer that processing the request message has failed |
| NotificationMessage                 | request            | x        | message is informative and no response is expected |
| LogMessage                          | request            |          | message that is used to transfer logs e.g. to the clearing house |
| MessageProcessedNotificationMessage | response           |          | message that notifies whether a message has been received and successfully processed |
| ConnectorUpdateMessage              | request            |          | message notifying the recipient(s) about the availability and current configuration of a connector |
| ConnectorUnavailableMessage         | request            |          | message indicating that a specific connector is unavailable |
| ResourceUpdateMessage               | request            | x        | message indicating the availability and current description of a specific resource |
| ResourceUnavailableMessage          | request            |          | message indicating that a specific resource is unavailable |
| QueryMessage                        | request            |          | message intended to be consumed by specific components |

`request` = initially send this kind of IDS message | `response` = response with this IDS message

## Sequences
