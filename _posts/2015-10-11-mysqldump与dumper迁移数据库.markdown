---
layout: post
title: "mysqldump与mydumper迁移数据库"
comments: true
share: true
tags: mysql
---


####mysql
**导出所有库**

```sql
mysqldump -h host_name -u user_name -p --all-databases > **.sql
```

**导出某些库**

```sql
mysqldump -h host_name -u user_name -p --databases db1 db2 > db1db2.sql
```

**导出某个数据库(会包含表结构和数据),terminal下执行:**

```sql
 mysqldump -h host_name -u user_name -p database_name > /path/un_named.sql
```

**导出数据库某表:**

```sql
 mysqldump -h host_name -u user_name -p database_name table_name > /path/un_named.sql
```

**mysql只导出一个数据库结构**

```sql
mysqldump -h host_name -u user_name -p -d database_name >**.sql
-d 不导出数据只导出结构
``` 

**导入数据库(不需要提前建库):**

```sql
 mysql -h host_name -u user_name -p database_name < /path/un_named.sql
```

**导入数据库(需要提前建库,需要在mysql命令行下):**

```sql
mysql>use database;
mysql>set names utf8;#设置数据库编码
mysql>source **.sql;
```

####Mydumper (推荐，多线程，文件越大，效果越好)
**Mydumper是一个使用C语言编写的多线程导出导入工具,并且能够保证多个表之间的一致性.当然不是线程越多越好(这个跟服务器的配置等诸多因素有关,只能作为一个经验值而不是绝对值,机器好的时候,线程越多越好).**

- **备注:`mac`下安装mydumper的命令参数和ubuntu下有所不同**

```sql
ubuntu 系统
sudo apt-get install mydumper
```

```sql
5G 数据量:
mysqldump导出数据库:
time mysqldump -h host_name -u user_name -p database_name >**.sql  

real	1m26.502s
user	0m52.783s
sys	0m11.118s
mydumper导出数据库(-t 8个线程,-B 指定数据库,-v 3打印出详细信息,-o 输出文件地址):
time mydumper -h host_name -u user_name -p password -B database_name -t 8 -v 3 -o ./

real	1m5.830s
user	0m22.901s
sys	0m10.185s
```

- **mydumper参数(mydumper --help)**

```sql
-B, --database              要备份的数据库，不指定则备份所有库
-T, --tables-list           需要备份的表，名字用逗号隔开
-o, --outputdir             备份文件输出的目录
-s, --statement-size        生成的insert语句的字节数，默认1000000
-r, --rows                  将表按行分块时，指定的块行数，指定这个选项会关闭 --chunk-filesize
-F, --chunk-filesize        将表按大小分块时，指定的块大小，单位是 MB
-c, --compress              压缩输出文件
-e, --build-empty-files     如果表数据是空，还是产生一个空文件（默认无数据则只有表结构文件）
-x, --regex                 是同正则表达式匹配 'db.table'
-i, --ignore-engines        忽略的存储引擎，用逗号分割
-m, --no-schemas            不备份表结构
-k, --no-locks              不使用临时共享只读锁，使用这个选项会造成数据不一致
--less-locking              减少对InnoDB表的锁施加时间（这种模式的机制下文详解）
-l, --long-query-guard      设定阻塞备份的长查询超时时间，单位是秒，默认是60秒（超时后默认mydumper将会退出）
--kill-long-queries         杀掉长查询 (不退出)
-b, --binlogs               导出binlog
-D, --daemon                启用守护进程模式，守护进程模式以某个间隔不间断对数据库进行备份
-I, --snapshot-interval     dump快照间隔时间，默认60s，需要在daemon模式下
-L, --logfile               使用的日志文件名(mydumper所产生的日志), 默认使用标准输出
--tz-utc                    跨时区是使用的选项，不解释了
--skip-tz-utc               同上
--use-savepoints            使用savepoints来减少采集metadata所造成的锁时间，需要 SUPER 权限
--success-on-1146           Not increment error count and Warning instead of Critical in case of table doesn't exist
-h, --host                  连接的主机名
-u, --user                  备份所使用的用户
-p, --password              密码
-P, --port                  端口
-S, --socket                使用socket通信时的socket文件
-t, --threads               开启的备份线程数，默认是4
-C, --compress-protocol     压缩与mysql通信的数据
-V, --version               显示版本号
-v, --verbose               输出信息模式, 0 = silent, 1 = errors, 2 = warnings, 3 = info, 默认为 2
```

- **myloader参数(myloader --help)**

```sql
-d, --directory                   备份文件的目录
-q, --queries-per-transaction     每次事物执行的查询数量，默认是1000
-o, --overwrite-tables            如果要恢复的表存在，则先drop掉该表，使用该参数，需要备份时候要备份表结构
-B, --database                    需要还原的数据库
-e, --enable-binlog               启用还原数据的二进制日志
-h, --host                        主机
-u, --user                        还原的用户
-p, --password                    密码
-P, --port                        端口
-S, --socket                      socket文件
-t, --threads                     还原所使用的线程数，默认是4
-C, --compress-protocol           压缩协议
-V, --version                     显示版本
-v, --verbose                     输出模式, 0 = silent, 1 = errors, 2 = warnings, 3 = info, 默认为2
```

```sql
实例
将导出的数据导入到hostname(/IP)的test2库中
myloader   -h hostname -u user_name -p passwd  -B database -e -t threading_nums  -d /path/test_table1_table2/ --overwrite-tables -v 3
```





