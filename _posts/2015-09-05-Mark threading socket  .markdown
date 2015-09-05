---
layout: post
title: "Mark threading socket  "
comments: true
share: true
tags: python
---

### Mark 一些经典的代码
一: threading
 

    1 # -*- coding: utf-8 -*-
    2 import string, threading, time
    3
    4 def thread_main(a):
        global count, mutex
        # 获得线程名
        threadname = threading.currentThread().getName()
        for x in xrange(0, int(a)): 
            # 取得锁
            mutex.acquire() 
            count = count + 1 # 释放锁
        14 mutex.release()
        15 print threadname, x, count
        16 time.sleep(1)
        17
    18 def main(num):
        19 global count, mutex
        20 threads = []
        21
        22 count = 1
        23 # 创建一个锁
        24 mutex = threading.Lock()
        25 # 先创建线程对象
        26 for x in xrange(0, num):
        27 threads.append(threading.Thread(target=thread_main, args=(10,)))
        28 # 启动所有线程
        29 for t in threads:
        30 t.start()
        31
        32
        33
        34 if __name__ == '__main__': 35 num=4
        # 主线程中等待所有子线程退出 for t in threads:
        t.join()
        36 #创建4个线程
        37 main(4)


二: socket
网络服务端的建立过程分为 6 个阶段,创建 Socket 对象、绑定端口、监听连接、接受请 求、数据收发、关闭端口
分 别 对 应 函 式 socket.socket() 、 socket.bind() 、 socket.listen() 、 socket.accept() socket.sendall()\socket.recv()、socket.close()
**server端:** 

    1 # coding:utf-8
    2 import socket
    3 # 监听本机 5678 端口,当有客户端请求时,回复指定字符串 4
    5 host = '127.0.0.1 '
    6 port = 5678
    7
    8 s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    9 #采用TCP协议
    10 s.bind((host, port))
    11 #绑定socket 12 s.listen(1)
    13 #服务器监听连接
    14
    15 while 1:
    16 #这里的whil循环,可以使程序多地响应多客户端的请求
    17 clientSocket,clientAddr = s.accept() 18 #接受客户端连接
    19 print 'Client connected!'
    20 clientSocket.sendall('Welcome to Python World!') 21 #向客户端发送字符串
    22 clientSocket.close()
    23 #关闭与客户端的连接

**client**

    1 # coding:utf-8
    2 import socket
    3 # 连接本机 5678 端口,并读取 socket,将结果打印屏幕 4
    5 host = '127.0.0.1'
    6 port = 5678
    7
    8 s = socket.socket(socket.AF_INET, socket.SOCK_STREAM) 9 #创建采用TCP协议的socket对象
    10 s.connect((host, port)) 11 #连接指定的服务器端
    12
    13 while 1:
    14 #从socket读取数据,并输出到屏幕,读完后退出程序 15 buf = s.recv(2048)
    16 17 18
    if not len(buf):
       break
    print buf


**来源:<<可爱的python>>pcs207 threading  pcs216 socket**
