# Private Endpoints `[Microsoft.Network/privateEndpoints]`

This module deploys a Private Endpoint.

## Navigation

- [Resource Types](#Resource-Types)
- [Usage examples](#Usage-examples)
- [Parameters](#Parameters)
- [Outputs](#Outputs)
- [Cross-referenced modules](#Cross-referenced-modules)
- [Data Collection](#Data-Collection)

## Resource Types

| Resource Type | API Version |
| :-- | :-- |
| `Microsoft.Authorization/locks` | [2020-05-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.Authorization/2020-05-01/locks) |
| `Microsoft.Authorization/roleAssignments` | [2022-04-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.Authorization/2022-04-01/roleAssignments) |
| `Microsoft.Network/privateEndpoints` | [2024-05-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.Network/2024-05-01/privateEndpoints) |
| `Microsoft.Network/privateEndpoints/privateDnsZoneGroups` | [2024-05-01](https://learn.microsoft.com/en-us/azure/templates/Microsoft.Network/2024-05-01/privateEndpoints/privateDnsZoneGroups) |

## Usage examples

The following section provides usage examples for the module, which were used to validate and deploy the module successfully. For a full reference, please review the module's test folder in its repository.

>**Note**: Each example lists all the required parameters first, followed by the rest - each in alphabetical order.

>**Note**: To reference the module, please use the following syntax `br/public:avm/res/network/private-endpoint:<version>`.

- [Using only defaults](#example-1-using-only-defaults)
- [Using large parameter set](#example-2-using-large-parameter-set)
- [Using private link service](#example-3-using-private-link-service)
- [WAF-aligned](#example-4-waf-aligned)

### Example 1: _Using only defaults_

This instance deploys the module with the minimum set of required parameters.


<details>

<summary>via Bicep module</summary>

```bicep
module privateEndpoint 'br/public:avm/res/network/private-endpoint:<version>' = {
  name: 'privateEndpointDeployment'
  params: {
    // Required parameters
    name: 'npemin001'
    subnetResourceId: '<subnetResourceId>'
    // Non-required parameters
    privateLinkServiceConnections: [
      {
        name: 'npemin001'
        properties: {
          groupIds: [
            'vault'
          ]
          privateLinkServiceId: '<privateLinkServiceId>'
        }
      }
    ]
  }
}
```

</details>
<p>

<details>

<summary>via JSON parameters file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "name": {
      "value": "npemin001"
    },
    "subnetResourceId": {
      "value": "<subnetResourceId>"
    },
    // Non-required parameters
    "privateLinkServiceConnections": {
      "value": [
        {
          "name": "npemin001",
          "properties": {
            "groupIds": [
              "vault"
            ],
            "privateLinkServiceId": "<privateLinkServiceId>"
          }
        }
      ]
    }
  }
}
```

</details>
<p>

<details>

<summary>via Bicep parameters file</summary>

```bicep-params
using 'br/public:avm/res/network/private-endpoint:<version>'

// Required parameters
param name = 'npemin001'
param subnetResourceId = '<subnetResourceId>'
// Non-required parameters
param privateLinkServiceConnections = [
  {
    name: 'npemin001'
    properties: {
      groupIds: [
        'vault'
      ]
      privateLinkServiceId: '<privateLinkServiceId>'
    }
  }
]
```

</details>
<p>

### Example 2: _Using large parameter set_

This instance deploys the module with most of its features enabled.


<details>

<summary>via Bicep module</summary>

```bicep
module privateEndpoint 'br/public:avm/res/network/private-endpoint:<version>' = {
  name: 'privateEndpointDeployment'
  params: {
    // Required parameters
    name: 'npemax001'
    subnetResourceId: '<subnetResourceId>'
    // Non-required parameters
    applicationSecurityGroupResourceIds: [
      '<applicationSecurityGroupResourceId>'
    ]
    customDnsConfigs: [
      {
        fqdn: 'abc.keyvault.com'
        ipAddresses: [
          '10.0.0.10'
        ]
      }
    ]
    customNetworkInterfaceName: 'npemax001nic'
    ipConfigurations: [
      {
        name: 'myIPconfig'
        properties: {
          groupId: 'vault'
          memberName: 'default'
          privateIPAddress: '10.0.0.10'
        }
      }
    ]
    location: '<location>'
    lock: {
      kind: 'CanNotDelete'
      name: 'myCustomLockName'
    }
    privateDnsZoneGroup: {
      name: 'default'
      privateDnsZoneGroupConfigs: [
        {
          name: 'config'
          privateDnsZoneResourceId: '<privateDnsZoneResourceId>'
        }
      ]
    }
    privateLinkServiceConnections: [
      {
        name: 'npemax001'
        properties: {
          groupIds: [
            'vault'
          ]
          privateLinkServiceId: '<privateLinkServiceId>'
          requestMessage: 'Hey there'
        }
      }
    ]
    roleAssignments: [
      {
        name: '6804f270-b4e9-455f-a11b-7f2a64e38f7c'
        principalId: '<principalId>'
        principalType: 'ServicePrincipal'
        roleDefinitionIdOrName: 'Owner'
      }
      {
        name: '<name>'
        principalId: '<principalId>'
        principalType: 'ServicePrincipal'
        roleDefinitionIdOrName: 'b24988ac-6180-42a0-ab88-20f7382dd24c'
      }
      {
        principalId: '<principalId>'
        principalType: 'ServicePrincipal'
        roleDefinitionIdOrName: '<roleDefinitionIdOrName>'
      }
    ]
    tags: {
      Environment: 'Non-Prod'
      'hidden-title': 'This is visible in the resource name'
      Role: 'DeploymentValidation'
    }
  }
}
```

</details>
<p>

<details>

<summary>via JSON parameters file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "name": {
      "value": "npemax001"
    },
    "subnetResourceId": {
      "value": "<subnetResourceId>"
    },
    // Non-required parameters
    "applicationSecurityGroupResourceIds": {
      "value": [
        "<applicationSecurityGroupResourceId>"
      ]
    },
    "customDnsConfigs": {
      "value": [
        {
          "fqdn": "abc.keyvault.com",
          "ipAddresses": [
            "10.0.0.10"
          ]
        }
      ]
    },
    "customNetworkInterfaceName": {
      "value": "npemax001nic"
    },
    "ipConfigurations": {
      "value": [
        {
          "name": "myIPconfig",
          "properties": {
            "groupId": "vault",
            "memberName": "default",
            "privateIPAddress": "10.0.0.10"
          }
        }
      ]
    },
    "location": {
      "value": "<location>"
    },
    "lock": {
      "value": {
        "kind": "CanNotDelete",
        "name": "myCustomLockName"
      }
    },
    "privateDnsZoneGroup": {
      "value": {
        "name": "default",
        "privateDnsZoneGroupConfigs": [
          {
            "name": "config",
            "privateDnsZoneResourceId": "<privateDnsZoneResourceId>"
          }
        ]
      }
    },
    "privateLinkServiceConnections": {
      "value": [
        {
          "name": "npemax001",
          "properties": {
            "groupIds": [
              "vault"
            ],
            "privateLinkServiceId": "<privateLinkServiceId>",
            "requestMessage": "Hey there"
          }
        }
      ]
    },
    "roleAssignments": {
      "value": [
        {
          "name": "6804f270-b4e9-455f-a11b-7f2a64e38f7c",
          "principalId": "<principalId>",
          "principalType": "ServicePrincipal",
          "roleDefinitionIdOrName": "Owner"
        },
        {
          "name": "<name>",
          "principalId": "<principalId>",
          "principalType": "ServicePrincipal",
          "roleDefinitionIdOrName": "b24988ac-6180-42a0-ab88-20f7382dd24c"
        },
        {
          "principalId": "<principalId>",
          "principalType": "ServicePrincipal",
          "roleDefinitionIdOrName": "<roleDefinitionIdOrName>"
        }
      ]
    },
    "tags": {
      "value": {
        "Environment": "Non-Prod",
        "hidden-title": "This is visible in the resource name",
        "Role": "DeploymentValidation"
      }
    }
  }
}
```

</details>
<p>

<details>

<summary>via Bicep parameters file</summary>

```bicep-params
using 'br/public:avm/res/network/private-endpoint:<version>'

// Required parameters
param name = 'npemax001'
param subnetResourceId = '<subnetResourceId>'
// Non-required parameters
param applicationSecurityGroupResourceIds = [
  '<applicationSecurityGroupResourceId>'
]
param customDnsConfigs = [
  {
    fqdn: 'abc.keyvault.com'
    ipAddresses: [
      '10.0.0.10'
    ]
  }
]
param customNetworkInterfaceName = 'npemax001nic'
param ipConfigurations = [
  {
    name: 'myIPconfig'
    properties: {
      groupId: 'vault'
      memberName: 'default'
      privateIPAddress: '10.0.0.10'
    }
  }
]
param location = '<location>'
param lock = {
  kind: 'CanNotDelete'
  name: 'myCustomLockName'
}
param privateDnsZoneGroup = {
  name: 'default'
  privateDnsZoneGroupConfigs: [
    {
      name: 'config'
      privateDnsZoneResourceId: '<privateDnsZoneResourceId>'
    }
  ]
}
param privateLinkServiceConnections = [
  {
    name: 'npemax001'
    properties: {
      groupIds: [
        'vault'
      ]
      privateLinkServiceId: '<privateLinkServiceId>'
      requestMessage: 'Hey there'
    }
  }
]
param roleAssignments = [
  {
    name: '6804f270-b4e9-455f-a11b-7f2a64e38f7c'
    principalId: '<principalId>'
    principalType: 'ServicePrincipal'
    roleDefinitionIdOrName: 'Owner'
  }
  {
    name: '<name>'
    principalId: '<principalId>'
    principalType: 'ServicePrincipal'
    roleDefinitionIdOrName: 'b24988ac-6180-42a0-ab88-20f7382dd24c'
  }
  {
    principalId: '<principalId>'
    principalType: 'ServicePrincipal'
    roleDefinitionIdOrName: '<roleDefinitionIdOrName>'
  }
]
param tags = {
  Environment: 'Non-Prod'
  'hidden-title': 'This is visible in the resource name'
  Role: 'DeploymentValidation'
}
```

</details>
<p>

### Example 3: _Using private link service_

This instance deploys the module with a private link service to test the application of an empty list of string for `groupIds`.


<details>

<summary>via Bicep module</summary>

```bicep
module privateEndpoint 'br/public:avm/res/network/private-endpoint:<version>' = {
  name: 'privateEndpointDeployment'
  params: {
    // Required parameters
    name: 'npepls001'
    subnetResourceId: '<subnetResourceId>'
    // Non-required parameters
    ipConfigurations: [
      {
        name: 'myIPconfig'
        properties: {
          groupId: ''
          memberName: ''
          privateIPAddress: '10.0.0.10'
        }
      }
    ]
    privateLinkServiceConnections: [
      {
        name: 'npepls001'
        properties: {
          groupIds: []
          privateLinkServiceId: '<privateLinkServiceId>'
        }
      }
    ]
  }
}
```

</details>
<p>

<details>

<summary>via JSON parameters file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "name": {
      "value": "npepls001"
    },
    "subnetResourceId": {
      "value": "<subnetResourceId>"
    },
    // Non-required parameters
    "ipConfigurations": {
      "value": [
        {
          "name": "myIPconfig",
          "properties": {
            "groupId": "",
            "memberName": "",
            "privateIPAddress": "10.0.0.10"
          }
        }
      ]
    },
    "privateLinkServiceConnections": {
      "value": [
        {
          "name": "npepls001",
          "properties": {
            "groupIds": [],
            "privateLinkServiceId": "<privateLinkServiceId>"
          }
        }
      ]
    }
  }
}
```

</details>
<p>

<details>

<summary>via Bicep parameters file</summary>

```bicep-params
using 'br/public:avm/res/network/private-endpoint:<version>'

// Required parameters
param name = 'npepls001'
param subnetResourceId = '<subnetResourceId>'
// Non-required parameters
param ipConfigurations = [
  {
    name: 'myIPconfig'
    properties: {
      groupId: ''
      memberName: ''
      privateIPAddress: '10.0.0.10'
    }
  }
]
param privateLinkServiceConnections = [
  {
    name: 'npepls001'
    properties: {
      groupIds: []
      privateLinkServiceId: '<privateLinkServiceId>'
    }
  }
]
```

</details>
<p>

### Example 4: _WAF-aligned_

This instance deploys the module in alignment with the best-practices of the Well-Architected Framework.


<details>

<summary>via Bicep module</summary>

```bicep
module privateEndpoint 'br/public:avm/res/network/private-endpoint:<version>' = {
  name: 'privateEndpointDeployment'
  params: {
    // Required parameters
    name: 'npewaf001'
    subnetResourceId: '<subnetResourceId>'
    // Non-required parameters
    applicationSecurityGroupResourceIds: [
      '<applicationSecurityGroupResourceId>'
    ]
    customNetworkInterfaceName: 'npewaf001nic'
    ipConfigurations: [
      {
        name: 'myIPconfig'
        properties: {
          groupId: 'vault'
          memberName: 'default'
          privateIPAddress: '10.0.0.10'
        }
      }
    ]
    privateDnsZoneGroup: {
      privateDnsZoneGroupConfigs: [
        {
          privateDnsZoneResourceId: '<privateDnsZoneResourceId>'
        }
      ]
    }
    privateLinkServiceConnections: [
      {
        name: 'npewaf001'
        properties: {
          groupIds: [
            'vault'
          ]
          privateLinkServiceId: '<privateLinkServiceId>'
        }
      }
    ]
    tags: {
      Environment: 'Non-Prod'
      'hidden-title': 'This is visible in the resource name'
      Role: 'DeploymentValidation'
    }
  }
}
```

</details>
<p>

<details>

<summary>via JSON parameters file</summary>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    // Required parameters
    "name": {
      "value": "npewaf001"
    },
    "subnetResourceId": {
      "value": "<subnetResourceId>"
    },
    // Non-required parameters
    "applicationSecurityGroupResourceIds": {
      "value": [
        "<applicationSecurityGroupResourceId>"
      ]
    },
    "customNetworkInterfaceName": {
      "value": "npewaf001nic"
    },
    "ipConfigurations": {
      "value": [
        {
          "name": "myIPconfig",
          "properties": {
            "groupId": "vault",
            "memberName": "default",
            "privateIPAddress": "10.0.0.10"
          }
        }
      ]
    },
    "privateDnsZoneGroup": {
      "value": {
        "privateDnsZoneGroupConfigs": [
          {
            "privateDnsZoneResourceId": "<privateDnsZoneResourceId>"
          }
        ]
      }
    },
    "privateLinkServiceConnections": {
      "value": [
        {
          "name": "npewaf001",
          "properties": {
            "groupIds": [
              "vault"
            ],
            "privateLinkServiceId": "<privateLinkServiceId>"
          }
        }
      ]
    },
    "tags": {
      "value": {
        "Environment": "Non-Prod",
        "hidden-title": "This is visible in the resource name",
        "Role": "DeploymentValidation"
      }
    }
  }
}
```

</details>
<p>

<details>

<summary>via Bicep parameters file</summary>

```bicep-params
using 'br/public:avm/res/network/private-endpoint:<version>'

// Required parameters
param name = 'npewaf001'
param subnetResourceId = '<subnetResourceId>'
// Non-required parameters
param applicationSecurityGroupResourceIds = [
  '<applicationSecurityGroupResourceId>'
]
param customNetworkInterfaceName = 'npewaf001nic'
param ipConfigurations = [
  {
    name: 'myIPconfig'
    properties: {
      groupId: 'vault'
      memberName: 'default'
      privateIPAddress: '10.0.0.10'
    }
  }
]
param privateDnsZoneGroup = {
  privateDnsZoneGroupConfigs: [
    {
      privateDnsZoneResourceId: '<privateDnsZoneResourceId>'
    }
  ]
}
param privateLinkServiceConnections = [
  {
    name: 'npewaf001'
    properties: {
      groupIds: [
        'vault'
      ]
      privateLinkServiceId: '<privateLinkServiceId>'
    }
  }
]
param tags = {
  Environment: 'Non-Prod'
  'hidden-title': 'This is visible in the resource name'
  Role: 'DeploymentValidation'
}
```

</details>
<p>

## Parameters

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`name`](#parameter-name) | string | Name of the private endpoint resource to create. |
| [`subnetResourceId`](#parameter-subnetresourceid) | string | Resource ID of the subnet where the endpoint needs to be created. |

**Conditional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`manualPrivateLinkServiceConnections`](#parameter-manualprivatelinkserviceconnections) | array | A grouping of information about the connection to the remote resource. Used when the network admin does not have access to approve connections to the remote resource. Required if `privateLinkServiceConnections` is empty. |
| [`privateLinkServiceConnections`](#parameter-privatelinkserviceconnections) | array | A grouping of information about the connection to the remote resource. Required if `manualPrivateLinkServiceConnections` is empty. |

**Optional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`applicationSecurityGroupResourceIds`](#parameter-applicationsecuritygroupresourceids) | array | Application security groups in which the private endpoint IP configuration is included. |
| [`customDnsConfigs`](#parameter-customdnsconfigs) | array | Custom DNS configurations. |
| [`customNetworkInterfaceName`](#parameter-customnetworkinterfacename) | string | The custom name of the network interface attached to the private endpoint. |
| [`enableTelemetry`](#parameter-enabletelemetry) | bool | Enable/Disable usage telemetry for module. |
| [`ipConfigurations`](#parameter-ipconfigurations) | array | A list of IP configurations of the private endpoint. This will be used to map to the First Party Service endpoints. |
| [`location`](#parameter-location) | string | Location for all Resources. |
| [`lock`](#parameter-lock) | object | The lock settings of the service. |
| [`privateDnsZoneGroup`](#parameter-privatednszonegroup) | object | The private DNS zone group to configure for the private endpoint. |
| [`roleAssignments`](#parameter-roleassignments) | array | Array of role assignments to create. |
| [`tags`](#parameter-tags) | object | Tags to be applied on all resources/resource groups in this deployment. |

### Parameter: `name`

Name of the private endpoint resource to create.

- Required: Yes
- Type: string

### Parameter: `subnetResourceId`

Resource ID of the subnet where the endpoint needs to be created.

- Required: Yes
- Type: string

### Parameter: `manualPrivateLinkServiceConnections`

A grouping of information about the connection to the remote resource. Used when the network admin does not have access to approve connections to the remote resource. Required if `privateLinkServiceConnections` is empty.

- Required: No
- Type: array

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`name`](#parameter-manualprivatelinkserviceconnectionsname) | string | The name of the private link service connection. |
| [`properties`](#parameter-manualprivatelinkserviceconnectionsproperties) | object | Properties of private link service connection. |

### Parameter: `manualPrivateLinkServiceConnections.name`

The name of the private link service connection.

- Required: Yes
- Type: string

### Parameter: `manualPrivateLinkServiceConnections.properties`

Properties of private link service connection.

- Required: Yes
- Type: object

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`groupIds`](#parameter-manualprivatelinkserviceconnectionspropertiesgroupids) | array | The ID of a group obtained from the remote resource that this private endpoint should connect to. If used with private link service connection, this property must be defined as empty string array `[]`. |
| [`privateLinkServiceId`](#parameter-manualprivatelinkserviceconnectionspropertiesprivatelinkserviceid) | string | The resource id of private link service. |

**Optional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`requestMessage`](#parameter-manualprivatelinkserviceconnectionspropertiesrequestmessage) | string | A message passed to the owner of the remote resource with this connection request. Restricted to 140 chars. |

### Parameter: `manualPrivateLinkServiceConnections.properties.groupIds`

The ID of a group obtained from the remote resource that this private endpoint should connect to. If used with private link service connection, this property must be defined as empty string array `[]`.

- Required: Yes
- Type: array

### Parameter: `manualPrivateLinkServiceConnections.properties.privateLinkServiceId`

The resource id of private link service.

- Required: Yes
- Type: string

### Parameter: `manualPrivateLinkServiceConnections.properties.requestMessage`

A message passed to the owner of the remote resource with this connection request. Restricted to 140 chars.

- Required: No
- Type: string

### Parameter: `privateLinkServiceConnections`

A grouping of information about the connection to the remote resource. Required if `manualPrivateLinkServiceConnections` is empty.

- Required: No
- Type: array

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`name`](#parameter-privatelinkserviceconnectionsname) | string | The name of the private link service connection. |
| [`properties`](#parameter-privatelinkserviceconnectionsproperties) | object | Properties of private link service connection. |

### Parameter: `privateLinkServiceConnections.name`

The name of the private link service connection.

- Required: Yes
- Type: string

### Parameter: `privateLinkServiceConnections.properties`

Properties of private link service connection.

- Required: Yes
- Type: object

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`groupIds`](#parameter-privatelinkserviceconnectionspropertiesgroupids) | array | The ID of a group obtained from the remote resource that this private endpoint should connect to. If used with private link service connection, this property must be defined as empty string array `[]`. |
| [`privateLinkServiceId`](#parameter-privatelinkserviceconnectionspropertiesprivatelinkserviceid) | string | The resource id of private link service. |

**Optional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`requestMessage`](#parameter-privatelinkserviceconnectionspropertiesrequestmessage) | string | A message passed to the owner of the remote resource with this connection request. Restricted to 140 chars. |

### Parameter: `privateLinkServiceConnections.properties.groupIds`

The ID of a group obtained from the remote resource that this private endpoint should connect to. If used with private link service connection, this property must be defined as empty string array `[]`.

- Required: Yes
- Type: array

### Parameter: `privateLinkServiceConnections.properties.privateLinkServiceId`

The resource id of private link service.

- Required: Yes
- Type: string

### Parameter: `privateLinkServiceConnections.properties.requestMessage`

A message passed to the owner of the remote resource with this connection request. Restricted to 140 chars.

- Required: No
- Type: string

### Parameter: `applicationSecurityGroupResourceIds`

Application security groups in which the private endpoint IP configuration is included.

- Required: No
- Type: array

### Parameter: `customDnsConfigs`

Custom DNS configurations.

- Required: No
- Type: array

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`ipAddresses`](#parameter-customdnsconfigsipaddresses) | array | A list of private IP addresses of the private endpoint. |

**Optional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`fqdn`](#parameter-customdnsconfigsfqdn) | string | FQDN that resolves to private endpoint IP address. |

### Parameter: `customDnsConfigs.ipAddresses`

A list of private IP addresses of the private endpoint.

- Required: Yes
- Type: array

### Parameter: `customDnsConfigs.fqdn`

FQDN that resolves to private endpoint IP address.

- Required: No
- Type: string

### Parameter: `customNetworkInterfaceName`

The custom name of the network interface attached to the private endpoint.

- Required: No
- Type: string

### Parameter: `enableTelemetry`

Enable/Disable usage telemetry for module.

- Required: No
- Type: bool
- Default: `True`

### Parameter: `ipConfigurations`

A list of IP configurations of the private endpoint. This will be used to map to the First Party Service endpoints.

- Required: No
- Type: array

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`name`](#parameter-ipconfigurationsname) | string | The name of the resource that is unique within a resource group. |
| [`properties`](#parameter-ipconfigurationsproperties) | object | Properties of private endpoint IP configurations. |

### Parameter: `ipConfigurations.name`

The name of the resource that is unique within a resource group.

- Required: Yes
- Type: string

### Parameter: `ipConfigurations.properties`

Properties of private endpoint IP configurations.

- Required: Yes
- Type: object

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`groupId`](#parameter-ipconfigurationspropertiesgroupid) | string | The ID of a group obtained from the remote resource that this private endpoint should connect to. If used with private link service connection, this property must be defined as empty string. |
| [`memberName`](#parameter-ipconfigurationspropertiesmembername) | string | The member name of a group obtained from the remote resource that this private endpoint should connect to. If used with private link service connection, this property must be defined as empty string. |
| [`privateIPAddress`](#parameter-ipconfigurationspropertiesprivateipaddress) | string | A private IP address obtained from the private endpoint's subnet. |

### Parameter: `ipConfigurations.properties.groupId`

The ID of a group obtained from the remote resource that this private endpoint should connect to. If used with private link service connection, this property must be defined as empty string.

- Required: Yes
- Type: string

### Parameter: `ipConfigurations.properties.memberName`

The member name of a group obtained from the remote resource that this private endpoint should connect to. If used with private link service connection, this property must be defined as empty string.

- Required: Yes
- Type: string

### Parameter: `ipConfigurations.properties.privateIPAddress`

A private IP address obtained from the private endpoint's subnet.

- Required: Yes
- Type: string

### Parameter: `location`

Location for all Resources.

- Required: No
- Type: string
- Default: `[resourceGroup().location]`

### Parameter: `lock`

The lock settings of the service.

- Required: No
- Type: object

**Optional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`kind`](#parameter-lockkind) | string | Specify the type of lock. |
| [`name`](#parameter-lockname) | string | Specify the name of lock. |

### Parameter: `lock.kind`

Specify the type of lock.

- Required: No
- Type: string
- Allowed:
  ```Bicep
  [
    'CanNotDelete'
    'None'
    'ReadOnly'
  ]
  ```

### Parameter: `lock.name`

Specify the name of lock.

- Required: No
- Type: string

### Parameter: `privateDnsZoneGroup`

The private DNS zone group to configure for the private endpoint.

- Required: No
- Type: object

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`privateDnsZoneGroupConfigs`](#parameter-privatednszonegroupprivatednszonegroupconfigs) | array | The private DNS zone groups to associate the private endpoint. A DNS zone group can support up to 5 DNS zones. |

**Optional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`name`](#parameter-privatednszonegroupname) | string | The name of the Private DNS Zone Group. |

### Parameter: `privateDnsZoneGroup.privateDnsZoneGroupConfigs`

The private DNS zone groups to associate the private endpoint. A DNS zone group can support up to 5 DNS zones.

- Required: Yes
- Type: array

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`privateDnsZoneResourceId`](#parameter-privatednszonegroupprivatednszonegroupconfigsprivatednszoneresourceid) | string | The resource id of the private DNS zone. |

**Optional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`name`](#parameter-privatednszonegroupprivatednszonegroupconfigsname) | string | The name of the private DNS zone group config. |

### Parameter: `privateDnsZoneGroup.privateDnsZoneGroupConfigs.privateDnsZoneResourceId`

The resource id of the private DNS zone.

- Required: Yes
- Type: string

### Parameter: `privateDnsZoneGroup.privateDnsZoneGroupConfigs.name`

The name of the private DNS zone group config.

- Required: No
- Type: string

### Parameter: `privateDnsZoneGroup.name`

The name of the Private DNS Zone Group.

- Required: No
- Type: string

### Parameter: `roleAssignments`

Array of role assignments to create.

- Required: No
- Type: array
- Roles configurable by name:
  - `'Contributor'`
  - `'DNS Resolver Contributor'`
  - `'DNS Zone Contributor'`
  - `'Domain Services Contributor'`
  - `'Domain Services Reader'`
  - `'Network Contributor'`
  - `'Owner'`
  - `'Private DNS Zone Contributor'`
  - `'Reader'`
  - `'Role Based Access Control Administrator'`

**Required parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`principalId`](#parameter-roleassignmentsprincipalid) | string | The principal ID of the principal (user/group/identity) to assign the role to. |
| [`roleDefinitionIdOrName`](#parameter-roleassignmentsroledefinitionidorname) | string | The role to assign. You can provide either the display name of the role definition, the role definition GUID, or its fully qualified ID in the following format: '/providers/Microsoft.Authorization/roleDefinitions/c2f4ef07-c644-48eb-af81-4b1b4947fb11'. |

**Optional parameters**

| Parameter | Type | Description |
| :-- | :-- | :-- |
| [`condition`](#parameter-roleassignmentscondition) | string | The conditions on the role assignment. This limits the resources it can be assigned to. e.g.: @Resource[Microsoft.Storage/storageAccounts/blobServices/containers:ContainerName] StringEqualsIgnoreCase "foo_storage_container". |
| [`conditionVersion`](#parameter-roleassignmentsconditionversion) | string | Version of the condition. |
| [`delegatedManagedIdentityResourceId`](#parameter-roleassignmentsdelegatedmanagedidentityresourceid) | string | The Resource Id of the delegated managed identity resource. |
| [`description`](#parameter-roleassignmentsdescription) | string | The description of the role assignment. |
| [`name`](#parameter-roleassignmentsname) | string | The name (as GUID) of the role assignment. If not provided, a GUID will be generated. |
| [`principalType`](#parameter-roleassignmentsprincipaltype) | string | The principal type of the assigned principal ID. |

### Parameter: `roleAssignments.principalId`

The principal ID of the principal (user/group/identity) to assign the role to.

- Required: Yes
- Type: string

### Parameter: `roleAssignments.roleDefinitionIdOrName`

The role to assign. You can provide either the display name of the role definition, the role definition GUID, or its fully qualified ID in the following format: '/providers/Microsoft.Authorization/roleDefinitions/c2f4ef07-c644-48eb-af81-4b1b4947fb11'.

- Required: Yes
- Type: string

### Parameter: `roleAssignments.condition`

The conditions on the role assignment. This limits the resources it can be assigned to. e.g.: @Resource[Microsoft.Storage/storageAccounts/blobServices/containers:ContainerName] StringEqualsIgnoreCase "foo_storage_container".

- Required: No
- Type: string

### Parameter: `roleAssignments.conditionVersion`

Version of the condition.

- Required: No
- Type: string
- Allowed:
  ```Bicep
  [
    '2.0'
  ]
  ```

### Parameter: `roleAssignments.delegatedManagedIdentityResourceId`

The Resource Id of the delegated managed identity resource.

- Required: No
- Type: string

### Parameter: `roleAssignments.description`

The description of the role assignment.

- Required: No
- Type: string

### Parameter: `roleAssignments.name`

The name (as GUID) of the role assignment. If not provided, a GUID will be generated.

- Required: No
- Type: string

### Parameter: `roleAssignments.principalType`

The principal type of the assigned principal ID.

- Required: No
- Type: string
- Allowed:
  ```Bicep
  [
    'Device'
    'ForeignGroup'
    'Group'
    'ServicePrincipal'
    'User'
  ]
  ```

### Parameter: `tags`

Tags to be applied on all resources/resource groups in this deployment.

- Required: No
- Type: object

## Outputs

| Output | Type | Description |
| :-- | :-- | :-- |
| `customDnsConfigs` | array | The custom DNS configurations of the private endpoint. |
| `groupId` | string | The group Id for the private endpoint Group. |
| `location` | string | The location the resource was deployed into. |
| `name` | string | The name of the private endpoint. |
| `networkInterfaceResourceIds` | array | The resource IDs of the network interfaces associated with the private endpoint. |
| `resourceGroupName` | string | The resource group the private endpoint was deployed into. |
| `resourceId` | string | The resource ID of the private endpoint. |

## Cross-referenced modules

This section gives you an overview of all local-referenced module files (i.e., other modules that are referenced in this module) and all remote-referenced files (i.e., Bicep modules that are referenced from a Bicep Registry or Template Specs).

| Reference | Type |
| :-- | :-- |
| `br/public:avm/utl/types/avm-common-types:0.5.1` | Remote reference |

## Data Collection

The software may collect information about you and your use of the software and send it to Microsoft. Microsoft may use this information to provide services and improve our products and services. You may turn off the telemetry as described in the [repository](https://aka.ms/avm/telemetry). There are also some features in the software that may enable you and Microsoft to collect data from users of your applications. If you use these features, you must comply with applicable law, including providing appropriate notices to users of your applications together with a copy of Microsoft’s privacy statement. Our privacy statement is located at <https://go.microsoft.com/fwlink/?LinkID=824704>. You can learn more about data collection and use in the help documentation and our privacy statement. Your use of the software operates as your consent to these practices.
