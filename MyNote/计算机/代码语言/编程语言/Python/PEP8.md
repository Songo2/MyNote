--Python Enhancement Proposal #8
官方唯一代码风格指南
#Python

# 核心原则:
## 可读性第一,代码被读的次数多于被写的次数.

## 代码规范一致性很重要,项目里的一致性大于社区的一致性.但是如果规范一致性妨碍了可读性,则应该打破规范保障可读性.

## 代码应该简洁优雅.


# 代码布局:

## 缩进:
### 缩进应该严格控制为4个空格.

### 严禁将Tab("\t")与空格混用

### 如果将一个语句分行表示可以使用两种方法:垂直对齐,即与括号内的第一个元素对齐.悬挂缩进,即与第一行相差一个缩进.


## 最大行长:
### 代码行一行应该不超过79个字符.

### 注释/文档字符串应该不超过72个字符.

### 如果需要续行,建议使用括号而非反斜杠


## 空行:
### 顶级函数/类之间空两行
```Python
def my_func():
	return 0
	
	
class MyClass:
	def __init__(self, id):
		self.id = id
```

### 类内部的方法空一行
```Python
class MyClass:
	def __init__(self, id):
		self.id=id

	def class_method():
		return 0
```

### 函数体内的逻辑块之间可以空一行,不要滥用.
```Python
def get_max_and_min(list):
	newlist = list.sort()

	max = newlist[0]
	min = newlist[-1]

	return max, min
```

## 编码
Python默认使用UTF-8


## 导入
### 位置
文件的顶部,在注释之后,在全局变量之前.
```Python
# something
import what_you_want
global pi = 3.14
```
### 分行
每个库都单独写一行导入
```Python
import a
import b
......
```
### 顺序
标准库,第三方库,本地自定义库,分组,每组之间空一行.
```Python
import os
import sys

import numpy

import my_module
```

### 禁忌
禁止使用通配符导入(import * )
```Python
# from math import **
import math
```

# 空白
## 禁止
### 括号内侧
T:f(x)  F:f( x )
```Python
# print( x )
print(x)
```

### 逗号/分号/冒号前
T:x: y  F:x : y
```Python
# print(x , y)
print(x, y)
```

### 中括号(索引/切片)
T:dict[key]  F:dict[ key ]
```Python
# my_list[ 1 ]
my_list[1]
```

### 形参赋默认值(无注解)
T:f(a=1)  F:f(a = 1)
```Python
# print("Hello world", end = ".")
printg("Hello,world",end=".")
```


## 推荐
### 二元运算符两侧
T:a + b  F:a+b
```Python
# x = a+b
x = a + b
```

### 逗号后
T:print(a, b)  F:print(a,b)
```Python
# print(a,b)
print(a, b)
```

### 注释的井号
T:# hello world  F:#hello world
```Python
#hello world
# hello,world
```
### 类型注解
T:f(a : int = 1)  F:f(a:int=1)
```Python
# print(a:int=1)
print(a : int = 1)
```

# 命名规范
[[编程语言标识符基本规则]]
## 变量/函数/模块/包
蛇形命名法
my_var my_func my_module my_module

## 类/异常
大驼峰/CapWords/PascalCase
MyClass MyError

## 常量
全大写/UPPER_CASE
MY_CONST

## 内部变量
加单下划线
\_inner

## 私有变量
加双下划线
\_\_private

## 魔术方法/内置特殊变量
两侧加双下划线
\_\_init__  \_\_main__

## 避免
尽量使用英文,不要使用中文或者拼音,不要混用大小写,不要使用单字符


# 注释
## 块注释
整段注释,每行以#开头,缩进与代码一致.
\#This is an example.
\#If you want to do, you can refer to this example.
## 行内注释
与代码隔至少两个空格,只写为什么,不写做什么.
T:speed = 0  # 速度初始化为0,防止空值报错
F:speed = 0  # 把0赋值给speed

## 文档字符串
文档字符串使用三重引号"""
所有的公有模块,函数,类,方法必须写


# 编程建议
## 字符串的引号
统一使用一种,如单引号或双引号,建议使用单引号.

## 复合语句
不要把多条语句写成一行如if x: print(a)

## 类型注解
推荐使用PEP484,提升可读性和IDE支持.

## 逻辑条件
None用is/is Not,不要用\=\=.
布尔值直接判断,不要\=\=True.