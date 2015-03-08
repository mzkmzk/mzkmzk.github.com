---
layout: post
title: "php 函数累积"
date: 2015-01-07 11:37:40 +0800
comments: true
categories: php
---

###截取字符串函数

	$str1 = substr($str,5);
	echo "从第5个字符开始取至最后：".$str1."
  
 参考链接<http://www.php100.com/html/php/hanshu/2013/0905/4650.html>
  
###随机函数

	//mt_rand生成一个介于33和126之间的数字 
	//chr()将数字转为字符串
	char(mt_rand(33, 126));
	
###php 获取 form表单传递过来的file文件

	$_FILES($_REQUEST("fiel控件的name"));
	
