---
layout: post
title: "Eclipse 多个工作空间共享快捷键"
date: 2014-12-11 11:37:40 +0800
comments: true
categories: Eclipse
---

###0x01

	//被共享的工作空间

	%Workspace%/.metadata/.plugins/org.eclipse.core.runtime/.settings/org.eclipse.ui.workbench.prefs  
	
	//里面xml
	
	org.eclipse.ui.commands=<?xml version/="1.0" encoding/="UTF-8"?> 
	//复制 org.eclipse.ui.commands=后面的内容到新的工作空间的位置即可
	
参考链接<http://forever8tf.iteye.com/blog/1255319>