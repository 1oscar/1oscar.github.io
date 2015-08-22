---
layout: post
title: "dive into MySQLdb"
comments: true
share: true
tags: mysql python
---

**数据库的连接**

    try:
        	con = mdb.connect(host = host, port = int(port), user = user, passwd = passwd, db = database, charset = 'utf8')#connect的参数设置见末文
    except Exception,e:
        	print str(e)
        	print 'Fail to connect to database'
        	sys.exit(1)

**获取操作游标**

    cur = con.cursor()

**cur常用的一些操作**:

    'execute', 'executemany', 'fetchall', 'fetchmany', 'fetchone', 'lastrowid', 'messages', 'nextset', 'rowcount', 'rownumber', 'scroll'

**默认的游标类型以元组的元组形式返回数据。当我们使用字典游标时，这些数据是以Python字典的形式返回。这样一来，我们就可以通过列名来访问数据**

    cur = con.cursor(mdb.cursors.DictCursor)
    
**创建数据库**

    sql = """CREATE TABLE IF NOT EXISTS `table_name` 
    		(`id` int(10) unsigned NOT NULL AUTO_INCREMENT,
    		`field_1` varchar(64) DEFAULT NULL, 
    		PRIMARY KEY (`id`)) 
    		ENGINE=InnoDB DEFAULT CHARSET=utf8;"""
    cur.execute(sql)

**插入一条记录**

    sql = """insert into table_name ("""+app_tuple[0][0]+""") values (%s)"""
    cur.execute(sql, map(lambda x: x[1], app_dict.items()))
    
    con.commit()
    cur.close()
    con.close()

**插入数据库图片**：  

    img = open("name.png", 'r').read()
    cursor.execute("INSERT INTO Images SET Data='%s'" % mdb.escape_string(img))
**更新**:

    cur.execute("UPDATE Writers SET Name = %s WHERE Id = %s",("Leo Tolstoy", "1"))

**MySQL数据库有多种不同的存储引擎。其中最常见的是MyISAM和InnoDB引擎，而MyISAM是默认的一个。<br>
 MyISAM表处理速度比较快，但不支持事务，所以commit()和rollback()方法也没有实现，这时调用这些方法不会做任何事情。<br>
 InnoDB在预防数据丢失方面比较安全，它们支持事务，但是处理速度相对比较慢。<br>
事务是指在一个或者多个数据库中对数据的原子操作。在一个事务中，所有SQL语句的影响要么全部提交到数据库，要么就全部回滚。<br>
InnoDB引擎 使用rollback()方法can丢弃(回滚)更新操作。每个方法执行完后都会开始一个新的事务。<br>
InnoDB拥有事务，如果你不使用 SET AUTOCOMMIT=0 ，MySQL 将会在一个会话中打开自动提交模式,在自动提交模式下，如果一条 SQL 语句没有返回任何错误，MySQL 将在这条 SQL 语句后立即提交。<br>
如果MySQLdb自动提交未开启，if在try里先有很多execute, 然后再commit 如果有一个execute出错，则except下的rollback后在try里的execute都会未执行。
commit之前出错，然后执行rollback会使得原先未commit的所有操作都不执行。<br>
MySQLdb使用innodb引擎，代码里已经默认设置了不开启自动提交模式，开启代码：**

    con.autocommit = True 
    #or con.autocommit(True) or con.autocommit=1
    cur = con.cursor()
**这样每一次cur.execute的insert更新操作都会引起数据库变化。<br>
如果不设置autocommit, MySQLdb默认不开启事务, 每一次cur.execute的都需要con.commit()操作。
con.connect的参数设置:**

    host
    string, host to connect
    user
    string, user to connect as
    passwd
    string, password to use
    db
    string, database to use
    port
    integer, TCP/IP port to connect to
    unix_socket
    string, location of unix_socket to use
    conv
    conversion dictionary, see MySQLdb.converters
    connect_timeout
    number of seconds to wait before the connection attempt fails.
    compress
    if set, compression is enabled
    named_pipe
    if set, a named pipe is used to connect (Windows only)
    init_command
    command which is run once the connection is created
    read_default_file
    file from which default client values are read
    read_default_group
    configuration group to use from the default file
    cursorclass
    class object, used to create cursors (keyword only)
    use_unicode
    If True, text-like columns are returned as unicode objects using the connection's character set. Otherwise, text-like columns are returned as strings. columns are returned as normal strings. Unicode objects will always be encoded to the connection's character set regardless of this setting.
    charset
    If supplied, the connection character set will be changed to this character set (MySQL-4.1 and newer). This implies use_unicode=True.
    sql_mode
    If supplied, the session SQL mode will be changed to this setting (MySQL-4.1 and newer). For more details and legal values, see the MySQL documentation.
    client_flag
    integer, flags to use or 0 (see MySQL docs or constants/CLIENTS.py)
    ssl
    dictionary or mapping, contains SSL connection parameters; see the MySQL documentation for more details (mysql_ssl_set()). If this is set, and the client does not support SSL, NotSupportedError will be raised.
    local_infile
    integer, non-zero enables LOAD LOCAL INFILE; zero disables

**备注:** <br>
 1. **MySQLdb的其余操作参见我的pdf文档**<br>
 2. **有价值的article:**<br>
     - [**MySQLdb用户指南,MySQLdb源码函数的介绍**](http://mysql-python.sourceforge.net/MySQLdb.html)<br>
     - [**Innodb中文手册,介绍Innodb引擎的数据库的不一样的操作**](http://man.chinaunix.net/database/mysql/inonodb_zh/)<br>
     - [**MySQL中文手册，介绍了所有sql语句操作**](http://man.chinaunix.net/database/mysql/zh-4.1.0/)

 

 

