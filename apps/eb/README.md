# Gurum - Elastic BeanStalk Application

Elastic BeanStalk Application.
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

Name           | Description     | Default         | Accepted Values
-------------- | --------------- | --------------- | ---------------
GurumApplicationName|Name of the Elastic BeanStalk application.|MyApp|String
SolutionStackName|The Elastic BeanStalk platform to run on.|64bit Amazon Linux 2018.03 v3.3.0 running Tomcat 8.5 Java 8|[https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts.platforms.html](Full List in Documentation)
MinSize|Min number of instances to scale to.|2|Int
MaxSize|Max number of instances to scale to.|6|Int

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
      GurumApplicationName: MyCoolApp
      SolutionStackName: 64bit Windows Server 2016 v2.3.0 running IIS 10.0
```

### Complete

```yaml
environments:
  - name: dev
    config:
      GurumApplicationName: MyCoolApp
      SolutionStackName: 64bit Windows Server 2016 v2.3.0 running IIS 10.0
      MinSize: 1
      MaxSize: 8
    env_vars:
      environment: prod
      YourVar: AnotherEnvVar
```
