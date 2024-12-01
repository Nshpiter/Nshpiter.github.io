[LitCTF 2023\]作业管理系统 | NSSCTF](https://www.nssctf.cn/problem/3867)
![image](https://github.com/user-attachments/assets/34131100-d9f3-4f1b-9873-730a9663da4f)
> [!TIP]
看到作业管理系统就想到了可能要登录

![image](https://github.com/user-attachments/assets/cf30752f-ae21-40f7-ac13-34c405c46ea1)
> 先尝试了admin 123456密码或账户错误（弱口令）

![image](https://github.com/user-attachments/assets/f28afdac-0c6e-4867-90ef-cd3b853ef8df)
发现了账号和密码
尝试登录成功
![image](https://github.com/user-attachments/assets/e5e1a83a-ff75-44ee-a691-f67f8ea31214)
> [!IMPORTANT]
**里面有上传功能!**

![image](https://github.com/user-attachments/assets/d983d977-6d08-4abd-8934-ed0454f06eff)
**前面的本地上传文件很简单所以会简单过一遍**
### 法一:蚁剑
不多说，本地写一个一句话木马试试看能不能上传
```php
<?php eval($_POST['cmd']); ?>
```
![image](https://github.com/user-attachments/assets/b15e650d-60d2-493f-85d2-06b20a4f994f)
这么容易就上传了
![image](https://github.com/user-attachments/assets/8cdf37d4-2c7b-4880-93c0-7a6d426dcdbb)
![image](https://github.com/user-attachments/assets/bb8a55d6-4068-4b05-94ce-d9d32d395b62)
![image](https://github.com/user-attachments/assets/a86742e6-2dba-404f-8477-5508c19c636f)
很容易在根目录里面找到flag
> [!IMPORTANT]
这个方法很简单直接，但很多网站会过滤掉php的文件，很多时候可能需要我们采用双后缀的方式并且利用网站前端检测漏洞用burpsuite来修改回php发送

### 法二:远程下载
> [!TIP]
本题还提供了远程下载,我们从这下手学习

> [!IMPORTANT]
本题也是**应对从法一无法上传一句话木马方法**，当然也要有这个远程下载哈

> [!NOTE]
 File协议，也称为本地文件传输协议，主要用于访问本地计算机中的文件。它类似于在Windows资源管理器中打开文件或通过右键菜单选择“打开”文件的方式。File协议的基本格式为`file:///文件路径`，例如`file:///C:/Users/CLi/AppData/Local/Temp/WindowsLiveWriter1627300719/supfiles52F410/wangdan-se-436963[2].jpg`表示访问位于C盘的该文件。
> File协议的主要特点包括：
1. **仅限本地访问**：File协议只能用于访问本地计算机上的文件，无法实现跨域访问。
2. **简单快捷**：由于File协议不涉及网络传输，因此访问速度较快，适用于本地开发和测试。
3. **安全性问题**：File协议没有HTTP协议提供的安全机制，如身份验证和加密，因此在安全性要求较高的场景下不建议使用。
4. **浏览器限制**：出于安全考虑，大多数浏览器禁止通过File协议加载跨域资源，因此在Web开发中通常不推荐使用File协议。
总结来说，File协议适用于需要快速访问本地文件的场景，但在涉及网络传输或安全性要求较高的应用中，建议使用HTTP或其他更安全的协议。

利用这个我们来试试
![image](https://github.com/user-attachments/assets/67296ac2-715c-43e1-a1a1-71acfc8a75bf)
点击下载
![image](https://github.com/user-attachments/assets/9ad605bb-ad22-475f-9bbf-9d62c9c1ff0d)
进入编辑得到flag内容
同样我们这个时候也可以访问url/flag，下载文件得到flag
![image](https://github.com/user-attachments/assets/0286e3b8-d3cc-4b2b-8d66-0365d1bd6343)
### 法三(感觉最快)
观察网页url,发现
http://node4.anna.nssctf.cn:28428/index.php?op=edit&fename=uploadFileName&folder=./
> [!NOTE]
由于页面所有的操作只有登录这一个鉴权，所有操作都没用敏感目录的过滤（完全没有过滤）

我们可以直接**修改uploadFileName为flag来访问**
同理可以得到flag
## 总结
- **file://协议**
- **文件上传**