---
layout: post
title: "js 函数累积"
date: 2014-12-16 11:37:40 +0800
comments: true
categories: javascript
---

jquery api<http://jquery.bootcss.com/>

###select 选中项

	设置select中value="paraValue"的Item为选中    
	document.all.objSelect.value = objItemValue;  
	
参考链接<http://www.cnblogs.com/Herist/archive/2007/09/24/903890.html>

###Dom元素加载完毕后调用方法 ready()

	$(document).ready(function(){
		$(".btn1").click(function(){
    		$("p").slideToggle();
    	});
    });
 
参考链接<http://www.w3school.com.cn/jquery/event_ready.asp>

###jquery 控制css
通过控制class为button_left的鼠标移入动作把id为up_page设置为可见

	$(".button_left").mouseover(function(){
	$("#up_page").css("visibility","visible");
	});
	
###参考链接

jquery api <http://api.jquery.com/>