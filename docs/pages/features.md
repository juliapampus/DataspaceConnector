---
layout: default
title: Features
nav_order: 3
description: ""
permalink: /Features
has_children: true
has_toc: true
---

# Features
{: .fs-9 }

Here, you can find a list of currently implemented features, which is continuously updated.
{: .fs-6 .fw-300 }

---

* Settings for TLS, proxy and Spring Boot basic authentication for backend endpoints
* Use valid IDS certificate and request DAT from DAPS
* Data resource registration (CRUD metadata) with internal H2 database or an external database
* Possibility to add multiple representations (different backend connections) to a resource
* Backend data handling internal (CRUD data) with internal H2 database or an external database
* Backend data handling external via `http GET` or `https GET` (with basic auth)
* IDS message handling with other IDS Connectors (as data provider and data consumer):
  `DescriptionRequestMessage`, `DescriptionResponseMessage`, `ArtifactRequestMessage`
  , `ArtifactResponseMessage`,
  `ContractRequestMessage`, `ContractAgreementMessage`, `ContractRejectionMessage`
  , `RejectionMessage`
* Read IDS response messages: deserialize and save requested data & metadata in internal database
* IDS message handling with the IDS Broker (IDS Lab): `ConnectorUpdateMessage`
  , `ConnectorUnavailableMessage`,
  `ResourceUpdateMessage`, `ResourceUnavailableMessage`, `QueryMessage`
* Further supported message types: sending `NotificationMessage` and `LogMessage`,
  receiving `NotificationMessage`
* Usage control with 8 ODRL policy patterns following the IDS policy language specifications:
  `provide access`, `prohibit access`, `usage during interval`, `n times usage`, `duration usage`,
  `usage until deletion`, `usage logging`, `usage notification`


## IDS Components

| Library | License | Owner | Contact |
| ------- | ------- | ----- | ------- |
| [IDS Information Model Library](https://maven.iais.fraunhofer.de/artifactory/eis-ids-public/de/fraunhofer/iais/eis/ids/infomodel/) | Apache 2.0 | Fraunhofer IAIS | [Sebastian Bader](mailto:sebastian.bader@iais.fraunhofer.de) |
| [IDS Information Model Serializer Library](https://maven.iais.fraunhofer.de/artifactory/eis-ids-public/de/fraunhofer/iais/eis/ids/infomodel-serializer/) | Apache 2.0 | Fraunhofer IAIS | [Sebastian Bader](mailto:sebastian.bader@iais.fraunhofer.de) |
| [IDS Framework](https://github.com/FraunhoferISST/IDS-Connector-Framework) | Apache 2.0 | Fraunhofer ISST | [Tim Berthold](mailto:tim.berthold@isst.fraunhofer.de) |
| [IDS Messaging Service](https://github.com/FraunhoferISST/IDS-Connector-Framework) | Apache 2.0 | Fraunhofer ISST | [Tim Berthold](mailto:tim.berthold@isst.fraunhofer.de) |

| Component | License | Owner | Contact |
| ------- | ------- | ----- | ------- |
| [IDS Broker](https://broker.ids.isst.fraunhofer.de/) | open core | Fraunhofer IAIS | [Matthias Böckmann](mailto:matthias.boeckmann@iais.fraunhofer.de) |
| [DAPS](https://daps.aisec.fraunhofer.de/) | open source | Fraunhofer AISEC | [Gerd Brost](mailto:gerd.brost@aisec.fraunhofer.de) |
| [ParIS]

The [ConfigManager](https://github.com/FraunhoferISST/IDS-ConfigurationManager) and its
[GUI](https://github.com/fkie/ids-configmanager-ui) are a part of the IDS connector's and aim to
facilitate the configuration of the Dataspace Connector and further IDS connector implementations.
Both projects are also open source.

The table below will document the compatibility of the component's versions.

| DSC Core Version | Configuration Manager | Configuration Manager GUI |
| --- | --- | --- |
| v4.x.x  |     |     |
| v5  |     |     |


### Core Functionality

For roadmap details,
see [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#core-functionality).

| Task                       | Responsible | Status  | Description                                  | Note |
|:---------------------------|:------------|:--------|:---------------------------------------------|:-----|
| Database Improvement       | ISST        | done    | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#database-improvement)      |      |
| Exception Handling         | ISST        | done    | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#exception-handling)        |      |
| Logging                    | ISST        | done    | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#logging)                   |      |
| Code Quality Improvements  | ISST        | done    | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#code-quality-improvements) |      |

### IDS Functionality

For roadmap details,
see [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#ids-functionality).

| Task                        | Responsible | Status | Description                                   | Note |
|:----------------------------|:------------|:-------|:----------------------------------------------|:-----|
| Ids-ready Test              | ISST        | done   | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#ids-ready-test)             |      |
| Config Manager Integration  | ISST        | done   | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#config-manager-integration) |      |
| Basic Policy Negotiation    | ISST        | done   | [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/roadmap#basic-policy-negotiation)   |      |
