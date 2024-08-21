# MYSQL

Connect to a local mysql instance

```bash
mysql -u acuity -pPASSWORDHEREWITHNOSPACE
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