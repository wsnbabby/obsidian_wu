


## 按时间过滤，近N天

```sql
-- 今天
select * from 表名 where to_days(时间字段名) = to_days(now());

-- 昨天
select * from 表名 where  to_days( now( ) ) – to_days( 时间字段名) <= 1 ;

-- 7天
select * from 表名 where date_sub(curdate(), interval 7 day) <= date(时间字段名) ;

-- 近30天
select * from 表名 where date_sub(curdate(), interval 30 day) <= date(时间字段名)

-- 本月  
select * from 表名 where date_formar( 时间字段名, ‘%Y%m’ ) = date_formar( curdate( ) , ‘%Y%m’ ) ;

-- 上一月
select * from 表名 where period_diff( date_format( now( ) , ‘%Y%m’ ) , date_format( 时间字段名, ‘%Y%m’ ) ) =1 ;
```