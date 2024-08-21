# MySQL

Connect to a MySQL server

```bash
# Local service
mysql -u acuity -pPASSWORDHEREWITHNOSPACE

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
