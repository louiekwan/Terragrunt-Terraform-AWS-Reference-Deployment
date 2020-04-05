# Infrastructure code for "Web App Reference Architecture"


[Terragrunt](https://terragrunt.gruntwork.io/) is used to work with Terraform configurations which allows to orchestrate dependent layers, update arguments dynamically and keep configurations [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself).

## Table of Contents

1. [Quick start](#quick-start)
1. [Configure access to AWS account](#configure-access-to-aws-account)
1. [Create and manage your infrastructure](#create-and-manage-your-infrastructure)
1. [References](#references)
1. [About modules.tf](#about-modulestf)


## Quick start

1. [Install Terraform 0.12 or newer](https://www.terraform.io/intro/getting-started/install.html)
1. [Install Terragrunt 0.22 or newer](https://terragrunt.gruntwork.io/docs/getting-started/install/)
1. Optionally, [install pre-commit hooks](https://pre-commit.com/#install) to keep Terraform formatting and documentation up-to-date.

If you are using macOS you can install all dependencies using [Homebrew](https://brew.sh/):

    $ brew install terraform terragrunt pre-commit

## Configure access to AWS account

The recommended way to configure access credentials to AWS account is using environment variables:

```
$ export AWS_DEFAULT_REGION=us-east-1
$ export AWS_ACCESS_KEY_ID=...
$ export AWS_SECRET_ACCESS_KEY=...
```

Alternatively, you can edit `terragrunt.hcl` and use another authentication mechanism as described in [AWS provider documentation](https://www.terraform.io/docs/providers/aws/index.html#authentication).

## Create and manage your infrastructure

Infrastructure consists of multiple layers (rds_2, rds_1, autoscaling_2, ...) where each layer is described using one [Terraform module](https://www.terraform.io/docs/configuration/modules.html) with `inputs` arguments specified in `terragrunt.hcl` in respective layer's directory.

Navigate through layers to review and customize values inside `inputs` block.

There are two ways to manage infrastructure (slower&complete, or faster&granular):
- **Region as a whole (slower&complete).** Run this command to create infrastructure in all layers in a single region:

```
$ cd us-east-1
$ terragrunt apply-all
```

- **As a single layer (faster&granular).** Run this command to create infrastructure in a single layer (eg, `rds_2`):

```
$ cd us-east-1/rds_2
$ terragrunt apply
```

After the confirmation your infrastructure should be created.


## References

* [Terraform documentation](https://www.terraform.io/docs/) and [Terragrunt documentation](https://terragrunt.gruntwork.io/docs/) for all available commands and features.
* [Terraform AWS modules](https://github.com/terraform-aws-modules/).
* [Terraform modules registry](https://registry.terraform.io/).

![Reference Diagram](/IaaS%20Reference%20App.jpg){:height="50%" width="50%"}

All content, including [Terraform AWS modules](https://github.com/terraform-aws-modules/) used in these configurations, is released under the MIT License.
