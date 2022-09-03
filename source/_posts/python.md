---
title: Python学习笔记
author: yikafu
date: 2022-02-24 11:28:00
updated: 2022-02-24 11:28:00
tags: python
categories: Code
cover: https://cdn.jsdelivr.net/gh/yikafu/blog_img/random_cover/cover3.jpg
---

# 转义字符(\\)

- ```\n```换行
- ```\t```空一个制表符的位置
- ```\b```退一个格
- ```\r```回车

```python
print("hello\bworld")
#输出world，world将hello覆盖
```
原字符：让转义字符失效，即在字符串前加上r或R。但是字符串的结尾不能有\
```python
例如：
print(r"hello\bworld")
#输出hello\bworld
print(r"hello\bworld\")
#报错：SyntaxError: EOL while scanning string literal
```
___


# 数据类型

- int：整型
- float：浮点数型
- bool：布尔类型 ——>Ture、False
- str：字符串类型

  
## 整型
二进制0b——数值转换bin()
八进制0o——数值转换oct()
十六进制0x——数值转换hex()


## 浮点型
对于浮点型的 计算，部分计算会存在不精确的情况

```python
print("1.1+2.2") #3.3000000000000003
```
以此需先导入库
```python
from decimal import Decimal
print("1.1+2.2") #3.3
```
## 字符串
使用单引号，双引号，三引号都可以。但是只有三引号的字符串可以分两行来写

## 数据类型转换
二进制0b——数值转换bin()
八进制0o——数值转换oct()
十六进制0x——数值转换hex()



str()——转换成字符串类型
int()——转换成整型，含文字和小数点的字符串无法转换，小数转换时抹零取整

float()——转换成浮点型，整数加".0"



## 列表

- 列表的索引--[跳到index函数](#jump)--
  - 正索引：第一个元素下标为0
  
  - 负索引：最后一个元素下标为-1
  
- 列表的切片（一次性获取多个元素）

  ```python
  列表名[start: stop: step]	# 含start不含stop
  ```

  



---

# 注释

单行注释用：#

代码块注释：''‘

中文编码声明注释：在文件开头写上 ```#coding:gdk```（无需理会）

---

# 函数

- input函数输入的是str类型，计算时应转换成int类型

- range函数

  ```python
  range(start,stop,step)
  # start默认为0，step(步长)默认为1
  ```

- <a id="jump">index函数</a>

  用于列表元素的索引，当其中有相同元素时，只返回第一个元素的下标值
  
  index其他用法
  
  ```python
  index("对象"，开始目标下标，结束目标下标)
  ```
  
  

# 运算符

- "/"是除法运算，"//"是整除（即向下取整）

  ```python
  print(11//2)   	#结果是5
  print(-11//2)  	#结果是-6
  ```

- " ** "是幂运算

  ```python
  print("2**2")  	#即2的2次方
  ```
- " % "求余运算   
- 解包赋值，同时解包赋值利于数值的交换        
	```python
	a,b,c=10,20,30
	#a=10 b=20 c=30
	
	a,b=10,20
	print(a,b)	#10 20
	a,b=b,a    	#直接交换
	print(a,b) 	#20 10
	```



- 比较运算符的输出结果是"bool"类型，即 false 或 true



- 比较对象的id用" is "

  ```python
  a=10
  b=20
  print(a is b)	#false
  ```



- 布尔运算

	- " and ":全为真才为真
	- " or "有一真即为真
	- " not "对运算
	- " in "内运算

  ```python
  a,b=1,2
  print(a==1 and b==2)	#ture
  print(a==1 and b<2)		#flase
  print(a==1 or b<2)		#ture
  -------------------------------------
  f=ture
  p=false
  print(not f)	#ture
  -------------------------------------
	s="hello"
	print('l' in s)		#ture
	```
- 位运算：将数字转换成二进制进行运算——[查看更多详情](https://blog.csdn.net/meng_xin_true/article/details/103548077)——

  - 位与&：对应数位为1时，结果才为1
  - 位或|：对应数位有一个为1时，结果为1

  ```python
  print(4&8)	#结果为0
  print(4|8)	#结果为12
  ```


- 左移位" << "：高位溢出，低位补零
- 右移位" << "：低位溢出，高位补零
- 运算顺序：算术——位运算——比较——布尔——赋值

---

# 结构

python里面没有" { } ",要注意缩进问题

### if语句

- if语句后要加冒号

  ```python
  if 条件句:
  	执行句1
  else:
  	执行句2
  ```

  


- if多分支

  ```python
  if 条件句1:
  		执行句1
  elif 条件句2:
  		执行句1
  elif 条件句3:
  		执行句3
  else :
      	执行句4
  ```


### 条件表达式

```python
x if 条件判断式 else y
# 如果条件成立，输出 x
# 如果条件不成立，输出 y
```

### pass表达式

- 用于代码还未成型时占位防报错

### while循环

- 需要加冒号
- 注意缩进

### for-in结构

```python
for a in b
	# 把b中每一个值依次赋予a
    # 当不需要自定义变量时用“ _ ”代替
```

