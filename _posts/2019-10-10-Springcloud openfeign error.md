---
title: OpenFeign error when start application
description: Solve OpenFeign problem in Spring Cloud service
categories:
 - SpringCloud
tags:
 - SpringCloud
 - Feign
 - SpringBoot
---

> Solve OpenFeign problem in Spring Cloud service

## Problem encountered

When use Spring Cloud OpenFeign, encounter error when start the application

```html
***************************
APPLICATION FAILED TO START
***************************

Description:

Field gameServiceClient in com.durain.bootuorder.controller.GameClientController required a bean of type 'org.springframework.cloud.openfeign.FeignContext' that could not be found.
	- Bean method 'feignContext' not loaded because @ConditionalOnClass did not find required class 'feign.Feign'


Action:

Consider revisiting the conditions above or defining a bean of type 'org.springframework.cloud.openfeign.FeignContext' in your configuration.
```

Let's take a look the version of original dependencies

- SpringBoot : 2.0.3
- SpringCloud : Finchley.SR1
- spring-cloud-starter-openfeign : 2.0.1

Search from internet, the solutions like

1. Add @EnableFeignClients into SpringBootApplication class

```java
@SpringBootApplication
@EnableFeignClients
public class BootApplication {

	public static void main(String[] args) {
		SpringApplication.run(BootApplication.class, args);
	}
}
```

But... I have already did this before run the applicaiton...

2. Or use Netflix Feign like

```xml
<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-feign</artifactId>
</dependency>
```

But this have deprecated, and recommond use spring-cloud-starter-openfeign.


## Solution

After few hours try and try... finally found the solution...

From maven dependencies, feign-core loaded version 9.5.1 based on spring-cloud-starter-openfeign version 2.0.1, but there have latest version 10.0.1 in maven repository, so try to use latest version

```xml
<dependency>  
    <groupId>io.github.openfeign</groupId>  
    <artifactId>feign-core</artifactId>  
    <version>RELEASE</version>  
</dependency>  
```

It works now!!
