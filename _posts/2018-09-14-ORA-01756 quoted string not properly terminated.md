---
title: ORA-01756: Quoted String Not Properly Terminated
description: Encounter ORA-01756 error when insert data
categories:
 - Database
tags:
 - Oracle
 - SQL
 - Insert
---

> Solve ORA-01756 error when insert data

## Problem encountered
When insert the big text into database like html, developer break the lines and concat using ||.

There's no problem run such script in Oracle SQL Developer, but encounter ORA-01756: Quoted String Not Properly Terminated error when execute script using SQLPlus.

## Solution

Generally ORA-01756 caused by tried to execute a statement that contained a string that was not surrounded by two single quotes. One of the quotes was entered without the second accompanying quote. like the script as below:

```sql
insert into posamezna_zival(ID_zivali, Datum_rojstva, Spol, Namestitev, Mati, Oce, Prihod, Odhod, Sorta_FK, Kupec_FK) 
values ('SI 9267 9903', 1.4.2010, 'M', 'hlev 4', 'SI 42144700', 'SI 707005', 1.4.2010, 'XXX', 3,  'XXX);
```

But it may also cause by big insert/update script in one block, for such case we should use BEGIN ... END Compound-Statement Syntax to solve such problem.


```sql
 DECLARE
   tempimg BLOB;
   tempdir BFILE:=BFILENAME('TEST_DIR','green.jpg');
   BEGIN
   INSERT INTO TEST01 VALUES ('green.jpg',EMPTY_BLOB()) RETURNING CONTENT INTO TEMPIMG;
   DBMS_LOB.FILEOPEN(tempdir);
   DBMS_LOB.LOADFROMFILE(tempimg,tempdir,DBMS_LOB.GETLENGTH(tempdir));
   DBMS_LOB.FILECLOSE(tempdir);
   COMMIT;
   END;
   /
```