---
layout: post
title: "jquery 实现 ajax"
date: 2015-01-03 11:37:40 +0800
comments: true
categories: jquery
---

##0x01 导入jquery.js

	<script type="text/javascript" src="./js/jquery.min.js"></script>
	
##0x02 调用 jquery 的ajax方法

	$(function(){
		$('#login').on('submit',function(){
			var $form = $(this),
			//将所需要提交的form表单 序列化为字符串
			postData = $form.serialize();
			// loading...
			//getJson第一个参数为要请求的url,第二个是传递过去的参数
			$.getJSON('LoginAction',postData).done(function(data){
				//data为返回来的json数据
				if(data.msg){
					location.href="Home.jsp";
					alert("登陆成功");
				}else{
					alert("账号/密码错误 请重新输入");
				}
			}).fail(function(){
				alert('登录出错：网络连接出现问题，请稍后再试。');
			}).complete(function(){
				// un loading...
			})
			return false;
		});
	});

参考链接<http://www.w3cschool.cn/ajax_getjson.html>