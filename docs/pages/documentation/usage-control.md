---
layout: default
title: Usage Control
nav_order: 5
description: ""
permalink: /Documentation/UsageControl
parent: Documentation
---

# Usage Control
{: .fs-9 }

Usage policies are an important aspect of IDS, further details are explained on this page.
{: .fs-6 .fw-300 }

---

The Dataspace Connector supports usage policies written in an IDS specific policy language following
the [ODRL](https://www.w3.org/TR/odrl-model/#policy) standard. Using this, the Dataspace Connector
does not support all specified attributes, but the ones to handle eight selected patterns.

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
runtime. There are three points in time when the policies are checked. We distinguish between the
provider and the consumer side.
