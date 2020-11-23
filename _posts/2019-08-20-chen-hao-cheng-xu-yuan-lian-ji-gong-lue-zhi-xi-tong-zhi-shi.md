---
date: 2019-08-20 12:04:05 +0800
category: programming
permalink: /cheng-xu-yuan-lian-ji-gong-lue-6
---
# 陈皓程序员练级攻略之系统知识

- [深入理解计算机系统](https://book.douban.com/subject/5333562/)
- [Unix高级环境编程](https://book.douban.com/subject/1788421/)
- [Unix网络编程第1卷：套接口API](https://book.douban.com/subject/1500149/)
- [Unix网络编程第1卷：进程间通信](https://book.douban.com/subject/4118577/)
- [TCP/IP详解：卷1协议](https://book.douban.com/subject/1088054/)
- [Wireshark数据包分析实战](https://book.douban.com/subject/21691692/)
- [C10K Problem](http://www.kegel.com/c10k.html)
- 实践项目
  - 实现一个 telnet 版本的聊天服务器，主要有以下需求
    - 每个客户端可以用使用telnet ip:port的方式连接到服务器上
    - 新连接需要用用户名和密码登录，如果没有，则需要注册一个
    - 然后可以选择一个聊天室加入聊天
    - 管理员有权创建或删除聊天室，普通人员只有加入、退出、查询聊天室的权力
    - 聊天室需要有人数限制，每个人发出来的话，其它所有的人都要能看得到
  - 实现一个简单的 HTTP 服务器，主要有以下需求
    - 解释浏览器传来的 HTTP 协议，只需要处理 URL path
    - 然后把所代理的目录列出来
    - 在浏览器上可以浏览目录里的文件和下级目录
    - 如果点击文件，则把文件打开传给浏览器（浏览器能够自动显示图片、PDF，或 HTML、CSS、JavaScript 以及文本文件）
    - 如果点击子目录，则进入到子目录中，并把子目录中的文件列出来
  - 实现一个生产者 / 消费者消息队列服务，主要有以下需求
    - 消息队列采用一个 Ring-buffer 的数据结构
    - 可以有多个 topic 供生产者写入消息及消费者取出消息
    - 需要支持多个生产者并发写
    - 需要支持多个消费者消费消息（只要有一个消费者成功处理消息就可以删除消息）
    - 消息队列要做到不丢数据（要把消息持久化下来）
    - 能做到性能很高
<!--kg-card-end: markdown-->