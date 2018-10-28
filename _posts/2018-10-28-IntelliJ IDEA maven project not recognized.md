---
title: IntelliJ IDEA maven project not recognized
description: New maven project created but not recognoized by IntelliJ
categories:
 - Java
tags:
 - Java
 - Maven
 - IntelliJ IDEA
---

> IntelliJ IDEA maven project not recognized

## Versions

- IntelliJ IDEA 2018.2.5 (Ultimate Edition)


## Problem and Solution

### Issues

- New maven module under the existing project, IntelliJ not recognize that as a maven project
- The File -> Project Strucure -> Sources and Dependencies not automated selected
- Right click on the new maven module, there's no maven in right click context menu, even there have pom.xml inside the project
- Right click on the src/main/java folder, there's no class option


### Solutions

1. Check the parent project is been added as maven supported project
2. Check the new module is been added as maven supported project


There have few ways to ensure parent project and module as maven project

1. Right click on the project then Add Framework Support -> maven 
2. Open Maven Projects in right menu bar, and select the pom file


My case was the parent project was removed from maven project support, result new Module -> Maven project are not recognized.

