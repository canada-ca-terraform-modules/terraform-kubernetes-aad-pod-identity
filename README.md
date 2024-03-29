# Terraform Kubernetes AAD Pod Identity

## Introduction

This module deploys and configures Azure Active Directory Pod Identity into a Kubernetes Cluster.

## Security Controls

The following security controls can be met through configuration of this template:

* TBD

## Dependencies

* None

## Optional (depending on options configured):

* None

## Usage

```terraform
module "helm_aad_pod_identity" {
  source = "https://github.com/canada-ca-terraform-modules/terraform-kubernetes-aad-pod-identity?ref=v3.0.1"

  chart_version = "1.6.0"
  depends_on  = [
    module.namespace_default,
  ]

  helm_namespace  = module.namespace_default.name
  helm_repository = "stable"

  resource_id = "/subscriptions/<subscription_id>/resourceGroups/<resource_group>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<named_identity>"
  client_id = "<client_id>"

  values = <<EOF

EOF
}
```

## Variables Values

| Name                     | Type   | Required | Value                                                         |
| ------------------------ | ------ | -------- | ------------------------------------------------------------- |
| chart_version            | string | yes      | Version of the Helm Chart                                     |
| helm_namespace           | string | yes      | The namespace Helm will install the chart under               |
| helm_repository          | string | yes      | The repository where the Helm chart is stored                 |
| helm_repository_username | string | no       | The username of the repository where the Helm chart is stored |
| helm_repository_password | string | no       | The password of the repository where the Helm chart is stored |
| resource_id              | string | yes      | The resource id to be used for the Managed Identity           |
| client_id                | string | yes      | The client id to be used for the Managed Identity             |
| values                   | list   | no       | Values to be passed to the Helm Chart                         |

## History

| Date     | Release    | Change                                              |
| -------- | ---------- | --------------------------------------------------- |
| 20190729 | 20190729.1 | Improvements to documentation and formatting        |
| 20190909 | 20190909.1 | 1st release                                         |
| 20200619 | v2.0.0     | Module now modified for Helm 3                      |
| 20200619 | v2.0.1     | Removed unneeded reference to kubernetes provider   |
| 20200621 | v2.0.2     | Removed unneeded dependency from helm_release       |
| 20201013 | v2.0.3     | Add the ability to specify a username and password. |
| 20210114 | v2.0.4     | Removed interpolation syntax                        |
| 20210824 | v3.0.0     | Update module for Terraform v0.13.                  |
| 20230202 | v3.0.1     | Specify sensitive variables                         |
