# Gurum - ECS Fargate Application on Shared Load Balancer

ECS Fargate Application running on a Shared Load Balancer.
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
DesiredCount|How many instances of this task to run across our cluster|1|Int
HealthCheckPath|The health check path to register with the Application Load Balancer|/|String
ServiceDiscoveryTTL|The amount of time, in seconds, that you want DNS resolvers to cache the settings for this record.|60|Double

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
environments:
  - name: dev
    config:
      DesiredCount: 1
      HealthCheckPath: '/'
      ServiceDiscoveryTTL: 60
```

### Complete

```yaml
environments:
  - name: dev
    config:
      DesiredCount: 4
      HealthCheckPath: '/health'
      ServiceDiscoveryTTL: 60
    env_vars:
      environment: prod
      YourVar: AnotherEnvVar
```
