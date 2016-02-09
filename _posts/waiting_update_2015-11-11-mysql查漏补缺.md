---
layout: post
title: "mysql 查漏补缺"
comments: true
share: true
tags: mysql
---


**查询数据库大小:**

```

use information_schema;
select concat(round(sum(data_length/1024/1024),2),'MB') as data from tables
where table_schema='wemedia';

```

或者

```sql
use 数据库名
SELECT sum(DATA_LENGTH)+sum(INDEX_LENGTH)
FROM information_schema.TABLES where TABLE_SCHEMA='数据库名';
```

**查询数据库某个表格大小:**

```sql
select concat(round(sum(data_length/1024/1024),2),'MB') as data from tables
where table_schema='atweiquan' and table_name='we_category';
```

**显示端口号**

```sql
mysql> SHOW GLOBAL VARIABLES LIKE 'PORT';
```