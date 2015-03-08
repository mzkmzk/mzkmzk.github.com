---
layout: post
title: "Mysql 问题集锦"
date: 2014-10-01 11:37:40 +0800
comments: true
categories: Mysql 
---
##1.mysql字符乱码

如要进行数据库定制，可到'/usr/local/mysql/support-files/'文件夹底下，把里面的任一个.cnf配置文件复制到/etc/目录底下并修改文件名称为my.cnf。

	sudo cp /usr/local/mysql/support-files/my-medium.cnf /etc/my.cnf

	sudo vi /etc/my.cnf
	
[mysqld]部分加入：

	character-set-server=utf8