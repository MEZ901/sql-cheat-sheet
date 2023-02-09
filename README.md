# sql-cheat-sheet

## ROUTE

- [Browsing](#browsing)
- [Select](#select)
- [Select-join](#select-join)
- [Conditions](#conditions)
- [Create / Open / Delete Database](#create--open--delete-database)
- [](#)
- [](#)
- [](#)
- [](#)
- [](#)
- [](#)

## BROWSING

```sql
SHOW DATABASES;
```
```sql
SHOW TABLES;
```
```sql
SHOW FIELDS FROM table / DESCRIBE table;
```
```sql
SHOW CREATE TABLE table;
```
```sql
SHOW PROCESSLIST;
```
```sql
KILL process_number;
```

## SELECT

```sql
SELECT * FROM table;
```
```sql
SELECT * FROM table1, table2;
```
```sql
SELECT field1, field2 FROM table1, table2;
```
```sql
SELECT ... FROM ... WHERE condition
```
```sql
SELECT ... FROM ... WHERE condition GROUP BY field;
```
```sql
SELECT ... FROM ... WHERE condition GROUP BY field HAVING condition2;
```
```sql
SELECT ... FROM ... WHERE condition ORDER BY field1, field2;
```
```sql
SELECT ... FROM ... WHERE condition ORDER BY field1, field2 DESC;
```
```sql
SELECT ... FROM ... WHERE condition LIMIT 10;
```
```sql
SELECT DISTINCT field1 FROM ...
```
```sql
SELECT DISTINCT field1, field2 FROM ...
```

## SELECT-JOIN

```sql
SELECT ... FROM t1 JOIN t2 ON t1.id1 = t2.id2 WHERE condition;
```
```sql
SELECT ... FROM t1 LEFT JOIN t2 ON t1.id1 = t2.id2 WHERE condition;
```
```sql
SELECT ... FROM t1 JOIN (t2 JOIN t3 ON ...) ON ...
```

## CONDITIONS

```sql
field1 = value1
```
```sql
field1 <> value1
```
```sql
field1 LIKE 'value _ %'
```
```sql
field1 IS NULL
```
```sql
field1 IS NOT NULL
```
```sql
field1 IS IN (value1, value2)
```
```sql
field1 IS NOT IN (value1, value2)
```
```sql
condition1 AND condition2
```
```sql
condition1 OR condition2
```

## CREATE / OPEN / DELETE DETABASE

```sql
CREATE DATABASE DatabaseName;
```
```sql
CREATE DATABASE DatabaseName CHARACTER SET utf8;
```
```sql
USE DatabaseName;
```
```sql
DROP DATABASE DatabaseName;
```
```sql
ALTER DATABASE DatabaseName CHARACTER SET utf8;
```

## BACKUP DATABASE TO SQL FILE

```sql
mysqldump -u Username -p dbNameYouWant > databasename_backup.sql
```

## RESTORE FROM BACKUP SQL FILE

```sql
mysql -u Username -p dbNameYouWant < databasename_backup.sql;
```

## RAPAIR TABLES AFTER UNCLEAN SHOUTDOWN

```sql
mysqlcheck --all-databases;
```
```sql
mysqlcheck --all-databases --fast;
```

## INSERT

```sql
INSERT INTO table1 (field1, field2) VALUES (value1, value2);
```

## DELETE

```sql
DELETE FROM table1 / TRUNCATE table1
```
```sql
DELETE FROM table1 WHERE condition
```
```sql
DELETE FROM table1, table2 WHERE table1.id1 = table2.id2 AND condition
```

## UPDATE

```sql
UPDATE table1 SET field1=new_value1 WHERE condition;
```
```sql
UPDATE table1, table2 SET field1=new_value1, field2=new_value2, ... WHERE table1.id1 = table2.id2 AND condition;
```

## CREATE / DELETE / MODIFY TABLE

### Create

```sql
CREATE TABLE table (field1 type1, field2 type2);
```
```sql
CREATE TABLE table (field1 type1, field2 type2, INDEX (field));
```
```sql
CREATE TABLE table (field1 type1, field2 type2, PRIMARY KEY (field1));
```
```sql
CREATE TABLE table (field1 type1, field2 type2, PRIMARY KEY (field1,field2));
```
```sql
CREATE TABLE table1 (fk_field1 type1, field2 type2, ..., FOREIGN KEY (fk_field1) REFERENCES table2 (t2_fieldA)) [ON UPDATE|ON DELETE] [CASCADE|SET NULL]
```
```sql
CREATE TABLE table1 (fk_field1 type1, fk_field2 type2, ..., FOREIGN KEY (fk_field1, fk_field2) REFERENCES table2 (t2_fieldA, t2_fieldB))
```
```sql
CREATE TABLE table IF NOT EXISTS;
```
```sql
CREATE TEMPORARY TABLE table;
```

### Drop

```sql
DROP TABLE table;
```
```sql
DROP TABLE IF EXISTS table;
```
```sql
DROP TABLE table1, table2, ...
```

### Alter

```sql
ALTER TABLE table MODIFY field1 type1
```
```sql
ALTER TABLE table MODIFY field1 type1 NOT NULL ...
```
```sql
ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1
```
```sql
ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1 NOT NULL ...
```
```sql
ALTER TABLE table ALTER field1 SET DEFAULT ...
```
```sql
ALTER TABLE table ALTER field1 DROP DEFAULT
```
```sql
ALTER TABLE table ADD new_name_field1 type1
```
```sql
ALTER TABLE table ADD new_name_field1 type1 FIRST
```
```sql
ALTER TABLE table ADD new_name_field1 type1 AFTER another_field
```
```sql
ALTER TABLE table DROP field1
```
```sql
ALTER TABLE table ADD INDEX (field);
```

### Change field order

```sql
ALTER TABLE table MODIFY field1 type1 FIRST
```
```sql
ALTER TABLE table MODIFY field1 type1 AFTER another_field
```
```sql
ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1 FIRST
```
```sql
ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1 AFTER another_field
```

## KEYS

```sql
CREATE TABLE table (..., PRIMARY KEY (field1, field2))
```
```sql
CREATE TABLE table (..., FOREIGN KEY (field1, field2) REFERENCES table2 (t2_field1, t2_field2))
```

## USERS AND PRIVILEGES

```sql
CREATE USER 'user'@'localhost';
```
```sql
GRANT ALL PRIVILEGES ON base.* TO 'user'@'localhost' IDENTIFIED BY 'password';
```
```sql
GRANT SELECT, INSERT, DELETE ON base.* TO 'user'@'localhost' IDENTIFIED BY 'password';
```
```sql
REVOKE ALL PRIVILEGES ON base.* FROM 'user'@'host'; -- one permission only
```
```sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'user'@'host'; -- all permissions
```
```sql
FLUSH PRIVILEGES;
```
```sql
SET PASSWORD = PASSWORD('new_pass');
```
```sql
SET PASSWORD FOR 'user'@'host' = PASSWORD('new_pass');
```
```sql
SET PASSWORD = OLD_PASSWORD('new_pass');
```
```sql
DROP USER 'user'@'host';
```

## MAIN DATA TYPES

- TINYINT (1o: -128 to +127)
- SMALLINT (2o: +-65 000)
- MEDIUMINT (3o: +-16 000 000)
- INT (4o: +- 2 000 000 000)
- BIGINT (8o: +-9.10^18)
- FLOAT(M,D)
- DOUBLE(M,D)
- FLOAT(D=0->53)
- TIME (HH:MM)
- YEAR (AAAA)
- DATE (AAAA-MM-JJ)
- DATETIME (AAAA-MM-JJ HH:MM; années 1000->9999)
- TIMESTAMP (like DATETIME, but 1970->2038, compatible with Unix)
- VARCHAR (single-line; explicit size)
- TEXT (multi-lines; max size=65535)
- BLOB (binary; max size=65535)
