+++
title = "azure_migrate_project Resource"
platform = "azure"
draft = false
gh_repo = "inspec-azure"

[menu.inspec]
title = "azure_migrate_project"
identifier = "inspec/resources/azure/azure_migrate_project Resource"
parent = "inspec/resources/azure"
+++

Use the `azure_migrate_project` InSpec audit resource to test the properties related to an Azure Migrate project.

## Azure Rest API Version, Endpoint, and HTTP Client Parameters

This resource interacts with API versions supported by the resource provider. The `api_version` can be defined as a resource parameter.
If not provided, the latest version will be used. For more information, refer to [`azure_generic_resource`]({{< relref "azure_generic_resource.md" >}}).

Unless defined, `azure_cloud` global endpoint and default values for the HTTP client will be used. For more information, refer to the resource pack [README](https://github.com/inspec/inspec-azure/blob/main/README.md).

## Installation

{{% inspec_azure_install %}}

## Syntax

`name` and `resource_group` are required parameters.

```ruby
describe azure_migrate_project(resource_group: 'RESOURCE_GROUP', name: 'PROJECT_NAME') do
  it                                      { should exist }
  its('name')                             { should eq 'zoneA_migrate_project' }
  its('type')                             { should eq 'Microsoft.Migrate/MigrateProjects' }
end
```

```ruby
describe azure_migrate_project(resource_group: 'RESOURCE_GROUP', name: 'PROJECT_NAME') do
  it  { should exist }
end
```

## Parameters

`name`
: Name of the Azure Migrate project to test.

`resource_group`
: Azure resource group where the targeted resource resides.

The parameter set that should be provided for a valid query is `resource_group` and `name`.

## Properties

`id`
: Path reference to the Migrate project.

`eTag`
: The eTag for concurrency control.

`name`
: Unique name of a Migrate project.

`type`
: Type of the object. `Microsoft.Migrate/MigrateProject`.

`properties`
: The nested properties.

For properties applicable to all resources, such as `type`, `name`, `id`, and `properties`, refer to [`azure_generic_resource`]({{< relref "azure_generic_resource.md#properties" >}}).

Also, refer to the [Azure documentation](https://docs.microsoft.com/en-us/rest/api/migrate/projects/migrate-projects/get-migrate-project) for other available properties.

Any attribute in the response nested within properties may be accessed with the key names separated by dots (`.`), and attributes nested in the assessment data are pluralized and listed as a collection.

## Examples

### Test that The Migrate project has a server instance type

```ruby
describe azure_migrate_project(resource_group: 'RESOURCE_GROUP', name: 'PROJECT_NAME') do
  its('properties.summary.servers.instanceType') { should eq 'Servers' }
end
```

## Matchers

This InSpec audit resource has the following special matchers. For a full list of available matchers, please visit our [Universal Matchers page](/inspec/matchers/).

### exists

```ruby
# If a Migrate project is found, it exists.

describe azure_migrate_project(resource_group: 'RESOURCE_GROUP', name: 'PROJECT_NAME') do
  it { should exist }
end

# If Migrate project is not found, it does not exist.

describe azure_migrate_project(resource_group: 'RESOURCE_GROUP', name: 'PROJECT_NAME') do
  it { should_not exist }
end
```

## Azure Permissions

{{% azure_permissions_service_principal role="contributor" %}}
