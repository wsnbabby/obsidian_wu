
## 官网地址
https://dev.mysql.com/doc/refman/8.0/en/alter-table.html


## 新增

- 修改表结构新增字段
```sql
ALTER TABLE table_name ADD column_name varchar(128) NOT NULL AFTER column_name
```


## 修改

- 修改字段默认值 
```sql
-- 修改表字段默认值
ALTER TABLE 表名 ALTER COLUMN 字段名 SET DEFAULT 默认值
-- 删除默认值
ALTER TABLE 表名 ALTER COLUMN 字段名 DROP DEFAULT
```

- 修改字段值是否为空
```sql
-- 设置为空
ALTER TABLE 表名 ALTER COLUMN 字段名 SET DEFAULT 默认值
-- 设置非空
ALTER TABLE 表名 ALTER COLUMN 字段名 DROP DEFAULT
```