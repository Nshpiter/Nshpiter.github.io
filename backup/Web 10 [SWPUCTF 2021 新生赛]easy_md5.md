## [SWPUCTF 2021 新生赛\]easy_md5 | NSSCTF](https://www.nssctf.cn/problem/386)
![image](https://github.com/user-attachments/assets/65365ddb-49aa-4d54-b8cf-1ee7846c4375)
题目说了是MD5，打开网页
![image](https://github.com/user-attachments/assets/bf14075d-fe28-4516-bb5a-a46f8bdd2f76)
> 题目意思：
- 1. `name`和`password`是通过GET和POST请求分别传递的参数。
- 2. `name`和`password`必须是不同的字符串（`$name !=$password`）。
- 3. 但它们的MD5哈希值必须相同（`md5($name) == md5($password)`）。
既要两变量个值不相同，又要两个变量md5值一样

可以发现此时判断md5值是否一样用的是`==`，这是php的弱类型比较
![image](https://github.com/user-attachments/assets/e98eb2bc-0e1c-4226-b6af-1b79001d68c9)
### **方法一：** 
> 可以使用带0e开头的数字穿进行传递参数，因为php会将0e开头的数字转化为0，故此时md5值相等，而两个变量值不相等

使用hackbar来操作
- load URL
- 在网址后输入/?name=240610708
- password=QLTHNDT

![image](https://github.com/user-attachments/assets/4cb01731-2b2d-430c-8fed-6148acb7e386)
![image](https://github.com/user-attachments/assets/7e96c01b-79c9-4316-b0d6-a2661e1c39ce)
拿到flag
> **name和password 的等号后面只需要输入会被MD5加密为0e开头的数字就行，但是内容不能一模一样。**

**NSSCTF{599b6374-4984-467d-aa61-3181aa93ff43}**
### 方法二：
看了其他师傅的wp，
> 可以传递数组，如name[]=123,password[]=456，md5不能加密数组，故两个md5返回的都是null

> 若遇到`===`这样的强类型比较，方法一就失效了，方法二仍然有效，或者还可以使用软件fastcoll进行md5碰撞，生成两个字符串使得他们的md5值相同

故传递数组作为`$name`和`$password`的值
```
$name = array('123');
$password = array('456');
```
或者在URL中传递
```
?name[]=123&password[]=456
```
## 总结
- MD5相关知识
- php的弱类型比较
