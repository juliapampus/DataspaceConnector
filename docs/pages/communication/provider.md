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
![Unsupported Pattern Settings](assets/images/config_pattern.png)

---
**Resource Updates**


---

## Example

```
{
  "title": "ExampleResource",
  "description": "ExampleResourceDescription",
  "policy": "...", 
  "representations": [
    {
      "uuid": "8e3a5056-1e46-42e1-a1c3-37aa08b2aedd",
      "type": "XML",
      "byteSize": 101,
      "name": "Example Representation",
      "source": {
        "type": "local"
      }
    }
  ]
}
```

```
{
  "@type" : "ids:Resource",
  "@id" : "https://w3id.org/idsa/autogen/resource/0573bfc3-4627-4c73-a0db-54745e120485",
  "ids:language" : [ {
    "@id" : "idsc:EN"
  } ],
  "ids:title" : [ {
    "@value" : "ExampleResource",
    "@language" : "en"
  } ],
  "ids:description" : [ {
    "@value" : "ExampleResourceDescription",
    "@language" : "en"
  } ],
  "ids:representation" : [ {
    "@type" : "ids:Representation",
    "@id" : "https://w3id.org/idsa/autogen/representation/8e3a5056-1e46-42e1-a1c3-37aa08b2aedd",
    "ids:instance" : [ {
      "@type" : "ids:Artifact",
      "@id" : "https://w3id.org/idsa/autogen/artifact/8e3a5056-1e46-42e1-a1c3-37aa08b2aedd",
      "ids:fileName" : "Example Representation",
      "ids:byteSize" : 101
    } ],
    "ids:language" : {
      "@id" : "idsc:EN"
    },
    "ids:mediaType" : {
      "@type" : "ids:IANAMediaType",
      "@id" : "https://w3id.org/idsa/autogen/iANAMediaType/0b2389b5-43df-4104-9c4c-9ae774f1cbb6",
      "ids:filenameExtension" : "XML"
    }
  } ],
  "ids:contractOffer" : [ {
    "@type" : "ids:ContractOffer",
    "@id" : "https://w3id.org/idsa/autogen/contractOffer/6ca796f6-a153-4080-9ab2-cd9260cfbfea",
    "ids:permission" : [ {
      "@type" : "ids:Permission",
      "@id" : "https://w3id.org/idsa/autogen/permission/1c8e936f-226a-4642-ab79-5e9e4d66c473",
      "ids:title" : [ {
        "@value" : "Example Usage Policy",
        "@type" : "http://www.w3.org/2001/XMLSchema#string"
      } ],
      "ids:description" : [ {
        "@value" : "provide-access",
        "@type" : "http://www.w3.org/2001/XMLSchema#string"
      } ],
      "ids:action" : [ {
        "@id" : "idsc:USE"
      } ]
    } ],
    "ids:provider" : {
      "@id" : "https://w3id.org/idsa/autogen/baseConnector/7b934432-a85e-41c5-9f65-669219dde4ea"
    }
  } ],
  "ids:keyword" : [ ],
  "ids:created" : {
    "@value" : "2021-01-24T17:43:50.930+01:00",
    "@type" : "http://www.w3.org/2001/XMLSchema#dateTimeStamp"
  },
  "ids:modified" : {
    "@value" : "2021-01-24T17:43:50.930+01:00",
    "@type" : "http://www.w3.org/2001/XMLSchema#dateTimeStamp"
  },
  "ids:resourceEndpoint" : [ {
    "@type" : "ids:ConnectorEndpoint",
    "@id" : "https://w3id.org/idsa/autogen/connectorEndpoint/e5e2ab04-633a-44b9-87d9-a097ae6da3cf",
    "ids:accessURL" : {
      "@id" : "/api/ids/data"
    }
  } ]
}
```

```
{
    "@type" : "ids:BaseConnector",
    "@id" : "https://w3id.org/idsa/autogen/baseConnector/d7468684-1283-40e5-9242-025fbdd4c78b",
    "ids:publicKey" : {
      "@type" : "ids:PublicKey",
      "@id" : "https://w3id.org/idsa/autogen/publicKey/3d0733f4-a8b9-4ae3-a109-7bb0ffa777f1",
      "ids:keyType" : {
        "@id" : "idsc:RSA"
      },
      "ids:keyValue" : "MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAuw6mFrdflXZTJgFOA5smDXC09SmpJWoGpyERZNEy31pKdsRGhTipR27j9irmmqihv7gIgzCnx6kIRNGI2u0oFQ5FgvO1xxgzcihdpF0CheOf9INgisPkq5hj8Ae/DYXkvjhQ6c6ak/ZYfj0NpqyEPcJ5MLRmYGexMaMZmTbqDJvJl5JG3+bE3Ya21hTZYOxiSicpfFgJ30kn5aUIAtd05IZy7z1sDiVLtTXlLfe/ZQC4pnjFts+tc12sX9ihImnCkd0Wvz3CTZoyBSsc1TdBkb9m0C5tvg0fQP4QgF/zH2QoZnnrI52uAZ8MomWtY2lt3D0kkpR69pfVDJ7y3vN/ewIDAQAB"
    },
    "ids:version" : "v3.0.0",
    "ids:description" : [ {
      "@value" : "IDS Connector with static example resources hosted by the Fraunhofer ISST",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:securityProfile" : {
      "@id" : "idsc:BASE_SECURITY_PROFILE"
    },
    "ids:maintainer" : {
      "@id" : "https://example.com"
    },
    "ids:curator" : {
      "@id" : "https://example.com"
    },
    "ids:title" : [ {
      "@value" : "Dataspace Connector",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:hasDefaultEndpoint" : {
      "@type" : "ids:ConnectorEndpoint",
      "@id" : "https://w3id.org/idsa/autogen/connectorEndpoint/455a1352-e053-4400-ab5b-b99488ff9d01",
      "ids:accessURL" : {
        "@id" : "/api/ids/data"
      }
    },
    "ids:inboundModelVersion" : [ "4.0.0" ],
    "ids:outboundModelVersion" : "4.0.0"
}
```
