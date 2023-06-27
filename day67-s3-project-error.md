# While creating S3 bucket and IAM role, policies faced below error:


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

# While applying the plan it failed with below error, due to insufficient permission for the user.

  Enter a value: yes

aws_iam_policy.new_policy_for_bucket: Creating...
aws_iam_role.test-role: Creating...
aws_s3_bucket.s3-bucket: Creating...
aws_iam_policy.new_policy_for_bucket: Creation complete after 1s [id=arn:aws:iam::434309355563:policy/policy-bucket]
aws_s3_bucket.s3-bucket: Creation complete after 2s [id=teraform-bucket-test1]
aws_s3_bucket_public_access_block.public_access: Creating...
aws_s3_bucket_versioning.s3-version: Creating...
aws_s3_bucket_public_access_block.public_access: Creation complete after 0s [id=teraform-bucket-test1]
aws_s3_bucket_versioning.s3-version: Creation complete after 2s [id=teraform-bucket-test1]
╷
│ Error: creating IAM Role (new-role): AccessDenied: User: arn:aws:iam::434309355563:user/terraform-user is not authorized to perform: iam:CreateRole on resource: arn:aws:iam::434309355563:role/new-role with an explicit deny in an identity-based policy
│       status code: 403, request id: 1d3d0568-2b7d-4e98-96de-593ef49671fc
│ 
│   with aws_iam_role.test-role,
│   on s3.tf line 61, in resource "aws_iam_role" "test-role":
│   61: resource "aws_iam_role" "test-role"{
