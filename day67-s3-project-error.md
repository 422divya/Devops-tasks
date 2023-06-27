

[ec2-user@ip-172-31-7-211 s3-policy-attach]$ terraform plan

Planning failed. Terraform encountered an error while generating this plan.

╷
│ Error: configuring Terraform AWS Provider: validating provider credentials: retrieving caller identity from STS: operation error STS: GetCallerIdentity, https response error StatusCode: 403, RequestID: c25ec792-a838-4ad2-b4b0-1ad68f38e6f2, api error InvalidClientTokenId: The security token included in the request is invalid.
│ 
│   with provider["registry.terraform.io/hashicorp/aws"],
│   on s3.tf line 12, in provider "aws":
│   12: provider "aws" {
│ 
╵
[ec2-user@ip-172-31-7-211 s3-policy-attach]$ aws configure
AWS Access Key ID [****************AAOV]: AKIAWKHW23AVXJE3SLNE
AWS Secret Access Key [****************VLbD]: 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
Default region name [None]: 
Default output format [None]: 
[ec2-user@ip-172-31-7-211 s3-policy-attach]$ 
[ec2-user@ip-172-31-7-211 s3-policy-attach]$ 
[ec2-user@ip-172-31-7-211 s3-policy-attach]$ terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:
