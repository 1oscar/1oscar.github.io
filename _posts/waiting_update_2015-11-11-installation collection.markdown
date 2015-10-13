---
layout: post
title: "installation collection" 
comments: true
share: true
tags: tools
---


I1. **ubuntu install pip :**

```sql 
sudo apt-get install python-pip python-dev build-essential
sudo pip install --upgrade pip
sudo pip install --upgrade virtualenv
```

I2. **ubuntu install mysqldb:**

```sql
sudo apt-get install python-mysqldb
```

I3. **ununtu install aws:**

```sql
安装aws命令 :
sudo apt-get install awscli  #ubuntu系统
sudo aws s3 ls s3://  # 列出所有的桶

配置was: 

aws configure    # 配置aws
AWS Access Key ID [None]: # 直接enter(ununtu是基于aws的)
AWS Secret Access Key [None]:  ＃直接enter
Default region name [None]: s   #中国一区
Default output format [None]: json     # 响应方式json
```

I3.1 **mac install aws**

```shell
sudo pip install awscli
配置was: 

aws configure    # 配置aws
AWS Access Key ID [None]: # 输入.csv 中的key
AWS Secret Access Key [None]:  ＃输入.csv 中的 secret key
Default region name [None]: s   #中国一区
Default output format [None]: json     # 响应方式json
```



I4. **install mydumper**

```sql
ununtu:
sudo apt-get install mydumper
```

