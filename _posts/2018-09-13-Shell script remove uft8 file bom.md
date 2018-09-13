---
title: Shell script remove uft8 file bom 
description: Solve special character when merge files by shell script
categories:
 - Shell
tags:
 - Ubuntu
 - Jenkins
 - Shell
 - UTF-8
---

> Solve special character when merge files by shell script

## Problem encountered

When using jenkins merge the SQL scripts in Ubuntu server, the result of the sql file contains special character like below

![](data:image/png;base64,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)

With this special character, the sqlplus not able run the script normally which report error
```sql
SP2-0734: unknown command beginning "﻿delete fr..." - rest of line ignored.
```
## Solution

The porblme caused by utf8 file contains the bom \xEF,\xBB,\xBF, it is cause the result contains special character after sed or cat files.

We can use sed to remove replace the bom to empty for the file

```bash
sed -i 's/^\xEF\xBB\xBF//g' test.txt
```


Or use grep to find all files (include sub folders) with utf8 bom and replace the bom to empty

```bash
grep -r -i -l $'^\xEF\xBB\xBF' . | xargs sed -i 's/^\xEF\xBB\xBF//g'
```
