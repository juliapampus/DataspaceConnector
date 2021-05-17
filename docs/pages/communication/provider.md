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

See how to provide data with the Dataspace Connector.
{: .fs-6 .fw-300 }

---

First of all, the connector provides an endpoint for requesting its self-description.
The self-description is returned as JSON-LD string and contains several information about the running
connector instance. This includes e.g. the title, the maintainer, the Information Model version, and
the resource catalog. At the public endpoint `/`, the resource catalog is not displayed. It can only
be accessed with admin credentials or by sending an IDS description request message (see
[here](#step-1-request-a-connectors-self-description)).

![Selfservice Endpoints](images/api-v1/endpoints-selfservice.png)

## Step by Step

For adding resources to the running connector as a data provider, have a look at the following steps.

### Step 1: Register Data Resources

The endpoint `POST /admin/api/resources/resource` can be used for registering resources at the
connector. This can be done by providing some important information as metadata in JSON format. An
example will be explained in the following. Adding a uuid by yourself is an optional feature.

```
{
  "title": "Sample Resource",
  "description": "This is an example resource containing weather data.",
  "keywords": [
    "weather",
    "data",
    "sample"
  ],
  "owner": "https://openweathermap.org/",
  "license": "http://opendatacommons.org/licenses/odbl/1.0/",
  "version": "1.0",
  "policy": "Example policy",
  "representations": [
    {
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

The values `title`, `description`, `keywords`, `owner`, `license`, and `version` describe the data
resource and will be used to fill in the IDS Information Model attributes for IDS communication with
a connector as data consumer.

If the resource was successfully registered, the endpoint will respond with the uuid of the created
data resource. The endpoints `PUT`, `GET`, and `DELETE` `/{resource-id}` provide standard CRUD
functions to read, update, and delete the metadata, respectively the data resource.

As a resource contains the metadata of a raw data string, it can contain several representations
that are used to setup a connection to the internal database or an external backend system.
By default, each resource must have at least one representation. Further details will be explained
in Step 3. A representation can be added to a resource by using the endpoint
`POST /admin/api/resources/{resource-id}/representation`. See this example:

```
{
  "uuid": "55795317-0aaa-4fe1-b336-b2e26a00597f",
  "type": "JSON",
  "byteSize": 101,
  "name": "Example Representation",
  "source": {
    "type": "http-get",
    "url": "https://samples.openweathermap.org/data/2.5/weather?lat=35&lon=139&appid=439d4b804bc8187953eb36d2a8c26a02",
    "username": "",
    "password": ""
  }
}
```

The attributes `type`, `byteSize`, and `name` give detailed information about the data source. The
`source` object contains details for the data providing connector on how to retrieve the data from
connected backend systems or existing APIs (as Open Weather in the example). Here as well, you can
set your own representation id.

As for the resources, several endpoints provide CRUD operations for representations.

![Resource Handling Endpoints](images/api-v1/endpoints-metadata-handling.png)

Further endpoints as `PUT` and `GET` `/contract` can be used to add and update the usage policy of
a resource without having to update the whole metadata model.

A resource must have at least one policy. By default, a `PROVIDE_ACCESS` pattern is added on each
created resource.

> **Note**: Since the IDS policy language is rather complicated and it is not trivial to create a
> valid policy by hand, endpoints are provided to obtain example policies
> (`POST /admin/api/example/usage-policy`) or to validate created strings (`POST /admin/api/example/policy-validation`).
>
> ![Policy Endpoints](images/api-v1/endpoints-example-policy.png)


### Step 2: Add Data to the Internal Database

For adding plain data to the registered resource, take the returned uuid and upload a string with
`PUT /{resource-id}/data`. With `GET`, the same endpoint can be used to request the data.
> **Note**: With source type `local`, always the first representation will be loaded.

The endpoint `/{resource-id}/{representation-id}/data` can be used to request a specific representation of a resource, if multiple have been created.

![Backend Data Handling Endpoints](images/api-v1/endpoints-data-handling.png)

### Step 3: Add Data from an External Database

To distinguish between internally and externally linked data, the resource representation provides
the property `source` and its attribute `type`. Based on the `type`, the connector knows how to
retrieve the data string on a data request. If it is set to `local`, the data will be loaded from
the internal database. Currently, the connector can further establish a connection with `http-get`,
`https-get`, and `https-get` with basic authentication. To setup `url`, `username`, and `password`,
the `source` class provides appropriate attributes.

In case an external REST API should be connected and this API usually expects query parameters from
the user, e.g. to retrieve the raw data in various formats, multiple representations can be created
for one resource. Each representation can then be connected to one specified http request or
database query with fix parameters. For this purpose, the connector provides CRUD operations for
`/representation`, which essentially correspond to those of a resource.

> **Note**: While the connector has the ability to store data resources internally, it never
> duplicates data connected by external systems into its internal memory. Instead, the data is only
> forwarded when a request is received. In addition, the backend connection credentials are never
> passed on to another connector, but are only used for internal data handling.

> **Note**: To build up a connection to a custom database endpoint, e.g. without using http REST,
> an interface for another source typ can be implemented and the method
> `OfferedResourceService.getDataString()` and linked methods edited accordingly.

### Step 4: Publish Resources at IDS Metadata Broker (optional)

For communicating with an IDS metadata broker, some endpoints are provided.
- `/broker/register` and `/broker/update`: send a `ConnectorUpdateMessage` with the connector's
  self-description as `payload`
- `/broker/unregister`: send a `ConnectorUnavailableMessage` to unregister the connector
- `/broker/update/{resource-id}`: update a previously registered resource
- `/broker/remove/{resource-id}`: remove a previously registered resource
- `/broker/query`: send a `QueryMessage` with a SPARQL command (request parameter) as `payload`

![Broker Communication Endpoints](images/api-v1/endpoints-broker-communication.png)

## Policy Enforcement

When the data provider receives an `ArtifactRequestMessage` from an external Connector, the
`ArtifactMessageHandler` checks the pattern of the policy that was added to the requested resource.
If the pattern matches one of the following five, an appropriate policy check is performed:
`PROVIDE_ACCESS`, `PROHIBIT_ACCESS`, `USAGE_DURING_INTERVAL`, `USAGE_UNTIL_DELETION`, or
`CONNECTOR_RESTRICTED_USAGE`.

Depending on the specified rules, the access permission will be set to true or false. If it is true,
the data provider returns the data. If not, it will respond with a `RejectionReason.NOT_AUTHORIZED`.

---

**Note**: The contract negotiation is enabled by default. To disable it, have a look at the
[configurations](../deployment/configuration.md#ids-settings).

---

## Resource Updates



## Example

```json
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

```json
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

```json
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
