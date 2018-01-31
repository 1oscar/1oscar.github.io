---
layout: post
title: "hadoop,hive,hbase知识串讲复习篇" 
comments: true
share: true
tags: hadoop,hbase 
---


一晃三年多，2014年5月，那时候还是hadoop人才一票难求的时候。开始自学hadoop，看视频，记笔记，搭建伪分布式集群，做项目；2014年9月，通过几层面试，进去CAS实习，做流式计算（hadoop，spark）的探究，写综述，写论文；2015年6月，在一家大数据公司实习，使用hive，hadoop接触广告数据；2015年12月，使用hadoop做招聘数据。一直到现在，偶尔会接触到hadoop。只能说，没有最深，只有不断的用到，再熟悉。而这一整个过程，世界久了，难免会记忆不牢靠啊。  然我写的都给我自个看的。



全文文字几乎没有，全是图片。

![1](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/1.jpg)

![2](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/2.jpg)

![3](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/3.jpg)

![4](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/4.jpg)

![5](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/5.jpg)

![6](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/6.jpg)


Derby数据库是一个纯用Java实现的内存数据库

hive存储方式：

![7](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/7.jpg)

hive的内存调优：

![8](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/8.jpg)

![9](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/9.jpg)

![10](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/10.png)

![11](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/11.jpg)

![12](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/12.png)

![13](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/13.jpg)

Hadoop的序列化格式：Writable

![14](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/14.jpg)

![15](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/15.jpg)

![16](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/16.png)

partitioner，适用于二次排序场景,分组，排序。

![17](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/17.jpg)

shuffle:

![18](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/18.jpg)

![19](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/19.jpg)

![20](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/20.jpg)

![21](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/21.jpg)

ZooKeeper是一个分布式的，开放源码的分布式应用程序协调服务
HBase利用HadoopHDFS作为其文件存储系统，利用HadoopMapReduce来处理HBase中的海量数据，利用Zookeeper作为协调工具。

![22](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/22.jpg)

![23](http://1oscar.github.io/photos/blogPhotos/hadoop%2Chive%2Chbase%E7%9F%A5%E8%AF%86%E4%B8%B2%E8%AE%B2%E5%A4%8D%E4%B9%A0%E7%AF%87/23.jpg)




