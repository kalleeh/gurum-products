# Gurum - GitHub Pipeline using the Elastic BeanStalk Deployment Provider

This is a version of the Gurum pipeline that CodePipeline Elastic BeanStalk Deployment Provider for deployment of application environments.
[https://aws.amazon.com/documentation/codepipeline/](https://aws.amazon.com/documentation/codepipeline/)

## Table of contents

* [Parameters](#parameters)
  * [Generic](#generic)
  * [Prescribed](#prescribed)
* [Examples](#examples)
  * [minimal](#minimal)
  * [complete](#complete)

## Parameters

### Generic

These parameters are required, but generic or require privileged access to the underlying AWS account.

Name           | Description     | Default         | Accepted Values
-------------- | --------------- | --------------- | ---------------
target_account_id|AWS Account ID to provision into (optional)||
region|AWS Region to create RDS instance in.|us-west-2|ap-northeast-1, ap-northeast-2, ap-south-1, ap-southeast-1, ap-southeast-2, ca-central-1, eu-central-1, eu-west-1, eu-west-2, sa-east-1, us-east-1, us-east-2, us-west-1, us-west-2

### Prescribed

These are parameters that are prescribed by the plan and are not configurable, should adjusting any of these be required please choose a plan that makes them available.

Name           | Description     | Value
-------------- | --------------- | ---------------
BucketName|Must contain only lowercase letters, numbers, periods (.), and hyphens. If set to Auto, a bucket name will be generated (-),Cannot end in numbers|Auto

## Examples

***Note:*** Examples do not include generic parameters, if you have not setup defaults for these you will need to add
them as additional parameters

### Minimal

```yaml
project:
  name: game
  source:
    provider: github-ecs
    repo: kalleeh/2048
```

### Complete

```yaml
project:
  name: game
  source:
    provider: github-ecs
    repo: kalleeh/2048
```
