---
date: 2018-12-27 00:27:57 +0800
category: programming
permalink: /cheng-xu-yuan-lian-ji-gong-lue-3
---
# 陈皓程序员练级攻略之入门篇

> “无论你做什么事，你都会面对各式各样的困难，这对每个人都是一样的，而只有兴趣、热情和成就感才能让你不怕这些困难。”

[The Key To Accelerating Your Coding Skills](http://blog.thefirehoseproject.com/posts/learn-to-code-and-be-self-reliant/)

> Once a developer has passed both the web development inflection point and the algorithm and data structures inflection point, they hold the keys to the kingdom.  
> .......  
> Programming is a life-long learning experience. Experienced software engineers seek to find solutions to problems they haven’t solved yet because it gives them the opportunity to learn more. If you find yourself waiting for the moment when you finally feel like you know everything there is to know about coding, know this: the day you’re waiting for will never come. And that is a wonderful thing.

[You Can’t Solve Real World Coding Problems Without These 3 Computer Science Fundamentals](http://blog.thefirehoseproject.com/posts/cant-solve-real-world-coding-problems-without-3-computer-science-fundamentals/)

> Trees, optimal algorithms, and recursion are 3 aspects of computer science that help developers solve everyday problems.

## 编程技能

1、[代码大全](https://book.douban.com/subject/1477390/)  
2、[Java核心技术·卷 I](https://book.douban.com/subject/26880667/)  
3、[Spring in Action](https://book.douban.com/subject/26767354/)  
4、[Spring Boot实战](https://book.douban.com/subject/26857423/)  
5、[鸟哥的Linux私房菜](https://book.douban.com/subject/4889838/)  
6、[HTTP文档](https://developer.mozilla.org/zh-CN/docs/Web/HTTP)  
7、[数据库设计的那些事](https://www.imooc.com/learn/117)  
8、[MySQL文档](https://dev.mysql.com/doc/)  
9、[MySQL必知必会](https://book.douban.com/subject/3354490/)  
10、[JQuery](https://jquery.com/)  
11、[Bootstrap](https://getbootstrap.com/)  
12、[ES6入门](http://es6.ruanyifeng.com/)  
13、[关于字符编码，你所需要知道的](http://www.imkevinyang.com/2010/06/%E5%85%B3%E4%BA%8E%E5%AD%97%E7%AC%A6%E7%BC%96%E7%A0%81%EF%BC%8C%E4%BD%A0%E6%89%80%E9%9C%80%E8%A6%81%E7%9F%A5%E9%81%93%E7%9A%84.html)  
14、[The history of Character Encoding](http://www.developerknowhow.com/1091/the-history-of-character-encoding)  
15、[Wikipedia - Character encoding](https://en.wikipedia.org/wiki/Character_encoding)  
16、[Awesome Unicode](https://github.com/jagracey/Awesome-Unicode)  
17、[Awesome Code Points Awesome](https://github.com/Codepoints/awesome-codepoints)

## 编程工具

1、[Eclipse](http://www.runoob.com/eclipse/eclipse-tutorial.html)  
2、[Intellij IDEA](https://www.gitbook.com/book/dancon/intellij-idea/details)  
3、[Vitual Studio Code](https://jeasonstudio.gitbooks.io/vscode-cn-doc/content/)  
4、[Git](https://git-scm.com/book/zh/v2/)  
5、[Chrome](http://www.igeekbar.com/igeekbar/post/156.htm)  
6、[MySQL WorkBench](https://dev.mysql.com/doc/workbench/en/)

## 实践项目

设计一个投票系统

- 业务需求如下：  
1、用户只有在登录后，才可以生成投票表单  
2、投票项可以单选，可以多选  
3、其它用户投票后显示当前投票结果（但是不能刷票）  
4、投票有相应的时间，页面上需要出现倒计时  
5、投票结果需要用不同颜色不同长度的横条，并显示百分比和人数
- 技术需求如下：  
1、后端用Java Spring Boot来实现，后端只返回JSON数据给前段  
2、前端用JQuery实现数据处理及操作，动态生成页面  
3、前端页面是响应式的，手机端和桌面端有不同呈现  
4、在微信中，通过微信授权后记录用户信息，以防止刷票  
5、不刷新页面就可以动态地看到投票结果的变化  
6、使用第三方画图表的JavaScript库，然后把图表画得风骚一些
