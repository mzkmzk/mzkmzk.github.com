---
layout: post
title: "php 解决乱码"
date: 2015-01-04 11:37:40 +0800
comments: true
categories: php
---

###0x01 php文件

	//php文件头中加入
	header("Content-Type: text/html; charset=utf-8");
	
###0x02 html 文件

	<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
	
###参考链接

<http://www.jb51.net/article/21118.htm>