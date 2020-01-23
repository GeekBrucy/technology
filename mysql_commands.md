# check engine

```sql
show engines;
```

# check current engine

```sql
show variables like '%storage_engine%';
```

# create table with specific engine

```sql
CREATE TABLE tb(
  id INT(4) AUTO_INCREMENT,
  name VARCHAR(5),
  dept VARCHAR(5),
  PRIMARY KEY(id),
)ENGINE=MyISAM AUTO_INCREMENT=1 DEFAULT CHARSET=utf8;
```
## difference between InnoDB and MyISAM

### InnoDB
#### Focus on Transaction and it is row lock, which is good for high concurrence

### MyISAM
#### Focus on Performance and it is table lock

# SQL Optimise
## SQL Execution Sequence
FROM > ON > JOIN > WHERE > GROUP BY > HAVING > SELECT [DISTINCT]> ORDER BY > LIMIT

## indexing
index is a kind of data structure, which include b-tree, hash tree, etc.

MySQL is using b-tree by default

# MySQL / MariaDB Error: ERROR 1130 (00000): Host ''xxx.xx.xxx.xxx'' is not allowed to connect to this MySQL server

It is possibly a security precaution. A new admin account could be created

```sql
CREATE USER 'monty'@'localhost' IDENTIFIED BY 'some_pass';
GRANT ALL PRIVILEGES ON *.* TO 'monty'@'localhost';
CREATE USER 'monty'@'%' IDENTIFIED BY 'some_pass';
GRANT ALL PRIVILEGES ON *.* TO 'monty'@'%';
```
# MariaDB DATEDIFF

```sql
SELECT DATEDIFF('2014-05-19', '2014-05-10');
```
Result: 9

```sql
SELECT DATEDIFF('2014-05-19 11:41:14', '2014-03-24');
```
Result: 56

```sql
SELECT DATEDIFF('2013-12-31', '2014-05-28');
```
Result: -148

# Search by column name

```sql
select distinct tab.table_schema as database_name,
    tab.table_name
from information_schema.tables as tab
    inner join information_schema.columns as col
        on col.table_schema = tab.table_schema
            and col.table_name = tab.table_name
            and column_name LIKE '%COLUMN_NAME%'
where tab.table_type = 'BASE TABLE'
order by tab.table_schema,
    tab.table_name;
```

# Search by table name

```sql
select table_schema as database_name,
    table_name
from information_schema.tables
where table_type = 'BASE TABLE'
#     and table_name = 'your table name'
    and table_name like '%your table name%'
    and table_name not like '%_version%'
order by table_name;
```