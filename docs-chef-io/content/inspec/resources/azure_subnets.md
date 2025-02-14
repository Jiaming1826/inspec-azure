+++
title = "azure_subnets Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_subnets"
identifier = "inspec/resources/azure/azure_subnets Resource"
parent = "inspec/resources/azure"
+++

Use the `azure_subnets` InSpec audit resource to test the properties related to subnets of a virtual network.

## Azure REST API Version, Endpoint, and HTTP Client Parameters

{{% inspec_azure_common_parameters %}}

## Installation

{{% inspec_azure_install %}}

## Syntax

The `resource_group` and `vnet` are required parameters.

```ruby
describe azure_subnets(resource_group: 'RESOURCE_GROUP', vnet: 'VNET_NAME') do
  #...
end
```

## Parameters

`resource_group`
: Azure resource group where the targeted resource resides.

`vnet`
: The virtual network where the subnet you wish to test is a part of.

## Properties

`ids`
: A list of the unique resource IDs.

: **Field**: `id`

`names`
: A list of all the resources being interrogated.

: **Field**: `name`

`etags`
: A list of etags defined on the resources.

: **Field**: `etag`

{{% inspec_filter_table %}}

## Examples

### Exists if any subnets exist for a specified virtual network in the resource group

```ruby
describe azure_subnets(resource_group: 'RESOURCE_GROUP', vnet: 'VNET_NAME') do
  it { should exist }
end
```

### Filters the results to only those that match the specified name

```ruby
describe azure_subnets(resource_group: 'RESOURCE_GROUP', vnet: 'VNET_NAME')
  .where(name: 'MySubnet') do
  it { should exist }
end
```

## Matchers

{{% inspec_matchers_link %}}

### exists

```ruby
# Should not exist if no subnets are in the virtual network.

describe azure_subnets(resource_group: 'RESOURCE_GROUP', vnet: 'VNET_NAME') do
  it { should_not exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal role="contributor" %}}
