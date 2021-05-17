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

See how to consume data with the Dataspace Connector.
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

![Connector Communication Endpoints](images/api-v1/endpoints-connector-communication.png)

For requesting data and metadata as a data consumer, two endpoints are provided. A description
request is used for requesting the metadata and an artifact request is used for requesting the raw
data.

> **Important**: For the following guide, note that the `/api/ids/data` endpoint may not be valid
> for other connector implementations. Check at which endpoint the data provider expects the IDS
> messages in advance.


### Step 1: Request a Connector's Self-description

For sending a `POST` request, two parameters have to be set: the recipient and the requested element.
As, in a first step, the data consumer only wants to read the self-description to get a list of
resources, the requested element needs to be left empty.

![Description Request](images/api-v1/endpoint-description-request.png)

If the request is successful, the response body will contain a `DescriptionResponseMessage` as
`header` and the data provider's self-description as `payload`. You will only see the payload string.
The value `ids:offeredResource` at `ids:catalog` provides a list of all available resources that are
offered by the data provider. This does **not** contain the raw data.

The URI at e.g. `"@type":"ids:Resource", "@id":"https://w3id.org/idsa/autogen/resource/a3d79eb3-328b-408e-b1b5-93c0459d98c4"`
is needed for further requests.

### Step 2: Request Metadata

To request the metadata of a specific data resource, use the same description request endpoint and
put the resource's URI (`@id`) as requested element.

If the request is successful, the response body will contain a `DescriptionResponseMessage` as
`header` and the data resource's metadata as `payload`. Here, again, wou will only see the payload.
This will be deserialized and the metadata stored into the internal database - by creating a new
`requested` resource. If the DAT token within the `RequestMessage` was not valid, the
requested element could not be found, a policy restriction was detected, or any other error arrived,
you will receive a `RejectionMessage` with an according rejection reason from the provider connector.

Next to the IDS resource as response, a UUID as validation key is provided. This one is indispensable
for requesting the data, as the provider should always first read the metadata and the included policy
as contract offer before receiving the actual data.

### Step 3: Request Data

As explained before, a single resource can contain multiple representations. Therefore, the data
consumer needs to check all available artifacts in the requested metadata and choose one for the
data request.

![Artifact Request](images/api-v1/endpoint-artifact-request.png)

The artifact request endpoint provides similar parameters as the description request endpoint. Next
to the recipient, the requested artifact, the transfer contract, and the validation key of the
description response have to be set.

---
**Negotiate Contract**

Before being able to request an artifact from the data provider, you have to negotiate a contract.
Within the description response, you receive the resource's metadata containing a contract offer.
Use the provided endpoint to put the received contract offer or a modified one in the payload and
start the contract negotiation for a specific artifact.

![Contract Request](images/api-v1/endpoint-contract-request.png)

The contract offer will be automatically turned into a contract request to then send is as the
`payload` of a `ContractRequestMessage`. The provider connector will read this contract request,
compare it to the artifact's (resp. the corresponding resource's) contract offer, return either a
`ContractRejectionMessage` or a `ContractAgreementMessage`.

If the negotiation has been successful, you receive a contract agreement id. The corresponding
contract agreement has been sent to the clearing house and stored in the provider's internal
database for later access control. Take this id and set it as `transferContract` within the artifact
request.

---

Similar to step 2, if the request is successful, the response body will contain an
`ArtifactResponseMessage` as `header` and the data resource's data as `payload`. This response's
payload, as well, will be deserialized and the data stored into the internal database - next to the
corresponding metadata. If the resource was saved successfully, you will get its UUID as response.
If the DAT token within the `RequestMessage` was not valid, the requested artifact could not
be found, the transfer contract was missing, a policy restriction was detected, or any other error
arrived, you will receive a `RejectionMessage` with a rejection reason.

---

**Note**: The Dataspace Connector only allows contract requests that correspond exactly to the
offer. Advanced negotiation will be an upcoming task. Also note that contract negotiation is 
enabled by default. To disable it, have a look at the 
[configurations](../deployment/configuration.md#ids-settings).

---

## Policy Enforcement

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

## Resource Updates



## Parametrized Data Consumption

Here, you can find details on how to use dynamic URLs for backends.
