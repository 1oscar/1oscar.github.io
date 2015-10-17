---
layout: post
title: "linux shell 操作点滴"
comments: true
share: true
tags: shell 
---


2015-10-07-linux shell 操作点滴

**只点滴我不是很熟练但还算重要的or 其他reasons**

**I1:常用命令帮助:**
查看程序的binary文件所在路径: $which command
查询命令command的说明文档: $man command
查询命令command的说明文档: $conmand --help（比man好,会把command参数或者例子打印在terminal上)

**I2:文件及目录管理:**
查找目标文件夹中是否有.o结尾的文件:`$find . -name '*.o'`
查看文件显示行号: `$cat -n file`
查看两个文件间的差别:`$diff file1 file2`
动态显示文本最新信息:`$tail -f *.log`
给文件增加别名:
`ln A A2 `:硬连接；删除一个，将仍能找到；
`ln -s A B` :符号链接(软链接)；删除源，另一个无法使用；（后面一个B 为新建的文件）
管道和重定向
批处理命令连接执行，使用 |

```shell
cat /etc/services | more 翻页 显示
cat /etc/services | less 不翻页，需要滑动才能显示
```
重定向：>: 新建 >>:累加到文件末尾
前面成功，则执行后面一条，否则，不执行:&&
前面失败，则后一条执行: || 
ls /proc && echo  suss! || echo failed.

**--------------terminal下快捷输入或删除-------------**
**--------------terminal下快捷输入或删除-------------**
Ctl-U   删除光标到行首的所有字符,在某些设置下,删除全行
Ctl-W   删除当前光标到前边的最近一个空格之间的字符
Ctl-H   backspace,删除光标前边的字符
Ctl-R   匹配最相近的一个文件，然后输出
**--------------terminal下快捷输入或删除-------------**
**--------------terminal下快捷输入或删除-------------**

**磁盘管理:**
查看磁盘空间利用大小:`df -h`(-h: human缩写，以易读的方式显示结果)
查看当前目录所占空间大小:`du -sh `(-h 人性化显示;-s 递归整个目录的大小)
查看当前目录下所有子文件夹大小`du -sh *`
打包和压缩
打包: `tar -cvf B.tar A`:把目录下的文件打包成B(-cvf有些系统中可以写成cvf，下同)
解包: `tar -xvf B.tar` : 解包B.tar到B.tar所在的目录下
打包压缩: `tar -zcvf B.tar.gz .`: 把目录下的文件打包压缩成B.tar.gz(or gzip file 直接在目录下生成file.gz)
解包: `tar -zxvf B.tar.gz ` : 解包B.tar.gz到B.tar.gz所在的目录下(or gzip -d file.gz直接在目录下生成file)
-c :打包选项
-v :显示打包进度
-f :使用档案文件

**进程管理工具**
查询正在运行的进程信息: `ps aux`
显示所有进程信息，连同命令行: `ps -ef`
显示进程信息，并实时更新: `top`
查看端口占用的进程状态：`lsof -i:3306` (lsof: list opened file)
强制杀死进程: `kill -9 pid`
查询指定目录下被进程开启的文件（使用+D 递归目录）：`$lsof +d mydir1/`

**性能监控**
查看内存使用量: `free -h`
查看路由状态: `route -n`

**用户管理工具**
添加用户: `$useradd -m username`
用户添加之后，设置密码: `$passwd username`
删除用户: `$userdel -r username`(不带选项使用 userdel，只会删除用户。用户的家目录将仍会在/home目录下。要完全的删除用户信息，使用-r选项；)
切换用户:`su username`
查看所有用户及权限:`$more /etc/passwd`
查看所有的用户组及权限:`$more /etc/group`
设置用户权限: `chmod `(r,w,x),(root用户，组内用户，组外用户,r:4,w:2,x:1,所以
chmod 421 file : file root只可读，组内用户只可写，组外用户只可执行)

```shell
格式chmod   权限   要修改权限的文件linux中的权限如下：
-rw------- (600) -- 只有属主有读写权限。
-rw-r--r-- (644) -- 只有属主有读写权限；而属组用户和其他用户只有读权限。
-rwx------ (700) -- 只有属主有读、写、执行权限。
-rwxr-xr-x (755) -- 属主有读、写、执行权限；而属组用户和其他用户只有读、执行权限。
-rwx--x--x (711) -- 属主有读、写、执行权限；而属组用户和其他用户只有执行权限。
-rw-rw-rw- (666) -- 所有用户都有文件读、写权限。这种做法不可取。
-rwxrwxrwx (777) -- 所有用户都有读、写、执行权限。更不可取的做
777对应了9位分别是属主有读、写、执行权限；和属组用户和其他用户的读、写、执行权限。
允许某个权限就置1，777（8进制）=111111111（2进制），9位都置一，就是所有权限都开 命令为：chmod 700 a.c
```
更改文件或目录的拥有者: `$chown username dirOrFile`
使用-R选项递归更改该目下所有文件的拥有者:` $chown -R weber server/`

**环境变量**

```sql
bashrc用于交互式non-loginshell，而profile用于交互式login shell。
用bash登陆,至今进入non-loginshell,默认加载.bashrc,su user进入login shell，默认加载.profile,一般在.profile手动执行`source .bashrc`
/etc/profile，/etc/bashrc 是系统全局环境变量设定
~/.profile，~/.bashrc用户目录下的私有环境变量设定
当登入系统获得一个shell进程时，其读取环境设置脚本分为三步:

首先读入的是全局环境变量设置文件/etc/profile，然后根据其内容读取额外的文档，如/etc/profile.d和/etc/inputrc
读取当前登录用户Home目录下的文件~/.bash_profile，其次读取~/.bash_login，最后读取~/.profile，这三个文档设定基本上是一样的，读取有优先关系
读取~/.bashrc
~/.profile与~/.bashrc的区别:

这两者都具有个性化定制功能
~/.profile可以设定本用户专有的路径，环境变量，等，它只能登入的时候执行一次
~/.bashrc也是某用户专有设定文档，可以设定路径，命令别名，每次shell script的执行都会使用它一次
```

```
查询CPU信息:`$cat /proc/cpuinfo`
查看内存信息::`cat /proc/meminfo`
显示当前系统时间: `date`
```
**htop**
htop 是一个 Linux 下的交互式的进程浏览器，可以用来替换Linux下的top命令。
**scp ,crontab**
对于用户cron，使用crontab命令来实现。
-l 查看自己的cron任务列表。
-e 打开用户自己的cron配置文件进行编辑。
-r 移除crontab文件

*shell**
**split**
split命令可以将一个大文件分割成很多个小文件。
-b(byte) : 按照大小分割
` 举例1：
split将date.txt文件分割成大小10KB的小文件：
split -b 10K date.txt
`
`举例2：
例1的文件被分割成多个带有字母的后缀文件，如果想用数字后缀可使用-d(digit)参数，同时可以使用-a length来指定后缀的长度：
split -b 10K  date.txt -d -a 3
`
`举例3：
为分割后的文件指定文件名的前缀：
split -b 10k date.txt -d -a 3 dkf
上面命令表示分割成的文件以dkf为前缀显示
`
-l :按照行数分割
`文件分割成每个包含10行的小文件:
split -l 10 date.txt
`

**cut**
cut 命令从文件的每一行剪切字节、字符和字段并将这些字节、字符和字段写至标准输出；
-b, --bytes=列表        //以**字节为单位进行分割 
 -c, --characters=列表       // 以字符**为单位进行分割。 
 -d, --delimiter=分界符   // 自定义分隔符，默认为制表符。  
 -f, --fields=列表        //只选中指定的这些域；并打印所有不包含分界符的行，除非-s 选项被指定  
 -n                (忽略)  
 -s, --only-delimited        //打印包含分界符的行  
 --output-delimiter=字符串    //使用指定的字符串作为输出分界符，默认采用输入 的分界符  
 --help        //显示此帮助信息并退出  
 --version        //显示版本信息并退出  
`
每种参数格式表示范围如下：  
 N    从第1 个开始数的第N 个字节、字符或域  
 N-    从第N 个开始到所在行结束的所有字符、字节或域  
 N-M    从第N 个开始到第M 个之间(包括第M 个)的所有字符、字节或域  
 -M    从第1 个开始到第M 个之间(包括第M 个)的所有字符、字节或域 
`
为什么会有“域”的提取呢，因为-b和-c只能在固定格式的文档中提取信息，而对于非固定格式的信息则束手无策。这时候“域”就派上用场了
`
'举例：
cut -b 1-10 test     //取得文件中第1个字节到第10个字节的内容
cut -b 1,4,5,7,10 test  //取文件中第1，4，5，7，10字节的内容  
cut -d : -f 1  test  //用-d来设置间隔符为冒号用来分割域，然后用-f来设置我要取的是第一个域，再按回车

**sort**
sort将文件的每一行作为一个单位，相互比较，比较原则是从首字符向后，依次按ASCII码值进行比较，最后将他们按升序输出。
sort -u *.txt  :删除重复行
sort -r *.txt  :以降序来排序，默认是升序
sort -r a.txt -o a.txt :将a.txt逆序后的结果存入到a.txt，此时a.txt存放的是逆序的结果。
sort -n *.txt ：依照数值的大小排序，一位数和两位数的时候首先比较第一位数的大小。
sort -t : -k 2 *.txt  : -t表示指定分隔符，-k表示指定第2列（第2个域）输出。

**awk:**
awk文本分析工具，会把文件逐行的读入，以空格为默认分隔符将每行切片，切开的部分再进行各种分析处理。
使用-F来设置定界符（默认为空格）

统计文件行数: awk 'END {print NR}' file
调换前两列的位置: awk '{temp = $1; $1 = $2; $2 = temp}' file
只查询根目录最大文件（ls查看完整的文件信息，过滤掉d开头的东东（目录），取出文件大小$5和名字$9两项，排序，取第一个）：
ls -l | awk '/[d]/ {print $5,$9}' | sort -nr | head -1

cat 1.txt|awk -F '^A' '{print $1"\t"$2}'
cat 1.txt|awk -F '' '{print $1}'|cut -b 1-14
[**awk还需要深入学习啊**](http://awk.readthedocs.org/en/latest/index.html)

