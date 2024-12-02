[suctf 2019\]EasySQL | NSSCTF](https://www.nssctf.cn/problem/19)
![image](https://github.com/user-attachments/assets/fd4a60a8-81cb-4471-8dc0-618692d2cb96)
> 前面使用了SQLMap来自动化注入，现在先来尝试手注

![image](https://github.com/user-attachments/assets/42b5cd88-216d-4e6c-8b98-9880fb253d32)
> 1.常规的单、双、括号、数字组合fuzzing一遍 PS:(fuzzing查资料)

![image](https://github.com/user-attachments/assets/ab1502d7-0f31-4a84-8117-1ba3e6e23d02)
返回这个值
> 2.再尝试直接输flag或者（order by、 union select 、information_schema）

![image](https://github.com/user-attachments/assets/47811f60-5185-474b-863d-308c77d71765)
看来是限制了flag等敏感词的输入
> 尝试其他可能的输出

可能有无输出的，页面不返回任何数据
> 回过头来看第一种情况，发现可以堆叠注入

> ### 1. **什么是堆叠注入？**

- **堆叠注入**是指在同一SQL查询中执行多个SQL语句的能力。通常，Web应用程序只执行一个SQL查询，但某些数据库（如MySQL）允许在同一连接中执行多个语句。
- 例如，在MySQL中，可以使用分号`;`来分隔多个SQL语句。

### 2. **如何识别堆叠注入？**

- **测试分号**：在输入框中尝试输入分号`;`，观察是否返回错误信息或异常行为。
- **测试多个语句**：尝试输入两个简单的SQL语句，如`1;SELECT 1`，观察返回结果。

### 3. **利用堆叠注入**

- **执行多个语句**：通过分号`;`分隔多个SQL语句，可以在同一连接中执行多个操作。
- **读取数据**：可以在第二个语句中读取数据库中的数据，如`SELECT`语句。
- **写入数据**：可以在第二个语句中写入数据，如`INSERT`、`UPDATE`或`DELETE`语句。

### 4. **具体步骤**

- **识别注入点**：首先找到可能的注入点，通常是用户输入的地方，如表单、URL参数等。

- **测试注入点**：使用常规的单引号、双引号、括号等组合进行fuzz测试，发现可以使用堆叠注入。

- **构造堆叠注入语句**：

  - 例如，假设注入点在`id`参数中，可以构造如下语句：

    sql

    复制

    ```
    id=1; SELECT 1;
    ```

  - 如果返回结果中包含`1`，说明成功执行了第二个语句。
  
尝试输入1,2,3,4

得到
![image](https://github.com/user-attachments/assets/66266a61-0d47-470f-8fc1-dea8edda6517)
发现并不是有规律的输出，到数字4的时候
> 想到是不是判断

尝试query=true,query=false

1.query=true返回

```
Array
(
    [0] => 1
)
```

2.query=false

```
Array
(
    [0] => 0
)
```

注意到如果只是单次注入的话无论什么情况下都是输出0或者1

推测算法

> select $_POST['query'] 逻辑运算符 某神秘字符;

> 后端将我们输入的字符与某神秘字符进行了逻辑运算，不过很明显，这串神秘字符本身的逻辑值应该是true。

那思路很清晰了，直接查flag不就行了？输入：`flag,2,3,4`，返回：

```
Nonono.
```
应该是被过滤了，禁用了

可以利用`*`星号匹配多列，输入：`*,2,3,4`
![image](https://github.com/user-attachments/assets/462712c2-6b32-4c66-8aac-7e360e55d640)

得到flag

**NSSCTF{74bbe503-55b5-45b3-8127-0be82ec04f41}**

后面发现本题使用SQLMap注入不行

![image](https://github.com/user-attachments/assets/224e0f06-c306-415d-ae81-eaf261f2525a)

## 总结

- SQL手注基本方法
