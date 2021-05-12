---
layout: default
title: Provider
nav_order: 1
description: ""
permalink: /CommunicationGuide/Provider
parent: Communication Guide
---

# Providing Data
{: .fs-9 }

Usage policies are an important aspect of IDS, further details are explained on this page.
{: .fs-6 .fw-300 }

---

**Policy Enforcement**

When the data provider receives an `ArtifactRequestMessage` from an external Connector, the
`ArtifactMessageHandler` checks the pattern of the policy that was added to the requested resource.
If the pattern matches one of the following five, an appropriate policy check is performed:
`PROVIDE_ACCESS`, `PROHIBIT_ACCESS`, `USAGE_DURING_INTERVAL`, `USAGE_UNTIL_DELETION`, or
`CONNECTOR_RESTRICTED_USAGE`.

Depending on the specified rules, the access permission will be set to true or false. If it is true,
the data provider returns the data. If not, it will respond with a `RejectionReason.NOT_AUTHORIZED`.

_Note that the Dataspace Connector is able to received resources with usage policies that follow
the IDS policy language but not one of the supported patterns. As, by default, the policy check on
the data consumer side would not allow to access data whose policies cannot be enforced, you are
able to ignore unsupported patterns with setting the boolean at the endpoint
`/api/configuration/pattern` or the property `policy.allow-unsupported-patterns` in the
`application.properties` to `true`. As a data consumer, you are legally bound to concluded
contract agreements that are technically mapped to IDS usage policies. Therefore, you have to
ensure, that your backend applications technically enforce the usage policies instead._
![Unsupported Pattern Settings](assets/images/docs/config-pattern.png)

---
**Resource Updates**


---
