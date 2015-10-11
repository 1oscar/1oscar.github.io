---
layout: post
title: "mysql 查漏补缺"
comments: true
share: true
tags: mysql
---


**查询数据库大小:**

```sql
use information_schema;
select concat(round(sum(data_length/1024/1024),2),'MB') as data from tables
where table_schema='wemedia';
```

**查询数据库某个表格大小:**

```sql
select concat(round(sum(data_length/1024/1024),2),'MB') as data from tables
where table_schema='atweiquan' and table_name='we_category';
```

