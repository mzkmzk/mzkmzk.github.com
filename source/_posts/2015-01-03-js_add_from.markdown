---
layout: post
title: "js动态添加 from表单元素"
date: 2015-01-03 11:37:40 +0800
comments: true
categories: javascript
---
	
	//from_this参数作用为Onsubmit事件传递过来的from表单 或者通过id获取也可以
	function  inser_Submit(from_this){
		 var NFC_ID=document.createElement("input");
		 NFC_ID.type="hidden";
		 NFC_ID.name="NFC_ID";
		 NFC_ID.value=document.getElementById("NFCID").value;
		 from_this.appendChild(NFC_ID);
	}