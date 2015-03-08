---
layout: post
title: "J2EE 问题集锦"
date: 2014-10-01 11:38:40 +0800
comments: true
categories: J2EE 
---
##1.Eclipse 无法部署MyEclipse过来的项目 

###1.1 MyEclipse导过来的项目无法部署到Eclipse的Tomcat里

因为只有`动态的Web项目`才可以发布到tomcat里  如果项目不能发布,说明不是`动态的Web项目`

1. 右键项目 ->  Proerties -> Project Facets
2. 选中图中所选项 ok 即可

![设置动态Web](/images/blog/0002.jpg)


###1.2 部署项目后的目录存在路径

双击Servers如下图设置 但是如果部署了项目的花 图中是灰色的.remove掉Tomcat里的项目即可 

![Servers视图](/images/blog/0003.jpg)

参考链接<http://www.cnblogs.com/zhuawang/p/3703643.html>

###1.3 源文件读取为WebContent转为WebRoot

打开项目中的.settings

	org.eclipse.wst.common.component文件 ，用记事本打开，

	<wb-module deploy-name="AMS">

         <wb-resource deploy-path="/" source-path="/ WebContent "/><!--WebContent改为WebRoot-->

        <wb-resource deploy-path="/WEB-INF/classes" source-path="/src"/>

        <property name="context-root" value="AMS"/>

        <property name="java-output-path" value="/AMS/ WebContent /WEB-INF/classes"/>

	 </wb-module>
	 
	 
右键项目Close Project 然后再打开即可

参考链接<http://kk580kk.lofter.com/post/1d5e28_865368>

##2.eclipse如何修改dynamic web module version

右击项目 ->Project Facets里面中选择Dynamic Web Module 讲3.0改成2.5但会显示

	cannot change version of project facet dynamic web module to 2.5
	
打开项目的.setting文件夹内的org.eclipse.wst.common.project.facet.core.xml

	<?xml version="1.0" encoding="UTF-8"?>
	<faceted-project>
	<runtime name="Apache Tomcat v5.5"/>
	<fixed facet="jst.web"/>
	<fixed facet="jst.java"/>
	<installed facet="jst.java" version="5.0"/>
	<!--讲这里的version改为2.5即可-->
	<installed facet="jst.web" version="2.5"/>
	<installed facet="wst.jsdt.web" version="1.0"/>
	</faceted-project>
	
##3.命令行启动Tomcat

	cd /Users/maizhikun/Learning/Tomcat7.0/apache-tomcat-7.0.55-src/bin

	sudo sh startup.sh
	
##4.Tomcat无法下载含中文的文件

  	<Connector connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443" URIEncoding="utf-8" /> 
  	
  	//添加URIEncoding="utf-8"即可
  	
##5.getGeneratedKeys方法
通过#getGeneratedKeys方法可以获取主键自增的返回值

	ResultSet rs=null;
	Serializable ret = null;
	stmt=....
	rs = stmt.getGeneratedKeys();  
		     if(rs.next()){  
		         ret = (Serializable) rs.getObject(1); 
		         Integer.parseInt(ret.toString());
		      }


所以主键若非自增则无返回结果
我犯的错误就是以为getGeneratedKeys方法的返回值是主键
然而我表中无自增主键 所以返回null

##6.OGNL里的parameters参数和字符串进行对比


    <s:property value="#parameters.queryType != 'add'"/>

绝对不能这么写平时取参数还可以这些
但是对比parameters和别的字符串的值的时候就必须这样

    <s:property value="#parameters.queryType[0] != 'add'"/>

以前就被坑过.但是没记住- -..

但是又遇到了一个问题

	<s:property value="#parameters.queryType[0] != 'add'"/>这样写的话

当parameters不存在queryType的话 以上这个表达式无法出现结果

应该是类似queryType还要get(0)这样的错误

所以这样判断就可以了

	<s:property value="#parameters.queryType!=null"/>

下面是网上找到的也有可能犯错的案例

1、判断单个字符：

	<s:if test="#session.user.username=='c'">

　　这样是从session中取出username的值，并且判断其是否为c，但是这样判断是不正确的，这样判断的话，根本判断不出来，要改成下面这样：

	<s:if test="#session.user.username=='c'.toString()">

或<s:if test='activityBean.searchForce=="c" '>

[参考链接](http://www.cnblogs.com/wendoudou/p/strutsif.html)
	
	
