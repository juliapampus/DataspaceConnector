---
layout: default
title: Roadmap
nav_order: 4
description: ""
permalink: /Features/Roadmap
parent: Features
---

# Roadmap
{: .fs-9 }

Ensuring developments following the same goal, the project's roadmap and each aspect are described in detail.
{: .fs-6 .fw-300 }

---

Some requirements are derived from the Dataspace Connector's [IDS-ready implementation concept](pages/archive/v4/files/DSC_implementation_concept_ids_ready_v4.pdf "IDS-ready implementation concept").

## Core-Functionality

This list follows no timeline. Instead, individual tasks can be priority-assigned. Thus, the implementation can be freely scheduled and extended, depending on the interests and projects of potential contributors. The rating ranges from 1 (= high priority) to 3 (= low priority).

| Priority | Task                                  | Responsible | Status      | Description                                              | Note        |
|----------|:--------------------------------------|:------------|:------------|:---------------------------------------------------------|:------------|
| 2        | Connector Orchestration in Kubernetes |             | in progress | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#connector-orchestration-in-kubernetes) | [guide](https://github.com/International-Data-Spaces-Association/DataspaceConnector/wiki/Kubernetes) |
| 3        | Network Support                       |             |             | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#network-support)                       |  |
| 2        | User Management                       |             |             | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#user-management)                       |  |
| 2        | Software Tests                        |             | ongoing     | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#software-tests)                        |  |
| 1        | Software Documentation                |             | ongoing     | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#software-documentation)                |  |
| 3        | Amazon AWS                            |             |             |  |  |
| 1        | Audit Logging                            |             |             |  |  |
| 1| Code Quality Improvements  | ISST        | in progress | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#code-quality-improvements) |      |
| 1| Database Improvement       | ISST        | in progress | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#database-improvement)      |      |

## IDS-Functionality

The implementation of the following requirements primarily focuses on IDS developments.
Responsible for this are mainly [@juliapampus](https://github.com/juliapampus), [@brianjahnke](https://github.com/brianjahnke), and [@ronjaquensel](https://github.com/ronjaquensel).

| Timeline | Task                                   | Responsible | Status      | Description                                    | Note        |
|:---------|:---------------------------------------|:------------|:------------|:-----------------------------------------------|:------------|
| Q1/21    | Routing (e.g. Apache Camel)            | ISST        | in progress | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#routing-eg-apache-camel)     |   |
|          | App (Store) Integration                | ISST        |             | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#app-store-integration)       |   |
|          | Query Broker                           | ISST        |             | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#query-broker)                |   |
|          | Integration of IDSCP 2.0               | ISST        |             | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#integration-of-idscp-20)     | postponed to Q2 |
|          | IDS-LDP Integration                    | ISST        |             | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#ids-ldp-integration)         | postponed to Q2 |
|          | Support Query Parameters               | ISST        | in review   |                                                |   |
|          | Basic Clearing House Integration       | ISST        | in progress | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#clearing-house-integration)  | in revision |
| Q2/21    | Usage Control Extension                | ISST        |             | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#usage-control-extension)     |   |
|          | Support ParIS                          | ISST        |             | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#support-paris)               |   |
|          | Support Vocabulary Provider            | ISST        |             | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#support-vocabulary-provider) |   |
|          | Extended Clearing House Integration    | ISST        |             | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#clearing-house-integration)  |   |
|          | Support of complex REST backends       | ISST        | in progress |                                                | IDS-proxy |

## Open Topics

Here, we will collect terms and topics whose implementation and integration can be discussed if required.

* [GUI Development](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#gui-development)
* Integration of hyperscalers
* Query Languages: https://partiql.org/
* Support streaming data
* Asynchronous message handling
* Push data from provider to consumer
* Additional encryption of transferred data


## Details

Please find a detailed explanation of the aforementioned roadmap items below.

### Ids-ready Test

✅ The test for the IDS-ready label comprises different requirements, which are assigned to the 3 levels base, trust and trust+. The last plugfest has shown that these 3 possible levels will be extended. With the DSC, we are aiming for the base profile. Currently, we are writing a concept for the IDS-ready label test. This includes exactly the criteria that will also be checked during the later certification. At that time, however, the connector has to actually implement the requirements.

### Config Manager Integration

✅ The Configuration Manager (CM) will provide a user-friendly interaction with the Dataspace Connector's endpoints by using a GUI. For compatibility, some further endpoints may need to be implemented and the structure of individual functionalities has to be modularized.

### GUI Development

✅ For now, providing a GUI with using the CM has no impact on the Dataspace Connector's implementation. Nevertheless, when creating endpoints, it is important to keep in mind that the user should be able to make small adjustments via the GUI. The GUI's source code can be found [here](https://github.com/fkie/ids-configmanager-ui).

We are open for any developments regarding a separate GUI for the Dataspace Connector. This would directly interact with the connector endpoints without using the CM.

### Basic Policy Negotiation

✅

### Clearing House Integration

❌

### Connector Orchestration in Kubernetes

❌

### Database Improvement

✅

### Routing (e.g. Apache Camel)

❌ As described [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/ids-connector-architecture), the integration of a routing framework as e.g. Apache Camel will improve and extend the data flow an its interception.

### Integration of IDSCP 2.0

❌ To support higher security profiles, the IDSCP 2.0 communication library is integrated into the IDS Framework used by the DSC. Possibly some modifications of the DSC will be necessary.

### IDS-LDP Integration

❌

### Usage Control Extension

❌ Currently, the DSC supports eight policy patterns out of 21. In order to support further policies, the integration of the PIPs is required.

❌ Policy enforcement should be configurable. For this, the current access and usage control must be modular and interchangeable. As a possible alternative, MyData and a corresponding interceptor for the data flow will be integrated into the DSC.

❌ Possibility to define policy patterns.

### Support ParIS

❌ In order to provide additional information about the IDS participants, the DSC needs the connection of the Participant Information Service (ParIS) provided by the Fraunhofer IAIS.

### Support Vocabulary Provider

❌ For the integration of user-specific vocabularies for data description, the Vocabulary Provider VoCol will be integrated.
