---
layout: post
title: "Dive into hive"
comments: true
share: true
tags: hadoop
---

### Introduce

Hive是Hadoop一个程序接口,使用了类SQL的语法,可以将其视为一个SQL语言的解释器，它能将DBA提交的SQL语句，转换成能够在HADOOP上执行的M-R作业,对于DBA或前端用户来说，不必再将精力花在编写M-R应用上，直接借助SQL的易用性来实现大规模数据的查询和分析。

### Inatll tutorial

One. 下载
   [**download**](http://apache.cs.utah.edu/hive/),我的版本是1.2.1

Two. `mv apache-hive-1.2.1-bin.tar.gz /usr/local/Cellar` 和`hadoop`在同一级目录下，方便查看

Three `tar -xzvf apache-hive-1.2.1-bin.tar.gz`

Four. 设置环境变量
   `vi /etc/profile` 添加
   
   ```
       export HIVE_HOME=/usr/local/Cellar/apache-hive-1.2.1-bin
       export PATH=$HIVE_HOME/bin:$PATH
   ```
   
Five. `cp  hive-env.sh.template hive-env.sh ` 
修改配置 `vim hive-env.sh`
   
   ```
       export HADOOP_HEAPSIZE=1024
       HADOOP_HOME=/usr/local/Cellar/hadoop/2.7.1
       export HIVE_CONF_DIR=/usr/local/Cellar/apache-hive-1.2.1-bin/conf
       export HIVE_AUX_JARS_PATH=/usr/local/Cellar/apache-hive-1.2.1-bin/lib
 
   ```
   
**补充：** 

1. hive-site.xml      hive的配置文件
2. hive-env.sh        hive的运行环境文件
3. hive-default.xml.template  默认模板
4. hive-env.sh.template     hive-env.sh默认配置
5. hive-exec-log4j.properties.template   exec默认配置
6. hive-log4j.properties.template log默认配置
 
Six. 启动`hadoop`  `sh hadoop/2.7.1/sbin/start_all.sh`

Seven. 启动`hive`, `apache-hive-1.2.1-bin/bin/hive`
    
   ```
       Logging initialized using configuration in jar:file:/usr/local/Cellar/apache-hive-1.2.1-bin/lib/hive-common-1.2.1.jar!/hive-log4j.properties
   
    hive> 
   ```

Eight. 出现`hive shell` 命令行说明安装成功

Nine: 配置hive

1. `cp hive-default.xml hive-site.xml`
2. `mkdir /usr/local/Cellar/iotmp`
3. `vim hive-site.xml` 把所有的`"system:java.io.tmpdir"`修改为`/usr/local/Cellar/iotmp`
4. 启动hive，成功
备注： `hive-site.xml`是用来配置**MySQL数据库驱动、数据库名、用户名及密码**;使用MySQL作为元数据库


Ten: [Get Apache, MySQL, PHP and phpMyAdmin working on OSX 10.10 Yosemite](http://coolestguidesontheplanet.com/get-apache-mysql-php-phpmyadmin-working-osx-10-10-yosemite/#mysql)

补充：mac OSX 10.10 Yosemite install msyql

1. [downloading](http://dev.mysql.com/downloads/mysql/)
2. **download:** Mac OS X ver. 10.9 (x86, 64-bit), DMG Archive 
3. 未完待续
   
   
