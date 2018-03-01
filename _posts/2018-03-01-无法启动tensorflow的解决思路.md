---
layout: post
title: "无法启动tensorflow的解决思路"
comments: true
share: true
tags: tensorflow,机器学习
---




记录tensorflow激活前后，都无法导入tensorflow的问题解决方式。

激活tensorflow环境后，在python交互式环境下，import tensorflow总是显示没有这个模块；
未激活tensorflow环境时，在python交互式环境下，import tensorflow总是提示：
ImportError: libcudart.so.9.0: cannot open shared object file: No such file or directory


conda list 发现tensorflow CPU版本安装了1.3.0
gpu版本安装了1.4.0,1.2.1,1.5.0,装的比较多，都卸载了。

pip install tensorflow-gpu,默认装1.5.0.

查看机器是否装了GPU：显卡是nvidia的。
cat /proc/driver/nvidia/gpus/0000\:05\:00.0/information
发现装了gpu。有8块。
0000:05:00.0  0000:06:00.0  0000:09:00.0  0000:0a:00.0  
0000:84:00.0  0000:85:00.0  0000:88:00.0  0000:89:00.0
有gpu才能装gpu版本的tensorflow。

但是还是报错。和之前的错误一样。

激活tensorflow环境后，在python交互式环境下，import tensorflow总是显示没有这个模块；
未激活tensorflow环境时，在python交互式环境下，import tensorflow总是提示：
ImportError: libcudart.so.9.0: cannot open shared object file: No such file or directory

猜测是：缺少GPU的cuda的一些包：

查找~/.bash_profile,
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda/lib64"
export CUDA_HOME=/usr/local/cuda
已经加入路径了（cuda是cuda-.8.0的软连接。）

查找：
vim /etc/ld.so.conf.d/nvidia.conf

/usr/local/cuda-8.0/lib64
/usr/local/cuda-8.0/lib
已经加入进去了。

查找~/.profile，加载~/.bashrc，查找~/.bashrc发现，最后，

export PATH="/root/anaconda2/bin:$PATH"
export LD_LIBRARY_PATH="/usr/local/nvidia/lib:/usr/local/nvidia/lib64"
export PATH="/workspace:/usr/local/nvidia/bin:/usr/local/cuda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/nvidia/bin:/usr/local/cuda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/nvidia/bin:/usr/local/cuda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

打印环境变量：
echo $PATH 
echo $LD_LIBRARY_PATH，
发现不少.bashrc里的设置，是.bash_profile里的设置。

分析：
当登入系统获得一个shell进程时，其读取环境设置脚本分为三步:
首先读入的是全局环境变量设置文件/etc/profile，然后根据其内容读取额外的文档，如/etc/profile.d和/etc/inputrc
读取当前登录用户Home目录下的文件~/.bash_profile，其次读取~/.bash_login，最后读取~/.profile，这三个文档设定基本上是一样的，读取有优先关系。
没明白为什么没有把bashrc的环境加进去。
我是ssh -p* root@ip ,不知道是不是和这样进去的方式有关系。

把.bashrc的路径强制加载进系统环境。
echo $PATH 
echo $LD_LIBRARY_PATH，
少了.bash_profile的环境。
发现.bashrc的设置bug，并去除PATH中的重复的：
修改如下：
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/nvidia/lib:/usr/local/nvidia/lib64"
export PATH="/workspace:/usr/local/nvidia/bin:/usr/local/cuda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:$PATH"

每次ssh进入后，都需要source ~/.bashrc，进入python环境，import tensorflow，正确。
在.bash_profile里强制加入一行：
source ~/.profile
这样，每次，ssh进入后，就不需要source了。

激活tensorflow，source activate tensorflow,
进入python交互环境，import tensorflow，没有这个模块。

打印环境变量：
echo $PATH 
echo $LD_LIBRARY_PATH，
发现，
/root/anaconda2/envs/tensorflow/bin:/workspace:/usr/local/nvidia/bin:/usr/local/cuda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/root/anaconda2/bin:/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/bin:/root/.linuxbrew/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:

相比较激活之前，多了个/root/anaconda2/envs/tensorflow/bin路径，却无法导入tensorflow，不解。
这部分路径从哪里过来的。

查找~/.conda，发现/root/anaconda2/envs/tensorflow,猜测可能是source这块，从这块过来的。

想起是 source activate tensorflow，这个命令导致环境变量变化，
查找：
vim ~/anaconda2/envs/tensorflow/bin/activate
发现：
export PATH="$_NEW_PART:$PATH"

在导入变量，新加的变量添加中PATH前面。
修改为：
export PATH="$PATH:$_NEW_PART"

保存，

激活tensorflow后，python交互环境，import tensorflow可以正常导入。

打印路径：
/workspace:/usr/local/nvidia/bin:/usr/local/cuda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/root/anaconda2/bin:/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/bin:/root/.linuxbrew/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games::/root/anaconda2/envs/tensorflow/bin

 不解的是：
 为什么:/root/anaconda2/envs/tensorflow/bin放到前面不行，后面却可以。
 
 



具体的安装tensorflow，可以参考：

https://github.com/Jinglue/TensorFlow-Guide/blob/master/preparation/installation_ubuntu.md


























备注：如何查看ununtu是否有GPU?




































