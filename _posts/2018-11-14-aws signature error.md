---
title: aws signature error 
description: You must be logged in to the server (Unauthorized)
categories:
 - VM
tags:
 - Virtualbox
 - Network
---

> aws signature error

## Versions

 - AWS
 - EKS

## Problem and Solution

### Issues

- The AWS IAM and kubectl config in one Ubuntu VM (hosted in VirtualBox), and it working fine whole day
- But after AFK few hours back, not able use kubectl command, and prompt error "You must be logged in to the server (Unauthorized)"
- If use AWS IAM sign agin, it prompt signature error like "Signature expired: 20170517T062414Z is now earlier than 20170517T062840Z (20170517T063340Z - 5 min.)""


### Solutions

Restart Ubuntu VM