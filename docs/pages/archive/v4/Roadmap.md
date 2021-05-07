---
layout: default
title: Roadmap
nav_order: 10
description: ""
permalink: /Archive/Roadmap
parent: Archive
---

# Roadmap

Some requirements are derived from the Dataspace Connector's [IDS-ready implementation concept](files/DSC_implementation_concept_ids_ready_v4.pdf "IDS-ready implementation concept").

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

### Logging

❌ **AUD 01 Access control logging**: Connector logs each access control decision in the form of an integrity protected log entry in its domain.

❌ **AUD 02 Data access logging**: Connector logs every access to data in the form of an integrity protected entry in its domain.

❌ **AUD 03 Configuration changes logging**: Connector logs any changes made to its configuration in the form of integrity protected entries in its domain.

❌ **CR 2.8 Auditable events**: The component shall provide the capability to generate audit records relevant to security for the following categories: a) access control; b) request errors; c) control system events; d) backup and restore event; e) configuration changes; and f) audit log events.  Individual audit records shall include:  g) timestamp; h) source (originating device, software process or human user account); i) category; j) type; k) event ID; and l) event result.

❌ **CR 2.9 Audit storage capacity**: The component shall a) provide the capability to allocate audit record storage capacity according to commonly recognized recommendations for log management; and b) provide mechanisms to protect against a failure of the component when it reaches or exceeds the audit storage capacity.

❌ **CR 2.10 Response to audit processing failures**: The component shall a) provide the capability to protect against the loss of essential services and functions in the event of an audit processing failure; and b) provide the capability to support appropriate actions in response to an audit processing failure according to commonly accepted industry practices and recommendations.

✅ **CR 2.11 Timestamps**: The component shall provide the capability to create timestamps (including date and time) for use in audit records.

### Routing (e.g. Apache Camel)

❌ As described [here](https://github.com/FraunhoferISST/DataspaceConnector/wiki/ids-connector-architecture), the integration of a routing framework as e.g. Apache Camel will improve and extend the data flow an its interception.

### App (Store) Integration

❌ **OS 01 Container support**: Connector supports installation and execution of containers.

❌ **APS 01 App signature**: Connector supports only apps possessing a valid signature. This signature is the signed check sum of the software artefact, which was created by means of a private key of the app publisher.

❌ **APS 02 App signature verification**: Connector verifies signature after app was downloaded and before it is installed, and before every execution of app. Public key of app publisher is contained in an X.509v3 certificate signed by a Certification Authority accepted by data provider and data consumer.

❌ **APS 05 App installation**: Connector supports apps delivered and installed as independent software containers (i.e. apps bring along possible dependencies of e.g. software modules themselves and can be used irrespective of Connector’s configuration).

❌ **APS 06 App Store**: Connector receives apps from a central app store.

❌ **CR 3.4 Software and information integrity**: Components shall provide the capability to perform or support integrity checks on software, configuration and other information as well as the recording and reporting of the results of these checks or be integrated into a system that can perform or support integrity checks.

❌ **NDR 2.4 Mobile code**: In the event that a network device utilizes mobile code technologies, the network device shall provide the capability to enforce a security policy for the usage of mobile code technologies. The security policy shall allow, at a minimum, the following actions for each mobile code technology used on the network device:  a) Control execution of mobile code; b) control which users (human, software process, or device) are allowed to transfer mobile code to/from the network device; and c) control the code execution based upon integrity checks on mobile code and prior to the code being executed.

❌ **NDR 3.2 Protection from malicious code**: The network device shall provide for protection from malicious code.

### Network Support

❌ **CR 7.3 Control system backup**: The component shall provide the capability to participate in system level backup operations in order to safeguard the component state (user- and system-level information). The backup process shall not affect the normal component operations.

❌ **CR 7.4 Control system recovery and reconstitution**: The component shall provide the capability to recovered and reconstitute to a known secure state after a disruption or failure.

❌ **CR 7.6 Network and security configuration settings**: The component shall provide the capability to be configured according to recommended network and security configurations as described in guidelines provided by the control system supplier. The component shall provide an interface to the currently deployed network and security configuration settings.

❌ **CR 7.7 Least functionality**: The component shall provide the capability to specifically restrict the use of unnecessary functions, ports, protocols and/or services.

❌ **NDR 1.13 Access via untrusted networks**: The network device supporting device access into a network shall provide the capability to monitor and control all methods of access to the network device via untrusted networks.

❌ **NDR 5.2 Zone boundary protection**: A network device at a zone boundary shall provide the capability to monitor and control communications at zone boundaries to enforce the compartmentalization defined in the risk-based zones and conduits model.

### Query Broker

❌ **BRK 01 Broker service inquiries**: Connector supports broker service inquiries by means of browsing self-descriptions of Connectors registered there.

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

### User Management

❌ **CR 1.1 (1) Unique identification and authentication**: The component shall provide the capability to uniquely identify and authenticate all human users.

❌ **CR 1.3 Account management**: The component shall provide the capability to support the management of all accounts directly or integrated into a system that manages accounts according to IEC 62443‑3‑3 SR 1.3.

❌ **CR 1.10 Authenticator feedback**: When a component provides an authentication capability, the component shall provide the capability to obscure feedback of authentication information during the authentication process.

❌ **CR 1.11 Unsuccessful login attempts**: When a component provides an authentication capability, the component shall provide the capability to:  a) enforce a limit of a configurable number of consecutive invalid access attempts by any user (human, software process or device) during a configurable time period; and b) deny access for a specified period of time or until unlocked by an administrator when this limit has been reached. An administrator may unlock an account prior to the expiration of the timeout period.

❌ **CR 2.5 Session lock**: If a component provides a human user interface, whether accessed locally or via a network, the component shall provide the capability a) to protect against further access by initiating a session lock after a configurable time period of inactivity or by manual initiation by the user (human, software process or device); and  b) for the session lock to remain in effect until the human user who owns the session, or another authorized human user, re-establishes access using appropriate identification and authentication procedures.

❌ **CR 2.12 Non-repudiation**: If a component provides a human user interface, the component shall provide the capability to determine whether a given human user took a particular action. Control elements that are not able to support such capability shall be listed in component documents.

❌ **CR 3.8 Session integrity**: The component shall provide mechanisms to protect the integrity of communications sessions including: a) the capability to invalidate session identifiers upon user logout or other session termination (including browser sessions); b) the capability to generate a unique session identifier for each session and recognize only session identifiers that are system-generated; and c) the capability to generate unique session identifiers with commonly accepted sources of randomness.

❌ **CR 4.1 Information confidentiality**: The component shall a) provide the capability to protect the confidentiality of information at rest for which explicit read authorization is supported; and b) support the protection of the confidentiality of information in transit as defined in IEC 62443-3-3 SR 4.1.

❌ **CR 6.1 Audit log accessibility**: The component shall provide the capability for authorized humans and/or tools to access audit logs on a read-only basis.

### Update Support

❌ **NDR 3.10 Support for updates**: Network devices shall support the ability to be updated and upgraded.

### Software Tests

❌ **T_CA.1 Test coverage analysis**: The test coverage analysis shall show a complete correspondence between the component’s interfaces and the tests in the test documentation.

❌ **T_CA.2 Test procedures for subsystems**: The test procedures shall contain descriptions of the security-related subsystem behavior and interaction that are tested.

❌ **T_TD.1 Test documentation**: The test documentation shall include scenarios for performing each test, expected test results and actual test results.

❌ **T_TD.2 Test configuration**: The test configuration shall be consistent with the configuration list (S_CM.6).

❌ **T_TD.3 Ordering Dependencies**: The test documentation shall provide sufficient instructions for any ordering dependencies of the tests.

### Software Documentation

❌ **D_AD.1 Secure initialization**: The development documentation shall include an architectural description stating how the component preserves security during initialization, i.e. how an initial secure state is reached.

❌ **D_AD.2 Tamper protection**: The development documentation shall include an architectural description stating how the component is able to protect itself from tampering by untrusted active entities.

❌ **D_AD.3 Security-enforcing mechanisms**: The development documentation shall include an architectural description containing an analysis that adequately describes how the security-enforcing mechanisms of the component cannot be bypassed.

✅ **D_IS.1 Interface purpose and usage**: The development documentation shall include an interface specification stating the purpose of and method of use for each interface of the component.

✅ **D_IS.2 Interface parameters**: The development documentation shall include an interface specification completely and accurately describing all parameters associated with every interface.

✅ **D_DD.1 Subsystem structure**: The development documentation shall include a design description stating the structure of the entire component in terms of subsystems.

❌ **G_AP.1 Acceptance procedures**: The developer shall provide a guidance documentation describing the acceptance procedures, i.e. the steps necessary for secure acceptance of the component by the end user.

✅ **G_AP.2 Installation procedures**: The developer shall provide a guidance documentation describing the installation procedures, i.e. the steps necessary for secure installation of the component and the secure preparation of the operational environment.

❌ **G_OG.1 Interface usage for each user role**: The developer shall provide an operational user guidance describing for each user role, the secure use of the available interfaces provided by the component.

❌ **G_OG.2 Possible modes of operation**: The operational user guidance shall identify all possible modes of operation of the component (including, if applicable, operation following failure or operational error), their consequences and implications for maintaining secure operation.

❌ **S_DL.1 Secure delivery**: The delivery documentation shall describe all procedures that are necessary to maintain security when distributing versions of the component or parts of it to the consumer.

### Exception Handling

✅ **CR 3.7 Error handling:** Components shall identify and handle error conditions in a manner that does not provide information that could be exploited by adversaries to attack the connector.

### Code Quality Improvements

✅ **S_CM.1 Unique component reference**: The component shall be labelled with a unique reference.

✅ **S_CM.2 Consistent usage of component reference**: The component shall be labelled with a unique reference.

❌ **S_CM.6 (1) Configuration list content (1)**: The configuration list shall include the following set of items: a) the component itself; b) the evaluation evidence required for the evaluation.

✅ **S_CM.7 Unique identification based on configuration list**: The configuration list shall uniquely identify each configuration item.

✅ **S_CM.8 Developer Information**: The configuration list shall indicate the developer of each security functionality relevant configuration item.

❌ **S_FR.1 Tracking of reported security flaws**: The flaw remediation procedures shall describe the procedures used to track all reported security flaws in each release of the component.

❌ **S_FR.2 Security flaw description**: The application of the flaw remediation procedures shall produce a description of each security flaw in terms of its nature and effects.

❌ **S_FR.3 Status of corrective measures**: The application of flaw remediation procedures shall identify the status of finding a correction to each security flaw.

### Others

Optional requirements from the IDS-ready concept:

❌ **IAM 03 Online certificate status check**: Connector supports online status check of certificates issued (e.g. Online Certificate Status Protocol, OCSP).

❌ **CR 1.12 System use notification**: When a component provides local human user access/HMI, it shall provide the capability to display a system use notification message before authenticating. The system use notification message shall be configurable by authorized personnel.

❌ **CR 1.14 Strength of symmetric key-based authentication**: For components that utilize symmetric keys, the component shall provide the capability to:  v) establish the mutual trust using the symmetric key; w) store securely the shared secret (the authentication is valid as long as the shared secret remains secret); x) restrict access to the shared secret; and y) ensure that the algorithms and keys used for the symmetric key authentication conform to 8.5.

❌ **CR 2.2 Wireless use control**: If a component supports usage through wireless interfaces it shall provide the capability to integrate into the system that supports usage authorization, monitoring and restrictions according to commonly accepted industry practices.

❌ **CR 3.5 Input validation**: The component shall validate the syntax, length and content of any input data that is used as an industrial process control input or input via external interfaces that directly impacts the action of the component.

❌ **CR 3.6 Deterministic output**: Components that physically or logically connect to an automation process shall provide the capability to set outputs to a predetermined state if normal operation as defined by the component supplier cannot be maintained.

❌ **NDR 1.6 Wireless Access Management**: A network device supporting wireless access management shall provide the capability to identify and authenticate all users (humans, software processes or devices) engaged in wireless communication.
