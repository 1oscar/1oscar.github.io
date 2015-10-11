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

 was configure    # 配置aws
AWS Access Key ID [None]: # 直接enter
AWS Secret Access Key [None]:  ＃直接enter
Default region name [None]: cn-north-1   #中国一区
Default output format [None]: json     # 响应方式json
```

I4. **install mydumper**

```sql
ununtu:
sudo apt-get install mydumper
```

