---
layout: post
title: "Octopress搭建和配置"
date: 2014-10-01 11:36:40 +0800
comments: true
categories: Octopress 
---
###1 Mac搭建Octopress
1.下载Octopress 

	git clone git://github.com/imathis/octopress.git  octopress 
	
2.安装环境

	cd octopress
	gem install bundler 
	bundle install    // 若出现ERROR:  Could not find a valid gem 'bundler' (>= 0), here is why:参考第三点
	
3.将Octopress部署上Github

登录Github，假设你的用户名是username，首先要新建一个命名为 username.github.com 的Repo

然后

	rake setup_github_pages
	按照提示输入刚才新建的Repo地址，类似：git@github.com:username/username.github.com或git@github.com:username/username.github.com.git。
	
	rake install
	rake generate
	rake preview
	rake deploy
参考链接<http://www.imeetyou.net/article.asp?id=478>


##2 换Octopress主题

先自己google找喜欢的主题~..例如我比较喜欢

 <http://zespia.tw/Octopress-Theme-Slash/index_tw.html>

	cd octopres
	
	$ git clone git://github.com/tommy351/Octopress-Theme-Slash.git .themes/slash

	$ rake install['slash']

	$ rake generate

	//之后可以本地预览一下

	$ rake preview
	
参考链接<http://www.cnblogs.com/sawyerzhu/p/3710374.html>
	
###3 如何解决国内安装gem的问题

	ERROR:  Could not find a valid gem 'bundler' (>= 0), here is why:
	
    Unable to download data from https://rubygems.org/ - Errno::ETIMEDOUT:
    
    Operation timed out - connect(2) (https://rubygems.org/latest_specs.4.8.gz)
    
	ERROR:  Possible alternatives: bundler
	
解决办法

	$ gem sources --remove https://rubygems.org/
	$ gem sources -a http://ruby.taobao.org/
	$ gem sources -l
	*** CURRENT SOURCES ***
	http://ruby.taobao.org
	# 请确保只有 ruby.taobao.org
	$ gem install rails
	
参考链接<http://github.kimziv.com/2013/07/19/how-to-install-ruby-gems-in-china/>

###4用EditPlus写Octopress保存为UTF-8时为无BOM模式&&删除临时备份.bak"

*Default encoding* 选择默认选择的保存编码

*UTF-8 signatrue*  选择Always remove signatrue 则保存为UTF-8时为无BOM模式

*Create backup file when sabing* 去掉对勾 修改时就不会产生.bak
如下图

{% img left /images/blog/1.png  %}

参考链接<http://williamherry.com/blog/2012/07/20/octopress-setup/>

	