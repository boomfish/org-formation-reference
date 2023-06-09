# Terraform

This CloudFormation stack creates resources for supporting [Terraform](https://www.terraform.io/) in a [multi-account AWS architecture](https://developer.hashicorp.com/terraform/language/settings/backends/s3#multi-account-aws-architecture).

It creates an S3 bucket for remote state storage, a DynamoDB table for remote state locking, and 2 IAM groups:

- An 'terraform-sdlc' group that permits managing remote state and assuming roles to manage resources under the sdlc organizational unit
- A 'terraform-prod' group that permits managing remote state and assuming roles to manage resources under the prod organizational unit
