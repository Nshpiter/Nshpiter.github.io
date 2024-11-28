[第五空间 2021\]WebFTP | NSSCTF](https://www.nssctf.cn/problem/344)
![image](https://github.com/user-attachments/assets/3f265409-b216-47f1-a787-804d809ea308)
> 打开网页，发现常见的登录页面，尝试登录

![image](https://github.com/user-attachments/assets/9795d8a3-4dd7-4004-bb44-367625dde3aa)
**常见的admin和密码报错并没有给我们很多提示，即我们无法知道用户和密码**
![image](https://github.com/user-attachments/assets/03a0376a-8755-40e5-bf66-358293f5dd97)
## 使用御剑后台
> [!TIP]
那就运用学过的扫描后台工具，找找有没有开放端口，或者网页目录文件

![image](https://github.com/user-attachments/assets/89542619-39e9-46f3-b9e6-dd9b30cb610a)
这里使用了==御剑后台==
> [!NOTE]
我们发现了目录phpinfo.php，以及.git目录
## 尝试访问第一个目录
![image](https://github.com/user-attachments/assets/53f85dad-da37-4bbb-aade-02f0fe75290f)
> 搜索flag

![image](https://github.com/user-attachments/assets/fef2627a-5e5f-4877-b23e-95b5a5cf1cc2)
> 得到flag-->**NSSCTF{2e5ccdd5-13f8-4048-838f-5080b489945a}**

思考另一种途径，.git目录
> [!TIP]
里面有readme.md文件,找到了服务器密钥，可以通过蚁剑连接上去

但是通过查找并没有找到有效flag文件，猜测还是在之前的目录下
**蛮迷惑的, 扫目录发现有.git目录, 但是从readme里面拿到密码登录进去其实没什么用, flag藏在phpinfo里面?**
> 因为通常情况下的.git文件是有上传记录的，我们可以看到用户的提交更改，这道题感觉多此一举有了

## 总结
- 1.虽然哈这道题目比之前做的题不知道容易多少倍去了，但是web的题感觉出发点都是一样的，我们的基操都是同扫描网站开发端口或者目录文件来实现漏洞，不知道说的对不对
- 2.网站安全一定要保护好php，而ctf很多都涉及php安全，比如一句话木马，之前尝试过蚁剑通过木马进入后台。(phpinfo.php 是一个常见的PHP脚本，用于显示当前PHP配置的详细信息。这个页面通常包含服务器的环境变量、PHP版本、扩展、配置选项等敏感信息。如果这个页面被意外暴露在公共访问中，攻击者可以通过分析这些信息来发现潜在的漏洞或配置错误。)