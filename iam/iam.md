# Getting Starting with YES3 Scanner: AWS IAM

We detail how to set up the AWS Identity and Access Management Infrastructure to run YES3 Scanner.  Check with your company to see if there are specific requirements for IAM Deployment such as required IAM Policies, tags, Permission Boundaries, etc.

YES3 Scanner is intended to be run on a local machine.  While it can be run in other environments, it must be run from a location where credentials are stored.  To configure your local environment, please see [AWS's documentation on how to configure credentials](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-authentication.html).

## Requirements

- an AWS IAM Principal (IAM Role or IAM User) with the 13 S3 service (s3:<action>) read/view permissions in [ransomware_prevent_read.json](ransomware_prevent_read.json).

YES3 Scanner only uses read/view permissions and does not need write, tagging, or permissions management actions in AWS.  Additionally, YES3 Scanner does not need data view permissions in S3. 

## Recommended Setup

Our ideal recommendation is to run YES3 Scanner with least privilege:
- An AWS IAM Role
- With the limited ransomware_prevent_read permissions either as a AWS IAM Managed Policy or an Inline Policy.

## Troubleshooting 

A couple checks if you're running into permission issues with YES3 Scanner:

- Check to see if YES3 Scanner's IAM Principal has the required IAM permissions as detailed above.
- Check resource-based policies that may be preventing YES3 Scanner from scanning (Bucket Policies)
- Check organizational policies such as SCPs and RCPs that may be restricting YES3 Scanner from scanning S3.
- Check for the presence of any deny policies in IAM that may override YES3 Scanner's allow permissions.

## Other Options

Note: We generally do not recommend using an IAM User due to the risk associated with the long-term credentials for an AWS IAM User.  If you prefer to use an IAM user for speed, please exercise caution and secure the credentials (Access Key and Secret Access Key) associated with your IAM User.

In some cases, you may already have an existing AWS IAM Principal.  If using an existing AWS IAM Principal, we recommend using an AWS IAM Principal with limited permissions (such as a read only role).

A few existing Read Only AWS Managed Policies that have the required permissions (and more):
- AmazonS3ReadOnlyAccess (arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess)
- ReadOnlyAccess (arn:aws:iam::aws:policy/ReadOnlyAccess)

We provide [ransomware_prevent_read.json](ransomware_prevent_read.json) to help you get started with least privilege as needed.  

NOTE: We recommend using an IAM role and only using the IAM User if you have no other options.  
