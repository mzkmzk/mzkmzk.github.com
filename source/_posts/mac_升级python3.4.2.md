#Mac 升级python3.4.2

###0x01

下载安装文件<https://www.python.org/downloads/>

###0x02 移动python的安装目录

`sudo mv /Library/Frameworks/Python.framework/Versions/3.4 /System/Library/Frameworks/Python.framework/Versions`

###0x03 更改权限

'sudo chown -R root:wheel /System/Library/Frameworks/Python.framework/Versions/3.4'

###0x04 更改链接

	sudo rm /System/Library/Frameworks/Python.framework/Versions/Current
	sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.4 /System/Library/Frameworks/Python.framework/Versions/Current

###0x05 删除旧的命令符号链接	

	sudo rm /usr/bin/pydoc
	sudo rm /usr/bin/python
	sudo rm /usr/bin/pythonw
	sudo rm /usr/bin/python-config
	
###0x06 重新建立新的命令符号链接

	sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.4/bin/pydoc3.4 /usr/bin/pydoc
	sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.4/bin/python3.4 /usr/bin/python
	sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.4/bin/pythonw3.4 /usr/bin/pythonw
	sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.4/bin/python3.4m-config /usr/bin/python-config
	
重启Consonle ok

###参考链接

<http://www.cnblogs.com/nokiaguy/p/3456590.html>