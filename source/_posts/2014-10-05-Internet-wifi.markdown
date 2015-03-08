---
layout: post
title: "Wifi网络抓包"
date: 2014-10-05 15:16:46 +0800
comments: true
categories: hack
---
#Wifi网络抓包duanU

环境
Mac OS X 10.9.4 

工具
WireShark1.10.6

1.创建airport软链接

	$sudo ln -s /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport   /usr/sbin/airport
	
2.确定无线网卡名

	$ifconfig
	en0: 		flags=8963<UP,BROADCAST,SMART,RUNNING,PROMISC,SIMPLEX,MULTICAST> mtu 1500
	ether ********
	inet6 ****
		inet *****
		 netmask 0xffffff00 broadcast *****
	nd6 options=1<PERFORMNUD>
	media: autoselect
	status: active
	
这里的en0是我的无线.

3.确认通道

	$airport en0 scan
	 SSID BSSID             RSSI CHANNEL HT CC SECURITY (auth/unicast/group)
	 JENNY-PC_Network **** -66  1,+1    Y  -- WPA(PSK/AES/AES) WPA2(PSK/AES/AES) 
	 我的通道是1
	$sudo airport -z//断开wifi
	$sudo airport -c1 //看CHANNEL的值
	
	确认一下~.
	$ airport -I
     agrCtlRSSI: 0
     agrExtRSSI: 0
    agrCtlNoise: 0
    agrExtNoise: 0
          state: init
        op mode: 
     lastTxRate: 0
        maxRate: 0
	lastAssocStatus: 65535
    802.11 auth: open
      link auth: wpa2-psk
          BSSID: 0:0:0:0:0:0
           SSID: 
            MCS: -1
        channel: 1
        
4.配置WireShark

双击wifi -en0 配置嗅探设置

![image](/images/blog/004.png)

设置wifi密码

Edit-> Peferences

![image](/images/blog//005.png)

![image](/images/blog//006.png)

启动监听 (只能监听到在监听后连接的设备)

![image](/images/blog//007.png)

参考链接<http://www.douban.com/note/328099725/>

