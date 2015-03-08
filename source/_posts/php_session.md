#php Warning: session_start(): The session id is too long or contains illegal characters, valid characters are a-z, A-Z, 0-9 and '-,'


突然发现在页面会显示这个错误 找到了暂时的解决办法

把session_start(); 改为

	function my_session_start()
	{
	if (ini_get('session.use_cookies') && isset($_COOKIE['PHPSESSID'])) {
		$sessid = $_COOKIE['PHPSESSID'];
	} elseif (!ini_get('session.use_only_cookies') && isset($_GET['PHPSESSID'])) {
		$sessid = $_GET['PHPSESSID'];
	} else {
		session_start();
		return false;
	}

	if (!preg_match('/^[a-z0-9]{32}$/', $sessid)) {
		return false;
	}
	session_start();

	return true;
	}
	
然后调用my_session_start()即可

###后续..

发现之后等候PHPSESSION一直为空 怎么设置都没有- -...然后换Safari试试...结果SESSION完全没问题..然后返回Chrome删除下COOKIE...就OK.....