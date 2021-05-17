---
layout: default
title: Introduction
nav_order: 2
description: ""
permalink: /Introduction
---

# Introduction
{: .fs-9 }

New to IDS? Get a short introduction and information about the reference architecture model at a glance.
{: .fs-6 .fw-300 }

---

Einleitung IDS

## IDS Ecosystem

Übersicht Ecosystem

## IDS Connector
Was ist ein Connector?

Ein IDS Connector wird durch das IDS RAM definiert
Zusätzliche Kriterien werden durch die Zertifizierung der Komponente vorgegeben

Austausch von Daten und Anreicherung dieser mit Metainformationen
Ontologie zur Beschreibung von Ressourcen
Nutzungsbedingungen
Vorteil: kein zentraler Datenspeicher
Datenintegration aus verschiedenen Datenquellen
Datenzugriff ausschließlich durch andere IDS Connectoren
Technische Umsetzung der Datensouveränität
Security Profile/Zertifizierung: base, trust, trust+

![RAM Connector Architecture](assets/images/ram_architecture.png)

Setzt sich zusammen aus verschiedenen Systemservices
Execution core container with Message Systems (Message Router/Bus)
Configuration Manager to configure the Connector (Execution Core Container, Application Container Management, Network, Firewalls, etc.)
Data Apps
Application Container Management
Hardware/Operating System

DIN EN Norm: IT-Sicherheit für industrielle Automatisierungssysteme
IDS Connector adressiert auch die Bereiche Application Container Management, Netzwerk, OS, Hardware etc.  Trust

DIN EN IEC 62443-4-2
IAC: Identification and authentication control
UC: Use Control
SI: System integrity
DC: Data confidentiality
RDF: Restricted data flow
RA: Resource availability
SAR: Software Application Requirements
NDR: Network device requirements

Secure Development: Testing, Documentation, etc.

IDS Specification
Communication Integrity
Data Usage Control
Informationsmodel
Identity and Access Management
Broker Service
Operating System
Apps and App Store Connection
Data Usage Transparency



## Reference Implementation
Implementierung am Beispiel des DSC

IDS Connector Referenzimplementierung der Abteilung Datenwirtschaft des Fraunhofer ISST
Open Source Softwareprojekt
Einfacher Einstieg in das IDS Ecosystem
Anschluss an den Data Space und Austausch von Daten
Prüfen und Durchsetzen von Nutzungsbedingungen

Entwicklung weiterer DSC und IDS Komponenten
ConfigManager zur Konfigration des Dataspace Connectors
Vereinfachte Bedienung über die Configmanager-GUI

Unterstützt und gefördert durch die IDSA




Verweis auf Architektur 

## Links

[IDS Information Model]() • [IDS RAM]() • [IDSA Jive]()
