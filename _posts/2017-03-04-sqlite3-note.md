---
layout: post
title: Sqlite3基本操作
date: '2017-03-04 12:00:44'
tags:
- programming
---

####安装
* Ubuntu：`sudo apt-get install sqlite3`  
* CentOS：`yum install sqlite`  

####数据库操作
* 创建或打开数据库：`sqlite3 DatabaseName.db`  
* 查看数据库列表：在`sqlite3`提示符下输入`.databases`  
* 导出数据库：`sqlite3 DatabaseName.db .dump > DatabaseName.sql`  
* 将sql文件导入数据库：`sqlite3 DatabaseName.db < DatabaseName.sql`  

####数据表操作
* 查看数据库中的所有表：`sqlite3 DatabaseName.db .tables`，或在`sqlite3`提示符下输入`.tables`  
* 查看表结构：`.schema TableName`
* 创建表：
```
CREATE TABLE database_name.table_name(
   column1 datatype PRIMARY KEY(one or more columns),
   column2 datatype NOT NULL(Optional),
   column3 datatype,
   .....
   columnN datatype,
);
```  

* 删除表：`DROP TABLE TableName`  
* 在表中添加新的数据：
```
INSERT INTO TABLE_NAME (column1, column2, column3,...columnN) 
VALUES (value1, value2, value3,...valueN);
```
以上为在指定的列中添加值，如果是在所有列中添加值，可直接用`INSERT INTO VALUES (value1, value2, value3,...valueN);`  

* 查找表中的记录：`SELECT column1, column2, columnN FROM TableName;`  
* 更新表中记录:`UPDATE TableName SET columnName=value Where [condition]`  
* 删除表中记录：`DELETE FROM TableName Where [condition]`  

####参考资料
1、http://www.runoob.com/sqlite/sqlite-like-clause.html