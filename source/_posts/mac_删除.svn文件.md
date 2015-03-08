#Mac 删除.svn文件

cd到其目录

	find . -type d -iname ".svn" -exec rm -rf {} \; 
	
参考链接<http://www.cnblogs.com/lr-ting/archive/2012/09/03/2666271.html>