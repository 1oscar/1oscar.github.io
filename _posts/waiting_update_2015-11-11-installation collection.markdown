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
**Mac OS X使用BSD版本的命令行工具,虽然都共同遵守POSIX标准,但其与GUN命令行工具仍然有很多的不同,而且明显不如GNU版本的命令好用。**

```sql
ununtu:
sudo apt-get install mydumper
```

I5. **GNU 工具脚本**

```shell
#!/usr/local/bin/bash

# add source
brew tap homebrew/dupes

# GNU Coreutils
brew install coreutils

# build tools
brew install autoconf
brew install m4
brew install make

# misc
brew install binutils
brew install diffutils
brew install ed --default-names
brew install findutils --default-names
brew install gawk
brew install gnu-indent --default-names
brew install gnu-sed --default-names
brew install gnu-tar --default-names
brew install gnu-which --default-names
brew install gnutls --default-names
brew install grep --default-names
brew install gzip
brew install screen
brew install watch
brew install wdiff --with-gettext
brew install wget

# third party 
brew install git
brew install less
brew install openssh --with-brewed-openssl
brew install python3 --with-brewed-openssl
brew install rsync
brew install unzip
brew install vim --override-system-vi
```

