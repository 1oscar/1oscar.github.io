---
layout: post
title: "MarkResources Pools"
comments: true
share: true
tags: python
---

## 一: 爬虫相关

### mechanize
**与web服务器交互复杂,如get，post等，使用 mechanize（模拟登陆);BeautifulSoup提取数据** 

1. [**IBM mechanize介绍**](http://www.ibm.com/developerworks/cn/linux/l-python-mechanize-beautiful-soup/#resources)
2. [**豆瓣 mechanize介绍**](http://site.douban.com/146782/widget/notes/15468638/note/355611270/) 
3. [**Beautiful Soup**](http://cuiqingcai.com/1319.html)

### urllib_proxy
1.  [**proxy tools**](https://github.com/the5fire/practice_demo/blob/master/tools/urllib_proxy.py)
2. [**httplib**](https://docs.python.org/2/library/httplib.html)
3. 低成本的获取IP池，这是一个难点

### cookie handle

```python
    br = mechanize.Browser()
    cj = cookielib.LWPCookieJar()
    br.set_cookiejar(cj)
```

### 爬虫框架

1. [**海量数据爬虫框架搭建**](http://blog.jobbole.com/46673/)
