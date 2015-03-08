---
layout: post
title: "Mac 搭建 MAMP环境"
date: 2015-01-06 11:37:40 +0800
comments: true
categories: Mac
---

###0x01 Apache 设置访问目录

默认的访问目录是

	http://localhost/~user_name
	
修改默认访问目录*vim /etc/apache2/httpd.conf*
	
	#在这里设置默认的访问路径...
	DocumentRoot "/Users/username/Sites"
	<Directory />
    Options Indexes MultiViews
    AllowOverride All
    Order allow,deny
    Allow from all
	</Directory>
	
以后有项目往这里扔就可以访问了
	
###0x02 更新php

	brew update
	brew tap homebrew/dupes
	brew tap josegonzalez/homebrew-php
	brew install php55 #Apache
	
修改php的cli路径 *vim /etc/bashrc*

	export PATH="/usr/local/bin:/usr/local/sbin:$PATH"
	

设置apache的使用的php版本 *vim /etc/apache2/httpd.conf*

	LoadModule php5_module /usr/local/Cellar/php55/5.5.20/libexec/apache2/libphp5.so
	
###0x03 安装mysql

由于我之前就安装了mysql...这里就直接引用参考链接..


	brew install mysql
	unset TMPDIR
	mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp
	sudo chown -R your_user /usr/local/var/mysql/

###参考链接
MAMP参考链接<http://yansu.org/2013/12/11/lamp-in-mac.html>

更多有关bashrc设置参考链接<http://www.tuicool.com/articles/7nu2E3R>	

	
	
	
	
	