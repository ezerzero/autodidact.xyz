---
date: 2017-05-02 09:53:39 +0800
category: programming
permalink: /redis-basic
---
# Redis基础知识

官网：http://redis.io  
默认端口：`6379`  
启动控制台：`redis-cli`  
常用命令：`info`、`select index`：选择数据库，index默认值为0；`keys regex`、`expire key seconds`、`expireat key timestamp`、`ttl key`、`sort`、`set key value [EX/PX]`、`get key`、`del key`、`flushdb/flushall`  
关键字（Keys）：用来标识数据块  
值（Values）：关联于关键字的实际值  
五种数据结构：字符串（Strings)、散列（Hashes）、列表（Lists）、集合（Sets）、分类集合（Sorted Sets）  
