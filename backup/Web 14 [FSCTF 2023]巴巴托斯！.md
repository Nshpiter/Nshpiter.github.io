[FSCTF 2023\]巴巴托斯！ | NSSCTF](https://www.nssctf.cn/problem/4560)
打开题目
![image](https://github.com/user-attachments/assets/5a705449-5967-4c4e-a3d5-d1026348b4c8)
发现需要FSCTF Browser
> 于是构造，F12打开hackbar

![image](https://github.com/user-attachments/assets/06c924c2-5516-4dcf-b7f6-0a4bb8e71c88)

出现新的提示

![image](https://github.com/user-attachments/assets/3e5a8ebc-d470-477b-affa-53e0579b0304)

猜测题目的意思，题目说问是不是local，猜想127.0.0.1

于是构造

![image](https://github.com/user-attachments/assets/f446ce21-bdc9-49ee-9068-69a7765aa1ea)

结果发现没有反应而且没有别的提示出来

思考`伪协议`

于是加入

```
php://filter/read=convert.base64-encode/resource=flag.php
```

![image](https://github.com/user-attachments/assets/623b0b25-d08a-4058-81fa-8b434f1f8e8c)

得到base64的内容

> `PD9waHANCiRmbGFnPSJOU1NDVEZ7MjU4NzE2ZjMtNTY1NS00NGNjLWE0MzktYzhhMGZkOTQ5NjcxfSI7DQo/Pg==`

解密即可

![image](https://github.com/user-attachments/assets/30c1ab9e-42fc-4c49-b8cb-bf72eb1b7611)

**flag=NSSCTF{258716f3-5655-44cc-a439-c8a0fd949671}**