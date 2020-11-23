---
layout: post
title: Ghost博客mail配置
date: '2017-03-04 16:10:08'
---

Ghost博客系统（0.11.7）发送邮件使用的是[Nodemailer](https://github.com/andris9/Nodemailer)，从package.json文件可知nodemailer的版本是0.7.1，Ghost的[官方文档](http://docs.ghost.org/zh/mail/)中只提到Mailgun、Amazon SES和Gmail的配置，按官网配置的Gmail无法发送邮件。查看nodemailer的文档，可知QQ邮箱的配置如下（亲测可用）：
```
mail:{
  transport:"SMTP",
  from:"username <YOUR_EMAIL>",
  options: {
      host: "smtp.qq.com",
      secureConnection: true,
      port: 465,
      auth: {
          user: "YOUR_EMAIL",
          pass:"****" //腾讯的授权码
      }
  }
}
```
Nodemailer支持的邮箱服务如下：  

* AOL  
* DynectEmail  
* Gmail  
* hot.ee  
* Hotmail  
* iCloud  
* mail.ee  
* Mail.Ru  
* Mailgun  
* Mailjet  
* Mandrill  
* Postmark  
* QQ  
* QQex (Tencent Business Email)  
* SendGrid  
* SendCloud  
* SES  
* Yahoo  
* yandex  
* Zoho  
####参考资料
1、https://community.nodemailer.com/nodemailer-0-7-deprecated/　　
2、http://byxfei.com/2016/01/22/ghost-mail-smtp-setting/
3、http://docs.ghost.org/zh/mail/