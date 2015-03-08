---
layout: post
title: "Android 问题集锦"
date: 2014-10-01 11:40:40 +0800
comments: true
categories: Android 
---

##1. MAC ADT下载提示 没安装 java se6

	//每个人的jdk版本不一样 路径文字不完全一样 建议tab补全输路径
	sudo vim  /Library/Java/JavaVirtualMachines/jdk1.7.0_67.jdk/Contents/Info.plist  
	
把原本的

	<key>JVMCapabilities</key>
                <array>
                        <string>CommandLine</string>
                </array>
           
修改成

	<key>JVMCapabilities</key>
                <array>
                        <string>JNI</string>
                        <string>BundledApp</string>
                        <string>WebStart</string>
                        <string>Applets</string>
                        <string>CommandLine</string>
                </array>
                
参考链接<http://smilejay.com/2013/11/mac-os-x-to-open-eclipse-you-need-a-java-se-6-runtime/>

##2. Android 导入工程出现Unable to resolve target 'android-xx'错误 

出现这样的错误可能会导致 .R文件无法生成..

首先打开其他你能运行的Android项目

到工作空间查看其project.properties文件

	target=android-?
	
然后再到你刚导入的项目改成和?即可

懒的话 直接把文件复制粘贴过去- -...应该也ok




