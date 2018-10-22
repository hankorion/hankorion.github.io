---
title: Tips for Spring Cloud Sleuth and Zipkin 
description: Some tips about integrate spring cloud sleuth and zipkin
categories:
 - Java
tags:
 - Java
 - Spring Cloud
 - Spring Boot
 - Sleuth
 - Zipkin
---

> Tips for Spring Cloud Sleuth and Zipkin 

## Versions

- Spring Cloud:	2.0.1.RELEASE
- Spring Boot:	2.0.3.RELEASE


Related dependencies

```xml
	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-zipkin</artifactId>
		</dependency>
	</dependencies>
```

## Problem and Solution

### Dependencies config

The artifict spring-cloud-starter-zipkin already contains the "spring-cloud-starter-sleuth" and "spring-cloud-sleuth-zipkin", so no need config again.


### Sleuth log showing false

If the console log show "false" like below, that's means the spans are not sending from Sleuth to Zipkin.

``` java
INFO [order,3d6babe713158be7,c89d0c6a4d7a71da,false]
```


It mostly due to "probability" setting for sampler, if debug in local we can set sampler.probality to 1.0 (all traces)

```yaml
  sleuth:
    enabled: true
    sampler:
      probability: 1.0
```

After above configuration, the log should shows "true" like

```java
2018-10-22 14:50:05.218  INFO [order,3d6babe713158be7,c89d0c6a4d7a71da,true] 27976
```


### Console shows sending to Zipkin, but no trace in Zipkin

May encounter the problem the Sleuth shows sending spans to Zipkin, but we cannot found the trace from Zipkin portal.

Add zipkin.sender.type to web, will solve this problem.

```yaml
  zipkin:
    base-url: http://localhost:9411/
    sender:
	  type: web
```

Offical document about this config:
```
If you have web, rabbit, or kafka together on the classpath, you might need to pick the means by which you would like to send spans to zipkin. To do so, set web, rabbit, or kafka to the spring.zipkin.sender.type property. The following example shows setting the sender type for web.
```