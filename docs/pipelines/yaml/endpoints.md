# YAML getting started - Endpoints

Endpoints can be specified by name. For example,

```yaml
queue: Hosted VS2017
steps:
- task: TODO@1
  inputs:
    subscription: MyAzureSubscription
```

Note, for rename resiliency, endpoints can be specified by their GUID instead of name.

For details about tasks, refer [here](tasks.md).

For details about endpoint authorization, refer [here](authz.md).
