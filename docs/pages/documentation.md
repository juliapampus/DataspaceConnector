---
layout: default
title: Documentation
nav_order: 7
description: ""
permalink: /Documentation
has_children: true
has_toc: true
---

# Software Documentation
{: .fs-9 }

For the developers, some software documentation is provided.
{: .fs-6 .fw-300 }

---

### Connector Architecture
The Dataspace Connector is a Java application following basic Spring Boot functionalities and
architecture patterns. It currently supports the IDS Information Model version 4.0.0 and integrates
the IDS Connector Framework Library for IDS functionalities and message handling. It provides a
REST API for loading, updating, and deleting IDS persisted resources in a local database.

![Connector Architecture](images/connector-architecture.png)

### Network Architecture
The Connector will support a segmented network. Every running container will be associated to a
different network zone by providing its own virtual network stack. The Connector as the core
container will have root rights and be able to manage network and firewall configurations for all
separated containers and their networks. As root namespace, it provides an external IP and can be
reached from an external network.

![Network Architecture](images/network-architecture.png)

## Class Diagrams

## Process Diagrams

## Sequence Diagrams

### Metadata & Data Exchange

![Message Sequence Overview](images/sequence-messages.png)

### Policy Negotiation

![Policy Negotiation Overview](images/sequence-negotiation.png)
