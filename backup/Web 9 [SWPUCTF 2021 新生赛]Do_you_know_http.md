[SWPUCTF 2021 新生赛\]Do_you_know_http | NSSCTF](https://www.nssctf.cn/problem/385)
![image](https://github.com/user-attachments/assets/d080fec3-3b71-4d01-83e9-25aca998f4fe)
> 本题考查burpsuite以及http的相关知识

![image](https://github.com/user-attachments/assets/369a7441-f579-485a-bb0e-fa5efc7e2b26)
题目要求我们使用WLLM浏览器打开，我们使用burpsuite抓包更改
![image](https://github.com/user-attachments/assets/5c45488e-e377-4ac2-adc6-c86f6a180e9c)
发现location处有新的地址,跟随重定向进到下一个文件
> **重定向**就是当用户访问一个网址时，服务器告诉浏览器去访问另一个网址。比如，你输入一个旧的网址，但服务器会自动把你带到新的网址，这就是重定向。简单来说，就是“你本来要去A地，但有人告诉你其实应该去B地”。

访问新的地址
![image](https://github.com/user-attachments/assets/b3940845-733a-406a-9716-666610f96625)
提示我们使用本地来访问，故添加
```
X-Forwarded-For:127.0.0.1
```
![image](https://github.com/user-attachments/assets/d4971d87-60be-4a82-9a80-1d6134a8e559)
访问地址即可拿到flag
**NSSCTF{51fe3534-cbaa-4dd8-9db5-017bbf9b1cbc}**