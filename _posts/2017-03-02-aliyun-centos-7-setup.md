---
layout: post
title: 阿里云服务器环境配置（CentOS 7）
date: '2017-03-02 16:01:41'
tags:
- programming
---

####初始化系统
######更改主机名
`hostnamectl set-hostname 主机名`
######添加普通用户
用root账号登录：`ssh root@Server_IP`  
添加普通用户：`adduser demo`  
设置密码：`passwd demo`  
添加root权限：`gpasswd -a demo wheel`  
切换用户：`su - demo`
######使用SSH登录
复制本地的public key至`/home/.ssh/`，将文件重命令为`authorized_keys`，`.ssh`目录权限设置为`700`：`chmod 700 .ssh`，`authorized_keys`的权限设置为`600`：`chmod 600 .ssh/authorized_keys`  

注：本地生成ssh key的命令为`ssh-keygen`，用`ssh-copy-id demo@SERVER_IP`可将public key直接复制到服务器。
######更改SSH设置
修改配置文件：`vi /etc/ssh/sshd_config`，将`#PermitRootLogin yes`改为`PermitRootLogin no`，将`PasswordAuthentication yes`改为`PasswordAuthentication no`

####Nginx
安装：`sudo yum install epel-release`，`sudo yum install nginx`  
启动：`sudo systemctl start nginx`  
测试：`http://Server_IP/`  
设置开机自动启动：`sudo systemctl enable nginx`  
配置：配置文件在`/etc/nginx/nginx.conf`,
```
// PHP site
server {
  listen 80;
  server_name example.com;
  root /home/www/example.com;
  index index.php index.html;

  location / {
    try_files $uri $uri/ /index.php?$query_string;
  }

  location ~ \.php$ {
    try_files $uri = 404;
    fastcgi_pass unix:/var/run/php-fpm/php-fpm.sock;
    fastcgi_index index.php;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
  }
}
// nodejs app
server {
    listen 80;
    server_name example.com;
    root /var/www/example.com/;
    location / {
        proxy_pass http://localhost:port;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
// nodejs app with https
server {
    listen       80;
    listen       [::]:80;
    listen       443 ssl;
    server_name  example.com;
    root         /var/www/example.com/;

    ssl_certificate   cert/filename.pem;
    ssl_certificate_key  cert/filename.key;
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;# Load configuration files for the default server block.
    include /etc/nginx/default.d/*.conf;

    location / {
      proxy_pass http://localhost:port;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection 'upgrade';
      proxy_set_header Host $host;
      proxy_cache_bypass $http_upgrade;
    }

    error_page 404 /404.html;
        location = /40x.html {
    }

    error_page 500 502 503 504 /50x.html;
        location = /50x.html {
    }
}
```
重启Nginx:`sudo systemctl restart nginx`，或重新加载配置文件`sudo nginx -s reload`
####MySQL（MariaDB）
######MySQL
查看MySQL Yum Repository：`https://dev.mysql.com/downloads/repo/yum/`  
下载安装包：`wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm`  
验证下载文件MD5值：`md5sum mysql57-community-release-el7-9.noarch.rpm`  
安装：`sudo rpm -ivh mysql57-community-release-el7-9.noarch.rpm`，`sudo yum install mysql-server`  
启动MySQL：`sudo systemctl start mysqld`  
查看root的初始密码：`sudo grep 'temporary password' /var/log/mysqld.log`  
设置MySQL：`sudo mysql_secure_installation`  
测试：`mysqladmin -u root -p version`
######MariaDB
安装：`sudo yum install mariadb-server mariadb`  
启动：`sudo systemctl start mariadb`  
配置：`sudo mysql_secure_installation`  
设置开机启动：`sudo systemctl enable mariadb`
####PHP
安装PHP：`sudo yum install php php-mysql php-fpm`  
修改PHP设置：`sudo vi /etc/php.ini`，将`;cgi.fix_pathinfo = 1`改为`cgi.fix_pathinfo = 0`  
修改php-fpm设置：`sudo vi /etc/php-fpm.d/www.conf`，将`listen = 127.0.0.1:9000`改为`listen = /var/run/php-fpm/php-fpm.sock`，将`;listen.owner = nobody`改为`listen.owner = nobody`，将`;listen.group = nobody`改为`listen.group = nobody`，将`user = apache`改为`user = nginx`，将`group = apache`改为`group = nginx`  
启动PHP：`sudo systemctl start php-fpm`  
设置开机启动：`sudo systemctl enable php-fpm`
####Nodejs和npm
下载文件：`curl --silent --location https://rpm.nodesource.com/setup_6.x | sudo bash -`  
安装：`sudo yum -y install nodejs`  
####MongoDB
创建repo文件：`sudo vim /etc/yum.repos.d/mongodb-org-3.6.repo`，文件内容如下：
```
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
```
安装MongoDB：`sudo yum install -y mongodb-org`  
启动服务：`sudo service mongod start`  
停止服务：`sudo service mongod stop`  
重启服务：`sudo service mongod restart`  
开机启动：`sudo chkconfig mongod on`
####PM2
安装：`npm install pm2 -g`  
使用：`pm2 start app.js`
####自动部署
######服务器端
安装Git：`sudo yum install git`  
建立repo：
```
cd /var
mkdir repo && cd repo
mkdir site.git && cd site.git
git init --bare
```
添加hooks：在`site.git/hooks/`目录下添加文件`post-receive`，文件内容为`git --work-tree=/var/www/domain.com --git-dir=/var/repo/site.git checkout -f`，给文件添加可执行权限：`chmod +x post-receive`  
######本地
添加远程库：`git remote add live ssh://user@mydomain.com/var/repo/site.git`  
push代码到远程库：`git push live master`  
####参考资料
1、https://www.digitalocean.com/community/tutorials/how-to-set-up-automatic-deployment-with-git-with-a-vps
2、https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-centos-7
3、https://nodejs.org/en/download/package-manager/#enterprise-linux-and-fedora
4、https://docs.mongodb.com/manual/tutorial/install-mongodb-on-red-hat/
5、http://pm2.keymetrics.io/
6、https://stackoverflow.com/questions/28911634/how-to-avoid-transparent-hugepage-defrag-warning-from-mongodb/