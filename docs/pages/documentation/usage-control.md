---
layout: default
title: Usage Control
nav_order: 5
description: ""
permalink: /Documentation/UsageControl
parent: Documentation
---

# IDS Usage Control Policies
{: .fs-9 }

Usage policies are an important aspect of IDS, further details are explained on this page.
{: .fs-6 .fw-300 }

---

The Dataspace Connector supports usage policies written
in the `IDS Usage Control Language` based on [ODRL](https://www.w3.org/TR/odrl-model/#policy).

"An IDS Contract is implicitly divided to two main sections: the contract specific metadata and the
`IDS Usage Control Policy` of the contract.
The contract specific information (e.g., date when the contract has been issued or references to the 
sensitive information about the involved parties) has no effect on the enforcement. However, the
`IDS Usage Control Policy` is the key motive of organizational and technical Usage Control 
enforcement.
Furthermore, an `IDS Usage Control Policy` contains several Data Usage Control statements (e.g., 
permissions, prohibitions and obligations) called `IDS Rules` and is specified in the `IDS Usage 
Control Language` which is a technology independent language. The technically enforceable rules
shall be transformed to a technology dependent policy (e.g., MYDATA) to facilitate the Usage Control 
enforcement of data sovereignty." (p.22, [IDSA Position Paper Usage Control in the IDS](https://internationaldataspaces.org/wp-content/uploads/IDSA-Position-Paper-Usage-Control-in-the-IDS-V3.0.pdf))

## Policy Patterns

Following the specifications of the IDSA Position Paper about Usage Control, the IDS defines 21 
policy classes. The Dataspace Connector currently implements eight of these.

Examples for each of them can be found by using the endpoint `POST /api/examples/policy`.
The usage policy is added to the metadata of a resource. The classes at
`io.dataspaceconnector.services.usagecontrol` read, classify, verify, and enforce the policies at
runtime.

| No. | Title                                          | Support | Implementation |
|:----|:-----------------------------------------------|:-------:|:-------|
| 1   | Allow the Usage of the Data                    | x       | provides data usage without any restrictions
| 2   | Connector-restricted Data Usage                | x       | allows data usage for a specific connector
| 3   | Application-restricted Data Usage              | -       |
| 4   | Interval-restricted Data Usage                 | x       | provides data usage within a specified time interval
| 5   | Duration-restricted Data Usage                 | x       | allows data usage for a specified time period
| 6   | Location Restricted Policy                     | -       |
| 7   | Perpetual Data Sale (Payment once)             | -       |
| 8   | Data Rental (Payment frequently)               | -       |
| 9   | Role-restricted Data Usage                     | -       |
| 10  | Purpose-restricted Data Usage Policy           | -       |
| 11  | Event-restricted Usage Policy                  | -       |
| 12  | Restricted Number of Usages                    | x       | allows data usage for n times
| 13  | Security Level Restricted Policy               | -       |
| 14  | Use Data and Delete it After                   | x       | allows data usage within a specified time interval with the restriction to delete it at a specified time stamp
| 15  | Modify Data (in Transit)                       | -       |
| 16  | Modify Data (in Rest)                          | -       |
| 17  | Local Logging                                  | x       | allows data usage if logged to the Clearing House
| 18  | Remote Notifications                           | x       | allows data usage with notification message
| 19  | Attach Policy when Distribute to a Third-party | -       |
| 20  | Distribute only if Encrypted                   | -       |
| 21  | State Restricted Policy                        | -       |

## Pattern Examples

### Provide Access
```
{
  "@context" : {
    "ids" : "https://w3id.org/idsa/core/"
  },
  "@type" : "ids:ContractOffer",
  "@id" : "https://w3id.org/idsa/autogen/contractOffer/0abdf773-3d1e-48fc-a1e9-b6dd9b61b300",
  "ids:permission" : [ {
    "@type" : "ids:Permission",
    "@id" : "https://w3id.org/idsa/autogen/permission/ae138d4f-f01d-4358-89a7-73e7c560f3de",
    "ids:description" : [ {
      "@value" : "provide-access",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:action" : [ {
      "@id" : "idsc:USE"
    } ],
    "ids:title" : [ {
      "@value" : "Example Usage Policy",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ]
  } ]
}
```

### Prohibit Access
```
    {
      "@context" : {
        "ids" : "https://w3id.org/idsa/core/"
      },
      "@type" : "ids:ContractOffer",
      "@id" : "https://w3id.org/idsa/autogen/contractOffer/6dc1ca18-1a6b-4cf0-a84a-f374d50fe82d",
      "ids:prohibition" : [ {
        "@type" : "ids:Prohibition",
        "@id" : "https://w3id.org/idsa/autogen/prohibition/ff1b43b9-f3b1-44b1-a826-2efccc199a76",
        "ids:description" : [ {
          "@value" : "prohibit-access",
          "@type" : "http://www.w3.org/2001/XMLSchema#string"
        } ],
        "ids:action" : [ {
          "@id" : "idsc:USE"
        } ],
        "ids:title" : [ {
          "@value" : "Example Usage Policy",
          "@type" : "http://www.w3.org/2001/XMLSchema#string"
        } ]
      } ]
    }
```

### N Times Usage
```
{
  "@context" : {
    "ids" : "https://w3id.org/idsa/core/"
  },
  "@type" : "ids:NotMoreThanNOffer",
  "@id" : "https://w3id.org/idsa/autogen/notMoreThanNOffer/05b8b8d6-2e9a-42cc-9637-7b964231e349",
  "ids:permission" : [ {
    "@type" : "ids:Permission",
    "@id" : "https://w3id.org/idsa/autogen/permission/ee842c6f-ce83-4512-8dd7-487a72f4a2b9",
    "ids:description" : [ {
      "@value" : "n-times-usage",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:action" : [ {
      "@id" : "idsc:USE"
    } ],
    "ids:title" : [ {
      "@value" : "Example Usage Policy",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:constraint" : [ {
      "@type" : "ids:Constraint",
      "@id" : "https://w3id.org/idsa/autogen/constraint/2030a8f2-f03d-4af9-bce5-b9222e129dce",
      "ids:rightOperand" : {
        "@value" : "5",
        "@type" : "xsd:double"
      },
      "ids:operator" : {
        "@id" : "idsc:LTEQ"
      },
      "ids:leftOperand" : {
        "@id" : "idsc:COUNT"
      },
      "ids:pipEndpoint" : {
        "@id" : "https://localhost:8080/admin/api/resources/"
      }
    } ]
  } ]
}
```

### Duration Usage
```
{
  "@context" : {
    "ids" : "https://w3id.org/idsa/core/"
  },
  "@type" : "ids:ContractOffer",
  "@id" : "https://w3id.org/idsa/autogen/contractOffer/a2f9fa88-7753-4227-8170-9365d20b189f",
  "ids:permission" : [ {
    "@type" : "ids:Permission",
    "@id" : "https://w3id.org/idsa/autogen/permission/6b8abe49-6a31-4df4-80c6-764ad16d4c29",
    "ids:description" : [ {
      "@value" : "duration-usage",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:action" : [ {
      "@id" : "idsc:USE"
    } ],
    "ids:title" : [ {
      "@value" : "Example Usage Policy",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:constraint" : [ {
      "@type" : "ids:Constraint",
      "@id" : "https://w3id.org/idsa/autogen/constraint/a5aa4243-432f-4360-aff4-c95da99eb266",
      "ids:rightOperand" : {
        "@value" : "PT4H",
        "@type" : "xsd:duration"
      },
      "ids:operator" : {
        "@id" : "idsc:SHORTER_EQ"
      },
      "ids:leftOperand" : {
        "@id" : "idsc:ELAPSED_TIME"
      }
    } ]
  } ]
}
```

### Usage During Interval
```
{
  "@context" : {
    "ids" : "https://w3id.org/idsa/core/"
  },
  "@type" : "ids:ContractOffer",
  "@id" : "https://w3id.org/idsa/autogen/contractOffer/4cc74797-d45c-4a14-ba9d-f9c7ccb00007",
  "ids:permission" : [ {
    "@type" : "ids:Permission",
    "@id" : "https://w3id.org/idsa/autogen/permission/ed3103a8-1cd9-44f6-9baa-8dddbcb1c6a5",
    "ids:description" : [ {
      "@value" : "usage-during-interval",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:action" : [ {
      "@id" : "idsc:USE"
    } ],
    "ids:title" : [ {
      "@value" : "Example Usage Policy",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:constraint" : [ {
      "@type" : "ids:Constraint",
      "@id" : "https://w3id.org/idsa/autogen/constraint/0b7c4ca7-1f9e-4e30-8fa1-7551700c1980",
      "ids:rightOperand" : {
        "@value" : "2020-07-11T00:00:00Z",
        "@type" : "xsd:dateTimeStamp"
      },
      "ids:operator" : {
        "@id" : "idsc:AFTER"
      },
      "ids:leftOperand" : {
        "@id" : "idsc:POLICY_EVALUATION_TIME"
      }
    }, {
      "@type" : "ids:Constraint",
      "@id" : "https://w3id.org/idsa/autogen/constraint/9f2e0197-2ad9-442b-806b-5bb4951a2943",
      "ids:rightOperand" : {
        "@value" : "2020-07-11T00:00:00Z",
        "@type" : "xsd:dateTimeStamp"
      },
      "ids:operator" : {
        "@id" : "idsc:BEFORE"
      },
      "ids:leftOperand" : {
        "@id" : "idsc:POLICY_EVALUATION_TIME"
      }
    } ]
  } ]
}
```

### Usage Until Deletion
```
{
  "@context" : {
    "ids" : "https://w3id.org/idsa/core/"
  },
  "@type" : "ids:ContractOffer",
  "@id" : "https://w3id.org/idsa/autogen/contractOffer/cbb9fbd1-ce14-4513-9cc1-7b98a0355653",
  "ids:permission" : [ {
    "@type" : "ids:Permission",
    "@id" : "https://w3id.org/idsa/autogen/permission/03d35035-b293-43d9-8194-93776c402031",
    "ids:description" : [ {
      "@value" : "usage-until-deletion",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:action" : [ {
      "@id" : "idsc:USE"
    } ],
    "ids:title" : [ {
      "@value" : "Example Usage Policy",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:constraint" : [ {
      "@type" : "ids:Constraint",
      "@id" : "https://w3id.org/idsa/autogen/constraint/a53b746d-f838-4db0-b5bc-414edec7cee1",
      "ids:rightOperand" : {
        "@value" : "2020-07-11T00:00:00Z",
        "@type" : "xsd:dateTimeStamp"
      },
      "ids:operator" : {
        "@id" : "idsc:AFTER"
      },
      "ids:leftOperand" : {
        "@id" : "idsc:POLICY_EVALUATION_TIME"
      }
    }, {
      "@type" : "ids:Constraint",
      "@id" : "https://w3id.org/idsa/autogen/constraint/7db8bb0b-06d0-4af0-86c7-f23c334c4a7e",
      "ids:rightOperand" : {
        "@value" : "2020-07-11T00:00:00Z",
        "@type" : "xsd:dateTimeStamp"
      },
      "ids:operator" : {
        "@id" : "idsc:BEFORE"
      },
      "ids:leftOperand" : {
        "@id" : "idsc:POLICY_EVALUATION_TIME"
      }
    } ],
    "ids:postDuty" : [ {
      "@type" : "ids:Duty",
      "@id" : "https://w3id.org/idsa/autogen/duty/770e6abb-dbe5-4ea3-bff5-aa4c29d29fb5",
      "ids:action" : [ {
        "@id" : "idsc:DELETE"
      } ],
      "ids:constraint" : [ {
        "@type" : "ids:Constraint",
        "@id" : "https://w3id.org/idsa/autogen/constraint/f2acf67f-bc4c-4e64-87fc-499eec24bc57",
        "ids:rightOperand" : {
          "@value" : "2020-07-11T00:00:00Z",
          "@type" : "xsd:dateTimeStamp"
        },
        "ids:operator" : {
          "@id" : "idsc:TEMPORAL_EQUALS"
        },
        "ids:leftOperand" : {
          "@id" : "idsc:POLICY_EVALUATION_TIME"
        }
      } ]
    } ]
  } ]
}
```

### Usage Logging
```
{
  "@context" : {
    "ids" : "https://w3id.org/idsa/core/"
  },
  "@type" : "ids:ContractOffer",
  "@id" : "https://w3id.org/idsa/autogen/contractOffer/bd4d0cf0-683d-4770-b0b8-5204e03c3bf4",
  "ids:permission" : [ {
    "@type" : "ids:Permission",
    "@id" : "https://w3id.org/idsa/autogen/permission/d5e58997-3337-49e9-bc01-d10aae3db52b",
    "ids:description" : [ {
      "@value" : "usage-logging",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:action" : [ {
      "@id" : "idsc:USE"
    } ],
    "ids:title" : [ {
      "@value" : "Example Usage Policy",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:postDuty" : [ {
      "@type" : "ids:Duty",
      "@id" : "https://w3id.org/idsa/autogen/duty/e9728a46-91a2-4bd2-b210-4c142f41c715",
      "ids:action" : [ {
        "@id" : "idsc:LOG"
      } ]
    } ]
  } ]
}
```

### Usage Notification
```
{
  "@context" : {
    "ids" : "https://w3id.org/idsa/core/"
  },
  "@type" : "ids:ContractOffer",
  "@id" : "https://w3id.org/idsa/autogen/contractOffer/76971cd1-2d98-4aee-929c-07091c39ced7",
  "ids:permission" : [ {
    "@type" : "ids:Permission",
    "@id" : "https://w3id.org/idsa/autogen/permission/467f86d5-d89d-46b2-baa2-bf5ced8151b2",
    "ids:description" : [ {
      "@value" : "usage-notification",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:action" : [ {
      "@id" : "idsc:USE"
    } ],
    "ids:title" : [ {
      "@value" : "Example Usage Policy",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:postDuty" : [ {
      "@type" : "ids:Duty",
      "@id" : "https://w3id.org/idsa/autogen/duty/33c8a7be-6119-4e44-bb33-de4ad22f928a",
      "ids:action" : [ {
        "@id" : "idsc:NOTIFY"
      } ],
      "ids:constraint" : [ {
        "@type" : "ids:Constraint",
        "@id" : "https://w3id.org/idsa/autogen/constraint/7c475c19-7b3a-4e0c-a00c-2d8abdcd466c",
        "ids:rightOperand" : {
          "@value" : "https://localhost:8000/api/ids/data",
          "@type" : "xsd:anyURI"
        },
        "ids:operator" : {
          "@id" : "idsc:DEFINES_AS"
        },
        "ids:leftOperand" : {
          "@id" : "idsc:ENDPOINT"
        }
      } ]
    } ]
  } ]
}
```

### Connector Restricted Usage
```
{
  "@context" : {
    "ids" : "https://w3id.org/idsa/core/"
  },
  "@type" : "ids:ContractOffer",
  "@id" : "https://w3id.org/idsa/autogen/contractOffer/edb9ae16-a3f2-4d09-9f99-7f8408119162",
  "ids:permission" : [ {
    "@type" : "ids:Permission",
    "@id" : "https://w3id.org/idsa/autogen/permission/478b29bd-e85e-4482-8816-0d507dc8683d",
    "ids:description" : [ {
      "@value" : "connector-restricted-usage",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:title" : [ {
      "@value" : "Example Usage Policy",
      "@type" : "http://www.w3.org/2001/XMLSchema#string"
    } ],
    "ids:action" : [ {
      "@id" : "idsc:USE"
    } ],
    "ids:constraint" : [ {
      "@type" : "ids:Constraint",
      "@id" : "https://w3id.org/idsa/autogen/constraint/fe8a40f9-38ad-4772-92c3-bb3eba2cba98",
      "ids:leftOperand" : {
        "@id" : "idsc:SYSTEM"
      },
      "ids:rightOperand" : {
        "@value" : "https://w3id.org/idsa/autogen/baseConnector/7b934432-a85e-41c5-9f65-669219dde4ae",
        "@type" : "xsd:anyURI"
      },
      "ids:operator" : {
        "@id" : "idsc:SAME_AS"
      }
    } ]
  } ]
}
```
