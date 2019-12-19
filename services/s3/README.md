# Gurum - Amazon S3 Documentation

<img align="right" src="https://s3.amazonaws.com/thp-aws-icons-dev/Storage_AmazonS3_LARGE.png" width="108"> <p align="center">Amazon Simple Storage Service (Amazon S3) is storage for the Internet. You can use Amazon S3 to store and retrieve any amount of data at any time, from anywhere on the web. You can accomplish these tasks using the simple and intuitive web interface of the AWS Management Console.
[https://aws.amazon.com/documentation/s3/](https://aws.amazon.com/documentation/s3/)'</p>

## Table of contents

* [Parameters](#parameters)
  * [production](#param-production)
  * [custom](#param-custom)
* [Bind Credentials](#bind-credentials)
* [Examples](#kubernetes-openshift-examples)
  * [production](#example-production)
  * [custom](#example-custom)

## Parameters

### production

Amazon Simple Storage Service (Amazon S3) is storage for the Internet. You can use Amazon S3 to store and retrieve any amount of data at any time, from anywhere on the web. You can accomplish these tasks using the simple and intuitive web interface of the AWS Management Console.

Pricing: [https://aws.amazon.com/s3/pricing/](https://aws.amazon.com/s3/pricing/)

#### Generic

These parameters are required, but generic or require privileged access to the underlying AWS account, we recommend they are configured with a broker secret, see [broker documentation](/docs/) for details.

Name           | Description     | Default         | Accepted Values
-------------- | --------------- | --------------- | ---------------
target_account_id|AWS Account ID to provision into (optional)||
target_role_name|IAM Role name to provision with (optional), must be used in combination with target_account_id||
region|AWS Region to create RDS instance in.|us-west-2|ap-northeast-1, ap-northeast-2, ap-south-1, ap-southeast-1, ap-southeast-2, ca-central-1, eu-central-1, eu-west-1, eu-west-2, sa-east-1, us-east-1, us-east-2, us-west-1, us-west-2

#### Prescribed

These are parameters that are prescribed by the plan and are not configurable, should adjusting any of these be required please choose a plan that makes them available.

Name           | Description     | Value
-------------- | --------------- | ---------------
BucketName|Must contain only lowercase letters, numbers, periods (.), and hyphens. If set to Auto, a bucket name will be generated (-),Cannot end in numbers|Auto
LoggingPrefix|Must contain only lowercase letters, numbers, periods (.), and hyphens (-),Cannot end in numbers|S3AccessLogs
EnableGlacierLifeCycle|enable archiving to Glacier Storage|False
GlacierLifeCycleTransitionInDays|Define how many days objects should exist before being moved to Glacier|30
LifeCyclePrefix|Must contain only lowercase letters, numbers, periods (.), and hyphens (-),Cannot end in numbers|Archive
EnableVersioning|enable versioning|True
BucketAccessControl|define if the bucket can be accessed from public or private locations|Private
EnableLogging|enable or discable S3 logging|True
PreventDeletion|With the PreventDeletion attribute you can preserve a resource when its stack is deleted|True

### custom

Amazon Simple Storage Service (Amazon S3) is storage for the Internet. You can use Amazon S3 to store and retrieve any amount of data at any time, from anywhere on the web. You can accomplish these tasks using the simple and intuitive web interface of the AWS Management Console.

Pricing: [https://aws.amazon.com/s3/pricing/](https://aws.amazon.com/s3/pricing/)

#### Optional

These parameters can optionally be declared when provisioning

Name           | Description     | Default         | Accepted Values
-------------- | --------------- | --------------- | ---------------
BucketName|Must contain only lowercase letters, numbers, periods (.), and hyphens. If set to Auto, a bucket name will be generated (-),Cannot end in numbers|Auto|
LoggingPrefix|Must contain only lowercase letters, numbers, periods (.), and hyphens (-),Cannot end in numbers|Archive|
EnableLogging|enable or discable S3 logging|True|True, False
EnableGlacierLifeCycle|enable archiving to Glacier Storage|False|True, False
GlacierLifeCycleTransitionInDays|Define how many days objects should exist before being moved to Glacier|0|
EnableVersioning|enable versioning|False|True, False
LifeCyclePrefix|Must contain only lowercase letters, numbers, periods (.), and hyphens (-),Cannot end in numbers|Archive|
BucketAccessControl|define if the bucket can be accessed from public or private locations|Private|Private, PublicRead, PublicReadWrite, AuthenticatedRead, LogDeliveryWrite, BucketOwnerRead, BucketOwnerFullControl, AwsExecRead
PreventDeletion|With the PreventDeletion attribute you can preserve a resource when its stack is deleted|True|True, False

#### Generic

These parameters are required, but generic or require privileged access to the underlying AWS account, we recommend they are configured with a broker secret, see [broker documentation](/docs/) for details.

Name           | Description     | Default         | Accepted Values
-------------- | --------------- | --------------- | ---------------
target_account_id|AWS Account ID to provision into (optional)||
target_role_name|IAM Role name to provision with (optional), must be used in combination with target_account_id||
region|AWS Region to create RDS instance in.|us-west-2|ap-northeast-1, ap-northeast-2, ap-south-1, ap-southeast-1, ap-southeast-2, ca-central-1, eu-central-1, eu-west-1, eu-west-2, sa-east-1, us-east-1, us-east-2, us-west-1, us-west-2

## Bind Credentials

These are the environment variables that are available to an application on bind.

Name           | Description
-------------- | ---------------
BUCKET_NAME|Name of the sample Amazon S3 bucket.
BUCKET_ARN|Name of the Amazon S3 bucket
LOGGING_BUCKET_NAME|Name of the logging bucket.

## Kubernetes/Openshift Examples

***Note:*** Examples do not include generic parameters, if you have not setup defaults for these you will need to add
them as additional parameters

### production

#### Minimal

```yaml
apiVersion: servicecatalog.k8s.io/v1beta1
kind: ServiceInstance
metadata:
  name: s3-production-minimal-example
spec:
  clusterServiceClassExternalName: s3
  clusterServicePlanExternalName: production
  parameters:
```

#### Complete

```yaml
apiVersion: servicecatalog.k8s.io/v1beta1
kind: ServiceInstance
metadata:
  name: s3-production-complete-example
spec:
  clusterServiceClassExternalName: s3
  clusterServicePlanExternalName: production
  parameters:
```

### custom

#### Minimal

```yaml
apiVersion: servicecatalog.k8s.io/v1beta1
kind: ServiceInstance
metadata:
  name: s3-custom-minimal-example
spec:
  clusterServiceClassExternalName: s3
  clusterServicePlanExternalName: custom
  parameters:
```

#### Complete

```yaml
import boto3

s3 = boto3.client('s3')

s3.get_object('mybucketName', 'myobject')
```
