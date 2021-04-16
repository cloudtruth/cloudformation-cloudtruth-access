# cloudformation
This cloudformation template will create an AWS Role providing [CloudTruth AWS integration](https://docs.cloudtruth.com/integrations/aws) access with inline policies for S3, SSM, and Secrets Manager. 

## Prerequisite
[AWS CLI Installed](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) with an appropriate [AWS credential Access Key](https://console.aws.amazon.com/iam/home#/security_credentials)

## Usage
:warning: The ``EXTERNAL_ID_FROM_CLOUDTRUTH`` is provided by the AWS Cloudtruth integration setup and the ``AWS_INTEGRATION_ROLE_NAME`` **must** match the CloudTruth AWS account role name. 

| Parameter | Description | Type | Default | Required |
|-----------|-------------|------|---------|:--------:|
| CloudTruthExternalId | The Unique External ID provided by the CloudTruth AWS Integration. | string | n/a | yes |
| CloudTruthRoleName | The Role name matching the CloudTruth AWS Integration role name. | string | n/a | yes |


## Installation
Provide the ``EXTERNAL_ID_FROM_CLOUDTRUTH`` and ``AWS_INTEGRATION_ROLE_NAME`` values.

Executing the following ``[aws cloudformation create-stack](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/cloudformation/create-stack.html)`` command will create the AWS role and configure three inline policies:


```
aws cloudformation create-stack --stack-name CloudTruthIntegration \
--template-url https://cloudtruth-production-packages.s3.amazonaws.com/cloudformation/cloudtruth-access/cloudTruth_AWS_access.json \
--capabilities CAPABILITY_NAMED_IAM \
--parameters ParameterKey=CloudTruthExternalId,ParameterValue=EXTERNAL_ID_FROM_CLOUDTRUTH ParameterKey=CloudTruthRoleName,ParameterValue=AWS_INTEGRATION_ROLE_NAME
```