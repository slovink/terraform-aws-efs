<<p align="center"> <img src="https://user-images.githubusercontent.com/50652676/62349836-882fef80-b51e-11e9-99e3-7b974309c7e3.png" width="100" height="100"></p>


<h1 align="center">
    Terraform AWS  EFS
</h1>


<p align="center">

<a href="https://www.terraform.io">
  <img src="https://img.shields.io/badge/Terraform-v1.7.0-green" alt="Terraform">
</a>
<a href="https://github.com/slovink/terraform-aws-efs/blob/master/LICENSE">
  <img src="https://img.shields.io/badge/License-APACHE-blue.svg" alt="Licence">
</a>



</p>
<p align="center">

<a href='https://www.facebook.com/Slovink.in=https://github.com/slovink/terraform-aws-efs'>
  <img title="Share on Facebook" src="https://user-images.githubusercontent.com/50652676/62817743-4f64cb80-bb59-11e9-90c7-b057252ded50.png" />
</a>
<a href='https://www.linkedin.com/company/101534993/admin/feed/posts/=https://github.com/slovink/terraform-aws-efs '>
  <img title="Share on LinkedIn" src="https://user-images.githubusercontent.com/50652676/62817742-4e339e80-bb59-11e9-87b9-a1f68cae1049.png" />
</a>



- [Introduction](#introduction)
- [Usage](#usage)
- [Module Inputs](#module-inputs)
- [Module Outputs](#module-outputs)
- [Examples](#examples)
- [License](#license)



## Prerequisites

This module has a few dependencies:

- [Terraform 1.x.x](https://learn.hashicorp.com/terraform/getting-started/install.html)
- [Go](https://golang.org/doc/install)



## Introduction
This Terraform module creates an AWS efs along with additional configuration options.

## Examples
For detailed examples on how to use this module, please refer to the [Examples](https://github.com/slovink/terraform-aws-efs/tree/master/_example) directory within this repository.

## Author
Your Name Replace **MIT** and **slovink** with the appropriate license and your information. Feel free to expand this README with additional details or usage instructions as needed for your specific use case.

## License
This project is licensed under the **MIT** License - see the [LICENSE](https://github.com/slovink/terraform-aws-efs/blob/master/LICENSE) file for details.

## Feedback
If you come accross a bug or have any feedback, please log it in our [issue tracker](https://github.com/slovink/terraform-aws-efs/issues), or feel free to drop us an email at [concat@slovink.com](concat@slovink.com).

If you have found it worth your time, go ahead and give us a ★ on [our GitHub](https://github.com/slovink/terraform-aws-efs)!



## About us

At [slovink][ https://slovink.com/], we offer expert guidance, implementation support and services to help organisations accelerate their journey to the cloud. Our services include docker and container orchestration, cloud migration and adoption, infrastructure automation, application modernisation and remediation, and performance engineering.

<p align="center">We are <b> The Cloud Experts!</b></p>
<hr />
<p align="center">We ❤️  <a href="https://github.com/slovink">Open Source</a> and you can check out <a href="https://github.com/slovink">our other modules</a> to get help with your new Cloud ideas.</p>


## Examples


**IMPORTANT:** Since the `master` branch used in `source` varies based on new modifications, we suggest that you use the release versions [here](https://github.com/slovink/terraform-aws-efs/releases).


### Simple Example
Here is an example of how you can use this module in your inventory structure:
  ```hcl
    module "efs" {
      source                    = "https://github.com/slovink/terraform-aws-efs.git?ref=v1.0.0"
      name                      = "efs"
      environment               = "test"
      creation_token            = "changeme"
      availability_zones        = local.availability_zones
      vpc_id                    = module.vpc.id
      subnets                   = module.subnets.public_subnet_id
      security_groups           = [module.vpc.vpc_default_security_group_id]
      efs_backup_policy_enabled = true
      allow_cidr                = [module.vpc.vpc_cidr_block] #vpc_cidr
      replication_enabled       = true
      replication_configuration_destination = {
        region                 = "eu-west-1"
        availability_zone_name = ["eu-west-1a", "eu-west-1b"]
      }
    }
  ```





## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| access\_point\_enabled | n/a | `bool` | `true` | no |
| allow\_cidr | Provide allowed cidr to efs | `list(any)` | `[]` | no |
| availability\_zones | Availability Zone IDs | `list(string)` | n/a | yes |
| creation\_token | A unique name (a maximum of 64 characters are allowed) used as reference when creating the EFS | `string` | n/a | yes |
| efs\_backup\_policy\_enabled | If `true`, it will turn on automatic backups. | `bool` | `true` | no |
| efs\_enabled | Set to false to prevent the module from creating any resources | `bool` | `true` | no |
| encrypted | If true, the file system will be encrypted | `bool` | `true` | no |
| environment | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `"test"` | no |
| kms\_key\_id | The ARN for the KMS encryption key. When specifying kms\_key\_id, encrypted needs to be set to true. | `string` | `""` | no |
| label\_order | label order, e.g. `name`,`application` | `list(any)` | <pre>[<br>  "name",<br>  "environment"<br>]</pre> | no |
| managedby | ManagedBy, eg 'slovink'. | `string` | `"hello@slovink.com"` | no |
| mount\_target\_description | n/a | `string` | `""` | no |
| mount\_target\_ip\_address | The address (within the address range of the specified subnet) at which the file system may be mounted via the mount target | `string` | `null` | no |
| name | Solution name, e.g. `app` | `string` | `""` | no |
| performance\_mode | The file system performance mode. Can be either `generalPurpose` or `maxIO` | `string` | `"generalPurpose"` | no |
| provisioned\_throughput\_in\_mibps | The throughput, measured in MiB/s, that you want to provision for the file system. Only applicable with `throughput_mode` set to provisioned | `string` | `0` | no |
| security\_groups | Security group IDs to allow access to the EFS | `list(string)` | n/a | yes |
| subnets | Subnet IDs | `list(string)` | n/a | yes |
| throughput\_mode | Throughput mode for the file system. Defaults to bursting. Valid values: `bursting`, `provisioned`. When using `provisioned`, also set `provisioned_throughput_in_mibps` | `string` | `"bursting"` | no |
| vpc\_id | VPC ID | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| arn | EFS ARN |
| id | EFS ID |
| mount\_target\_ids | List of EFS mount target IDs (one per Availability Zone) |
| mount\_target\_ips | List of EFS mount target IPs (one per Availability Zone) |
| network\_interface\_ids | List of mount target network interface IDs |
| tags | The tags of the ecs cluster |


<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.6.4, < 1.7.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 5.32.1 |
| <a name="requirement_tls"></a> [tls](#requirement\_tls) | >= 3.0.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 5.32.1 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_label"></a> [label](#module\_label) | git@github.com:slovink/terraform-aws-labels.git | 1.0.0 |

## Resources

| Name | Type |
|------|------|
| [aws_efs_access_point.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/efs_access_point) | resource |
| [aws_efs_backup_policy.policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/efs_backup_policy) | resource |
| [aws_efs_file_system.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/efs_file_system) | resource |
| [aws_efs_file_system_policy.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/efs_file_system_policy) | resource |
| [aws_efs_mount_target.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/efs_mount_target) | resource |
| [aws_efs_replication_configuration.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/efs_replication_configuration) | resource |
| [aws_security_group.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_iam_policy_document.policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_access_point_enabled"></a> [access\_point\_enabled](#input\_access\_point\_enabled) | n/a | `bool` | `true` | no |
| <a name="input_allow_cidr"></a> [allow\_cidr](#input\_allow\_cidr) | Provide allowed cidr to efs | `list(any)` | `[]` | no |
| <a name="input_availability_zones"></a> [availability\_zones](#input\_availability\_zones) | Availability Zone IDs | `list(string)` | n/a | yes |
| <a name="input_bypass_policy_lockout_safety_check"></a> [bypass\_policy\_lockout\_safety\_check](#input\_bypass\_policy\_lockout\_safety\_check) | A flag to indicate whether to bypass the `aws_efs_file_system_policy` lockout safety check. Defaults to `false` | `bool` | `false` | no |
| <a name="input_creation_token"></a> [creation\_token](#input\_creation\_token) | A unique name (a maximum of 64 characters are allowed) used as reference when creating the EFS | `string` | n/a | yes |
| <a name="input_deny_nonsecure_transport"></a> [deny\_nonsecure\_transport](#input\_deny\_nonsecure\_transport) | Determines whether `aws:SecureTransport` is required when connecting to elastic file system | `bool` | `false` | no |
| <a name="input_efs_backup_policy_enabled"></a> [efs\_backup\_policy\_enabled](#input\_efs\_backup\_policy\_enabled) | If `true`, it will turn on automatic backups. | `bool` | `true` | no |
| <a name="input_efs_enabled"></a> [efs\_enabled](#input\_efs\_enabled) | Set to false to prevent the module from creating any resources | `bool` | `true` | no |
| <a name="input_egress_cidr_blocks"></a> [egress\_cidr\_blocks](#input\_egress\_cidr\_blocks) | Security group IDs to allow access to the EFS | `list(string)` | <pre>[<br>  "0.0.0.0/0"<br>]</pre> | no |
| <a name="input_egress_from_port"></a> [egress\_from\_port](#input\_egress\_from\_port) | Security group IDs to allow access to the EFS | `number` | `0` | no |
| <a name="input_egress_protocol"></a> [egress\_protocol](#input\_egress\_protocol) | Security group IDs to allow access to the EFS | `number` | `-1` | no |
| <a name="input_egress_to_port"></a> [egress\_to\_port](#input\_egress\_to\_port) | Security group IDs to allow access to the EFS | `number` | `0` | no |
| <a name="input_enable_aws_efs_file_system_policy"></a> [enable\_aws\_efs\_file\_system\_policy](#input\_enable\_aws\_efs\_file\_system\_policy) | A flag to enable or disable aws efs file system policy . Defaults to `false` | `bool` | `false` | no |
| <a name="input_encrypted"></a> [encrypted](#input\_encrypted) | If true, the file system will be encrypted | `bool` | `true` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `"test"` | no |
| <a name="input_from_port"></a> [from\_port](#input\_from\_port) | Security group IDs to allow access to the EFS | `number` | `2049` | no |
| <a name="input_kms_key_id"></a> [kms\_key\_id](#input\_kms\_key\_id) | The ARN for the KMS encryption key. When specifying kms\_key\_id, encrypted needs to be set to true. | `string` | `""` | no |
| <a name="input_label_order"></a> [label\_order](#input\_label\_order) | label order, e.g. `name`,`application` | `list(any)` | <pre>[<br>  "name",<br>  "environment"<br>]</pre> | no |
| <a name="input_managedby"></a> [managedby](#input\_managedby) | ManagedBy, eg 'slovink'. | `string` | `"hello@slovink.com"` | no |
| <a name="input_mount_target_description"></a> [mount\_target\_description](#input\_mount\_target\_description) | n/a | `string` | `"this is mount target security group "` | no |
| <a name="input_mount_target_ip_address"></a> [mount\_target\_ip\_address](#input\_mount\_target\_ip\_address) | The address (within the address range of the specified subnet) at which the file system may be mounted via the mount target | `string` | `null` | no |
| <a name="input_name"></a> [name](#input\_name) | Solution name, e.g. `app` | `string` | `""` | no |
| <a name="input_override_policy_documents"></a> [override\_policy\_documents](#input\_override\_policy\_documents) | List of IAM policy documents that are merged together into the exported document. In merging, statements with non-blank `sid`s will override statements with the same `sid` | `list(string)` | `[]` | no |
| <a name="input_performance_mode"></a> [performance\_mode](#input\_performance\_mode) | The file system performance mode. Can be either `generalPurpose` or `maxIO` | `string` | `"generalPurpose"` | no |
| <a name="input_policy_statements"></a> [policy\_statements](#input\_policy\_statements) | A list of IAM policy [statements](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document#statement) for custom permission usage | `any` | `[]` | no |
| <a name="input_protocol"></a> [protocol](#input\_protocol) | Security group IDs to allow access to the EFS | `string` | `"tcp"` | no |
| <a name="input_provisioned_throughput_in_mibps"></a> [provisioned\_throughput\_in\_mibps](#input\_provisioned\_throughput\_in\_mibps) | The throughput, measured in MiB/s, that you want to provision for the file system. Only applicable with `throughput_mode` set to provisioned | `string` | `0` | no |
| <a name="input_replication_configuration_destination"></a> [replication\_configuration\_destination](#input\_replication\_configuration\_destination) | A destination configuration block | `any` | `{}` | no |
| <a name="input_replication_enabled"></a> [replication\_enabled](#input\_replication\_enabled) | Set to false to prevent the module from creating any resources | `bool` | `true` | no |
| <a name="input_security_groups"></a> [security\_groups](#input\_security\_groups) | Security group IDs to allow access to the EFS | `list(string)` | n/a | yes |
| <a name="input_source_policy_documents"></a> [source\_policy\_documents](#input\_source\_policy\_documents) | List of IAM policy documents that are merged together into the exported document. Statements must have unique `sid`s | `list(string)` | `[]` | no |
| <a name="input_subnets"></a> [subnets](#input\_subnets) | Subnet IDs | `list(string)` | n/a | yes |
| <a name="input_throughput_mode"></a> [throughput\_mode](#input\_throughput\_mode) | Throughput mode for the file system. Defaults to bursting. Valid values: `bursting`, `provisioned`. When using `provisioned`, also set `provisioned_throughput_in_mibps` | `string` | `"bursting"` | no |
| <a name="input_to_port"></a> [to\_port](#input\_to\_port) | Security group IDs to allow access to the EFS | `number` | `2049` | no |
| <a name="input_vpc_id"></a> [vpc\_id](#input\_vpc\_id) | VPC ID | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_arn"></a> [arn](#output\_arn) | EFS ARN |
| <a name="output_id"></a> [id](#output\_id) | EFS ID |
| <a name="output_mount_target_ids"></a> [mount\_target\_ids](#output\_mount\_target\_ids) | List of EFS mount target IDs (one per Availability Zone) |
| <a name="output_mount_target_ips"></a> [mount\_target\_ips](#output\_mount\_target\_ips) | List of EFS mount target IPs (one per Availability Zone) |
| <a name="output_network_interface_ids"></a> [network\_interface\_ids](#output\_network\_interface\_ids) | List of mount target network interface IDs |
| <a name="output_tags"></a> [tags](#output\_tags) | The tags of the ecs cluster |
<!-- END_TF_DOCS -->
