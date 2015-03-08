---
layout: post
title: "android 设置两个控件各占屏幕的一半"
date: 2014-12-27 11:37:40 +0800
comments: true
categories: android
---

我的需求是一行里 两个TextView 各占屏幕的 一半

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal" 
    android:id="@+id/book_access"
    >
     <TextView
             android:id="@+id/book_name"
             android:layout_width="0dp" //设置0dp好像会提高效率
             android:layout_height="wrap_content"
             android:layout_weight="1"
             android:background="#ffffffff"
             android:gravity="center"
             android:text="@string/str_navi_home_navi_left" />
          <TextView
              android:id="@+id/book_accessTime"
              android:layout_width="0dp"
              android:layout_height="wrap_content"
              android:layout_weight="1"
              android:background="#ffffffff"
              android:gravity="center"
              android:text="@string/str_navi_home_navi_right" />
	</LinearLayout>
	
如果要设置成其他的比例 只需要计算出 对应的layout_weight即可

参考链接<http://bbs.csdn.net/topics/390801550>
