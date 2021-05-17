---
layout: default
title: Consumer
nav_order: 2
description: ""
permalink: /CommunicationGuide/Consumer
parent: Communication Guide
---

# Consuming Data
{: .fs-9 }

Usage policies are an important aspect of IDS, further details are explained on this page.
{: .fs-6 .fw-300 }

---

**Policy Enforcement**

After the requested data and its metadata are saved in the Connector's database, it can be
accessed by using the according endpoint. If the user wants to get the data from the data consumer's
database, the usage policies of the requested data resource are checked for the following patterns:
`USAGE_DURING_INTERVAL`, `DURATION_USAGE`, `USAGE_UNTIL_DELETION`, `USAGE_LOGGING`,
`USAGE_NOTIFICATION`, and `N_TIMES_USAGE`. The policy is then implemented using the detected
pattern.

As described above, depending on the rule values, the access permission will be set to true or
false, and correspondingly, the data is either displayed or not.

On top of that, the Dataspace Connector performs a periodic policy check. If a duty determining the
deletion date and time, as in `USAGE_UNTIL_DELETION`, is detected, usage control is executed and
the data concerned is deleted.

_Note that the Dataspace Connector is able to received resources with usage policies that follow
the IDS policy language but not one of the supported patterns. As, by default, the policy check on
the data consumer side would not allow to access data whose policies cannot be enforced, you are
able to ignore unsupported patterns with setting the boolean at the endpoint
`/api/configuration/pattern` or the property `policy.allow-unsupported-patterns` in the
`application.properties` to `true`. As a data consumer, you are legally bound to concluded
contract agreements that are technically mapped to IDS usage policies. Therefore, you have to
ensure, that your backend applications technically enforce the usage policies instead._
![Unsupported Pattern Settings](assets/images/config_pattern.png)

---

**Parametrized Data Consumption**

Here, you can find details on how to use dynamic URLs for backends.

---
**Resource Updates**


---
