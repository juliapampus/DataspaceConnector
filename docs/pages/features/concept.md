---
layout: default
title: IDS-ready
nav_order: 5
description: ""
permalink: /Features/Ids-ready
parent: Features
---

# IDS-ready Implementation Concept
{: .fs-9 }

Following the IDS certification criteria, the IDS Connector has to provide certain software criteria.
{: .fs-6 .fw-300 }

---

The ids-ready implementation concept of the Dataspace Connector can be found 
[here](assets/files/DSC_implementation_concept_ids_ready_v4.pdf). In the table below is an overview 
of all criteria for the base profile and whether it is already implemented or not. A more detailed 
description of the individual issues can be found in the PDF file.

|    | No.         | Title       | 
|:---|:------------|:------------|
| ✅ | COM 01      | Protected connection |
| ✅ | COM 02      | Mutual authentication |
| ✅ | COM 03      | State of the art cryptography |
| ✅ | USC 01      | Definition of usage policies |
| ✅ | _USC 02_    | _Sending of usage policies_ |
| ✅ | _USC 03_    | _Usage policy enforcement_ |
| ✅ | INF 01      | Self-Description (at Connector) |
| ✅ | INF 02      | Self-Description (at Broker) |
| ✅ | INF 03      | Self-Description content |
| ✅ | INF 04      | Self-Description evaluation |
| ✅ | INF 05      | Dynamic attribute tokens |
| ✅ | IAM 01      | Connector identifier |
| ✅ | IAM 02      | Time Service |
| ✅ | IAM 03      | Online certificate status check |
| ✅ | IAM 04      | Attestation of dynamic attributes |
| ❌ | BRK 01      | Broker service inquiries |
| ✅ | BRK 02      | Broker registration |
| ✅ | BRK 03      | Broker registration update |
| ❌ | OS 01       | Container support |
| ❌ | APS 01      | App signature |
| ❌ | APS 02      | App signature verification |
| ❌ | APS 05      | App installation |
| ❌ | APS 06      | App Store |
| ❌ | AUD 01      | Access control logging |
| ❌ | AUD 02      | Data access logging |
| ❌ | AUD 03      | Configuration changes logging |
| ✅ | CR 1.1      | Human user identification and authentication |
| ❌ | CR 1.1 (1)  | Unique identification and authentication |
| ✅ | CR 1.2      | Software process and device identification and authentication |
| ✅ | CR 1.2 (1)  | Unique identification and authentication |
| ❌ | CR 1.3      | Account management |
| ❌ | CR 1.4      | Identifier management |
| ❌ | CR 1.5      | Authenticator management |
| ❌ | CR 1.7      | Strength of password-based authentication |
| ❌ | CR 1.8      | Public key infrastructure certificates |
| ❌ | CR 1.9      | Strength of public key-based authentication |
| ✅ | CR 1.10     | Authenticator feedback |
| ❌ | CR 1.11     | Unsuccessful login attempts |
| ❌ | CR 1.12     | System use notification |
| ❌ | CR 1.14     | Strength of symmetric key-based authentication |
| ✅ | CR 2.1      | Authorization enforcement |
| ❌ | CR 2.2      | Wireless use control |
| ❌ | CR 2.5      | Session lock |
| ❌ | CR 2.8      | Auditable events |
| ❌ | CR 2.9      | Audit storage capacity |
| ❌ | CR 2.10     | Response to audit processing failures |
| ✅ | CR 2.11     | Timestamps |
| ❌ | CR 2.12     | Non-repudiation |
| ✅ | CR 3.1      | Communication integrity |
| ✅ | CR 3.1 (1)  | Communication authentication |
| ❌ | CR 3.3      | Security functionality verification |
| ❌ | CR 3.4      | Software and information integrity |
| ❌ | CR 3.5      | Input validation |
| ❌ | CR 3.6      | Deterministic output |
| ✅ | CR 3.7      | Error handling |
| ❌ | CR 3.8      | Session integrity |
| ✅ | CR 4.1      | Information confidentiality |
| ❌ | CR 4.2 (1)  | Erase of shared memory resources |
| ✅ | CR 4.3      | Use of cryptography |
| ❌ | CR 5.1      | Network segmentation |
| ❌ | CR 6.1      | Audit log accessibility |
| ❌ | CR 7.1      | Denial of service protection |
| ❌ | CR 7.2      | Resource management |
| ❌ | CR 7.3      | Control system backup |
| ❌ | CR 7.4      | Control system recovery and reconstitution |
| ❌ | CR 7.6      | Network and security configuration settings |
| ✅ | CR 7.7      | Least functionality |
| ❌ | SAR 2.4     | Mobile code |
| ❌ | SAR 2.4 (1) | Mobile code integrity check |
| ❌ | SAR 2.4 (1) | Protection from malicious code |
| ❌ | NDR 1.6     | Wireless Access Management |
| ❌ | NDR 1.13    | Access via untrusted networks |
| ❌ | NDR 2.4     | Mobile code |
| ❌ | NDR 3.2     | Protection from malicious code |
| ❌ | NDR 3.10    | Support for updates |
| ❌ | NDR 3.14    | Integrity of the boot process |
| ❌ | NDR 5.2     | Zone boundary protection |
| ❌ | NDR 5.3     | General purpose, person-to-person communication restrictions |
| ❌ | D_AD.1      | Secure initialisation |
| ❌ | D_AD.2      | Tamper protection |
| ❌ | D_AD.3      | Security-enforcing mechanisms |
| ✅ | D_IS.1      | Interface purpose and usage |
| ✅ | D_IS.2      | Interface parameters |
| ✅ | D_DD.1      | Subsystem structure |
| ❌ | G_AP.1      | Acceptance procedures |
| ✅ | G_AP.2      | Installation procedures |
| ✅ | G_OG.1      | Interface usage for each user role |
| ❌ | G_OG.2      | Possible modes of operation |
| ✅ | S_CM.1      | Unique component reference |
| ✅ | S_CM.2      | Consistent usage of component reference |
| ❌ | S_CM.6 (1)  | Configuration list content (1) |
| ❌ | S_CM.7      | Unique identification based on configuration list |
| ❌ | S_CM.8      | Developer Information |
| ❌ | S_DL.1      | Secure delivery |
| ❌ | S_FR.1      | Tracking of reported security flaws |
| ❌ | S_FR.2      | Security flaw description |
| ❌ | S_FR.3      | Status of corrective measures |
| ✅ | T_CA.1      | Test coverage analysis |
| ❌ | T_CA.2      | Test procedures for subsystems |
| ❌ | T_TD.1      | Test documentation |
| ❌ | T_TD.2      | Test configuration |
| ❌ | T_TD.3      | Ordering Dependencies |
