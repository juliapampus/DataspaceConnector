---
layout: default
title: Configuration
nav_order: 1
description: ""
permalink: /Deployment/Configuration
parent: Deployment
---

# Configuration
{: .fs-9 }

Here, you can find instructions for using Camel with the Dataspace Connector.
{: .fs-6 .fw-300 }

---


## Example

```
{
  "@context" : {
    "ids" : "https://w3id.org/idsa/core/",
    "idsc" : "https://w3id.org/idsa/code/"
  },
  "@type" : "ids:ConfigurationModel",
  "@id" : "https://w3id.org/idsa/autogen/configurationModel/2ead2f4c-7569-462b-8db9-ea7bef7ed152",
  "ids:connectorStatus" : {
    "@id" : "idsc:CONNECTOR_ONLINE"
  },
  "ids:connectorProxy" : [ {
    "@type" : "ids:Proxy",
    "@id" : "https://w3id.org/idsa/autogen/proxy/8787228d-38ad-437f-b17d-6fb4bc4d794e",
    "ids:proxyAuthentication" : {
      "@type" : "ids:BasicAuthentication",
      "@id" : "https://w3id.org/idsa/autogen/basicAuthentication/abad7f6a-7658-431f-a9d8-be92a1f20a4a"
    },
    "ids:proxyURI" : {
      "@id" : "proxy.dortmund.isst.fraunhofer.de:3128"
    },
    "ids:noProxy" : [ {
      "@id" : "https://localhost:8080/"
    }, {
      "@id" : "http://localhost:8080/"
    } ]
  } ],
  "ids:connectorDescription" : {...},
  "ids:configurationModelLogLevel" : {
    "@id" : "idsc:NO_LOGGING"
  },
  "ids:connectorDeployMode" : {
    "@id" : "idsc:TEST_DEPLOYMENT"
  }
}
```
