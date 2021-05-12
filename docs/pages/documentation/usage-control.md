---
layout: default
title: Usage Control
nav_order: 5
description: ""
permalink: /Documentation/UsageControl
parent: Documentation
---

# IDS Usage Control Policies
{: .fs-9 }

Usage policies are an important aspect of IDS, further details are explained on this page.
{: .fs-6 .fw-300 }

---

"An IDS Contract is implicitly divided to two main sections: the contract specific metadata and the
`IDS Usage Control Policy` of the contract. 

The contract specific information (e.g., date when the contract has been issued or references to the 
sensitive information about the involved parties) has no effect on the enforcement. However, the
`IDS Usage Control Policy` is the key motive of organizational and technical Usage Control 
enforcement.

Furthermore, an `IDS Usage Control Policy` contains several Data Usage Control statements (e.g., 
permissions, prohibitions and obligations) called `IDS Rules` and is specified in the `IDS Usage 
Control Language` which is a technology independent language. The technically enforceable rules
shall be transformed to a technology dependent policy (e.g., MYDATA) to facilitate the Usage Control 
enforcement of data sovereignty." (p.22, IDSA Position Paper Usage Control in the IDS)

Following the specifications [here](https://internationaldataspaces.org/wp-content/uploads/IDSA-Position-Paper-Usage-Control-in-the-IDS-V3.0.pdf),
the IDS currently defines 21 policy classes. The Dataspace Connector supports usage policies written 
in the `IDS Usage Control Language` based on [ODRL](https://www.w3.org/TR/odrl-model/#policy). 
Using this, the Dataspace Connector does not support all specified attributes, but the ones to 
handle eight selected patterns.

Example policies for each of them can be found by using the endpoint `POST /api/examples/policy`.
- **Provide Access**: provides data usage without any restrictions
- **Prohibit Access**: prohibits the data usage
- **Usage During Interval**: provides data usage within a specified time interval
- **N Times Usage**: allows data usage for n times
- **Duration Usage**: allows data usage for a specified time period
- **Usage Until Deletion**: allows data usage within a specified time interval with the restriction
  to delete it at a specified time stamp
- **Usage Logging**: allows data usage if logged to the Clearing House
- **Usage Notification**: allows data usage with notification message
- **Connector Restricted Usage**: allows data usage for a specific connector

The usage policy is added to the metadata of a resource. The classes at
`io.dataspaceconnector.services.usagecontrol` read, classify, verify, and enforce the policies at
runtime. 

## Policy Patterns 

_Position Paper | Version 3.0 | March 2021_

| Number | Title                                          | Supported |
|:-------|:-----------------------------------------------|:---------:|
| 1      | Allow the Usage of the Data                    | x         |
| 2      | Connector-restricted Data Usage                | x         |
| 3      | Application-restricted Data Usage              | -         |
| 4      | Interval-restricted Data Usage                 | x         |
| 5      | Duration-restricted Data Usage                 | x         |
| 6      | Location Restricted Policy                     | -         |
| 7      | Perpetual Data Sale (Payment once)             | -         |
| 8      | Data Rental (Payment frequently)               | -         |
| 9      | Role-restricted Data Usage                     | -         |
| 10     | Purpose-restricted Data Usage Policy           | -         |
| 11     | Event-restricted Usage Policy                  | -         |
| 12     | Restricted Number of Usages                    | x         |
| 13     | Security Level Restricted Policy               | -         |
| 14     | Use Data and Delete it After                   | x         |
| 15     | Modify Data (in Transit)                       | -         |
| 16     | Modify Data (in Rest)                          | -         |
| 17     | Local Logging                                  | x         |
| 18     | Remote Notifications                           | x         |
| 19     | Attach Policy when Distribute to a Third-party | -         |
| 20     | Distribute only if Encrypted                   | -         |
| 21     | State Restricted Policy                        | -         |
