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